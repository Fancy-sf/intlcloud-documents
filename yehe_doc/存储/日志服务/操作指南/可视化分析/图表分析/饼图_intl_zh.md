饼图描述的是不同分类的占比情况，通过扇区大小来衡量各分类项的占比情况。错误码占比情况分析等占比统计场景适用。

## 图表配置

### 通用配置



| 配置项   | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 基础信息 | 图表名称：设置图表的显示名称，可为空。                                 |
| 图例     | 设置图表的图例内容，可以控制图例的样式与位置。同时也支持在图例中添加对比数据。 |
| 标准配置 | 设置图表内所有指标类型的字段单位。详情请参考 [单位配置](https://intl.cloud.tencent.com/document/product/614/47788)。     |


### 饼图配置



| 配置项 | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| 饼图   | 展示方式：控制饼图的样式，实心为饼图，空心为环形图。<br />排序方式：控制扇区的排序方式，支持升序或降序，默认不排序。<br />扇区合并：合并 TOPN 以外的扇区为一个其他分区。当扇区分类过多时，可用此功能聚焦 TOPN 对象。默认不合并。<br />标签：显示饼图标签，可选择标签内容为：名称、数值、百分比中的一项或多项。 |

标签示例：
![](https://qcloudimg.tencent-cloud.cn/raw/afa20ede15058bb180dfc771aa2189dc.png)





