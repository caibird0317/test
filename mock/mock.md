
## 接口文档 ##
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
> ##### 3.2 我的借款
>>##### 3.2.1 获取借款列表
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
>> ##### 3.2.2 借款详情
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
>##### 3.3 还款记录
>> ##### 3.3.1 还款记录
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
>> ##### 3.3.2 还款记录详情
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
> ##### 3.4 我的认证
>> ##### 3.4.1 认证状态
>>- **请求URL**
>>     /app/getInactiveStatus
>>- **请求参数**
>> ----暂无
>> 
>>- **返回参数**
>>```javascript
>>{
>>   // TODO 各个状态码后台给出后待讨论
>>   status: "xx", // 认证状态
>>   statusText: "已激活", // 已经认证 
>>   idStatus: "",    // 身份状态
>>   contactStatus: "", // 联系人信息认证状态
>>   unitStatus: "",  // 单位或学校认证状态
>>   moreStatus: "", //  更多信息认证状态
>> }
>>```
>> ##### 3.4.2 获取身份信息
>>- **请求URL**
>>     /app/getIdInfo
>>- **请求参数**
>> ----暂无
>> 
>>- **返回参数**
>>```javascript
>>{
>>   user: "", // 姓名
>>   card: ""  // 身份ID
>> }
>> ```
>> ##### 3.4.3 设置身份信息
>>- **请求URL**
>>     /app/setIdInfo
>>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | user|  String| 姓名 用户输入|
>> | card|  String| 身份证 用户输入|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>> }
>> ```
>> ##### 3.4.3 获取联系人的关系列表
>>- **请求URL**
>>     /app/getPersonRelation
>>- **请求参数**
>> ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   list: [
>>     {
>>        text: "兄弟",
>>        value: "xd",
>>     },
>>     {
>>        text: "父母",
>>        value: "fm",
>>     },
>>     {
>>        text: "朋友",
>>        value: "py",
>>     },
>>     {
>>        text: "其他关系",
>>        value: "other",
>>     }
>>   ]
>> }
>> ```
>> ##### 3.4.4 获取联系人信息
>>- **请求URL**
>>     /app/getPersonInfo
>>- **请求参数**
>> ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   frequentContacts: "张三", // 常用联系人
>>   frequenTel: "13597979797", // 常用联系人电话
>>   frequentRelation: "兄妹",  // 常用联系人关系
>>   urgentContacts: "李四", // 紧急联系人
>>   urgentTel: "13597979797", // 紧急联系人电话
>>   urgentRelation: "父母" // 紧急联系人关系
>> }
>> ```
>> ##### 3.4.4 设置联系人信息
>>- **请求URL**
>>     /app/setPersonInfo
>>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | frequentContacts|  String| 常用联系人 从通讯录选择|
>> | frequenTel|  String| 常用联系人 从通讯录选择|
>> | frequentRelation|  String| 传获取到的列表的vlaue 下拉框选择|
>> | urgentContacts|  String| 紧急联系人  从通讯录选择|
>> | urgentTel|  String| 紧急联系人电话  从通讯录选择|
>> | urgentRelation|  String| 紧急联系人关系传获取到的列表的vlaue  下拉框选择|
>>- **返回参数**
>>```javascript
>>{
>>   result:0
>> }
>> ```
>> ##### 3.4.5 获取学生资源下拉列表
>>- **请求URL**
>>     /app/getStudentSelect
>>- **请求参数**
>>  暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 学历
>>   studyLevel:[
>>     {
>>        text: "初中",
>>        value: "cz",
>>     },
>>     {
>>        text: "高中",
>>        value: "gz",
>>     },
>>     {
>>        text: "本科",
>>        value: "bk",
>>     }
>>   ],
>>   // 学制
>>   schoolSystem:[
>>     {
>>        text: "全日制",
>>        value: "qrz",
>>     },
>>     {
>>        text: "非全日制",
>>        value: "fqrz",
>>     }
>>   ]
>> }
>> ```
>> ##### 3.4.6 获取学生信息
>>- **请求URL**
>>     /app/getStudentInfo
>>- **请求参数**
>>  ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   schoolName: "清华大学", // 学校名 
>>   province: "xxx-xxx-xxx", // 省市区
>>   detailAddress: "幸福里小区"， //详细地址 
>>   goSchoolOfDate: "2011-10-10",  // 入学时间
>>   studyLevel: "本科", //学历
>>   schoolSystem: "全日制" //学制
>> }
>> ```
>> ##### 3.4.7 设置学生信息
>>- **请求URL**
>>     /app/getStudentInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | schoolName|  String| 学校名 用户输入|
>> | province|  String| 省市区 用户选择|
>> | detailAddress|  String| 详细地址 用户输入|
>> | goSchoolOfDate|  String| 入学时间  用户选择|
>> | studyLevel|  String| 在读学历  用户选择|
>> | schoolSystem|  String| 学制 选择|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>> }
>> ```
>> ##### 3.4.8 获取单位信息
>>- **请求URL**
>>     /app/getWorkInfo
>>- **请求参数**
>>  ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   workName: "阿里巴巴", // 单位名称 
>>   province: "xxx-xxx-xxx", // 省市区
>>   detailAddress: "幸福里小区"， //街道 
>>   tel: "13897979797"  //单位电话
>> }
>> ```
>> ##### 3.4.9 获取单位信息
>>- **请求URL**
>>     /app/setWorkInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | workName|  String| 单位名 用户输入|
>> | province|  String| 省市区 用户选择|
>> | detailAddress|  String| 详细地址 用户输入|
>> | tel|  String| 单位电话  用户输入|
>>- **返回参数**
>>```javascript
>>{
>>   result：0
>> }
>> ```
----