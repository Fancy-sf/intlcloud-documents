本文为您介绍如何通过云数据库 MySQL 控制台修改数据库代理的网络。

## 前提条件
已 [开通数据库代理](https://intl.cloud.tencent.com/document/product/236/42052)。

## 注意事项
- 更换网络会导致该实例数据库代理 IP 变化，IP 默认保留24小时，最长保留时间支持设置168小时，旧的访问 IP 会失效，请及时修改客户端程序。
- 若旧 IP 地址的回收时间设置为0小时，更换网络后会立即回收旧 IP 地址。
- 只能选择 MySQL 实例所在地域下的 VPC 网络，但不限制子网可用区的选择，并可查看子网地址范围。

## 操作步骤
1. 登录 [MySQL 控制台](https://console.cloud.tencent.com/cdb)，在上方选择地域，然后单击目标实例 ID，进入实例管理页。
2. 在实例管理页，选择**数据库代理**页。
3. 在数据库代理页的**概览** > **连接地址** > **网络类型**下，单击![](https://qcloudimg.tencent-cloud.cn/raw/0286958e4f0522141375f4080708ceec.png)。
![](https://qcloudimg.tencent-cloud.cn/raw/ee84c770775763a4c4d20beee04a36ae.png)
4. 在弹出的对话框，选择相关配置，单击**确定**。
   - 设置旧 IP 地址回收时间，可设置范围为0 - 168小时。
   - 选择系统自动分配 IP 地址或手动指定 IP 地址。
![](https://qcloudimg.tencent-cloud.cn/raw/f48ad92683bd8eae4baa76580af03d7b.png)
5. 更换网络成功后，可在**连接地址**下查询变更后的网络。

