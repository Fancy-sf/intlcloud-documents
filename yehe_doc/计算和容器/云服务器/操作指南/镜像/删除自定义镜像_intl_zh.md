## 操作场景

本文档指导您删除自定义镜像。

## 注意事项
执行删除操作前，请您注意以下事项：
 - 删除自定义镜像后，无法通过此镜像创建实例，但不影响已启动的实例。如果您需要删除所有从此镜像启动的实例，可参考 [回收实例](https://intl.cloud.tencent.com/document/product/213/4931) 或 [销毁/退还实例](https://intl.cloud.tencent.com/document/product/213/4930)。
 - 已共享的镜像无法删除，需要先取消所有共享后才可删除。取消共享镜像可参见 [取消共享自定义镜像](https://intl.cloud.tencent.com/document/product/213/7148)。
 - 仅自定义镜像能被删除，公共镜像和共享镜像均无法主动删除。

## 操作步骤
<dx-tabs>
::: 通过控制台删除
1. 登录云服务器控制台，选择左侧导航栏中的 [**镜像**](https://console.cloud.tencent.com/cvm/image)。
2. 选择**自定义镜像**页签，进入自定义镜像的管理页面。
3. 根据实际需求，选择删除自定义镜像的操作方式。
 - **删除单个镜像**：列表中找到需要删除的自定义镜像，单击**更多**>**删除**。如下图所示：
  ![](https://qcloudimg.tencent-cloud.cn/raw/1211de56434b4b6034dccb1ff9ce4aa1.png)
 - **删除多个镜像**：列表中勾选所有要删除的自定义镜像，单击顶部**删除**。如下图所示：
  ![](https://qcloudimg.tencent-cloud.cn/raw/9f002d5cce1cfa2c94931ea3bca25ac2.png)
4. 在弹出的提示框中，单击**确定**。
无法删除时，将会提示原因。
:::
::: 通过\sAPI\s删除
用户可以使用 DeleteImages 接口共享镜像，具体内容可以参考 [删除镜像](https://intl.cloud.tencent.com/document/product/213/33275)。
:::
</dx-tabs>
