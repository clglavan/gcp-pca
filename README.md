# gcp-pca

## Big Data

### Cloud IoT Core
- fully managed service to connect, manage and ingest device data globally
- device manager handles identity, authentication, configuration and control of devices
- protocol bridge publishes incoming telemetry data to Pub/Sub for processing
- Cloud IoT Core features
  - secure connection via HTTPS or MQTT
  - CA signed certs verify device ownershiptwo-way comms allow updates, on and offline
  - two-way comms allow updates, on and offline

### Cloud Pub/Sub
- global messaging and ingestion service, based on at-least-once publish/subscribe model
- connects many services together and helps small increments of data to flow better
- supports both push and pull modes with exactly-once processing
- pull mode delivers message and waits for ACK
- Cloud pub/sub features:
  - truly global: consistent latency from anywhere
  - messages can be ordered and/or filtered
  - lower-cost Pub/Sub Lite is available, requiring more management and lower availability and durability

### Cloud BigQuery
- a serverless, multi-regional, multi-cloud, SQL cloumn-store data warehouse
- scales to handle terabytes of data in seconds and petabytes in minutes
- built-in integration for machine learning and backbone for Business Inteliigence Engine
- supports real-time analytics with streams form Pub/Sub, Dataflow and Datastream
- automatically replicates data and keeps seven-day history of changes

### Cloud Dataprep
- visually explores, cleans and prepares data for analysis and machine learning, used by data analysts
- an integrated parner service operated by Trifacta in conjuction with Google
- automatically detects schemas, data types, possible joins and anomalies like missing values, outliers and duplicates.
- interprets data transformation intent by user selection and predicts next transformation
- transformation functions include: aggregation, pivot, unpivot, joins, union, extraction, calculation, comparison, condition, merge and regulat expressions
- works with CSV, JSON or relationa data from Cloud Storage, BigQuery or upload
- outputs to Dataflow, BigQuery or exports to other file formats

### Cloud Dataproc
- zonal resource that manages Spark and Hadoop clusters for batch MapReduce processing
- can be scaled (up or down) while running jobs
- offers image versioning to switch between versions of Spark, Hadoop and other tools
- best for migrating existing Spark or Hadoop jobs to cloud
- most VMs in cluster can be preemtible, but at least one node must be non-preemtible

### Cloud Dataflow
- new serverless, fast and cost-effective
- handles both batch and streaming data with one processing model
- fully managed service, suitable for a wide variety of data processing patterns
- horizontal autoscaling with reliable, consistent exactly-once processing
- based on the open-source Apache Beam
  - open source, unified model for defining both batch and streaming data-parallel processing pipelines
  - use a Beam SDK to build a program that defines the pipeline
  - as an Apache Beam supported distributed processing backend, Dataflow executes the pipeline

### Big data flowchart
- Need to explore, clean and prepare data for analysis
  - yes: Cloud Dataprep
  - no: Apache Hadoop/Spark ecosystem tools or dependencies?
    - yes: Cloud Dataproc
    - no: DevOps or Serverless?
      - DevOps: Cloud Dataproc
      - Serverless: Cloud Dataflow
