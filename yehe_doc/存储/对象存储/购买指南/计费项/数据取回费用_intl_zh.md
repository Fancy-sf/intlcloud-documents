当读取低频存储、归档存储和深度归档存储类型的数据时，会产生数据取回费用，数据取回量根据用户实际读取的上述类型数据大小计算。

>?关于存储类型的更多介绍，请参见 [存储类型概述](https://intl.cloud.tencent.com/document/product/436/30925)。
> 


## 低频存储数据取回费用

| 计费项说明                                                   | 适用的存储类型 | 适用的计费方式 |
| ------------------------------------------------------------ | -------------- | -------------- |
| 对于低频存储类型的数据，当您读取或下载此类数据时，后台需要先取回数据后才可以读取或下载。 此类数据的取回费用按照用户实际读取的数据大小计算。 | 低频存储       | 按量计费       |

## 归档存储/深度归档存储数据取回费用

| 计费项说明                                                   | 适用的存储类型            | 适用的计费方式 |
| ------------------------------------------------------------ | ------------------------- | -------------- |
| 对于归档存储、深度归档存储类型的数据，未恢复（解冻）前不可读取和下载，如需读取和下载该类数据，需先恢复为标准存储类型的副本。此时数据取回也可以被称为数据解冻（即把归档数据恢复至标准数据这一过程）。 </br></br>按照不同的归档类型和恢复模式，划分为以下几种费用：<li>归档快速取回费用</li><li>归档标准取回费用</li><li>归档批量取回费用</li><li>深度归档标准取回费用</li><li>深度归档批量取回费用</li> | 归档存储</br>深度归档存储 | 按量计费       |


## 数据取回费用的计费方式和计算方法

<table>
   <tr>
      <th>计费方式</td>
      <th>适用的计费项</td>
      <th>计算方法 </td>
   </tr>
   <tr>
      <td rowspan=2>按量计费</td>
      <td><li>低频存储数据取回费用</li><li>归档存储数据取回费用</li></td>
      <td><li>按日结算</li><li>数据取回费用 = 每 GB 单价 x 日数据取回量</li></td>
   </tr>
   <tr>
      <td>深度归档取回费用</td>
      <td><li>按日结算</li><li>数据取回费用 = 每 GB 单价 x 日数据取回量</li></td>
   </tr>
</table>


## 数据取回定价

关于不同类型的数据取回单价，请查看 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。




## 计费案例

>?
> - 以下案例中出现的费用价格仅供参考，实际价格请参见 COS [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。
> - 存储量以二进制计算，例如1TB = 1024GB。
> 

### 案例：低频存储容量费用 + 低频存储数据取回费用 + 低频存储请求费用 + 外网下行流量费用

假设用户 B 于2020年11月1日上传了一个5GB低频存储类型的数据至广州地域的 COS 存储桶，产生了100次请求，第2天使用公网且不开启 CDN 的情况下读取该数据，产生了100次请求，其余时间无其他操作，按照每日对上一日产生的费用进行结算。那么：

- 低频存储容量费用：在2020年11月2日开始每天结算。
- 低频存储数据取回费用：在2020年11月2日结算。
- 低频存储请求费用：在2020年11月2日、3日结算。
- 外网下行流量费用：在2020年11月3日结算。
费用分析如下：


 - 低频存储容量费用 = 0.018美元/GB/月 /30 x 5GB x 30天 = 0.09美元
 - 低频存储数据取回费用 = 0.002美元/GB x 5GB = 0.01美元
 - 低频存储请求费用 = 0.01美元/万次 x 100次 / 10000 x 2 = 0.0002美元
 - 外网下行流量费用 = 0.1美元/GB x 5GB = 0.5美元

综合上面分析得出，整个11月用户 B 总花费0.09 + 0.01 + 0.0002 + 0.5 = 0.6002美元。
