FROM confluentinc/cp-kafka:5.0.1

RUN groupadd -g 1000 broker \
 && useradd -r -m -u 1000 -g broker broker \
 && chown -hR broker:broker /var/lib/kafka \
 && chown -hR broker:broker /var/log/kafka

ENV PROMETHEUS_JMX_EXPORTER_PORT=9011
ENV PROMETHEUS_JMX_EXPORTER_CONF=/etc/jmx_exporter/kafka_broker.yaml
ENV PROMETHEUS_JMX_EXPORTER_VERSION=0.3.1

RUN mkdir -p /etc/jmx_exporter /opt/lib \
 && curl -L "https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/$PROMETHEUS_JMX_EXPORTER_VERSION/jmx_prometheus_javaagent-$PROMETHEUS_JMX_EXPORTER_VERSION.jar" \
  -o /opt/lib/jmx_prometheus_javaagent.jar \
 && echo "---" > $PROMETHEUS_JMX_EXPORTER_CONF \
 && sed -i "s/^EXTRA_ARGS=.*/EXTRA_ARGS=\${EXTRA_ARGS-'-name kafkaServer -loggc -javaagent:\/opt\/lib\/jmx_prometheus_javaagent.jar='\$PROMETHEUS_JMX_EXPORTER_PORT:\$PROMETHEUS_JMX_EXPORTER_CONF}/" /usr/bin/kafka-server-start

# Add customer principal builder and set permissions on jar file for read by group/others.
ADD https://github.com/Nordstrom/kafka-regex-principal-builder/releases/download/v0.0.3/kafka-regex-principal-builder-0.0.3.jar /usr/share/java/kafka/
RUN chmod 644 /usr/share/java/kafka/kafka-regex-principal-builder-0.0.3.jar

USER broker
