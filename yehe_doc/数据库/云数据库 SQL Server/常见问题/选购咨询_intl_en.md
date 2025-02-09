### How do I select an appropriate architecture of TencentDB for SQL Server?
TencentDB for SQL Server offers the following architectures: Basic Edition (single-node architecture), Dual-Server High Availability Edition (primary/replica dual-node architecture), and Cluster Edition (primary/replica dual-node architecture). To guarantee the instance's high availability, we recommend you select a dual-node architecture (Dual-Server High Availability or Cluster Edition). If your business requires to open the SA permissions, you can use the Basic Edition. Differences between those architecture editions are as detailed below:
- Dual-Server High Availability Edition: It supports the database mirroring (high-availability replication) scheme to enable automatic switch in seconds, lowering the data loss to "zero".
- Cluster Edition: It supports SQL Server 2017 and 2019 and adopts the Always On technology to build a SQL Server cluster that features high performance, high availability, high reliability, and easy maintenance.
- Basic Edition: It is deployed on a single node with storage/computing separation, uses Premium Cloud Storage cloud disks for three-replica storage to avoid data losses, and fully opens up its SA permissions.

For detailed differences, see [Architecture](https://intl.cloud.tencent.com/document/product/238/3254) and [Instance Types](https://intl.cloud.tencent.com/document/product/238/46494).

### How do I select an appropriate TencentDB for SQL Server architecture and edition if my business requires read-only instances?
If read-only instances are required, we recommend you use SQL Server 2017/2019 Enterprise Cluster Edition to sync data more efficiently and stably. For more information, see [Read-Only Instance Overview](https://intl.cloud.tencent.com/document/product/238/43142) and [Read-Only Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46493).

### How is the performance of TencentDB for SQL Server?
TencentDB for SQL Server provides the single-node architecture (Basic Edition) and primary/replica dual-node architecture (Dual-Server High Availability and Cluster Editions):
- The highest TPM of the single-node architecture (Basic Edition - Premium Cloud Storage) is 1.32 million.
- The highest TPM of the single-node architecture (Basic Edition - SSD cloud disk) is 1.38 million.
- The highest TPM of the primary/replica dual-node architecture (Dual-Server High Availability/Cluster Edition) is 4.58 million.

For more information, see [Performance Test Report](https://intl.cloud.tencent.com/document/product/238/32561).

[](id:ZCLNXGG)
### Which specifications does TencentDB for SQL Server support?
For specifications of TencentDB for SQL Server Basic, Dual-Server High Availability, and Cluster Edition instances, see [Primary Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46492). For specifications of read-only instances, see [Read-Only Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46493).

### How do I select an appropriate TencentDB for SQL Server instance specification?
The TencentDB for SQL Server instance specification can be selected based on two factors: required storage capacity and performance. For supported instance specifications, see [Primary Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46492) and [Read-Only Instance Specifications](https://intl.cloud.tencent.com/document/product/238/46493). For performance details, see [Performance Test Report](https://intl.cloud.tencent.com/document/product/238/32561).

### In which regions is TencentDB for SQL Server available?
For regions and AZs where TencentDB for SQL Server can be deployed, see [Regions and AZs](https://intl.cloud.tencent.com/document/product/238/7520).

### How is the version compatibility of TencentDB for SQL Server?
TencentDB for SQL Server is backward compatible. For example, you can upgrade or migrate TencentDB for SQL Server 2016 to 2019 but cannot downgrade or migrate TencentDB for SQL Server 2019 to 2016.

### What features does TencentDB for SQL Server offer?
Supported features vary by TencentDB for SQL Server edition. For more information, see [Features and Differences](https://intl.cloud.tencent.com/document/product/238/46495) and [Constraints and Limits](https://intl.cloud.tencent.com/document/product/238/2021).

### What are the feature differences between different TencentDB for SQL Server editions?
For features supported by different TencentDB for SQL Server editions, see [Features and Differences](https://intl.cloud.tencent.com/document/product/238/46495).

[](id:DSGSJK)
### How many databases can I create at most in a TencentDB for SQL Server instance?
For performance considerations, we recommend you create databases in a TencentDB for SQL Server instance within the following limits:
- Basic Edition: The number of databases that can be created is unlimited theoretically, but we recommend you keep it below 100.
- Dual-Server High Availability/Cluster Edition: The number of databases that can be created is limited in the console, but we recommend you keep it below 70.

You can also use SSMS to connect to the instance and create databases, and databases created via SSMS will be automatically synced to the replica instance. However, to avoid exceptions during primary-replica sync, we recommend you not create more databases than the relevant limit.

### Does TencentDB for SQL Server support real-time hot backup?
TencentDB for SQL Server Dual-Server High Availability/Cluster Editions both support real-time hot backup in a one-primary-one-replica architecture.

### What are the use cases of TencentDB for SQL Server?
TencentDB for SQL Server can be used in various use cases, including industry utility, mobile OA, gaming, healthcare, medicine, media, internet, IoT, retail, ecommerce, logistics, securities, technical service, automobile, travel, and finance. For more information, see [Use Cases](https://intl.cloud.tencent.com/document/product/238/3248).

### What high availability and disaster recovery capabilities does TencentDB for SQL Server have?
TencentDB for SQL Server provides disaster recovery capabilities at different levels, including instance, server, data center, AZ, and region, to ensure the business continuity on healthy systems with the minimum data loss in case of natural disasters, device failures, and maloperations.
Backup is the basis of all disaster recovery systems and the last line of defense in the high data availability architecture. TencentDB for SQL Server features rich backup capabilities, ensuring that the data can be restored quickly even after a total system crash to guarantee the business continuity as much as possible.
TencentDB for SQL Server provides instances in various architectures with guaranteed high availability:
- A Dual-Server High Availability Edition instance is in the primary/replica dual-node architecture, where the underlying layer is deployed on a physical machine. It supports the database mirroring (high-availability replication) scheme to implement automatic HA switch within seconds.
- A Cluster Edition instance is in the primary/replica dual-node architecture, where the underlying layer is deployed on a physical machine. It adopts the Always On technology to build a SQL Server cluster that features high performance, high availability, high reliability, and easy maintenance and implements automatic HA switch within seconds.
- A Basic Edition instance is in the single-node architecture, where the underlying layer is deployed in a CVM instance, storage and computing are separated, and data is stored in three replicas in Premium Cloud Storage to avoid data loss. In extreme cases where an instance fails, a new instance will be started to automatically restore the data from data and log backups. The specific restoration time is subject to the data volume. The servers of two TencentDB instances are usually on the same physical machine.

For intra-region disaster recovery, TencentDB for SQL Server provides multi-AZ deployment capabilities. Different AZs in the same region are interconnected over the private network, and failures can be isolated between AZs. For instances in the primary/replica dual-node architecture, the primary and replica instances can be deployed in different AZs in the same region (for example, one primary instance in the primary AZ and one replica instance in the replica AZ). This improves the business continuity and guarantees the data availability in case of instance failures or AZ disconnections. You can also manually switch between the primary and replica instances in the console to verify the business robustness. Switches within the same AZ and between different AZs are imperceptible to the application.

For remote disaster recovery, cross-region backup capabilities are offered to store backup files in another region. You can set the cross-region backup retention period and multiple backup regions. After a cross-region backup policy is enabled, the instance backup files will be automatically stored in the target region. In this way, if an instance in a region fails, you can restore its backup files in the remote region to a new instance there for guaranteed business continuity. Cross-region backup implements the high availability of database restoration and meets the requirements for data availability and security, remote backup and restoration, remote disaster recovery, long-term data archive, and regulation compliance.

In addition, TencentDB for SQL Server also has rich backup capabilities to guarantee the data security and prevent data loss or corruption. Specifically, you can configure automatic backup, manual backup, data backup, log backup, backup file format (unarchived files or archive file), instance backup, and multi-database backup. You can also customize the backup policy, backup retention period (7–1,830 days), and backup cycle.

Moreover, TencentDB for SQL Server comes with comprehensive disaster recovery capabilities at both the data and business management layers. Cross-region disaster recovery for databases is meaningful only if the business also features cross-region disaster recovery. However, cross-region distributed deployment of the business inevitably causes the split-brain problem. At the business management layer, the business is deployed in three AZs (two intra-region AZs and one remote AZ) to ensure the business continuity. Before an actual failover occurs, the system will always check whether the database sync status (database sync system table) is normal to avoid faulty failover.

[](id:NXCPYS)
### What strengths does TencentDB for SQL Server have?
Licensed by Microsoft, TencentDB for SQL Server continuously provides you with the latest features and helps you avoid the risks with unauthorized use of the software. It features out-of-the-box usage, high stability, reliability, and security, elastic scaling, data security protection, and failover in a matter of seconds, enabling you to focus more on application development itself.
- Diverse editions: Three deployment architectures are available, namely, single-node architecture on Basic Edition, dual-node architecture on Dual-Server High Availability Edition (mirror), and dual-node architecture on Cluster Edition (Always On), to comprehensive guarantee the high service availability.
- Genuine license: Licensed by Microsoft, TencentDB for SQL Server continuously provides you with the latest features, helping you avoid the risks of using unauthorized software and enhance the trustworthiness of your business in competitive markets.
- Excellent performance: The new ultra-high specification of 90-core 720 GB MEM is released, with a TPM of up to 4.5 million. Both performance and cost performance have been improved by more than 30% once again, breaking Tencent Cloud's own performance record in the industry.
- High stability and reliability: TencentDB for SQL Server delivers a 99.9996% data reliability and 99.95% service availability. It provides easy-to-use cloud-based control capabilities, such as monitoring and alarming, backup and restoration, data migration, and elastic scaling.
- Ease of management: Various management tasks can be finished with ease in the Tencent Cloud console or SSMS, such as database management, permission configuration, and monitoring and alarming. This eliminates your concerns over database installation and Ops.
- Monitoring and alarming: Dozens of key metrics can be viewed in the console, such as the number of connections and requests, disk I/O, and buffer hit rate, helping you comprehensively monitor database conditions and accurately understand the database load and system health. User-defined resource threshold alarms are supported to help you discover database exceptions timely and resolve potential system problems quickly.
- BI: SSIS + BI analysis services are provided, which integrate data storage, ETL, and visual analysis to help meet your diversified needs in various use cases, including BI analysis, high-value data mining, and primary data management system setup.

### What strengths does TencentDB for SQL Server have over self-built SQL Server?
TencentDB for SQL Server has the following strengths over self-built databases:
<table>
<thead><tr><th>Feature</th><th>TencentDB for SQL Server</th><th>Self-Built SQL Server</th></tr></thead>
<tbody>
<tr>
<td>Service availability</td><td>For more information, see <a href="https://intl.cloud.tencent.com/document/product/238/3252" target="_blank">Service Level Agreement</a>.</td><td>You have to guarantee the service availability and set up primary/replica replication and RAID capabilities on your own.</td></tr>
<tr>
<td>System security</td><td>Anti-DDoS is supported, and various database security vulnerabilities are fixed in time. The data security meets all mainstream national and international security standards.</td><td>You have to deploy security services and fix vulnerabilities on your own at high costs. Security compliance is not guaranteed, and the security requirements cannot be quickly met.</td></tr>
<tr>
<td>Database performance</td><td>High-performance devices with a TPM of up to 4.5 million are used. For more information, see <a href="https://intl.cloud.tencent.com/document/product/238/32561" target="_blank">Performance Test Report</a>.</td><td>General devices without optimization and fine-tuning are used.</td></tr>
<tr>
<td>Software and hardware investment</td><td>No hardware or software investment is required, and the service is pay-as-you-go.</td><td>Database servers are costly.</td></tr>
<tr>
<td>System hosting</td><td>There are no hosting fees.</td><td>The hosting fees are high.</td></tr>
<tr>
<td>Deployment and scaling</td><td>The out-of-the-box service can be quickly deployed and elastically scaled.</td><td>You have to purchase hardware devices, host them in data centers, and deploy them on your own. You also have to solve stability problems and set up many supporting modules and management tools, which require heavy investments in technology and take a long period of time.</td></tr>
<tr>
<td>Resource utilization</td><td>The service is billed by the actual usage and supports elastic scaling to ensure a high resource utilization.</td><td>You have to consider traffic spikes, and the resource utilization is low.</td></tr>
<tr>
<td>Data disaster recovery</td><td>Primary/Replica replication and backup are configured by default. Both intra-region and cross-region disaster recovery schemes are supported, such as multi-AZ deployment and cross-region backup.
</td><td>You have to find the backup storage space and regularly verify whether backups can be restored, which cost more money and time.</td></tr>
<tr>
<td>Control and management services</td><td>Comprehensive cloud-based instance lifecycle management capabilities are available for various objects, including monitoring and alarming, backup and restoration, instance, database, account, network, parameter, and log.</td><td>You have to implement all control and management capabilities on your own.</td></tr>
<tr>
<td>Procurement costs</td><td>Instances are priced transparently and even more cost-effective than CVM.</td><td>In addition to instances, you also have to set up disaster recovery, monitoring, and management systems on your own at totally uncontrollable costs.</td></tr>
<tr>
<td>License</td><td>Genuine licenses from Microsoft continuously provide you with the latest features, eliminating your need to purchase additional licenses.</td><td>Pirated services lead to legal risks, while genuine licenses are expensive.</td></tr>
<tr>
<td>Ops costs</td><td>Tencent Cloud provides a professional team to guarantee the service quality for key accounts 24/7, eliminating your need to manually perform Ops.</td><td>You have to hire dedicated DBAs for database maintenance, which incurs high labor costs.</td></tr>
</tbody></table>

[](id:QYDSQL)
### How do I migrate data to TencentDB for SQL Server?
You can migrate data from self-built SQL Server databases in local IDCs, CVM instances, and cloud servers provided by other cloud vendors, cloud SQL Server databases provided by other cloud vendors, and TencentDB for SQL Server databases to TencentDB for SQL Server through either [cold backup migration](https://intl.cloud.tencent.com/document/product/238/39005) or [DTS](https://intl.cloud.tencent.com/document/product/238/39006) as appropriated based on your business scenarios.
- If your business allows you to shut down the database for backup, you can use [cold backup migration ](https://intl.cloud.tencent.com/document/product/238/39005), i.e., restoring data from .bak backup files to migrate the source database to a TencentDB for SQL Server instance. You can download COS files or upload local files for migration. Three data restoration modes are supported: full backups, full backups + log backups, and full backups + differential backups.
- If your business doesn't allows you to shut down the database and requires smooth migration, you can [use DTS for migration](https://intl.cloud.tencent.com/document/product/238/39006). DTS supports two migration modes: full migration and full + incremental migration. It supports multiple access types, such as public network, self-build on CVM, Direct Connect, VPN, CCN, and database.
