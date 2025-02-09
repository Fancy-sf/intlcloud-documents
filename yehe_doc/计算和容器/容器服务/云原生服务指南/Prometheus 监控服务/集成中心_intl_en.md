TMP integrates commonly used programming languages, middleware, big data, and infrastructure databases. It supports quick installation and custom installation. You only need to follow the instructions to monitor the corresponding components. It also provides out-of-the-box Grafana monitoring dashboards. The integration center covers three major monitoring scenarios of basic service monitoring, application layer monitoring, and TKE cluster monitoring, making it easier for you to connect and use.


 ## List of Supported Services

 <table>
	<tr>
	<th>Service Type</th>
	<th>Service</th>
	<th>Monitoring Metric</th>
	<th>Quick Installation</th>
	<th>Integration Guide</th>
	</tr>
	<tr>
		<td rowspan="2">Big data</td>
		<td>Elasticsearch</td>
	<td>Cluster/Index/Node monitoring</td>
<td>Supported</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43223">Elasticsearch Exporter Integration</a></td>
	</tr>
    <tr>
	    <td>Flink</td>
		<td>Cluster/Job/Task monitoring</td>
		<td>Not supported</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43217">Flink Integration</a></td>
	</tr>
	<tr>
		<td rowspan="3">Programming language</td>
		<td>Go</td>
		<td>GC/Heap/Thread/Goroutine monitoring</td>
		<td>Not supported</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43221">Go Application Integration</a></td>
	</tr>
	<tr>
		<td>JVM</td>
		<td>Heap/Thread/GC/CPU/File monitoring</td>
		<td>Not supported</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43220">JVM Integration</a></td>
	</tr>
	<tr>
		<td>Spring MVC</td>
		<td>HTTP API/Exception/JVM monitoring</td>
			<td>Not supported</td>
			<td><a href="https://intl.cloud.tencent.com/document/product/1116/43219">Spring Boot Integration</a></td>
	</tr>
	<tr>
		<td rowspan="4">Middleware</td>
		<td>Kafka</td>
		<td>Broker/Topic/Consumer group monitoring</td>
		<td>Supported</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43224">Kafka Exporter Integration</a></td>
	</tr>
		<tr>
		<td>Consul</td>
		<td>Consul monitoring</td>
		<td>Supported</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43230">Consul Exporter Integration</a></td>
	</tr>
			<tr>
		<td>etcd</td>
		<td>etcd monitoring</td>
		<td>Not supported</td>
				<td>-</td>
	</tr>
			<tr>
		<td>Istio</td>
		<td>Istio monitoring</td>
		<td>Not supported</td>
				<td>-</td>
	</tr>
	<tr>
		<td>Infrastructure</td>
		<td>Kubernetes</td>
		<td>API server/DNS/Workload/Network monitoring</td>
		<td>Supported</td>
						<td><a href="https://intl.cloud.tencent.com/document/product/1116/43183">Agent Management</a></td>
</tr>
	<tr>
		<td rowspan="5">Database</td>
		<td>TencentDB for MongoDB</td>
		<td>File count/Read and write performance/Network traffic monitoring</td>
		<td>Supported</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43225">MongoDB Exporter Integration</a></td>
</tr>
<tr>
		<td>TencentDB for MySQL</td>
		<td>Network/Connection count/Slow query monitoring</td>
		<td>Supported</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43229">MySQL Exporter Integration</a></td>
</tr>
<tr>
		<td>TencentDB for PostgreSQL</td>
		<td>CPU/Memory/Transaction/Lock/Read/Write monitoring</td>
			<td>Supported</td>
		<td><a href="https://intl.cloud.tencent.com/document/product/1116/43226">PostgreSQL Exporter Integration</a></td>
</tr>
<tr>
		<td>TencentDB for Redis</td>
		<td>Memory utilization/Connection count/Command execution status monitoring</td>
		<td>Supported</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43228">Redis Exporter Integration</a></td>
</tr>
<tr>
		<td>TencentDB for Memcached</td>
	<td>Memcached monitoring</td>
	<td>Supported</td>
				<td><a href="https://intl.cloud.tencent.com/document/product/1116/43231">Memcached Exporter Integration</a></td>
</tr>
<tr>
		<td>Inspection</td>
		<td>Health check</td>
		<td>Blackbox can be used to regularly test the connectivity of the target service, helping you stay up to date with the service health and discover exceptions in time.</td>
			<td>Supported</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43233">Health Check</a></td>
</tr>
<tr>
		<td >CM</td>
		<td>Cloud Monitoring</td>
		<td>Tencent Cloud service monitoring</td>
			<td>Supported</td>
<td>-</td>
</tr>
<tr>
		<td rowspan="2">Custom</td>
		<td>Scrape task</td>
		<td>The native `static_config` can be used to configure a scrape task.</td>
			<td>Supported</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43214">Scrape Configuration Description</a></td>
</tr>
<tr>
		<td>CVM scrape task</td>
		<td>The extended `cvm_sd_config` can be used to configure a CVM scrape task.</td>
			<td>Supported</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1116/43214">Scrape Configuration Description</a></td>
</tr>
</table>



## Directions
### Quick installation
Some services support quick agent installation. For more information, see [Integration Center](https://intl.cloud.tencent.com/document/product/1116/43163).

1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Go to the instance details page and click **Integration Center**.
4. In the **Integration Center**, select the service that supports quick installation and click **Install** in the bottom-left corner.
![](https://qcloudimg.tencent-cloud.cn/raw/270a1592ff70e8cdfc2d446d4ec02222.png)
5. On the integration list page, enter the metric collection name, address, and other information and click **Save**. The following takes Kafka as an example.
![](https://qcloudimg.tencent-cloud.cn/raw/98888f5b23e80e6b7279084e64247994.png)

### Custom installation
1. Log in to the [TMP console](https://console.cloud.tencent.com/monitor/prometheus).
2. In the instance list, select the corresponding TMP instance.
3. Go to the instance details page and click **Integration Center**.
4. Select the target service in the integration center. You can click **Integration Guide** to view the integration guide. After successful integration, you can monitor the corresponding service in real time. You can also click **Install/Upgrade** in **Dashboard Operation** to install or upgrade the Grafana dashboard for the service.
![](https://qcloudimg.tencent-cloud.cn/raw/9f2ad0a579a4677f7f2fe1da1af970fb.png)

