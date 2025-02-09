## Overview
This document describes how to create a container-based EMR cluster in the EMR console.
## Prerequisites
1. You have completed the role authorization. For more information, see [Role Authorization](https://intl.cloud.tencent.com/document/product/1026/34539).
2. You have completed the COS authorization. When you create a cluster, if COS access has not been granted, the following prompt will be displayed. Click **Authorize now** to authorize COS. After successful COS authorization, you won't need to authorize COS again when creating clusters in the future.
<img src="https://qcloudimg.tencent-cloud.cn/raw/ae0386f2599df15cec25a53c2b5818a4.png" style="zoom:50%;" />

## Directions
1. Log in to the [EMR console](https://console.cloud.tencent.com/emr/static/containerdeploy) and click **Create Cluster** on the container-based cluster list page.
![](https://qcloudimg.tencent-cloud.cn/raw/5896d77781f4688682577b4cc7c1f0dc.png)
2. On the **Create Cluster** page, configure the following items:
	
| Field | Description |
|---------|---------|
| Cluster Name 	| <li>The name can contain 6–36 letters, digits, hyphens, and underscores. <li>A random cluster name will be generated by default. |
| Region 	| A region is the physical location of an IDC. Currently supported regions include Beijing, Shanghai, Guangzhou, and Nanjing. |
| Cluster Type 	| Currently, the Spark cluster type is supported. |
| Component Version 	| Components and their version information under the selected cluster type. |
| Container Type | If you want to select a EKS cluster but there is none in your region, a hidden EKS cluster (counted against the quota) will be automatically created to expand EMR compute resources. |
| Container Network 	| Set a network dedicated for the hidden EKS cluster. If you have selected a container network for this EKS cluster, it is bound and cannot be changed. |
| COS Bucket | <li>Select an existing bucket or create a new one in the COS console. <li>Before using COS, you need to grant COS read/write permissions to the EMR cluster first. |

3. Click **Create**. Then, you can view the newly created cluster in the EMR console.