## Feature Description
The group management feature allows creating a group, joining a group, getting the joined groups, leaving a group, or disbanding a group through methods in the `V2TIMGroupManager(Android)` / `V2TIMManager(Group)(iOS and macOS)` core class.

[](id:listener)
## Group Event Listener
In the group management feature as described below, the IM SDK will automatically trigger the group event notification callback, for example, when someone joins or leaves a group.

Call `addGroupListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a8dde0362f00a454945e7811c8a726a38) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#af583b113cdec570b08ae80d682fba52c)) to add a group event listener.

Group events are defined in `V2TIMGroupListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html)), including group member notification, group lifecycle notification, group join request notification, and topic event listening callback.

To stop receiving group events, call `removeGroupListener` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ab4d57bd5fd4b2d71c29daaeee8b9b760) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a2b2093489bf869f70c03be39f4ed08a1)) to remove the group event listener.

If you have configured a group event listener but don't receive events as expected, you can log in to the [IM console](https://console.cloud.tencent.com/im) to check or configure the group system notification as follows:
<img src="https://qcloudimg.tencent-cloud.cn/raw/8097e0506da8dde2b56a75892983d897.png" alt="Group system notification configuration" style="zoom:90%;" />

> ! Audio-video groups don't support configuring the notifications of group member change and group profile change.

Sample code:
<dx-tabs>
::: Android
```java
V2TIMGroupListener groupListener = new V2TIMGroupListener() {
  // Group member notification, group lifecycle notification, group join request notification, topic event listening callback, etc.
  @Override
  public void onMemberEnter(String groupID, List<V2TIMGroupMemberInfo> memberList) {
    // A member joined the group. All the group members can receive the notification.
  }
  @Override
  void onMemberLeave(String groupID, V2TIMGroupMemberInfo member)	{
    // A member left the group. All the group members can receive the notification.
  }

  @Override
  public void onReceiveRESTCustomData(String groupID, byte[] customData) {
    // Custom system notification sent by the server
  }
};

V2TIMManager.getInstance().addGroupListener(groupListener);
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] addGroupListener:self];

// Group member notification, group lifecycle notification, group join request notification, topic event listening callback, etc.
- (void)onMemberEnter:(NSString *)groupID memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // A member joined the group. All the group members can receive the notification.
}

- (void)onMemberLeave:(NSString *)groupID member:(V2TIMGroupMemberInfo *)member {
    // A member left the group. All the group members can receive the notification.
}

- (void)onReceiveRESTCustomData:(NSString *)groupID data:(NSData *)data {
    // Custom system notification sent by the server
}
```
:::
</dx-tabs>

[](id:createGroup)
## Creating a Group
### Ordinary API
Call the `createGroup` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#af836e4912f668dddf6cc679233cfb0bb) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a3bbcf819c1ec70e520b7f9a42cfbb989)) and specify parameters to create a group.

The `createGroup` parameters are as described below:

| Parameter | Definition | Required | Description |
| --- | --- | --- | --- |
| groupType | Group type | Yes | For more information, see [Group System](https://intl.cloud.tencent.com/document/product/1047/33529). |
| groupID | Group ID | No | If it is left empty, an ID will be automatically assigned after a group is created successfully.<br>It can be customized as instructed in [Group System](https://intl.cloud.tencent.com/document/product/1047/33529).|
| groupName | Group name | Yes | It can contain up to 30 bytes. |

If you have called `addGroupListener` to add a group event listener as instructed in [Group Event Listener](#advance_page), `onGroupCreated` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a93504c985480a2bb87ca716809e3dd00) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aa5c08185c8c9ddaace6421e1e153711d)) will be called back after a group is created successfully.


Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().createGroup(V2TIMManager.GROUP_TYPE_WORK, null, "groupA", new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String s) {
  	// Created the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to create the group
  }
});
// Listen for the group creation notification
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGroupCreated(String groupID) {
  	// A group was created. `groupID` is the ID of the created group.
  }
});
```
:::
::: iOS and macOS
```objectivec
// Create a group
[[V2TIMManager sharedInstance] createGroup:GroupType_Work groupID:nil groupName:@"groupA" succ:^(NSString *groupID) {
    // Created the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to create the group
}];

