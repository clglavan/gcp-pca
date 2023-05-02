# gcp-pca


## Cloud Pub/Sub
- global messaging and ingestion service, based on at-least-once publish/subscribe model
- connects many services together and helps small increments of data to flow better
- supports both push and pull modes with exactly-once processing
- pull mode delivers message and waits for ACK
- Cloud pub/sub features:
  - truly global: consistent latency from anywhere
  - messages can be ordered and/or filtered
  - lower-cost Pub/Sub Lite is available, requiring more management and lower availability and durability
