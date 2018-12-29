docker-confluent
----------------

Docker images for deploying and running Kafka services based on the [Confluent Platform](https://www.confluent.io/product/confluent-platform/).

[![Docker Repository on Quay](https://quay.io/repository/nordstrom/confluent-kafka-broker/status "Docker Repository on Quay")](https://quay.io/repository/nordstrom/confluent-kafka-broker)

## about

The images are based on [confluentinc/cp-docker-images](https://github.com/confluentinc/cp-docker-images) and have been modified to:
- Execute as non-privileged users
- Include a [Prometheus JMX exporter](https://github.com/prometheus/jmx_exporter)
- Include a [customized PrincipalBuilder](https://github.com/Nordstrom/kafka-regex-principal-builder)
- Remove behaviors attached to `KAFKA_ADVERTISED_LISTENERS` env variable

## example

Build and run with [Docker Compose](https://docs.docker.com/compose/):

```
docker-compose build
docker-compose up
kafkacat -b localhost:9092 -L
curl -s http://localhost:9011/metrics
```

- view RegexPrincipalBuilder metrics (ErrorsPerSec, RequestsPerSec)

```
curl -s http://localhost:9011/metrics | grep kafka_security_RegexPrincipalBuilder
```