// Listen for the group creation notification
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onGroupCreated:(NSString *)groupID {
    // A group was created. `groupID` is the ID of the created group.
}
```
:::
</dx-tabs>

### Advanced API
To initialize the group information such as group introduction, group profile photo, and existing group members when creating a group, call the `createGroup` advanced API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a121d53137a38d0fc0bc8a8e0a9c55647) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a59824434b6096180b94d8152183dcd2c)), and the `groupID` will be returned in the callback for successful creation.

Sample code:

<dx-tabs>
::: Android
```java
// Use the `createGroup` advanced API to create a work group 
V2TIMGroupInfo v2TIMGroupInfo = new V2TIMGroupInfo();
v2TIMGroupInfo.setGroupName("testWork");
v2TIMGroupInfo.setGroupType("Work");
v2TIMGroupInfo.setIntroduction("this is a test Work group");

List<V2TIMCreateGroupMemberInfo> memberInfoList = new ArrayList<>();
V2TIMCreateGroupMemberInfo memberA = new V2TIMCreateGroupMemberInfo();
memberA.setUserID("vinson");
V2TIMCreateGroupMemberInfo memberB = new V2TIMCreateGroupMemberInfo();
memberB.setUserID("park");
memberInfoList.add(memberA);
memberInfoList.add(memberB);

V2TIMManager.getGroupManager().createGroup(
    v2TIMGroupInfo, memberInfoList, new V2TIMValueCallback<String>() {
	@Override
	public void onError(int code, String desc) {
		// Failed to create
	}
	@Override
	public void onSuccess(String groupID) {
		// Created successfully
	}
});
```
:::
::: iOS and macOS
```objectivec
// Use the `createGroup` advanced API to create a work group 
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupName = @"testWork";
info.groupType = @"Work";
NSMutableArray *memberList = [NSMutableArray array];
V2TIMCreateGroupMemberInfo *memberInfo = [[V2TIMCreateGroupMemberInfo alloc] init];
memberInfo.userID = @"vinson";
[memberList addObject:memberInfo];
[[V2TIMManager sharedInstance] createGroup:info memberList:memberList succ:^(NSString *groupID) {
    // Created the group successfully
} fail:^(int code, NSString *msg) {
    // Failed to create the group
}];
```
:::
</dx-tabs>

[](id:joinGroup)
## Joining a Group
The method for joining a group may vary by group type as follows:

| Type | Method for Joining a Group |
| --- | --- |
| Work group (Work)| By invitation |
| Public group (Public)| On request from the user and on approval from the group owner or admin |
| Meeting group (Meeting)| Free to join |
| Community (Community)| Free to join |
| Audio-video group (AVChatRoom)| Free to join |

The following describes how to join the groups in an easy-to-hard sequence.

> ! You need to call `addGroupListener` to add a group event listener in advance as instructed in [Group Event Listener](#advance_page) to receive the following group events.

#### Free to join a group
Meeting groups (Meeting), audio-video groups (AVChatRoom), and communities are mainly used for free interaction scenarios, such as online meeting and live show. The process of joining such groups is the simplest:
1. The user calls `joinGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a)) to join the group.
2. After the user has successfully joined the group, all the group members (including the user) will receive the `onMemberEnter` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11)).

Sample code:
<dx-tabs>
::: Android
```java
// Join a group
V2TIMManager.getInstance().joinGroup("groupA", "it's me!", new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Joined the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to join the group
  }
});

// Listen for the group join event
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberEnter(String groupID, List<V2TIMGroupMemberInfo> memberList) {
  	// A user joined the group.
  }
});

```
:::
::: iOS and macOS
```objectivec
// Join a group
[[V2TIMManager sharedInstance] joinGroup:@"groupA" msg:@"it's me!" succ:^{
    // Joined the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to join the group
}];

// Listen for the group join event
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberEnter:(NSString *)groupID memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // A user joined the group.
}
```
:::
</dx-tabs> 

#### Joining a group by invitation
Work groups (Work) are suitable for communication in work environments. The interaction pattern is designed to disable proactive group joining and only allow users to be invited to join the group by group members.
The steps to join a group are as follows:

1. A group member calls `inviteUserToGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#afd219107653b877e446c149531d65e92) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a942d75fdea66e22cdbd8c131cf18e1ea)) to invite a user to the group.
2. All the group members (including the inviter) receive the `onMemberInvited` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#af6119ca3c6eabcc63acbf012f508b1b1) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a6bff27f9f6859caefcaaf361b9c6fe68)), which can contain some UI tips.


Sample code:
<dx-tabs>
::: Android
```java
// Invite the `userA` user to join the `groupA` group
List<String> userIDList = new ArrayList<>();
userIDList.add("userA");
V2TIMManager.getGroupManager().inviteUserToGroup("groupA", userIDList, new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
  	// Invited the user to the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to invite the user to the group
  }
});

