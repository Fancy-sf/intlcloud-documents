## 功能描述
会话里面已经发送成功的消息，会话内任意成员可以针对消息做二次修改。消息修改成功后会同步给会话的全部成员。

## 变更消息

变更消息的接口。变更成功后，自己和对端用户（C2C）或群组成员（Group）都会收到 [MESSAGE_MODIFIED](https://web.sdk.qcloud.com/im/doc/en/module-EVENT.html#.MESSAGE_MODIFIED) 事件。

>!
>- v2.20.0起支持。
>- 不支持修改在线消息；不支持修改直播群消息；请勿修改消息的 random，sequence，time 等字段。
>- 只支持修改文本消息、自定义消息、地理位置消息和表情消息。
>- 如果在修改消息过程中，消息已经被其他人修改，SDK 会返回错误码2480，表示修改消息时发生冲突。

*接口**

<dx-codeblock>
:::  js

tim.modifyMessage(message);

:::
</dx-codeblock>

**参数**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| message          | Message | 消息实例 |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

// 监听 MESSAGE_MODIFIED 事件，当修改消息成功后，SDK 会派发此事件
let onMessageModified = function(event) {
  // event.data - 存储被修改过的 Message 对象的数组 - [Message]
};
tim.on(TIM.EVENT.MESSAGE_MODIFIED, onMessageModified);

// 将 txtMessage 的文本内容改为 "Hello Tencent"
txtMessage.payload.text = "Hello Tencent";

let promise = tim.modifyMessage(txtMessage);
promise.then(function(imResponse) {
  const { message } = imResponse.data;
  // 修改消息成功，message 是最新的消息
}).catch(function(imError) {
  // 修改消息失败
  const { code, data } = imError;
  if (code === 2480) {
    // 修改消息发生冲突，data.message 是最新的消息
  } else if (code === 2481) {
    // 不支持修改直播群消息
  } else if (code === 20026) {
    // 消息不存在
  }
});

:::
</dx-codeblock>