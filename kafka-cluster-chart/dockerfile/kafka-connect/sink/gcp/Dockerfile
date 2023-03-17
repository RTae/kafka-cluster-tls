FROM quay.io/strimzi/kafka:0.33.1-kafka-3.3.1
USER root:root

RUN mkdir -p /opt/kafka/plugins
ADD https://github.com/aiven/gcs-connector-for-apache-kafka/releases/download/v0.9.0/aiven-kafka-connect-gcs-0.9.0.tar /opt/kafka/plugins
RUN cd /opt/kafka/plugins && tar -xf aiven-kafka-connect-gcs-0.9.0.tar && rm -rf aiven-kafka-connect-gcs-0.9.0.tar

USER 1001