// Listen for the group invitation event
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberInvited(String groupID, V2TIMGroupMemberInfo opUser, List<V2TIMGroupMemberInfo> memberList) {
  	// A user was invited to the group. This callback can contain some UI tips.
  }
});
```
:::
::: iOS and macOS
```objectivec
// Invite the `userA` user to join the `groupA` group
[[V2TIMManager sharedInstance] inviteUserToGroup:@"groupA" userList:@[@"userA"] succ:^(NSArray<V2TIMGroupMemberOperationResult *> *resultList) {
    // Invited the user to the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to invite the user to the group
}];

// Listen for the group invitation event
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberInvited:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList {
    // This callback can contain some UI tips.
}
```
:::
</dx-tabs>

#### Joining a group on request and on approval
A public group (Public) is similar to the interest group and clan group of QQ. Anyone can join it on request and on approval from the group owner or admin.

The steps to join a group on request and on approval are as follows:
![](https://main.qcloudimg.com/raw/9164de02268e14b178937bbd85465f4f.png)

Description of process:
1. The user calls `joinGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#ad64a09bea508672d6d5a402b3455b564) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a4762156b7a98489eb4715de53028e12a)) to request to join the group.

2. The group owner or admin receives the `onReceiveJoinApplication` group join request notification ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#adf0b34684efd46d6e31d31e7bc3643f9) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a481ab06916795cc9445fa3fc465c69ab)) and calls `getGroupApplicationList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a240db7bdc023ad6fc63e9ee9b72714c4) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a29c36ad685159850a30d61a6b9c637e8)) to get the group join request list.

3. The group owner or admin traverses the group join request list and calls `acceptGroupApplication` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad743008d30c909ef0be0f8aa91102e07) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a51bb9b4f965cb3d01546fef348ac75e4)) to approve a request or `refuseGroupApplication` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#aa518c54e77f7c0f6e7dd129d6c433acd) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a46aa78c54986b2c0b7cc0012a3dc94ef)) to reject it.

4. After the request to join the group is approved or rejected, the user will receive the `onApplicationProcessed` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#ac833c624e33036ec0454fe5444b8f00a) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a850a50e7ea6b86a2d28afa1a569245ca)). Here, if `isAgreeJoin` is `true`/`YES`, the request is approved; otherwise, it is rejected.
   
5. On approval, all the group members (including the user) will receive the `onMemberEnter` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a85cbb33a40aaa41781e4835bf802db6d) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#aed6a96e6b304863586a107c45ba33f11)), notifying the group members that someone joined the group.

Sample code:

