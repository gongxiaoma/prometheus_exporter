# prometheus_exporter
附：exporter采集数据到prometheus，安装exporter自动注册到consul。

## kafka-exporter
+ kafka-exporter安装
说明：分集群模式和单机模式两种监控方式，我这里选择集群模式，只需要在集群其中一个节点安装接口。如果监控云Kafka，选择一台应用服务器做代理安装即可。
bash install_kafka_exporter.sh 10.1.9.1:9092 10.1.9.2:9092  10.1.9.3:9092
systemctl daemon-reload
systemctl restart kafka_exporter
 
 
