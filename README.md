# prometheus_exporter
附：exporter采集数据到prometheus，安装exporter自动注册到consul。

1、kafka-exporter
分集群模式和单机模式两种监控方式，我这里选择集群模式，只需要在集群其中一个节点安装接口。如果监控云Kafka，选择一台应用服务器做代理安装即可。
bash install_kafka_exporter.sh 10.1.9.1:9092 10.1.9.2:9092  10.1.9.3:9092

备注：如果kafka开启了sasl认证，需要更新systemd文件或者改成手动启动，具体sasl相关参数请见kafka配置。
更新systemd文件
修改/usr/lib/systemd/system/kafka_exporter.service文件的ExecStart参数，示例：
ExecStart=/usr/local/prometheus/kafka_exporter/kafka_exporter --kafka.server=10.1.9.1:9092 --kafka.server=10.1.9.2:9092 --kafka.server=10.1.9.3:9092 --topic.filter=^[A-Za-z0-9].* --sasl.enabled --sasl.username='username' --sasl.password='xxx' --sasl.mechanism='scram-sha256' --kafka.version='版本'
 
启动
systemctl daemon-reload
systemctl restart kafka_exporter
 
 
