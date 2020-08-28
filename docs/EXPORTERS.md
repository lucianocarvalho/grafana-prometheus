# Exporters

A ideia aqui é coletar algumas métricas de ferramentas utilizadas no dia-a-dia.

### Apache Kafka Exporter

O exporter do Kafka utilizado é esse aqui: **[danielqsj/kafka_exporter](https://github.com/danielqsj/kafka_exporter)**.

```bash
docker run -ti --rm -d --network bubble --name kafkaexporter -p 9308:9308 danielqsj/kafka-exporter \
            --kafka.server=kafka1:9092 \
            --kafka.server=kafka2:9092 \
            --kafka.server=kafka3:9092
```

As métricas dos brokers serão acessíveis em **[http://localhost:9308/metrics](http://localhost:9308/metrics)**.

#### Algumas queries

```pomsql
# Puxando o offset atual de um tópico
kafka_topic_partition_current_offset{topic="benchmark"}

# Puxando o topic lag de um tópico
kafka_consumergroup_lag_sum{consumergroup="php-worker", topic="benchmark"}

# Offset atual de um consumer group
kafka_consumergroup_current_offset{consumergroup="php-worker", topic="benchmark"}
```