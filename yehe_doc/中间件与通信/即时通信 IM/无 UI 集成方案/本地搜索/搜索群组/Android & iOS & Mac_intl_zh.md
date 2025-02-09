## 功能描述
您只能搜索本地存储过的群组，例如已加入的群组列表，拉取过的群组资料等。

> ? 群组搜索功能仅 5.4.666 及以上版本支持。

## 搜索本地群组
您可以调用接口 `searchGroups` ([Android](https://im.sdk.qcloud.com/doc/en/classcom_1_1tencent_1_1imsdk_1_1v2_1_1V2TIMGroupManager.html#a94a72082b7e2682942f35196a7e28023) / [iOS & Mac](https://im.sdk.qcloud.com/doc/en/categoryV2TIMManager_07Group_08.html#ac9a960921e512621340159d82a4b5259)) 搜索本地群组。
您可以设置搜索关键字 `keywordList`，并指定搜索的范围，即是否搜索群组的 `userID`、`groupName` 字段。

示例代码如下：

<dx-tabs>
::: Android

```java
V2TIMGroupSearchParam searchParam = new V2TIMGroupSearchParam();
searchParam.setKeywordList(keywordList);
searchParam.setSearchGroupID(true);
searchParam.setSearchGroupName(true);

V2TIMManager.getGroupManager().searchGroups(searchParam, new V2TIMValueCallback<List<V2TIMGroupInfo>>() {
  @Override
  public void onSuccess(List<V2TIMGroupInfo> v2TIMGroupInfos) {
		// 搜索群组成功
  }

  @Override
  public void onError(int code, String desc) {
  	// 搜索群组失败
  }
});
```
:::
::: iOS & Mac
```objectivec
V2TIMGroupSearchParam *searchParam = [[V2TIMGroupSearchParam alloc] init];
searchParam.keywordList = @[@"keyword1", @"keyword2"];
searchParam.isSearchGroupID = YES;
searchParam.isSearchGroupName = YES;
[[V2TIMManager sharedInstance] searchGroups:searchParam succ:^(NSArray<V2TIMGroupInfo *> *groupList) {
    // 搜索群组成功
} fail:^(int code, NSString *desc) {
    // 搜索群组失败
}];
```
:::
</dx-tabs>


