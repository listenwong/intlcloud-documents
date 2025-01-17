## 1. API Description

API request domain name: as.tencentcloudapi.com.

This API (DescribeAutoScalingActivities) describes on or more scaling activities for the specified scaling group.

Default API request frequency limit: 20 times/second.

Note: This API supports financial availability zones. Because financial availability zones and non-financial availability zones are isolated. When specifying a financial availability zone (e.g., ap-shanghai-fsi) in the Region (a common parameter), you should also choose the financial availability zone preferably in the same region as that one specified in Region for the domain, such as as.ap-shanghai-fsi.tencentcloudapi.com.



## 2. Input Parameters

The following parameters are required for requesting this API, including action-specific parameters and common parameters. For more information about common parameters for all requests, see [Common Request Parameters](/document/api/377/30987).

| Parameter name | Required | Type | Description |
|---------|---------|---------|---------|
| Action | Yes | String | Common parameter; the name of this API: DescribeAutoScalingActivities |
| Version | Yes | String | Common parameter; the version of this API: 2018-04-19 |
| Region | Yes | String | Common parameters; for details, see the [Region List](/document/api/377/30987#.E5.9C.B0.E5.9F.9F.E5.88.97.E8.A1.A8). |
| ActivityIds.N | No | Array of String | Query by one or more scaling activity IDs. Scaling activity ID example: `asa-5l2ejpfo`. The upper limit per request is 100. The parameter does not support specifying both `ActivityIds` and `Filters` at the same time. |
| Filters.N | No | Array of [Filter](/document/api/377/31018#Filter) | Filter. <br/><li> auto-scaling-group-id - String - Required: No - (Filter) Filter by scaling group ID. </li><li> activity-status-code - String - Required: No - (Filter) Filter by scaling activity status. (INIT: initializing &#124; RUNNING: running &#124; SUCCESSFUL: succeeded &#124; PARTIALLY_SUCCESSFUL: partially succeeded &#124; FAILED: failed &#124; CANCELLED: canceled) </li><li> activity-type - String - Required: No - (Filter) Filter by scaling activity type. (SCALE_OUT: scale-out &#124; SCALE_IN: scale-in &#124; ATTACH_INSTANCES: adding an instance &#124; REMOVE_INSTANCES: terminating an instance &#124; DETACH_INSTANCES: removing an instance &#124; TERMINATE_INSTANCES_UNEXPECTEDLY: terminating an instance in the CVM console &#124; REPLACE_UNHEALTHY_INSTANCE: replacing an unhealthy instance &#124; UPDATE_LOAD_BALANCERS: updating a load balancer) </li><li> activity-id - String - Required: No - (Filter) Filter by scaling activity ID. </li><br/>The maximum number of `Filters` per request is 10. The upper limit for `Filter.Values` is 5. The parameter does not support specifying both `ActivityIds` and `Filters` at the same time. |
| Limit | No | Integer | Number of returned results, 20 by default, up to 100. For more information about `Limit`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |
| Offset | No | Integer | Offset, 0 by default. For more information about `Offset`, see the relevant section in the API [overview](https://cloud.tencent.com/document/api/213/15688). |

## 3. Output Parameters

| Parameter name | Type | Description |
|---------|---------|---------|
| TotalCount | Integer | Number of eligible scaling activities. |
| ActivitySet | Array of [Activity](/document/api/377/31018#Activity) | Information set of eligible scaling activities. |
| RequestId | String | The ID of the request. Each request returns a unique ID. The RequestId is required to troubleshoot issues. |

## 4. Sample

### Using Filters to View the Scaling Activity List

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&Filters.0.Name=activity-id
&Filters.0.Values.0=asa-o4v87ae9
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "TotalCount": 1,
        "ActivitySet": [
            {
                "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
                "AutoScalingGroupId": "asg-2umy3jbd",
                "ActivityRelatedInstanceSet": [
                    {
                        "InstanceId": "ins-q3ss14yo",
                        "InstanceStatus": "SUCCESSFUL"
                    }
                ],
                "ActivityType": "SCALE_OUT",
                "ActivityId": "asa-o4v87ae9",
                "StartTime": "2018-11-20T08:33:56Z",
                "CreatedTime": "2018-11-20T08:33:56Z",
                "EndTime": "2018-11-20T08:34:52Z",
                "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
                "StatusMessageSimplified": "Success",
                "StatusMessage": "Success",
                "StatusCode": "SUCCESSFUL"
            }
        ],
        "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
    }
}
```

### Querying Scaling Activity List by Scaling Activity ID

#### Input Sample Code

```
https://as.tencentcloudapi.com/?Action=DescribeAutoScalingActivities
&ActivityIds.0=asa-o4v87ae9
&<Common request parameter>
```

#### Output Sample Code

```
{
    "Response": {
        "TotalCount": 1,
        "ActivitySet": [
            {
                "Description": "Activity was launched in response to a difference between desired capacity and actual capacity, scale out 1 instance(s).",
                "AutoScalingGroupId": "asg-2umy3jbd",
                "ActivityRelatedInstanceSet": [
                    {
                        "InstanceId": "ins-q3ss14yo",
                        "InstanceStatus": "SUCCESSFUL"
                    }
                ],
                "ActivityType": "SCALE_OUT",
                "ActivityId": "asa-o4v87ae9",
                "StartTime": "2018-11-20T08:33:56Z",
                "CreatedTime": "2018-11-20T08:33:56Z",
                "EndTime": "2018-11-20T08:34:52Z",
                "Cause": "Activity was launched in response to a difference between desired capacity and actual capacity.",
                "StatusMessageSimplified": "Success",
                "StatusMessage": "Success",
                "StatusCode": "SUCCESSFUL"
            }
        ],
        "RequestId": "1082ab5d-c985-4d8c-bb9d-0d05e282b4a7"
    }
}
```


## 5. Developer Resources

### API Explorer

**This tool provides various capabilities such as online call, signature verification, SDK code generation, and quick API retrieval that significantly reduce the difficulty of using TencentCloud API.**

* [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer?Product=as&Version=2018-04-19&Action=DescribeAutoScalingActivities)

### SDK

TencentCloud API 3.0 integrates software development toolkits (SDKs) that support various programming languages to make it easier for you to call the APIs.

* [Tencent Cloud SDK 3.0 for Python](https://github.com/TencentCloud/tencentcloud-sdk-python)
* [Tencent Cloud SDK 3.0 for Java](https://github.com/TencentCloud/tencentcloud-sdk-java)
* [Tencent Cloud SDK 3.0 for PHP](https://github.com/TencentCloud/tencentcloud-sdk-php)
* [Tencent Cloud SDK 3.0 for Go](https://github.com/TencentCloud/tencentcloud-sdk-go)
* [Tencent Cloud SDK 3.0 for NodeJS](https://github.com/TencentCloud/tencentcloud-sdk-nodejs)
* [Tencent Cloud SDK 3.0 for .NET](https://github.com/TencentCloud/tencentcloud-sdk-dotnet)

### TCCLI

* [Tencent Cloud CLI 3.0](https://cloud.tencent.com/document/product/440/6176)

## 6. Error Codes

The following error codes are API business logic-related. For other error codes, see [Common Error Codes]

| Error Code | Description |
|---------|---------|
| InternalError | Internal error |
| InvalidParameter.Conflict | Parameters that cannot co-exist are specified at the same time. |
| InvalidParameterValue.Filter | Invalid filter. |
| InvalidParameterValue.LimitExceeded | The value exceeds the limit. |
