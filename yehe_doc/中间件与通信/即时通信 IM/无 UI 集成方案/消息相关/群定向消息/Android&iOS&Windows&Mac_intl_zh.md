## 功能描述
群定向消息是指向群内部分成员发送消息，其他群成员无法收到该消息。

> ?
> 1. 仅增强版 SDK 6.0.1975 及以上版本支持。
> 2. 该功能仅对旗舰版客户开放，详情请参考 [基础服务详情](https://intl.cloud.tencent.com/document/product/1047/34350)。
> 3. 创建定向群消息的原始消息对象不支持群 @ 消息。
> 4. 社群（Community）和直播群（AVChatRoom）不支持发送定向群消息。
> 5. 定向群消息默认不计入群会话的未读计数。

## 发送群定向消息
定向消息是指，向群内部分指定的成员发送消息，而未被指定的群成员无法收到该消息。

* 如果您希望向群里的单个群成员发定向消息，同时传入 groupID 和 receiver 即可。
* 如果您希望向群里的多个群成员发定向消息，可以按照下面的方式实现：
  1. 调用 `createXxxMessage` (其中 Xxx 表示具体的消息类型) 接口创建一条原始消息对象 `V2TIMMessage`。
  2. 调用 `createTargetedGroupMessage` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMMessageManager.html#a4def1515746b2840e4b82047a53b91a2) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Message_08.html#a8bddd2f566a53362b4da5448fdd18fbc) / [Windows](https://im.sdk.qcloud.com/doc/en/classV2TIMMessageManager.html#aceeef38fd6308e91154cdd8310c6012f)) 接口根据原始消息对象创建定向消息对象 `V2TIMMessage`，并指定消息接收成员列表。
  3. 调用 `sendMessage` 接口发送定向消息。

示例代码如下：
<dx-tabs>
::: Android
```java
// 创建原始消息对象
V2TIMMessage v2TIMMessage = V2TIMManager.getMessageManager().createTextMessage("这是一个群定向消息");
// 创建定向群消息对象，指定群消息接收者 "vinson" "denny"
List<String> targetGroupMemberList = new ArrayList<>();
targetGroupMemberList.add("vinson");
targetGroupMemberList.add("denny");
V2TIMMessage targetGroupMessage = V2TIMManager.getMessageManager().createTargetedGroupMessage(v2TIMMessage, targetGroupMemberList);

// 在群 "groupA" 发送群定向消息
V2TIMManager.getMessageManager().sendMessage(targetGroupMessage, null, "groupA",  V2TIMMessage.V2TIM_PRIORITY_DEFAULT, false, null, new V2TIMSendCallback<V2TIMMessage>() {
  @Override
  public void onError(int code, String desc) {
  	// 发送失败
  }
  @Override
  public void onSuccess(V2TIMMessage v2TIMMessage) {
  	// 发送成功
  }
  @Override
  public void onProgress(int progress) {

  }
});
```
:::
::: iOS & Mac
```objectivec
// 创建原始消息对象
V2TIMMessage *message = [V2TIMManager.sharedInstance createTextMessage:@"这是一个群定向消息"];

// 创建定向群消息对象，指定群消息接收者 "vinson" "denny"
NSMutableArray *receiverList = [NSMutableArray array];
[receiverList addObject:@"vinson"];
[receiverList addObject:@"denny"];
V2TIMMessage *targetGroupMessage = [V2TIMManager.sharedInstance createTargetedGroupMessage:message receiverList:receiverList];

// 在群 "groupA" 发送定向消息
[[V2TIMManager sharedInstance] sendMessage:targetGroupMessage receiver:nil groupID:@"groupA"
priority:V2TIM_PRIORITY_DEFAULT onlineUserOnly:NO offlinePushInfo:nil progress:^(uint32_t progress) {
} succ:^{
    // 消息发送成功
} fail:^(int code, NSString *msg) {
    // 消息发送失败
}];
```
:::
::: Windows
```cpp
class SendCallback final : public V2TIMSendCallback {
public:
    using SuccessCallback = std::function<void(const V2TIMMessage&)>;
    using ErrorCallback = std::function<void(int, const V2TIMString&)>;
    using ProgressCallback = std::function<void(uint32_t)>;

    SendCallback() = default;
    ~SendCallback() override = default;

    void SetCallback(SuccessCallback success_callback, ErrorCallback error_callback,
                     ProgressCallback progress_callback) {
        success_callback_ = std::move(success_callback);
        error_callback_ = std::move(error_callback);
        progress_callback_ = std::move(progress_callback);
    }

    void OnSuccess(const V2TIMMessage& message) override {
        if (success_callback_) {
            success_callback_(message);
        }
    }
    void OnError(int error_code, const V2TIMString& error_message) override {
        if (error_callback_) {
            error_callback_(error_code, error_message);
        }
    }
    void OnProgress(uint32_t progress) override {
        if (progress_callback_) {
            progress_callback_(progress);
        }
    }

private:
    SuccessCallback success_callback_;
    ErrorCallback error_callback_;
    ProgressCallback progress_callback_;
};

// 创建原始消息对象
V2TIMMessage message =
    V2TIMManager::GetInstance()->GetMessageManager()->CreateTextMessage(u8"这是一条群 @ 文本消息");
// 创建定向群消息对象，指定群消息接收者 "vinson" "denny"
V2TIMStringVector receiverList;
receiverList.PushBack("vinson");
receiverList.PushBack("denny");
V2TIMMessage targetGroupMessage =
    V2TIMManager::GetInstance()->GetMessageManager()->CreateTargetedGroupMessage(message, receiverList);

auto callback = new SendCallback{};
callback->SetCallback(
    [=](const V2TIMMessage& message) {
        // 群定向消息发送成功
        delete callback;
    },
    [=](int error_code, const V2TIMString& error_message) {
        // 群定向消息发送失败
        delete callback;
    },
    [=](uint32_t progress) {});

// 在群 "groupA" 发送群定向消息
V2TIMManager::GetInstance()->GetMessageManager()->SendMessage(
    targetGroupMessage, {}, "groupA", V2TIMMessagePriority::V2TIM_PRIORITY_NORMAL, false, {}, callback);
```
:::
</dx-tabs>

## 接收群定向消息
定向群消息默认不计入群会话的未读计数。
接收群定向消息跟接收普通消息是一样的操作步骤，参考 [接收消息](https://intl.cloud.tencent.com/document/product/1047/47995)。

