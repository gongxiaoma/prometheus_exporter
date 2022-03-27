# prometheus_exporter  
附：exporter采集数据到prometheus，安装exporter自动注册到consul。  
  
## kafka-exporter  
### kafka-exporter安装  
使用集群模式监控，只需在集群其中一个节点安装即可。如果监控云Kafka，选择一台应用服务器做代理即可。  
+ bash install_kafka_exporter.sh 10.1.9.1:9092 10.1.9.2:9092  10.1.9.3:9092  
+ systemctl daemon-reload  
+ systemctl restart kafka_exporter  

### 告警设置
- alert: KafkaConsumerGroupLag1
  expr: kafka_consumergroup_lag{id="erp-10.1.9.1-kafka", consumergroup!~"oa|erp", topic!="test"} > 50000
  for: 5m
  labels:
    severity: "一般告警"
    tag: erp
  annotations:
    message: "来源：prometheus\n项目：{{ $labels.project }}\n环境：{{ $labels.environment }}\n服务：{{ $labels.service }}\n主机：{{ $labels.instance }}\n详情：Kafka {{ $labels.id }} 消费组 {{$labels.consumergroup}} topic {{$labels.topic}} 单个分区 {{$labels.partition}} 消息堆积数超过5万条\n当前值：{{ humanize $value }}\n联系人：{{ $labels.user }}\n"
- alert: KafkaConsumerGroupLag2
  expr: kafka_consumergroup_lag{id="erp-10.1.9.1-kafka", consumergroup!~"oa|erp", topic!="test"} > 100000
  for: 5m
  labels:
    severity: "严重告警"
    tag: erp
  annotations:
    message: "来源：prometheus\n项目：{{ $labels.project }}\n环境：{{ $labels.environment }}\n服务：{{ $labels.service }}\n主机：{{ $labels.instance }}\n详情：Kafka {{ $labels.id }} 消费组 {{$labels.consumergroup}} topic {{$labels.topic}} 单个分区 {{$labels.partition}} 消息堆积数超过10万条\n当前值：{{ humanize $value }}\n联系人：{{ $labels.user }}\n"

 
 
