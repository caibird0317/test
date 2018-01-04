
## 接口文档 ##
[TOC]
### 1、登录页面 
#### 用户登录
- **请求URL**
> /app/login
- **请求参数**
>
 | 请求参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| user|  String|  取登录框的用户名，不能为空|
| password|   String|  取登录框的密码，不能为空|
- **返回参数**
```javascript
{
  // 登录结果
  result: 0, // 0成功，其他失败
  // 是否认证状态有四种类型  未认证、待审核、已通过、未通过
  cerStatus: xx,
  msg: "" // 成功或失败的原因
}
```
----
### 2、注册页面 
#### 2.1 获取短信验证码
- **请求URL**
> /app/getSMSCode
- **请求参数**
>
 | 请求参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| phone|  Number|  用于接受短信的手机号码|
- **返回参数**
```javascript
{
  // 返回来的验证码，一般客户端会做60S等待
  content: "您好，您在美丽贷的短信验证码为：000124 请妥善保存，30分钟有效"
}
```
#### 2.2 用户注册
- **请求URL**
> /app/register
- **请求参数**
>
 | 请求参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| phone|  Number|  注册本人手机号码 必填|
| password|  String|  注册登录密码 必填|
| jtNumer|  Number|  推荐人的手机号码 非必填|
| agentNumber|  Number|  代理人手机号码 非必填|
| checkCode|  String|  获取到的验证码 必填|
- **返回参数**
```javascript
{
  // 注册结果
  result: 0, // 0成功，其他失败
  msg: ""    // 如果是失败，给失败的原因
}
```
----
### 3、首页面 
>#### 3.1申请贷款
>> ##### 3.1.1 获取贷款额度
>>- **请求URL**
>>     /app/getLoanline
>>- **请求参数**
>> -暂无
>>- **返回参数**
>>```javascript
>>{
>>  // 最小贷款
>>  min: "2000",
>>  // 最大贷款
>>  max: "3000"
>>}
>>```
>> ##### 3.1.2 提交申请借款
>>- **请求URL**
>>     /app/submitLoanline
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | loanAmount|  Number|  贷款金额 必填|
>> | reDate|  Date|  还款日期 必填|
>> | description|  String|  抵押说明 非必填|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>>}
>>```
>> ##### 3.1.3 我的借款
>>- **请求URL**
>>     /app/getMyLoanList
>>- **请求参数**
>> --- 暂无
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>>   //借款列表 取当前用户的所有借款列表
>>   list: [
>>     {
>>        status:0,  //借款状态。  0申请中，1已生效
>>        loanId: "20180101",  //借款编号
>>        totalLoanMoney: "50000.00" // 贷款总额
>>     },
>>     {
>>        status: 1,   //借款状态。  0申请中，1已生效
>>        loanId: "20180101",  //借款编号
>>        totalLoanMoney: "50000.00", // 贷款总额
>>        lessLoanMoney:"3000.00",   // 贷款余额
>>        issuesNumer: "5期",         //已还第几期
>>        issuesDate: "12月15号应还¥1000.00",  //第几期还的钱
>>        activeDate: "2017-12-10",  // 生效日期
>>        finishDate: "2018-10-10"   // 结束日期       
>>     }
>>   ]
>>}
>>```
>> ##### 3.1.3 我的借款详情
>>- **请求URL**
>>     /app/getMyLoanDetail
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | loanId|  String|  上一个页面传入|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>>   //借款详情
>>   loanId: "JKBH-20171207", //借款编号
>>   loanDate: "2017.12.07",  // 借款日期
>>   loanMoney: "8000.00",  // 贷款金额
>>   replayLoanType: "等额本金", // 还款类型
>>   serverFee: "50.00",       // 服务费
>>   interestRate: "1.5%",     //利率
>>   loanStatusText: "已生效",  // 贷款状态，这里尽量给文本，前端就不用做map映射    
>>   reloanTimes: "12",   // 还款期数
>>   hasloanTimes: "5",   // 已还期数
>>   ownMoney: "5000.00",   // 尚欠金额
>>   description: "吧啦啦啦", // 抵押说明
>>   sales: "张三",   // 业务员  
>>   salesTel: "13797979797", // 业务员电话 
>>   activeDate: "2017-12-10",      // 生效日期
>>   repaymentTypeText: "银行转账",  // 还款方式   
>>   repaymentAccount："6214 **** **** 5533", //还款账号
>>   repaymentBankText: "招商银行"
>> }
>>```
>> ##### 3.1.4 还款记录
>>- **请求URL**
>>     /app/getRepaymentlist
>>- **请求参数**
>>  --- 暂无
>>- **返回参数**
>>```javascript
>>{
>>   result: 0,
>>   //还款列表
>>   list: [
>>     {
>>        loanId: "JKBH-20171207", //借款编号
>>        loanDate: "2017.12.07",  // 借款日期
>>        activeDate: "2017-12-10",      // 生效日期
>>        totalLoanMoney: "50000.00", // 贷款总额
>>        lessLoanMoney:"3000.00",   // 贷款余额
>>        reloanTimes: "12",   // 还款期数
>>        hasloanTimes: "5",   // 已还期数
>>     },
>>     {
>>        loanId: "JKBH-20171207", //借款编号
>>        loanDate: "2017.12.07",  // 借款日期
>>        activeDate: "2017-12-10",      // 生效日期
>>        totalLoanMoney: "50000.00", // 贷款总额
>>        lessLoanMoney:"3000.00",   // 贷款余额
>>        reloanTimes: "12",   // 还款期数
>>        hasloanTimes: "5",   // 已还期数
>>     }
>>   ]
>>}
>>```
>> ##### 3.1.5 还款记录详情
>>- **请求URL**
>>     /app/getRepaymentDetail
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | loanId|  String|  上一个页面传入|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0,
>>   hasTotalRepayment: "8000.00", // 已还款
>>   currentRepayment: "1000.00",  //本期应还
>>   activeDate: "2017-12-11",  // 生效日期
>>   totalCapital: "10000.00",     // 本金
>>   totalBreakMoney: "100.00",    // 违约金
>>   totalInterest: "100.00",      // 利息
>>   totalServerFee: "20.00",      // 服务费
>>   currentRepaymentTimes: "5",  // 本期期数
>>   lessRepaymentTimes: "7",    // 剩余期数
>>   // 已还款记录列表
>>   recordList: [
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     }
>>   ]
>>}
>>```
----