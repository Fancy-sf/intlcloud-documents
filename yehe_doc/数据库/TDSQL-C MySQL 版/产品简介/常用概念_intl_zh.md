本文为您介绍产品相关的常用概念，帮助您更好地选购和使用 TDSQL-C MySQL 版。

## 相关概念
- **腾讯云控制台**：基于 Web 的用户界面。

- **地域**：地域是指物理的数据中心。一般情况下，TDSQL-C MySQL 版实例应该和云服务器实例位于同一地域，以实现最高的访问性能。
- **可用区**：可用区是指在某个地域内拥有独立电力和网络的物理区域。同一地域的不同可用区之间没有实质性区别。
- **多可用区**：是在单可用区的级别上，将同一地域的多个单可用区组合成的物理区域。
- **读写实例**：腾讯云上的 TDSQL-C MySQL 版数据库资源，一个集群中仅支持一个读写实例。
- **只读实例**：仅提供读功能的计算节点，一个集群中可包含0 - 15个只读实例。
- **计费模式**：实例资源的收费方式，分为包年包月、按量计费和 Serverless。
- **按量计费**：后计费购买，先按需申请资源使用，在结算时会按您的实际资源使用量收取费用。
- **包年包月**：预付费购买，用户根据自身对云资源的使用需求，一次性支付一个月、多个月或多年的费用。
- **Serverless**：后付费模式，即计算先按需设置最大和最小算力范围，在结算时会按您的实际计算和存储资源使用量收取费用。
- **实例类型**：包括通用型和独享型。
- **兼容数据库版本**：兼容的数据库版本，目前兼容 MySQL 5.7和8.0。
- **实例规格**：每个计算实例的规格配置，例如2核16GB。
- **项目**：用于对实例资源的分类和管理。
- **标签**：是腾讯云提供的云资源管理工具，您可以从不同维度对具有相同特征的云资源进行分类、搜索和聚合，从而轻松管理云上资源。
- **维护时间**：为保证云数据库实例的稳定性，后台系统会不定期对实例进行维护操作的一个时间范围。您可对业务实例设置自己可接受的维护时间，一般设置在业务低峰期，将对业务的影响降到最低。
- **安全组**：对实例进行安全的访问控制，指定进入实例的 IP、协议及端口规则。
- **网络**：由若干节点和连接这些节点的链路构成，表示诸多对象及其相互联系。出于性能安全考虑，目前仅支持私有网络（VPC）。
- **读写内网地址**：用户 VPC 网络内，分配给数据库使用并支持读请求和写请求的 IP 和 port。
- **只读内网地址**：用户 VPC 网络内，分配给数据库使用仅支持读请求的 IP 和 port。
- **读写外网地址**：提供外网访问，支持读请求和写请求的 IP 和 port。
- **只读外网地址**：提供外网访问，仅支持读请求的 IP 和 port。
- **端口**：port，指计算机内部或交换机路由器内的端口。
- **数据库**：是一个长期存储在计算机内的、有组织的、可共享的、统一管理的大量数据的集合。
- **数据库帐号**：用以登录管理数据库的用户名。
- **字符集**：包括字符编码集和字符编码，简单理解就是一个映射关系，一个编码规则。将字符集对应的码点映射为一个个二进制序列，从而使得计算机可以存储和处理。
- **云服务器**：（Cloud Virtual Machine，CVM）是腾讯云提供的可扩展的计算服务。
- **监控**：方便用户查看和掌握实例的运行信息，TDSQL-C MySQL 版提供丰富的性能监控项与便捷的监控功能（自定义视图、时间对比、合并监控项等）。
- **告警策略**：在某些监控指标异常时，创建告警来及时通知您采取措施。告警在一定周期内监控某些特定指标，并根据给定的阈值，每隔若干个时间段通过多种方式（微信、短信、邮件、电话和企业微信）发送告警通知。
- **回收站**：销毁的实例还未下线时存放的地方，可以在回收站恢复已销毁的实例。
- **备份**：为应对文件、数据丢失或损坏等可能出现的意外情况，将数据单独贮存或形成文件副本保存。
- **自动备份**：目前支持快照备份，通过设置备份的时间实现系统自主保存数据的方式。
- **手动备份**：支持在任意时间通过人为手动去创建备份文件的方式，手动备份暂时仅支持全量备份。
- **数据库审计**：记录对数据库的访问及 SQL 语句执行情况，帮助企业进行风险控制，提高数据安全等级。
