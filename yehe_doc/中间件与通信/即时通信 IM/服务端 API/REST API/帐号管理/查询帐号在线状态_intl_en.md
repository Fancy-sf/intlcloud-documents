## Feature Description
This API is used to query the current login status of a user.

## API Call Description
### Sample request URL
```
https://xxxxxx/v4/openim/query_online_status?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```


### Request parameters

The following is a list of the parameters commonly used when calling this API and their descriptions. For more parameters, see the [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter | Description |
| ------------------ | ------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com ` <li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com`|
| v4/openim/query_online_status | The request API that is used. |
| sdkappid | The SDKAppID assigned via the IM console when the application is created. |
| identifier | The value must be the app admin account. For more information, see [App Admin](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | The signature generated by the app admin account. For more information on the operation, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | The value must be a random 32-bit unsigned integer. Value range: 0 to 4294967295. |
| contenttype | Request format. The value is always `json`. |

### Maximum call frequency

This API can be called up to 200 times per second.

### Sample request packets
#### When detailed login platform information is not needed
```
{
    "To_Account":["id1","id2","id3","id4"],
}

```

#### When detailed login platform information is needed
```
{
    "IsNeedDetail": 1,
    "To_Account": ["id1", "id2", "id4"]
}
```

### Request packet fields

| Field | Type | Property | Description |
|---------|---------|---------|---------|
| To_Account | Array | Required | The one or more UserIDs whose login statuses are to be queried. This API can be used to query the login statuses of up to 500 UserIDs at a time. |
| IsNeedDetail | Integer | Optional | Specifies whether detailed login platform information is needed in the response. 0: not needed. 1: needed. |

### Sample response packet body
#### When detailed login platform information is not needed

```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0
    "QueryResult": [
        {
            "To_Account": "id1",
            "State": "Offline"
        },
        {
            "To_Account": "id2",
            "State": "Online"
        },
        {
            "To_Account": "id3",
            "State": "PushOnline"
        }
    ],
    "ErrorList": [
        {
            "To_Account": "id4",
            "ErrorCode": 70107
        }
    ]    
}

```
#### When detailed login platform information is needed
```
{
    "ActionStatus":"OK",
    "ErrorInfo":"",
    "ErrorCode": 0
    "QueryResult": [
        {
            "To_Account": "id1",
            "State": "Online",
            "Detail": [
                {
                    "Platform": "IPhone",
                    "Status": "PushOnline"
                },
                {
                    "Platform": "Web",
                    "Status": "Online"
                }
            ]
        },
        {
            "To_Account": "id2",
            "State": "Offline",
        }        
    ],
    "ErrorList": [
        {
            "To_Account": "id4",
            "ErrorCode": 70107
        }
    ]      
}
```

#### Request error
```
{
    "ActionStatus": "FAIL",
    "ErrorInfo": "Fail to Parse json data of body, Please check it",
    "ErrorCode": 90001
}
```

### Response packet fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | The processing result of the request. OK: succeeded. FAIL: failed. |
| ErrorInfo | String | Detailed information on the error. |
| ErrorCode | Integer | The error code returned for the request. <li>If the status query for any account succeed, the value is 0.</li><li>If the query for all the accounts failed, the return value is not 0.</li> |
| QueryResult | Array | The returned structured information of the login status of the user. |
| QueryResult.To_Account | String | The UserID of the user whose status is returned. |
| QueryResult.Status | String | The returned login status. Valid values: <ul style="margin:0;"><li>Online: after the user logs in to the client, the client remains in a persistent connection with the IM backend.</li><li>PushOnline: the client enters the PushOnline state when the iOS or Android process is disconnected due to a network error or is killed by the operating system. In this state, the client still can receive offline messages. However, if the client’s process is not terminated by the operating system after the client is switched to the background, the client is in Online state.</li><li>Offline: the user has logged out of the client properly or has not logged in to the client for at least 7 days since the last login.</li></ul>If the user logs in to the client on multiple devices, the value is Online provided that the client is in the Online state on any device. |
| QueryResult.Detail | Object | The detailed information on the login platform. |
| QueryResult.Detail.Platform | String | The type of the login platform. Valid values: "iPhone",  "Android",  "Web",  "PC", "iPad", and "Mac".  || QueryResult.Detail.Status | String | The status of the login platform. |
| ErrorList | Array | The list of accounts whose statuses failed to be queried. The target accounts in this list were not found or their statuses failed to be queried. If the status query for all accounts succeeded, the value of the ErrorList field is blank. |
| ErrorList.To_Account | String | The target account whose status failed to be queried. |
| ErrorList.ErrorCode | Integer | The error code indicating that the status query failed. If the error code for a target account is 70107, the account was not found. |

>!The IM backend stores the PushOnline state for only 7 days. If a user has not logged in to the client within 7 days since the previous login, the user enters the Offline state.

## Error Codes
The HTTP return code for this API is 200 unless an network error such as error 502 occurs. The actual error code and error information are indicated by ErrorCode and ErrorInfo respectively in the response packet body.
For public error codes 60000 to 79999, see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The private error codes for this API are as follows:

| Error Code | Description |
|---------|---------|
| 70107 | The requested UserID does not exist. |
| 70169 | The server timed out. Try again later. |
| 90001 | JSON format parsing failed. Check whether the request packet meets the JSON specification, or whether To_Account is a null array. |
| 90003 | The value of the To_Account field in the JSON format request packet does not meet the message format requirements. Please check whether the type of the To_Account field is String. |
| 90009 | The request requires the app admin’s permissions. |
| 90011 | The number of target accounts to which the message is to be sent exceeds 500. Reduce the number of target accounts in To_Account. |
| 90992 | The backend service timed out. Please try again. |
| 90994 | An internal service error occurred. Please try again. |
| 90995 | An internal service error occurred. Please try again. |
| 91000 | An internal service error occurred. Please try again. |

## API Debugging Tool
To debug this API, you can use the [Online RESTful API Debugging Tool](https://tcc.tencentcs.com/im-api-tool/#/v4/openim/admin_msgwithdraw?locale=en-US).

## References

- Importing an Account ([v4/im_open_login_svc/account_import](https://intl.cloud.tencent.com/document/product/1047/34953))
- Batch Importing Multiple Accounts ([v4/im_open_login_svc/multiaccount_import](https://intl.cloud.tencent.com/document/product/1047/34954))
- Deleting an Account ([v4/im_open_login_svc/account_delete](https://intl.cloud.tencent.com/document/product/1047/34955))
- Querying an Account ([v4/im_open_login_svc/account_check](https://intl.cloud.tencent.com/document/product/1047/34956))
- Invalidating the Login Status of an Account ([v4/im_open_login_svc/kick](https://intl.cloud.tencent.com/document/product/1047/34957))
