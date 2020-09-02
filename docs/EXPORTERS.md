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

### InfluxDB

Vamos subir um InfluxDB para coletar algumas métricas.

```bash
docker run -ti --rm -d --network bubble \
    -e INFLUXDB_ADMIN_USER_PASSWORD=admin \
    --name influxdb bitnami/influxdb:latest
```

Para acessar o CLI do Influx, rode:

```bash
docker exec -ti influxdb \
    influx -username admin -password admin
```

Vamos usar o Chronograf para verificar os dados do InfluxDB.

```bash
docker run -ti --rm -d --network bubble -p 8888:8888 chronograf
```

Abra **[http://localhost:8888](http://localhost:8888)** para acessá-lo.

### MySQL Exporter

```bash
docker run -ti --rm -d -p 9104:9104 --link=container --network bubble \
        -e DATA_SOURCE_NAME="root:root@(container:3306)/database" prom/mysqld-exporter
```