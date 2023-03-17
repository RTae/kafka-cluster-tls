FROM quay.io/strimzi/kafka:0.33.1-kafka-3.3.1
USER root:root

RUN mkdir -p /opt/kafka/plugins
ADD https://repo1.maven.org/maven2/io/debezium/debezium-connector-sqlserver/1.9.7.Final/debezium-connector-sqlserver-1.9.7.Final-plugin.tar.gz /opt/kafka/plugins
RUN cd /opt/kafka/plugins && tar -xzf debezium-connector-sqlserver-1.9.7.Final-plugin.tar.gz && rm -rf debezium-connector-sqlserver-1.9.7.Final-plugin.tar.gz**
USER 1001 