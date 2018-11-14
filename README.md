docker-confluent
----------------

Docker images for deploying and running Kafka services based on the [Confluent Platform](https://www.confluent.io/product/confluent-platform/).

## about

The images are based on [confluentinc/cp-docker-images](https://github.com/confluentinc/cp-docker-images) and have been modified to:
- [x] Execute as non-privileged users
- [x] Include a [Prometheus JMX exporter](https://github.com/prometheus/jmx_exporter)
- [ ] Include a [customized PrincipalBuilder](https://docs.confluent.io/current/kafka/authorization.html#user-names)

## example

Build and run with [Docker Compose](https://docs.docker.com/compose/):

```
docker-compose build
docker-compose up
kafkacat -b localhost:9092 -L
curl http://localhost:9011/metrics
```
