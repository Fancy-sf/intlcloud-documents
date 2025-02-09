## 操作场景

预留实例计费是账户中按量计费实例所应用的一种折扣，相比按量计费模式价格更优惠。本文档指导您如何在控制台创建预留实例计费实例。

## 前提条件
当前预留实例计费只对国际站白名单用户开放，请前往预留实例计费[内测申请](https://intl.cloud.tencent.com/apply/p/bvrqmrrp5ns)使用资格。

## 操作步骤
1.	登陆[云服务器控制台](https://console.cloud.tencent.com/cvm/instance/index?rid=1)。
2.	左侧导航栏中，单击【预留实例】，进入预留实例计费管理页面。
3.	单击【创建预留实例计费】，进入预留实例计费购买页面。

![image-20200909172355330](https://main.qcloudimg.com/raw/f604c27f8faeded74797d78d66ada9c2.png)

4. 根据页面提示，配置以下信息：

| <div style="width:100px">类别</div>         | 必选/可选 | 配置说明                                |
| ------------------ | --------- | ------------------------------------------------------------ |
| 地域/可用区 | 必选      | 请选择您需要匹配的按量计费实例对应的地域和可用区。           |
| 操作系统     | 必选      | 当前支持Windows和Linux操作系统。                                    |
| 时长         | 必选      | 预留实例计费的有效时长，当前只支持一年。                     |
| 实例         | 必选      | 请选择您需要匹配的按量计费实例对应的实例类型。</br>  按量计费必须在预留实例计费正常生命周期范围内且属性与预留实例完全匹配才能享受账单折扣。 |
| 预留实例名称 | 可选      | 用户自定义，表示需要创建的预留实例计费的名称。 <li> 如果不定义预留实例计费名称，创建后预留实例计费称为“未命名”。</li>  <li>  如果定义了预留实例计费名称，该名称需限制在60个字符以内。</li> |
| 付费类型     | 必选      | 请根据实际需求进行选择：</br> <ul><li>全预付：购买时预付所有费用，在预留实例的使用期内不再缴纳其它费用。与以上两种按需实例的定价相比，此选项为您提供最大的折扣。</li><li>部分预付：购买时支付较低额度的预付款，在预留实例的使用期内，按月付费或折扣的小时费率支付实例费用。</li> <li>零预付：购买时无需支付任何费用，在预留实例的使用期内，按月付费或折扣的小时费率支付实例费用。  更多关于预留实例计费付费类型的介绍，请参考[预留实例计费模式](https://intl.cloud.tencent.com/document/product/213/37070)</li> </ul>|
| 数量         | 必选      | 表示需购买的预留实例计费的数量。                             |


5. 单击【立即购买】，完成支付。当您付款完成后，即可进入[预留实例列表页面](https://console.cloud.tencent.com/cvm/reservedinstances/) 查看、搜索、管理您的预留实例计费。您可以点击【创建实例】来通过预留实例计费创建云服务器，也可以点击【查看账单】来查看预留实例计费的抵扣详情。

   ![image-20200909173059650](https://main.qcloudimg.com/raw/86912bb5b8ceabbb071fbb6cfa06cadf.png)
