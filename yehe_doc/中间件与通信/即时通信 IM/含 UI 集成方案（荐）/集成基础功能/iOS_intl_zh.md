## 开发环境要求
- Xcode 10 及以上
- iOS 9.0 及以上

## CocoaPods 集成
TUIKit 从 5.7.1435 版本开始支持模块化集成，您可以根据自己的需求选择所需模块集成。

1. 根据实际业务需求在 Podfile 中添加对应的 TUI 组件，例如需要聊天功能，可以添加 `pod 'TUIChat'`；需要会话列表功能，可以添加 `pod 'TUIConversation'`；需要音视频通话功能，可以添加 `pod 'TUICallKit'`。TUI 组件之间相互独立，添加或删除均不影响工程编译。
```
# 防止 TUI 组件里的 *.xcassets 与您项目里面冲突。
install! 'cocoapods', :disable_input_output_paths => true  

# TUI 组件依赖了静态库，需要屏蔽如下设置，如果报错，请参考常见问题说明。
# use_frameworks!

# 集成聊天功能
pod 'TUIChat'
# 集成会话功能
pod 'TUIConversation'
# 集成关系链功能
pod 'TUIContact'
# 集成群组功能
pod 'TUIGroup'
# 集成搜索功能（需要购买旗舰版套餐）
pod 'TUISearch'
# 集成音视频通话功能
pod 'TUICallKit'
```
2. 执行以下命令，安装 TUI 组件。
```bash
pod install
```
 如果无法安装 TUIKit 最新版本，执行以下命令更新本地的 CocoaPods 仓库列表。
```bash
 pod repo update
```
**TUI 组件集成后效果**：
 <img src="https://qcloudimg.tencent-cloud.cn/raw/6e34bd1058ab0f84109bed307a38e134.png" width = "300"/> 


## 快速搭建
常用的聊天软件都是由会话列表、聊天窗口、好友列表、音视频通话等几个基本的界面组成，参考下面步骤，您仅需几行代码即可在项目中快速搭建这些 UI 界面。

### 步骤1：组件登录
```objectivec
#import "TUILogin.h"
// 您可以在用户 UI 点击登录的时候登录 UI 组件
- (void)loginSDK:(NSString *)userID userSig:(NSString *)sig succ:(TSucc)succ fail:(TFail)fail {
    // SDKAppID 可以在 即时通信 IM 控制台中获取
    // userSig生成见 GenerateTestUserSig.h
    [TUILogin login:SDKAppID userID:userID userSig:sig succ:^{
        NSLog(@"-----> 登录成功");
    } fail:^(int code, NSString *msg) {
        NSLog(@"-----> 登录失败");
    }];
}
```

### 步骤2：构建会话列表
会话列表只需要创建 `TUIConversationListController` 对象即可。会话列表会从数据库中读取最近联系人，当用户点击联系人时，`TUIConversationListController` 将该事件回调给上层。

```java
@implementation ConversationController // 您自己的 ViewController
- (void)viewDidLoad {
    [super viewDidLoad];
    // 创建 TUIConversationListController
    TUIConversationListController *conv = [[TUIConversationListController alloc] init];
    conv.delegate = self;
    // 把 TUIConversationListController 添加到自己的 ViewController
    [self addChildViewController:conv];
    [self.view addSubview:conv.view];
}

- (void)conversationListController:(TUIConversationListController *)conversationController didSelectConversation:(TUIConversationCell *)conversation
{
    // 会话列表点击事件，通常是打开聊天界面
}
@end
```

### 步骤3：构建聊天窗口
初始化聊天界面时，上层需要传入当前聊天界面对应的会话信息，示例代码如下：

```java
@implementation ChatViewController // 您自己的 ViewController
- (void)viewDidLoad {
   // 创建会话信息
   TUIChatConversationModel *data = [[TUIChatConversationModel alloc] init];
   data.userID = @"userID";    
   // 创建 TUIC2CChatViewController
   TUIC2CChatViewController *vc = [[TUIC2CChatViewController alloc] init];  
   [vc setConversationData:data];
   // 把 TUIC2CChatViewController 添加到自己的 ViewController
   [self addChildViewController:conv];
   [self.view addSubview:conv.view];
}
@end
```
>?`TUIC2CChatViewController` 会自动拉取该用户的历史消息并展示出来。

### 步骤4：构建通讯录界面
通讯录界面不需要其它依赖，只需创建对象并显示出来即可。

```java
@implementation ContactController // 您自己的 ViewController
- (void)viewDidLoad {    
   // 创建 TUIContactController
   TUIContactController *vc = [[TUIContactController alloc] init];
   // 把 TUIContactController 添加到自己的 ViewController
   [self addChildViewController:conv];
   [self.view addSubview:conv.view];
}
@end
```

