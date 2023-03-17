# Kafka cluster chart

1. Create namespace

    ```bash
    k create namespace kafka
    ```

2. Install strimzi kafka operator

    ```bash
    helm repo add strimzi https://strimzi.io/charts/
    ```

3. Install release chart

    ```bash
    helm install strimzi-kafka  strimzi/strimzi-kafka-operator --namespace kafka
    ```

4. Install helm chart

    ```bash
    helm install kafka-cluster kafka-cluster-chart  \
    --values kafka-cluster-chart/values.yaml \
    --namespace kafka
    ```

5. Generate user certificate

    ```bash
    make create-secret cluster=cluster user=user password=123qweasdzxc
    ```

6. Update helm chart (optinal)

    ```bash
    helm upgrade kafka-cluster kafka-cluster-chart  \
    --values kafka-cluster-chart/values.yaml \
    --namespace kafka
    ```
