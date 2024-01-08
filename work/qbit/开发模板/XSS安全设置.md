参考：
[xssFilter: xss过滤器 (gitee.com)](https://gitee.com/l502387174/xss-filter)

https://blog.csdn.net/weixin_51596697/article/details/128169250

https://developer.aliyun.com/article/1204193

https://www.cnblogs.com/blbl-blog/p/17188558.html

XssFilter

```java
package com.qbit.common.xss;

import com.qbit.common.xss.wrapper.XssHttpServletRequestWrapper;
import org.springframework.stereotype.Component;

import javax.servlet.*;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

/**
 * @author zero
 * {@code @Date} 17:53 2023/12/27
 * {@code @Description} xss攻击处理拦截
 **/
@Component
public class XssFilter implements Filter {

    // 忽略权限检查的url地址
    private final String[] excludeUrls = new String[]{
            "api/admin/addNews",
            "api/admin/editNews",
            "/api/thunes/webhook"
    };

    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {

        HttpServletRequest req = (HttpServletRequest) servletRequest;
        HttpServletResponse response = (HttpServletResponse) servletResponse;

        //获取请求你ip,端口后的全部路径
        String uri = req.getRequestURI();
        //注入xss过滤器实例
        XssHttpServletRequestWrapper xssHttpServletRequestWrapper = new XssHttpServletRequestWrapper(req);
        //过滤掉不需要的Xss校验的地址
        for (String str : excludeUrls) {
            if (uri.contains(str)) {
                filterChain.doFilter(req, response);
                return;
            }
        }

        filterChain.doFilter(xssHttpServletRequestWrapper, response);
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

处理Xss攻击

```java
package com.qbit.common.xss.wrapper;

import cn.hutool.core.text.CharSequenceUtil;
import cn.hutool.http.HtmlUtil;
import cn.hutool.json.JSONUtil;
import lombok.Cleanup;

import javax.servlet.ReadListener;
import javax.servlet.ServletInputStream;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletRequestWrapper;
import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.LinkedHashMap;
import java.util.Map;

/**
 * @author zero
 * {@code @Date} 17:43 2023/12/27
 * {@code @Description} 处理xss攻击
 **/
public class XssHttpServletRequestWrapper extends HttpServletRequestWrapper {
    /**
     * The default behavior of this method is to return getInputStream() on the
     * wrapped request object.
     */
    @Override
    public ServletInputStream getInputStream() throws IOException {
        @Cleanup InputStream inputStream = super.getInputStream();
        @Cleanup InputStreamReader reader = new InputStreamReader(inputStream, StandardCharsets.UTF_8);
        @Cleanup BufferedReader buffer = new BufferedReader(reader);// 读取的高效性
        StringBuilder body = new StringBuilder();
        String line = buffer.readLine();
        while (line != null) {
            body.append(line);
            line = buffer.readLine();
        }

        if (!body.isEmpty()) {
            /*将读取的body进行数据转换，因为客户端提交是json格式的，
        java是不支持原生json格式，需将json格式数据转为map对象*/
            Map<String, Object> map = JSONUtil.parseObj(body.toString());
            /*对map进行转译*/
            Map<String, Object> result = new LinkedHashMap<>();
            map.keySet().forEach(key -> {
                Object val = map.get(key);
                if (val != null) {
                    if (val instanceof String) {
                        result.put(key, HtmlUtil.unescape(HtmlUtil.filter(val.toString())));
                    } else {
                        result.put(key, val);
                    }
                }
            });
            String json = JSONUtil.toJsonStr(result);
            ByteArrayInputStream bain = new ByteArrayInputStream(json.getBytes());

            return new ServletInputStream() {
                @Override
                public int read() {
                    return bain.read();
                }

                @Override
                public boolean isFinished() {
                    return false;
                }

                @Override
                public boolean isReady() {
                    return false;
                }

                @Override
                public void setReadListener(ReadListener readListener) {

                }
            };
        } else {
            return null;
        }
    }

    /**
     * Constructs a request object wrapping the given request.
     *
     * @param request The request to wrap
     * @throws IllegalArgumentException if the request is null
     */
    public XssHttpServletRequestWrapper(HttpServletRequest request) {
        super(request);
    }

    /**
     * The default behavior of this method is to return getParameter(String
     * name) on the wrapped request object.
     * 重写getParameter方法，将参数名和参数值都做xss过滤。
     */
    @Override
    public String getParameter(String name) {
        String value = super.getParameter(name);
        if (CharSequenceUtil.hasEmpty(value)) {
            return value;
        }

        value = HtmlUtil.unescape(HtmlUtil.filter(value));

        return value;
    }


    /**
     * The default behavior of this method is to return
     * getParameterValues(String name) on the wrapped request object.
     * 做转译处理
     */
    @Override
    public String[] getParameterValues(String name) {
        String[] values = super.getParameterValues(name);
        if (values == null) {
            return null;
        }

        for (int i = 0; i < values.length; i++) {
            String value = values[i];
            if (value != null) {
                value = HtmlUtil.unescape(HtmlUtil.filter(value));
            }
            values[i] = value;
        }
        return values;
    }

    /**
     * The default behavior of this method is to return getParameterMap() on the
     * wrapped request object.
     */
    @Override
    public Map<String, String[]> getParameterMap() {
        Map<String, String[]> parameters = super.getParameterMap();
        LinkedHashMap<String, String[]> map;
        map = new LinkedHashMap<>();
        if (parameters != null) {
            for (String key : parameters.keySet()) {
                String[] values = parameters.get(key);
                for (int i = 0; i < values.length; i++) {
                    String value = values[i];
                    if (value != null) {
                        value = HtmlUtil.unescape(HtmlUtil.filter(value));
                    }
                    values[i] = value;
                }
                map.put(key, values);
            }
        }
        return map;
    }

    /**
     * The default behavior of this method is to return getHeader(String name)
     * on the wrapped request object.
     */
    @Override
    public String getHeader(String name) {
        String value = super.getHeader(name);
        if (value != null) {
            value = HtmlUtil.unescape(HtmlUtil.filter(value));
        }
        return value;
    }
}
```

