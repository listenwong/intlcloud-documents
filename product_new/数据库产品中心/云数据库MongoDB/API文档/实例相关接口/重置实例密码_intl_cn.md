## 1. 接口描述
本接口(ResetMongoDBPassword)用于重置实例密码。
接口请求域名：<font style='color:red'>mongodb.api.qcloud.com </font>

密码规则： 长度为8-16个字符；至少包含字母、数字和字符（!@#%^()）中的两种

## 2. 输入参数
以下请求参数列表仅列出了接口请求参数，正式调用时需要加上公共请求参数，见<a href='https://intl.cloud.tencent.com/document/product/213/6976' title='公共请求参数'>公共请求参数</a>页面。其中，此接口的Action字段为ResetMongoDBPassword。

| 参数名称 | 是否必选  | 类型 | 描述 |
|---------|---------|---------|---------|
| instanceId | 是 | String | 待操作的实例ID，可通过 [DescribeMongoDBInstances](https://intl.cloud.tencent.com//document/product/240/8312) 接口返回值中的 instanceId 获取。 |
| password | 是 | String | 实例新密码，密码规则：长度为8-16个字符；至少包含字母、数字和字符（!@#%^()）中的两种|

## 3. 输出参数

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| code | Int | 公共错误码, 0表示成功，其他值表示失败。详见错误码页面的<a href='https://intl.cloud.tencent.com/document/product/377/8946'>公共错误码</a>。 |
| message | String | 错误信息描述, 成功时，该值为空 |
| codeDesc | String | 业务侧错误码英文描述。成功时返回Success，错误时返回具体业务错误原因。 |
| data | Object |任务ID|

其中，data 表示任务ID，其参数构成如下：

| 参数名称 | 类型 | 描述 |
|---------|---------|---------|
| data.jobId | Int | 任务ID，可通过 [GetMongoDBJobInfo](https://intl.cloud.tencent.com//document/product/240/8310) 接口查询任务执行情况 |


## 4. 错误码
以下错误码表列出了该接口的业务逻辑错误码。

| 错误代码 | 英文提示 | 错误描述 |
|---------|---------|---------|
|11050|InvalidParameter|业务参数错误|
|11056|InstanceNotExists|没有找到对应实例|
|11057|InstanceBeenLocked|实例正被其它流程锁定，暂时不能执行该操作|
|10702|InstanceStatusAbnormal|实例状态异常,暂时不能执行该操作（比如：流程中或已隔离或已删除）|
|11059|PasswordRuleError|密码规则错误，密码必须是8-16位字符，且至少包含字母、数字和字符（!@#%^*()）中的两种|

## 5. 示例
<pre>
https://mongodb.api.qcloud.com/v2/index.php?Action=ResetMongoDBPassword
&<<a href="https://intl.cloud.tencent.com/doc/api/229/6976">公共请求参数</a>>
&instanceId=cmgo-6ozqe0uh
&password=12D3E@!r5ed
</pre>
返回示例如下：
```
{
    "code": 0,
    "message": "",
    "codeDesc": "Success",
    "data": {
        "jobId": 73605
    }
}

```