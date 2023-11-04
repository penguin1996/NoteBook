Mybatis的缓存时基于JVM堆内存实现的，会将所有缓存数据都放在Java对象中。缓存采用装饰器模式设计，Cache接口会有一个基本的实现类，即PerpetualCache。通过HashMap存放缓存对象，它重写了equals()方法，当两个缓存对象的Id相同时，即认为缓存对象相同。

缓存的优化：

开启二级缓存

步骤一 setting文件中

![image-20231029223952431](image/image-20231029223952431.png)

步骤二：xml映射文件中

![image-20231029224132135](image/image-20231029224132135.png)

将某个查询的二级缓存关闭：
![image-20231029224108215](C:\Users\pengu\AppData\Roaming\Typora\typora-user-images\image-20231029224108215.png)

源码：

![image-20231029224441132](image/image-20231029224441132.png)

通过Redis客户端，将缓存数据放到Redis中。或者放入Ehcache中。实现接口，重写putObject，getObject方法接口。

![image-20231029225026637](image/image-20231029225026637.png)