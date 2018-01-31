
## 接口文档 ##
### 1、登录页面 
#### 用户登录
- **请求URL**
> /app/login
- **请求参数**
>
 | 请求参数      |     参数类型 |   参数说明   |
| :-------- | :--------| :------ |
| phone|  String|  取登录框的电话号码，不能为空|
| password|   String|  取登录框的密码，不能为空|
- **返回参数**
```javascript
{
  // 登录结果
  result: 0, // 0成功，其他失败
  userId: "XXXX", // 用户ID
  // 是否认证状态有0：未激活 1：已激活
  cerStatus: 0,
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
  // 服务器返回来的验证码，须告知短信的规则，前端便于获取验证码，一般客户端会做60S等待
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
| jtNubmer|  Number|  推荐人的手机号码 非必填|
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
>> ##### 3.1.1 获取贷款的字典信息
>>- **请求URL**
>>     /app/getLoanline
>>- **请求参数**
>> -暂无
>>- **返回参数**
>>```javascript
>>{
>>  // 套餐选择
>>  prodList: [
>>    {
>>       productId: "111", // 贷款项目编号
>>       productName: "青年套餐", // 贷款项目名称
>>       minArea: 5000.00, // 可贷款最小区间
>>       maxArea: 8000.00, // 可贷款最大区间
>>       repayArea: "6"     // 还款期限后台设定，前端仅做展示
>>       repayType:0,      //还款类型 （0:按日还款，1：按天还款，2：按月还款）
>>       repayMode:0,        //还款方式(0:本息同还)
>>       coverCharges：2000,     //服务费
>>       interestRate：1.5,      //利率
>>       interestType：0,         //利率类型（0：按日计息，1：按月计息，2：按季计息，3：按年计息）
>>       overdueInterestRate：5.5, //逾期利率
>>       description：幸福贷3号      //说明
>>    }，
>>    {
>>       productId: "111", // 贷款项目编号
>>       productName: "青年套餐", // 贷款项目名称
>>       minArea: 5000.00, // 可贷款最小区间
>>       maxArea: 8000.00, // 可贷款最大区间
>>       repayArea: "6"     // 还款期限后台设定，前端仅做展示
>>       repayType:0,      //还款类型 （0:按日还款，1：按天还款，2：按月还款）
>>       repayMode:0,        //还款方式(0:本息同还)
>>       coverCharges：2000,     //服务费
>>       interestRate：1.5,      //利率
>>       interestType：0,         //利率类型（0：按日计息，1：按月计息，2：按季计息，3：按年计息）
>>       overdueInterestRate：5.5, //逾期利率
>>       description：幸福贷3号      //说明
>>    }
>>  ]
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
>> | productId|  String|  产品id 必填|
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
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | currentPage|  Number|  获取第几页参数，第一次默认第一页 必填|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>>   // 借款列表 取当前用户的所有借款列表
>>   list: [
>>     {
>>        productId: "xxx", // 借款套餐id 
>>        status:0,  //借款状态  0审核中，1：已生效，-1：未通过
>>        loanId: "20180101",  //借款编号
>>        totalLoanMoney: "50000.00" // 贷款总额
>>     },
>>     {
>>        productId: "xxx", // 借款套餐id 
>>        status: 1,   //借款状态。  0审核中，1：已生效，-1：未通过
>>        loanId: "20180101",  //借款编号
>>        totalLoanMoney: "50000.00", // 贷款总额
>>        lessLoanMoney:"3000.00",   // 贷款余额
>>        issuesNumber: "5期",         //已还第几期
>>        totalNumber: "12",         //共多少期
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
>>   productId: "xxx", // 借款套餐id 
>>   loanId: "JKBH-20171207", //借款编号
>>   loanDate: "2017.12.07",  // 借款日期
>>   loanMoney: "8000.00",  // 贷款金额
>>   replayLoanType: 0, // 还款类型 0:按日还款 1:按月还款 2:按年还款
>>   serverFee: "50.00",       // 服务费
>>   interestRate: "1.5%",     //利率
>>   loanStatus: 0,  // 贷款状态 
>>   reloanTimes: "12",   // 还款期数
>>   hasloanTimes: "5",   // 已还期数
>>   ownMoney: "5000.00",   // 尚欠金额
>>   description: "吧啦啦啦", // 抵押说明
>>   sales: "张三",   // 业务员  
>>   salesTel: "13797979797", // 业务员电话 
>>   activeDate: "2017-12-10",      // 生效日期 
>>   repaymentAccount："6214 **** **** 5533", //还款账号
>>   repaymentBankText: "招商银行"
>> }
>>```
>##### 3.3 还款记录
>> ##### 3.3.1 还款记录
>>- **请求URL**
>>     /app/getRepaymentlist
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | currentPage|  Number|  获取第几页参数，第一次默认第一页 必填|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0,
>>   //还款列表
>>   list: [
>>     {
>>        productId: "xxx", // 借款套餐id 
>>        loanId: "JKBH-20171207", //借款编号
>>        loanDate: "2017.12.07",  // 借款日期
>>        activeDate: "2017-12-10",      // 生效日期
>>        totalLoanMoney: "50000.00", // 贷款总额
>>        lessLoanMoney:"3000.00",   // 贷款余额
>>        reloanTimes: "12",   // 还款期数
>>        hasloanTimes: "5",   // 已还期数
>>     },
>>     {
>>        productId: "xxx", // 借款套餐id 
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
>>   productId: "xxx", // 借款套餐id 
>>   hasTotalRepayment: "8000.00", // 已还款
>>   currentRepayment: "1000.00",  //本期应还
>>   repaymentDateLine: "2017-12-11",  // 还款期限
>>   totalCapital: "10000.00",     // 本金
>>   totalBreakMoney: "100.00",    // 违约金
>>   totalInterest: "100.00",      // 利息
>>   totalServerFee: "20.00",      // 服务费
>>   currentRepaymentTimes: "5",  // 本期期数
>>   lessRepaymentTimes: "7",    // 剩余期数
>>   description: "" //补充描述
>>   // 已还款记录列表
>>   recordList: [
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        overDay: 1, // 逾期天数
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        overDay: 1, // 逾期天数
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        overDay: 1, // 逾期天数
>>        status: "已结清", // 状态
>>        capital: "10000.00", // 本金
>>        interest: "0.00",  // 利息
>>        breakMoney: "100.00",    // 违约金
>>        serverFee: "20.00" // 服务费
>>     },
>>     {
>>        date: "2017.10.11",  // 日期
>>        totalMoney: "2000.00", // 总金额
>>        overDay: 1, // 逾期天数
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
>>   //激活状态 0没激活，1已激活
>>   status: "1", // 认证状态
>>   statusText: "已激活", // 已经认证 
>>  // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   idStatus: "",    // 身份状态
>>   contactStatus: "", // 联系人信息认证状态
>>   unitStatus: "",  // 单位或学校认证状态
>>   customerType: 0, // 0：已工作  1：学生  -1不知道身份
>>   // 只有三个状态 0：未认证；  2：已认证；-1：认证失败 
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
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 身份状态
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
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 联系人状态
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
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 学生信息状态
>>   schoolName: "清华大学", // 学校名 
>>   province: "xxx-xxx-xxx", // 省份
>>   city: "xxx", //市
>>   area: "xxx", // 区or县
>>   detailAddress: "幸福里小区"， //详细地址 
>>   goSchoolOfDate: "2011-10-10",  // 入学时间
>>   studyLevel: "本科", //学历
>>   schoolSystem: "全日制" //学制
>> }
>> ```
>> ##### 3.4.7 设置学生信息
>>- **请求URL**
>>     /app/setStudentInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | schoolName|  String| 学校名 用户输入|
>> | province|  String| 省 用户选择|
>> | city|  String| 市 用户选择|
>> | area|  String| 区 用户选择|
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
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 单位信息状态
>>   workName: "阿里巴巴", // 单位名称 
>>   province: "xxx-xxx-xxx", // 省份
>>   city: "xxx", //市
>>   area: "xxx", // 区or县
>>   detailAddress: "幸福里小区"， //街道 
>>   tel: "13897979797"  //单位电话
>> }
>> ```
>> ##### 3.4.9 设置单位信息
>>- **请求URL**
>>     /app/setWorkInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | workName|  String| 单位名 用户输入|
>> | province|  String| 省 用户选择|
>> | city|  String| 市 用户选择|
>> | area|  String| 区 用户选择|
>> | detailAddress|  String| 详细地址 用户输入|
>> | tel|  String| 单位电话  用户输入|
>>- **返回参数**
>>```javascript
>>{
>>   result：0
>> }
>> ```
>> ##### 3.4.10 获取更多认证信息
>>- **请求URL**
>>     /app/getMoreStatusInfo
>>- **请求参数**
>> --- 暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 枚举类型 根据后台实现进行约定
>>   bankAccountStatus: "0", // 银行账号认证状态 已认证、未认证
>>   qqStatus: "0",       // QQ认证状态 
>>   weixinStatus: "0",   // 微信认证状态
>>   addressStatus: "0",  // 住址认证状态
>>}
>> ```
>> ##### 3.4.11 获取银行数据字典信息
>>- **请求URL**
>>     /app/getBankList
>>- **请求参数**
>> --- 暂无
>>- **返回参数**
>>```javascript
>>{
>>   list: [
>>      {
>>         text:"工商银行"，
>>         value:"ICBC"
>>      },
>>      {
>>         text:"中国银行"，
>>         value:"BOC"
>>      },
>>      {
>>         text:"招商银行"，
>>         value:"CMB"
>>      }
>>   ]
>>}
>> ```
>> ##### 3.4.12 获取当前用户的银行账号信息
>>- **请求URL**
>>     /app/getUserOfBank
>>- **请求参数**
>> --- 暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 银行账号状态
>>   payeeUser: "张三",  // 收款人姓名
>>   payeeAccount: "4562 4551 5623 7813", // 收款人账号
>>   payeeBankName: "工商银行",    //收款账号所属银行
>>   payeeBankCode: "ICBC",   // 所属银行代码
>>   repaymentUser： "李四", // 还款人姓名
>>   repaymentAccount: "4562 4551 5623 7813", // 还款人账号
>>   repaymentBankName: "工商银行",    //还款账号所属银行
>>   repaymentBankCode: "ICBC",   // 所属银行代码
>>}
>> ```
>> ##### 3.4.13 设置当前用户银行账号信息
>>- **请求URL**
>>     /app/setUserOfBank
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | payeeUser|  String| 收款人姓名 用户输入|
>> | payeeAccount|  String| 收款人账号 用户输入|
>> | payeeBankName|  String| 所属银行 用户选择|
>> | repaymentUser|  String| 还款人账号 用户输入|
>> | repaymentAccount|  String| 还款账号所属银行 用户输入|
>> | repaymentBankName|  String| 所属银行 用户选择|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0
>>}
>> ```
>> ##### 3.4.14 获取当前用户QQ账号信息
>>- **请求URL**
>>     /app/getQQInfo
>>- **请求参数**
>> ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 认证状态
>>   QQ: "555544443333" // QQ账号
>>}
>> ```
>> ##### 3.4.15 设置当前用户QQ账号信息
>>- **请求URL**
>>     /app/setQQInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | qq|  String| QQ账号 用户输入，后台注意成功后QQ的认证状态|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0 // QQ账号
>>}
>> ```
>> ##### 3.4.16 获取当前用户微信账号信息
>>- **请求URL**
>>     /app/getWeixinInfo
>>- **请求参数**
>> ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 认证状态
>>   weixin: "555544443333" // 微信账号
>>}
>> ```
>> ##### 3.4.17 设置当前用户微信账号信息
>>- **请求URL**
>>     /app/setWeixinInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | weixin|  String| weixin账号 用户输入，后台注意成功后weixin的认证状态|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0 // 
>>}
>> ```
>> ##### 3.4.18 获取当前用户住址信息
>>- **请求URL**
>>     /app/getAddressInfo
>>- **请求参数**
>> ---暂无
>>- **返回参数**
>>```javascript
>>{
>>   // 0：未认证；1：认证中  2：已认证；-1：认证失败 
>>   status: "",    // 认证状态
>>   address: "湖南省长沙市岳麓区xxxxxx" // 地址
>>}
>> ```
>> ##### 3.4.19 设置当前用户QQ账号信息
>>- **请求URL**
>>     /app/setAddressInfo
>>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | address|  String| 地址 用户输入|
>>- **返回参数**
>>```javascript
>>{
>>   result: 0 // 
>>}
>> ```
----