### 步骤5：构建音视频通话功能
TUI 组件支持在聊天界面对用户发起音视频通话，仅需要简单几步就可以快速集成：
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>视频通话<br></b></th>
    <th style="text-align:center;"><b>语音通话</b><br></th>
  </tr>
  <tr>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/44d4c8a412752abda898341665a90016.png"/></td>
    <td><img src="https://qcloudimg.tencent-cloud.cn/raw/5eb84936666da81b0331a28c3c779b77.png"/></td>
	 </tr>
</table>


1. **开通音视频服务**
	1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片，进入应用的基础配置页面。
	2. 在开通腾讯实时音视频服务功能区，单击**免费体验**即可开通 TUICallKit 的 7 天免费试用服务。
	3. 在弹出的开通实时音视频 TRTC 服务对话框中，单击确认，系统将为您在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 创建一个与当前 IM 应用相同 SDKAppID 的实时音视频应用，二者帐号与鉴权可复用。
2. **集成 TUICallKit 组件**
在 podfile 文件中添加以下内容。
```objectivec
// 集成音视频通话组件
pod 'TUICallKit'                  
```
3. **发起和接收视频或语音通话**
<table style="text-align:center;vertical-align:middle;width: 800px">
  <tr>
    <th style="text-align:center;" ><b>消息页发起通话<br></b></th>
    <th style="text-align:center;" ><b>联系人页发起通话<br></b></th>
  </tr>
  <tr>
    <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/b34f84493214ca44bef32d0257d66693.png"/></td>
    <td><img style="width:400px" src="https://qcloudimg.tencent-cloud.cn/raw/65d76fa2bea287a22c11b1f972996397.png"/></td>
     </tr>
</table>
<ul>
<li>集成 TUICallKit 组件后，聊天界面和联系人资料界面默认会出现 “视频通话” 和 “语音通话” 两个按钮，当用户点击按钮时，TUIKit 会自动展示通话邀请 UI，并给对方发起通话邀请请求。</li>
<li>当用户<strong>在线</strong>收到通话邀请时，TUIKit 会自动展示通话接收 UI，用户可以选择同意或者拒绝通话。</li>
<li>当用户<strong>离线</strong>收到通话邀请时，如需唤起 App 通话，就要使用到离线推送能力，离线推送的实现请参考 <a href="#Step5.4">添加离线推送</a>。</li>
</ul>

4. **添加离线推送**
在使用离线推送之前，您需要开通 [IM 离线推送](https://intl.cloud.tencent.com/document/product/1047/39157) 服务。
关于 App 的配置，您可以参考文档：[集成 TUIOfflinePush 跑通离线推送功能](https://intl.cloud.tencent.com/document/product/1047/47949)。

**配置完成后，当单击接收到的「音视频通话离线推送通知」时， TUICallKit 会自动拉起「音视频通话邀请界面」。**




## 常见问题
#### 提示 "target has transitive dependencies that include statically linked binaries" 如何处理？
如果在 pod 过程中出现该错误，是因为 TUIKit 使用到了第三方静态库，需要在 podfile 中注释掉 `use_frameworks!`。
如果在某种情况下，需要使用 `use_frameworks!`，则请使用 cocoapods 1.9.0 及以上版本进行 `pod install`，并修改为：
```
use_frameworks! :linkage => :static
```
如果您使用的是 swift，请将头文件引用改成 @import 模块名形式引用。

#### TUICallKit 和自己集成的音视频库冲突了？
腾讯云的 [音视频库](https://intl.cloud.tencent.com/document/product/647/34615) 不能同时集成，会有符号冲突，如果您使用了非 [TRTC](https://intl.cloud.tencent.com/document/product/647/34615#TRTC) 版本的音视频库，建议先去掉，然后 pod 集成 `TUICallKit/Professional` 版本，该版本依赖的 [LiteAV_Professional](https://intl.cloud.tencent.com/document/product/647/34615#.E4.B8.93.E4.B8.9A.E7.89.88.EF.BC.88professional.EF.BC.89) 音视频库包含了音视频的所有基础能力。**如果您使用了 [LiteAV_Enterprise](https://intl.cloud.tencent.com/document/product/647/34615#Enterprise) 音视频库，暂不支持和 TUICallKit 共存。**具体解决方案可以参考文档：[音视频常见问题](https://www.tencentcloud.com/document/product/1047/50024#.E5.B8.B8.E8.A7.81.E9.97.AE.E9.A2.98)。

#### 通话邀请的超时时间默认是多久？
通话邀请的默认超时时间是 30 秒.

#### 在邀请超时时间内，被邀请者如果离线再上线，能否立即收到邀请？

- 如果是单聊通话邀请，被邀请者离线再上线可以收到通话邀请，TUIKit 内部会自动唤起通话邀请界面。
- 如果是群聊通话邀请，被邀请者离线再上线后会自动拉取最近 30 秒内的邀请，TUIKit 会自动唤起群通话界面。



