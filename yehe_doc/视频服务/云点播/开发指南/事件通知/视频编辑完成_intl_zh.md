## 事件名称
EditMediaComplete

## 事件说明
当 App 配置了事件通知，并且在编辑视频完成后，App 后台即可通过“普通回调”或“可靠回调”的方式获取该事件通知。事件通知内容为 [EditMediaTask 结构](https://intl.cloud.tencent.com/document/product/266/34187#EditMediaTask)。

## 示例
### 普通回调
如果选择普通回调模式，则回调 URL 会接收到来自云点播的 HTTP 请求。请求采用 POST 方法，请求内容在 BODY 中，如下所示（省略了值为 null 的字段）。

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaCompleteEvent":{
        "TaskId":"1256768367-EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "Input":{
            "InputType":"File",
            "FileInfoSet":[
                {
                    "FileId":"24961954183381008",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381009",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381010",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                }
            ]
        },
        "Output":{
            "FileType":"mp4",
            "FileId":"24961954183923290",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        },
        "ProcedureTaskId":""
    }
}
```


### 可靠回调
如果选择可靠回调模式，调用 [拉取事件通知](https://www.tencentcloud.com/document/product/266/34183) API 会接收到如下形式的 HTTP 应答（省略了值为 null 的字段）。

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandle.N",
				"EventType": "EditMediaComplete",
				"EditMediaCompleteEvent": {
        			"TaskId": "EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        			"Status": "FINISH",
        			"ErrCode": 0,
        			"Message": "SUCCESS",
        			"Input": {
						"InputType": "File",
						"FileInfoSet": [
							{
								"FileId": "24961954183381008",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381009",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381010",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							}
						]
					},
        			"Output": {
						"FileType": "mp4",
						"FileId": "24961954183923290",
						"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
					},
        			"ProcedureTaskId": ""
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