<dx-tabs>
::: Android
```java
// ******Group owner******//
// 1. The group owner changes the group join option to approval required.
V2TIMGroupInfo groupInfo = new V2TIMGroupInfo();
groupInfo.setGroupID("groupB");
groupInfo.setGroupAddOpt(V2TIMGroupInfo.V2TIM_GROUP_ADD_AUTH);
V2TIMManager.getGroupManager().setGroupInfo(groupInfo, new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Changed the group join option successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to change the group join option
  }
});

// 2. The group owner listens for and processes requests to join the group.
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onReceiveJoinApplication(String groupID, V2TIMGroupMemberInfo member, String opReason) {
    V2TIMManager.getGroupManager().getGroupApplicationList(new V2TIMValueCallback<V2TIMGroupApplicationResult>() {
      @Override
      public void onSuccess(V2TIMGroupApplicationResult v2TIMGroupApplicationResult) {
        List<V2TIMGroupApplication> groupApplicationList = v2TIMGroupApplicationResult.getGroupApplicationList();
        for (V2TIMGroupApplication application : groupApplicationList) {
          if (application.getGroupID().equals(groupID) && application.getFromUser().equals(member.getUserID())) {
            // Approve group join
            if (agree) {
              // Approve the group join request
              V2TIMManager.getGroupManager().acceptGroupApplication(application, "agree", new V2TIMCallback() {
                @Override
                public void onSuccess() {
                	// Approved the group join request successfully
                }

                @Override
                public void onError(int code, String desc) {
                	// Failed to approve the group join request
                }
              });
            } else {
              // Reject the group join request
              V2TIMManager.getGroupManager().refuseGroupApplication(application, "not agree", new V2TIMCallback() {
                @Override
                public void onSuccess() {
                	// Rejected the group join request successfully
                }

                @Override
                public void onError(int code, String desc) {
                	// Failed to reject the group join request
                }
              });
            }
            return;
          }
        }
        
        V2TIMManager.getGroupManager().setGroupApplicationRead(new V2TIMCallback() {
          @Override
          public void onSuccess() {
            // Marked the group join request list as read successfully
          }

          @Override
          public void onError(int code, String desc) {
            // Failed to mark the group join request list as read
          }
        });
      }

      @Override
      public void onError(int code, String desc) {
      // Failed to obtain the group join request list
      }
    });
  }
});

// ******User******//
// 1. The user requests to join the group.
V2TIMManager.getInstance().joinGroup("groupB", "it's me!", new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Joined the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to join the group
  }
});
// 2. The user listens for the request review result.
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onApplicationProcessed(String groupID, V2TIMGroupMemberInfo opUser, boolean isAgreeJoin,
  String opReason) {
  	// The request to join the group is processed.
  }

  @Override
  public void onMemberEnter(String groupID, List<V2TIMGroupMemberInfo> memberList) {
  	// This callback will be received if the group join request is approved.
  }
});
```
:::
::: iOS and macOS
```objectivec
// ******Group owner******//
// 1. The group owner changes the group join option to approval required.
V2TIMGroupInfo *info = [[V2TIMGroupInfo alloc] init];
info.groupID = @"groupA";
info.groupAddOpt = V2TIM_GROUP_ADD_AUTH;
[[V2TIMManager sharedInstance] setGroupInfo:info succ:^{
    // Changed the group join option successfully
} fail:^(int code, NSString *desc) {
    // Changed the group join option successfully
}];

// 2. The group owner listens for and processes requests to join the group.
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onReceiveJoinApplication:(NSString *)groupID member:(V2TIMGroupMemberInfo *)member opReason:(NSString *)opReason {
    [[V2TIMManager sharedInstance] getGroupApplicationList:^(V2TIMGroupApplicationResult *result) {
        for (V2TIMGroupApplication *application in result.applicationList) {
            if ([application.groupID isEqualToString:groupID] && [application.fromUser isEqualToString:member.userID]) {
                // Approve group join
                [[V2TIMManager sharedInstance] acceptGroupApplication:application reason:@"agree" succ:^{
                    // Approved the group join request successfully
                } fail:^(int code, NSString *desc) {
                    // Failed to approve the group join request
                }];
                
                // Reject group join
                [[V2TIMManager sharedInstance] refuseGroupApplication:application reason:@"refuse" succ:^{
                    // Rejected the group join request successfully
                } fail:^(int code, NSString *desc) {
                    // Failed to reject the group join request
                }];
                
                // Mark the request as read
                [[V2TIMManager sharedInstance] setGroupApplicationRead:^{
                    // Marked the group join request list as read successfully
                } fail:^(int code, NSString *desc) {
                    // Failed to mark the group join request list as read
                }];
            }
        }
    } fail:^(int code, NSString *desc) {
        // Failed to obtain the group join request list
    }];
}

// ******Request******//
// 1. The user requests to join the group.
[[V2TIMManager sharedInstance] joinGroup:@"groupA" msg:@"it's me!" succ:^{
    // Joined the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to join the group
}];

// 2. The user listens for the request review result. 
[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onApplicationProcessed:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser opResult:(BOOL)isAgreeJoin opReason:(NSString *)opReason {
    // The request to join the group is processed.
}
- (void)onMemberEnter:(NSString *)groupID memberList:(NSArray<V2TIMGroupMemberInfo *>*)memberList; {
    // This callback will be received if the group join request is approved.
}
```
:::
</dx-tabs>

The group owner or admin can also call the `setGroupInfo` API ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#ad4ceef92975fa00c4a5dddc8f7e1edcf) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#aa9519a479493e56d7920e40aba796144)) to change the group join option (`V2TIMGroupAddOpt`) to "no group join allowed" or "no approval required".

`V2TIMGroupAddOpt` has the following options:

| Group Join Option | Description |
| --- | --- |
| V2TIM_GROUP_ADD_FORBID | No users can join the group. |
| V2TIM_GROUP_ADD_AUTH | Approval from the group owner or admin is required to join the group (default value). |
| V2TIM_GROUP_ADD_ANY | Any user can join the group without approval. |

