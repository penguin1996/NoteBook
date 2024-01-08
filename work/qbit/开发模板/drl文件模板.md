```java
package rules;
dialect "java"
import java.util.*
import com.qbit.drools.DroolsRuleExecuteDto
import java.util.Map
import java.util.HashMap

// 需求文档：https://axss9gjoff.feishu.cn/wiki/NMSYwVPGjiJSvukUZAWcI6kinQN 内容部分：法币出金 USD
// 处理类：com.qbit.drools.action.risk.CurrencyOutboundRiskAction

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW001"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 出金大于等于3个不同的收款方
    DroolsRuleExecuteDto(map["payerCountMap"] >= 3)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW002"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 收款方账户单日收到大于等于3个账户的出金
    DroolsRuleExecuteDto(map["payeeCountMap"] >= 3)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW003"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 客户单日单笔出金金额大于190000
    DroolsRuleExecuteDto(map["singleOutGeAmountMap"] >= 190000)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW004"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 客户单日累计出金数量大于5笔
    DroolsRuleExecuteDto(map["singleOutCountMap"] >= 5)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW005"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 客户单日累计出金金额大于等于800000
    DroolsRuleExecuteDto(map["singleSumGeAmountMap"] >= 800000)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW006"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 客户单笔交易大于等于50000
    // 近7日交易金额最大的一笔交易*1.7全部小于该单笔交易（T为交易发起日，近7日为T-8至T-1日，T-x日（x大于等于8）不为0）
    DroolsRuleExecuteDto(map["singleOutGeAmountMap"] >= 50000 && (map["singleOutGeAmountMap"] > map["singleMaxLtAmount"]) && map["singleMaxLtAmount"] != 0)
then
end

rule "483aee0e-0417-44a9-adf4-26d3f5005826_LCW007"
salience 1
when
    $t:DroolsRuleExecuteDto()
    // 客户单日交易大于等于230000USD
    // 近7日交易金额最大的一笔交易*1.7全部小于该日交易（T为交易发起日，近7日为T-8至T-1日，T-x日（x大于等于8）不为0）
    DroolsRuleExecuteDto(map["singleSumGeAmountFilterFailMap"] >= 230000 && (map["singleSumGeAmountFilterFailMap"] > map["singleMaxLtAmount"]) && map["singleMaxLtAmount"] != 0)
then
end
```

