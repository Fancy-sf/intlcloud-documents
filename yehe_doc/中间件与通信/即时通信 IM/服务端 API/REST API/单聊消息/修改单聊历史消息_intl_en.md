## API Calling Description

- This API is used by the admin to modify historical one-to-one messages.
- You can modify the `MsgBody` and `CloudCustomData` fields individually or at the same time for a message by overwriting the field values in a historical message with those specified in requests.
- You can obtain the `MsgKey` of the one-to-one message to modify by the following means:
	- Enable [callback before sending a one-to-one message](https://intl.cloud.tencent.com/document/product/1047/34364) or [callback after sending a one-to-one message](https://intl.cloud.tencent.com/document/product/1047/34365) to record the `MsgKey` of each one-to-one message.
	- Use the [API for querying one-to-one messages](https://intl.cloud.tencent.com/document/product/1047/35478) to query the `MsgKey` of the one-to-one message to modify.
	- For one-to-one messages sent through the RESTful APIs for [sending one-to-one messages to one user](https://intl.cloud.tencent.com/document/product/1047/34919) and [sending one-to-one messages to multiple users](https://intl.cloud.tencent.com/document/product/1047/34920), the message `MsgKey` is contained in response packets.

>!Messages modified by this API cannot be restored.

### Sample request URL

```
https://xxxxxx/v4/openim/modify_c2c_msg?sdkappid=88888888&identifier=admin&usersig=xxx&random=99999999&contenttype=json
```

### Request parameters

The following table describes only the modified parameters when this API is called. For other parameters, see [RESTful API Overview](https://intl.cloud.tencent.com/document/product/1047/34620).

| Parameter                    | Description                                                         |
| ------------------------- | ------------------------------------------------------------ |
| https       | The request protocol is HTTPS, and the request method is POST.       |
| xxxxxx  | The country/region where your SDKAppID is located.<li>China:  `console.tim.qq.com `<li>Singapore:  `adminapisgp.im.qcloud.com `<li>Seoul: `adminapikr.im.qcloud.com`<li>Frankfurt: `adminapiger.im.qcloud.com`<li>India: `adminapiind.im.qcloud.com` || v4/openim/modify_c2c_msg | Request API                                                     |
| sdkappid | SDKAppID assigned by the IM console when an app is created |
| identifier | App admin account. For more information, see the **App Admin** section in [Login Authentication](https://intl.cloud.tencent.com/document/product/1047/33517). |
| usersig | Signature generated by the app admin account. For operation details, see [Generating UserSig](https://intl.cloud.tencent.com/document/product/1047/34385). |
| random | A random 32-bit unsigned integer ranging from 0 to 4,294,967,295 |
| contenttype   |Request format, which should always be `json`.|

### Maximum call frequency

200 calls per second

### Sample request

#### Modifying only the `MsgBody` information of the message object
```
{
	"From_Account": "dramon1",
	"To_Account": "dramon2",
	"MsgKey": "1_2_3",
	"MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hello"
            }
        }
    ]
}

```

#### Modifying only the `CloudCustomData` information of the message object
```
{
	"From_Account": "dramon1",
	"To_Account": "dramon2",
	"MsgKey": "1_2_3",
    "CloudCustomData": "your cloud custom data"
}

```

#### Modifying both the `MsgBody` and `CloudCustomData` information of the message object
```
{
	"From_Account": "dramon1",
	"To_Account": "dramon2",
	"MsgKey": "1_2_3",
	"MsgBody":[
        {
            "MsgType": "TIMTextElem",
            "MsgContent":{
                "Text": "hello"
            }
        }
    ],
    "CloudCustomData": "your cloud custom data"
}

```

### Request fields

| Field | Type | Required | Description |
|---------|---------|----|---------|
| From_Account | String | Yes | The UserID of the message sender. |
| To_Account | String | Yes | `UserID` of the recipient |
| MsgKey | String | Yes | Unique identifier of the message to be modified. For how to obtain the `MsgKey` of the message, see the API description.  |
| MsgBody | Array | No | Message body. For details on formats, see [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527). (Note: a message can contain multiple message elements, in which case `MsgBody` is an array.) |
| CloudCustomData | String | No | Custom message data. It is saved in the cloud and will be sent to the peer end. Such data can be pulled after the app is uninstalled and reinstalled. |


#### Sample response

```
{
    "ActionStatus": "OK",
    "ErrorCode": 0,
    "ErrorInfo": "succeed"
}
```

### Response fields

| Field | Type | Description |
|---------|---------|---------|
| ActionStatus | String | Request result. `OK`: Successful; `FAIL`: Failed |
| ErrorCode| Integer | Error code. `0`: Successful; other values: Failed |
| ErrorInfo| String | Error information |

## Error Codes

The returned HTTP status code for this API is always 200 unless a network error (such as error 502) occurs. The specific error code and details can be found in the response fields `ErrorCode` and `ErrorInfo` respectively.
For public error codes (60000 to 79999), see [Error Codes](https://intl.cloud.tencent.com/document/product/1047/34348).
The following table describes the error codes specific to this API:

| Error Code | Description |
| ------------- | ------------------------------------------------------------ |
| 20001 | Invalid request. |
| 20002 | `UserSig` or `A2` has expired. |
| 20003 | The `UserID` of the sender or recipient is invalid or does not exist. Make sure that the `UserID` has been imported into IM. |
| 20004 | Network exception. Try again. |
| 20005 | Internal server error. Try again. |
| 90001 | Failed to parse the JSON request. Make sure the format is valid. |
| 90002 | The `MsgBody` in the JSON request does not meet message format requirements or `MsgBody` is not an array. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90003 | The JSON request does not contain the `To_Account` field or the `To_Account` field is not a string. |
| 90007 | The `MsgBody` field in the JSON request is not an array. Change it to an array. |
| 90009 | The request requires app admin permissions. |
| 90010 | The JSON request does not meet message format requirements. For more information, see the **Message Element TIMMsgElement** section in [Message Formats](https://intl.cloud.tencent.com/document/product/1047/33527#.E6.B6.88.E6.81.AF.E5.85.83.E7.B4.A0-timmsgelement). |
| 90012 | The account specified in `To_Account` does not exist or is not registered. Make sure the account has been imported to IM and is correct. |
| 91000 | Internal service error. Try again. |
| 90992 | Internal service error. Try again. If this error code is returned for all requests and third-party callback is enabled, make sure the app server returns the callback results to the IM backend normally. |

## API Debugging Tool

Use the [RESTful API online debugging tool](https://29294-22989-29805-29810.cdn-go.cn/api-test.html#v4/openim/modify_c2c_msg) to debug this API.

## References
Sending One-to-One Messages to Multiple Users ([v4/openim/batchsendmsg](https://intl.cloud.tencent.com/document/product/1047/34920))
Querying One-to-One messages ([v4/openim/admin_getroammsg](https://intl.cloud.tencent.com/document/product/1047/35478))
Recalling One-to-One Messages ([v4/openim/admin_msgwithdraw](https://intl.cloud.tencent.com/document/product/1047/35015))
