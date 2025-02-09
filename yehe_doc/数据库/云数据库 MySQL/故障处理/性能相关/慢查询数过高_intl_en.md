## Issue Description
When a slow query problem occurs, it is usually accompanied by the simultaneous surge of multiple monitoring metrics, such as CPU utilization and the number of slow queries.

## Possible Causes
Generally, this is because that the execution efficiency of SQL statements is not high enough, which causes a large number of requests to accumulate in TencentDB for MySQL. There are two common causes:
- [](id:yy1)Cause 1: the SQL statements didn't use indexes or used inefficient indexes.
- [](id:yy2)Cause 2: the QPS pressure exceeded the load limit of the current instance.

## Solutions
There are different solutions for the two possible causes:
- Solution 1: optimize the SQL statements to improve their execution efficiency. For more information, please see [Measure 1](#cs1).
- Solution 2: adjust the configuration of the TencentDB for MySQL instance to meet QPS requirement. For more information, please see [Measure 2](#cs2).

## Troubleshooting Procedure
### [Measure 1: optimize SQL statements](id:cs1)
You can directly use DBbrain to optimize slow queries, which will analyze the SQL statements and give advice for adding indexes.
1. Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/performance/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database at the top and select the **Slow SQL Analysis** tab.
2. You can click a single time period or drag to select multiple time periods for slow queries in the **SQL Statistics** bar chart, and the aggregated SQL template and execution information (including the number of executions, total execution duration, scanned rows, and returned rows) will be displayed below.
![](https://main.qcloudimg.com/raw/0659dcb5dfb47bf00c4df2646946f0ce.png)
3. Click an aggregated SQL template, and specific SQL analysis and statistics will be displayed on the right. You can view the corresponding index advice.
![](https://main.qcloudimg.com/raw/f72dcf38d05fc7381007502e930f3014.png)

### [Measure 2: adjust the TencentDB for MySQL instance configuration](id:cs2)
View the Reference Test Result in [Performance White Paper](https://intl.cloud.tencent.com/document/product/236/8842) of each instance specification, compare it with the QPS data of the current instance, and adjust the corresponding [MySQL CPU and memory specifications](https://intl.cloud.tencent.com/document/product/236/19707).