### 4、发现模块
>#### 4.1 获取发现模块信息
>- **请求URL**
> /app/getFindInfo
>- **请求参数**
>> 暂无
>- **返回参数**
>```javascript
>{
>  list: [
>    {
>      type: "1", // 1 是抽奖消息，2活动
>      newsId: "0317", // 编号
>      title: "幸运大转盘"，
>      simpleText: "你是否时常感觉工作时间不够？原有的事情完不成，又有新的任务下达？你是否永远因为解决紧急的突发事件推迟了本有的工作，导致本有的工作完不成？",  // 简单描述
>      img: "http://images.xxx.com/sss/1.png",  // 图片地址
>      date: "2017-12-12",
>      isDraw: 0  // 0没抽过，1已抽过奖
>    },
>    {
>      type: "2", // 1 是抽奖消息，2活动
>      newsId: "0317", // 编号
>      title: "这是一条普通的系统公告"，
>      simpleText: "你是否时常感觉工作时间不够？原有的事情完不>成，又有新的任务下达？你是否永远因为解决紧急的突发事件推>迟了本有的工作，导致本有的工作完不成？",  // 简单描述
>      img: "http://images.xxx.com/sss/1.png",  // 图片地址
>      date: "2017-12-12"，
>      isDraw: 0  // 0没抽过，1已抽过奖
>    }
>  ]
>}
>```
>#### 4.2 获取抽奖内容
>- **请求URL**
>> /app/getPrizeList
>- **请求参数**
>> 暂无
>- **返回参数**
>```javascript
>{
>  list: [
>    "50M免费流量包",
>    "10元",
>    "谢谢参与",
>    "5元",
>    "10M免费流量包",
>    "20M免费流量包",
>    "20元 ",
>    "30M免费流量包",
>    "100M免费流量包",
>    "2元"
>  ]
>}
>```
>#### 4.3 获取抽奖结果
>- **请求URL**
>> /app/getPrizeIndex
>- **请求参数**
>> 暂无
>- **返回参数**
>```javascript
>{
>    index: x // 这里的xx是根据奖品列表来的，如果奖品有10个，则 x属于[1,10]的区间
>}
>```
>#### 4.4 获取普通公告详情
>> 此处和系统公告共用同一个接口
----
### 5、我的模块
> #### 5.1获取我的模块信息
>- **请求URL**
>> /app/getMyInfo
>- **请求参数**
>> 暂无
>- **返回参数**
>```javascript
>{
>   user: "张三", //用户
>   userId: "xd00001", //用户ID
>   userPhone: "13544445555", // 手机号
>   balance: "5000.00", // 余额
>   uReadMymsg:"5" // 个人未读消息个数 
>   uReadSysmsg: "2",   // 系统未读消息个数
>   userStatus: 0    // 激活状态
>}
>```
> #### 5.2 获取系统公告列表
>- **请求URL**
>> /app/getSysMsgList
>- **请求参数**
>
>> | 请求参数 | 参数类型 | 参数说明 |
>> | :-------- | :--------| :------ |
>> | currentPage| Number| 获取第几页参数，第一次默认第一页 必填|
>- **返回参数**
>```javascript
>{
>   list: [
>      {
>        msgId:"1111", //消息ID
>        msgTitle: "系统消息一",
>        msgIntroduction: "这是一条系统消息的简讯",
>        date: "2017-12-12"
>      },
>      {
>        msgId:"1111", //消息ID
>        msgTitle: "系统消息一",
>        msgIntroduction: "这是一条系统消息的简讯",
>        date: "2017-12-12"
>      },
>      {
>        msgId:"1111", //消息ID
>        msgTitle: "系统消息一",
>        msgIntroduction: "这是一条系统消息的简讯",
>        date: "2017-12-12"
>      }
>   ]
>}
>```
>#### 5.3 获取系统公告详情
>- **请求URL**
>> /app/getSysMsgDetail
>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | msgId|  String| 消息ID,上一个页面传入|
>- **返回参数**
>```javascript
>{
>        msgId:"1111", //消息ID
>        msgTitle: "系统消息一",
>        content: "这是一条系统消息的的详情", // 建议传入富文本
>        date: "2017-12-12"
>}
>```
>#### 5.4 获取个人消息的列表
>- **请求URL**
>> /app/getMyMsgList
>- **请求参数**>
>> | 请求参数 | 参数类型 | 参数说明 |
>> | :-------- | :--------| :------ |
>> | currentPage| Number| 获取第几页参数，第一次默认第一页 必填|
>- **返回参数**
>```javascript
>{
>   list: [
>      {
>        msgId:"1111", //消息ID
>        msgType: 2, // "2" 个人还款通知； "3" 普通通知 
>        title: "还款通知",
>        content: "2017-12-25 你还需要还款 ¥500.00",
>        date: "2017-12-12"
>      },
>      {
>        msgId:"1111", //消息ID
>        msgType: 2, // "2" 个人还款通知； "3" 普通通知 
>        title: "还款通知",
>        content: "2017-12-25 你还需要还款 ¥500.00",
>        date: "2017-12-12"
>      },
>      {
>        msgId:"1111", //消息ID
>        msgType: 2, // "2" 个人还款通知； "3" 普通通知 
>        title: "还款通知",
>        content: "2017-12-25 你还需要还款 ¥500.00",
>        date: "2017-12-12"
>      }
>   ]
>}
>```
>#### 5.5 获取个人消息详情（还款）
>- **请求URL**
>> /app/getMyMsgDetail
>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | msgId|  String| 消息ID,上一个页面传入|
>- **返回参数**
>```javascript
>{
>     date: "2017-10-10", //消息时间
>     msgType: 2, // "2" 个人还款通知； "3" 普通通知 
>     title: "还款通知",
>     msgShort:"", // 简介
>     content: "2017-12-25 你还需要还款 ¥500.00", //消息内容
>     capital: "10000.00",     // 本金
>     breakMoney: "100.00",    // 违约金
>     interest: "100.00",      // 利息
>     serverFee: "20.00",      // 服务费
>     currentRepaymentTimes: "5",  // 本期期数
>     lessRepaymentTimes: "7"    // 剩余期数
>}
>```
>#### 5.6 获取意见反馈的数据字典
>- **请求URL**
>> /app/getFacebackList
>- **请求参数**
>>  暂无
>- **返回参数**
>```javascript
>{
>   list: [
>      {
>         text:"服务态度太差"，
>         value:"1"
>      },
>      {
>         text:"利息太高"，
>         value:"2"
>      },
>      {
>         text:"其他"，
>         value:"3"
>      }
>   ] 
>}
>```
>#### 5.7 提交意见反馈内容
>- **请求URL**
>> /app/submitFaceBack
>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | type|  String| 反馈类型,从后台拿|
>> | content|  String| 补充信息 用户输入|
>> | img|  String| 图片地址,提交base64数据，后台返回来地址|
>- **返回参数**
>```javascript
>{
>   result:0
>}
>```
>#### 5.8 修改密码
>- **请求URL**
>> /app/restPwd
>- **请求参数**
>> 
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | oldPwd|  String| 用户输入|
>> | newPwd|  String| 用户输入|
>- **返回参数**
>```javascript
>{
>   result:0
>}
>```
>#### 5.9 图片上传
>- **请求URL**
>> /app/uploadfile
>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | fileName|  String| 图片名称|
>> | stream|  String| base64数据流|
>- **返回参数**
>```javascript
>{
>   url: "" // 图片地址
>}
>```
>#### 5.10 注销
>- **请求URL**
>> /app/logOut
>- **请求参数**
>> 暂无
>- **返回参数**
>```javascript
>{
>   result:0
>}
>```
### 6 升级检测接口
- **请求URL**
> /app/getLastedVersion
- **请求参数**

 | 请求参数      |     参数类型 |   参数说明   |
 | :-------- | :--------| :------ |
 | MachineType|  iOS或Android| 传平台的值|