[](id:getJoinedGroup)
## Getting the Joined Groups
Call `getJoinedGroupList` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a0199b7cacc6919938d8342474bd252da) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#a4599e99791c150cc9f3e2492e8b4ce04)) to get the list of joined work groups (Work), public groups (Public), meeting groups (Meeting), and communities (Community, which **don't support** the topic feature). Audio-video groups (AVChatRoom) and communities (Community, which **support** the topic feature) are not included in this list.

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getGroupManager().getJoinedGroupList(new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
  	// Obtained the list of joined groups successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to obtain the list of joined groups
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] getJoinedGroupList:^(NSArray<V2TIMGroupInfo *> *groupList) {
    // Obtained the list of joined groups successfully
} fail:^(int code, NSString *desc) {
    // Failed to obtain the list of joined groups
}];
```
:::
</dx-tabs>

[](id:quitGroup)
## Leaving a Group

Call `quitGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#a6d140dbeb44906de9cb69f69c2ce5919) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#ac2a43b3ada447131df0c5f19e8079be5)) to leave a group.
The member who left the group will receive the `onQuitFromGroup` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a489004526f1bd8daba7ac63fb0ad965f) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9d4a0c42366ea13f688a3c369f91e80f)).
Other group members will receive the `onMemberLeave` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a2169676423875e4c9c376796245ca8d5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a27ca737d915d21810b7f54e8677922e0)).

> ! The group owner **cannot** leave a public group (Public), meeting group (Meeting), community, or audio-video group (AVChatRoom) and can only [disband it](#dismiss).

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().quitGroup("groupA", new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Left the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to leave the group
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberLeave(String groupID, V2TIMGroupMemberInfo member) {
		// A group member left the group.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] quitGroup:@"groupA" succ:^{
    // Left the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to leave the group
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onMemberLeave:(NSString *)groupID member:(V2TIMGroupMemberInfo *)member {
    // A group member left the group.
}
```
:::
</dx-tabs>


[](id:dismiss)
## Disbanding a Group

Call `dismissGroup` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMManager.html#afd0221c0c842a6dcfa0acc657e50caeb) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/interfaceV2TIMManager.html#a5bd55cb04867985253949d8cc78f860e)) to disband a group, and all the group members will receive the `onGroupDismissed` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a6e89728e160e126460a6b8eeddf00ad5) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a9063ce1847731024581f2b1ad6b9ed0a)).

If you have allowed automatically disbanding an inactive group on the server, when the group is automatically disbanded by the server, the SDK will receive the `onGroupRecycled` callback ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a49de77b919f679f1631981ba2b186a55) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a5388d6acb25b007be79ed5ea49f756fb)).

Sample code:

<dx-tabs>
::: Android
```java
V2TIMManager.getInstance().dismissGroup("groupA", new V2TIMCallback() {
  @Override
  public void onSuccess() {
  	// Disbanded the group successfully
  }

  @Override
  public void onError(int code, String desc) {
  	// Failed to disband the group
  }
});

V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGroupDismissed(String groupID, V2TIMGroupMemberInfo opUser) {
  	// The group was disbanded.
  }
  
  @Override
  public void onGroupRecycled(String groupID, V2TIMGroupMemberInfo opUser) {
  	// The group was reclaimed.
  }
});
```
:::
::: iOS and macOS
```objectivec
[[V2TIMManager sharedInstance] dismissGroup:@"groupA" succ:^{
    // Disbanded the group successfully
} fail:^(int code, NSString *desc) {
    // Failed to disband the group
}];

[[V2TIMManager sharedInstance] addGroupListener:self];
- (void)onGroupDismissed:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser {
    // The group was disbanded.
}

- (void)onGroupRecycled:(NSString *)groupID opUser:(V2TIMGroupMemberInfo *)opUser {
    // The group was reclaimed.
}
```
:::
</dx-tabs>

## Receiving a Custom Group System Notification
If you call the RESTful API on the server [to send custom system messages to the group](https://intl.cloud.tencent.com/document/product/1047/34958), the SDK will call back `onReceiveRESTCustomData` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupListener.html#a0775a137d293473aaed4cf9fc4c18795) / [iOS and macOS](https://im.sdk.qcloud.com/doc/en/protocolV2TIMGroupListener-p.html#a989347c455869dc0aa44572f4f2b7041)) and return the custom data you send.


