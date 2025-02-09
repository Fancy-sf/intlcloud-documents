## 功能描述

IM SDK 提供获取会话的接口，可以获取指定的单个、多个会话的 [Conversation](https://web.sdk.qcloud.com/im/doc/en/Conversation.html) 对象信息。

## 获取会话列表

>!
>- 该接口获取的会话列表中的资料是不完整的（仅包括头像、昵称等，能够满足会话列表的渲染需求），若要查询详细会话资料，可参考 [getConversationProfile](https://web.sdk.qcloud.com/im/doc/en/SDK.html#getConversationProfile)。
>- 客户端默认可从云端拉取100个最近联系人会话，升级旗舰版后可配置从云端拉取最多500个最近联系人会话。
>- 会话保存时长跟会话最后一条消息保存时间一致，消息默认保存7天，即会话默认保存7天。
>-  v2.15.0起支持获取指定的多个会话。

**接口**

<dx-codeblock>
:::  js

tim.getConversationList(options);

:::
</dx-codeblock>

**参数**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| options          | undefined \| Array | 参数选项。<br/><li>options 不传表示获取全部会话</li><li>options 传入数组参数表示获取指定的多个会话，且不能传入空数组</li> |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

// 获取全量的会话列表
let promise = tim.getConversationList();
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // 全量的会话列表，用该列表覆盖原有的会话列表
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // 获取会话列表失败的相关信息
});

:::
</dx-codeblock>


<dx-codeblock>
:::  js

// 获取指定的会话列表
let promise = tim.getConversationList([conversationID1, conversationID2]);
promise.then(function(imResponse) {
  const conversationList = imResponse.data.conversationList; // 缓存中已存在的指定的会话列表
}).catch(function(imError) {
  console.warn('getConversationList error:', imError); // 获取会话列表失败的相关信息
});

:::
</dx-codeblock>

## 获取会话详细资料

**接口**

<dx-codeblock>
:::  js

tim.getConversationProfile(conversationID);

:::
</dx-codeblock>


**参数**

| Name               | Type     | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| conversationID          | String | 会话 ID。会话 ID 组成方式：<br/><li>C2C${userID}（单聊）</li><li>GROUP{groupID}（群聊）</li><li>@TIM#SYSTEM（系统通知会话）</li> |

**返回值**

`Promise` 对象。

**示例**

<dx-codeblock>
:::  js

let promise = tim.getConversationProfile(conversationID);
promise.then(function(imResponse) {
  // 获取成功
  console.log(imResponse.data.conversation); // 会话资料
}).catch(function(imError) {
  console.warn('getConversationProfile error:', imError); // 获取会话资料失败的相关信息
});

:::
</dx-codeblock>