- **返回参数**
```javascript
{
   title:"版本更新",
   version:"0.0.1",
   note: "更新点说明",
   url: "更新下载地址"
}
```
### 7 默默上传的接口
>#### 7.1 经纬度上传接口
> - **请求URL**
>> /app/submitGeo
>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | longitude|  String| 经度|
>> | latitude|  String| 纬度|
>- **返回参数**
>```javascript
>{
>   result: 0 
>}
>```
>#### 7.2 短信上传接口
> - **请求URL**
>> /app/submitMessage
>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | phone|  Number| 电话号码(待确认，看能否拿到~)|
>> | content|  String| 短信内容|
>> | type|  (in/out)String| 接收还是发送 |
>- **返回参数**
>```javascript
>{
>   result: 0 
>}
>```
>#### 7.3 通讯录上传接口
> - **请求URL**
>> /app/submitContact
>- **请求参数**
>>
>> | 请求参数      |     参数类型 |   参数说明   |
>> | :-------- | :--------| :------ |
>> | contacts|  String| 通讯录的数组对象序列化|
>
>- **返回参数**
>```javascript
>{
>   result: 0 
>}
>```
>#### 7.4 获取服务器当前时间
> - **请求URL**
>> /app/getServerTime
>- **请求参数**
>>
>> 暂无
>
>- **返回参数**
>```javascript
>{
>   timestamp: 1516893149668 
>}
>```
