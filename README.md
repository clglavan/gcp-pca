# gcp-pca

# Processing Data

## Compute

### Fast-Booting VMs
- highly configurable, zonal service
- choose your machine type: General purpose, compute-optimized, memory-optimized or processor-optimized (GPU)
- select public or private disk image
- preemtible VMs
- sole-tenant node
- instance groups (managed and unmanaged)

### GKE
- regional, managed container service
- standard (total contro) and autopilot (fully managed)
- support auto repair and auto upgrade
- kubectl synax
- private clusters
- how to deploy, scale and expose services

### App Engine Standard
- regional, platform as a service for serverless applications
- zero server management and configuration
- instantaneous scaling, down to zero VMs
- standard environment features second generation: Python 3, Java 11, Node.js, PHP 7, Ruby, and Go 1.12+ ; first generation is more priprietary with limited runtimes

### App Engine Flex
- for containerized applications
- zero server management and configuration
- best for apps with consistent traffic where more gradual scaling is acceptable
- robutst runtimes such as Python 2.7/3.6, Java 8, Node.js, PHP 5/7, Ruby, Go and .Net

### Cloud Run
- great for modern websites, backend REST APIs and back-office administration
- regional, fully managed, serverless service for containers
- integrated support for all Cloud Operations services
- build on knative open-source standards for easy portability
- supports any language, any library and any binary

### Cloud Functions
- regional, event-driver, serverless Functions-as-a-Service FaaS
- Available triggers: HTTP, Cloud Storage, Cloud Pub/Sub, Cloud Firestore, Audit Logs, Cloud Scheduler
- totally serverless
- automatic horizontal scaling
- networks well with hybrid and multi-cloud
- acts as the glue between services


### Chose the right compute
Are you a mobile/html5 developer?
- yes: **Firebase**
- no:
  - are you developing an event-driven app?
    - yes: **Cloud Functions**
    - no: Is your application using ANY of the following: specific OS or kernel, Monolithic workloads
      - yes: **Compute Engine**
      - no: Does your application use or need any of the following: Hybrid or multi-cloud deployment, licensed software, use of protocols besides HTTP/S, persistent disks
        - no: App Engine, does the app require rapid, frequent scaling?
          - yes: **App Engine Standard**
          - no: **App Engine Flex**
        - yes: Will your app be in containers
          - no: **Compute Engine**
          - yes: Do you need a high degree of customization?
            - no: **Cloud Run**
            - yes: **GKE**

### Autoscaling

| Service     | Absolute Minimum | High availability | How | Speed |
| ----------- | ---------------- | ----------------- | --- | ----- |
| Compute Engine      | 1 instance | 2 instances | MIG or MIG + Load Blaancer | Moderate/better | 
| GKE Pods   | 1 pod        | 2 pod deployment | Load-based Internal Kubernetes | Decent |
| GKE Node Pool   | 1 instance        | 3 instances | Kubenretes pod back-pressure | Slow |
| App Engine Standard   | 0        | 0 | Request-based | Almost instantaneous |
| Cloud Run   | 0        | 0 / Adjustable | Request-based | Extremely fast |
| Cloud Functions   | 0        | 0 / Optional | Request-based | Almost instantaneous |


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

## Key lessons
- GCP has a full spectrum of compute services, ranging from the highly customizable Compute engine to the fully-managed Cloud Functions
- App Engine not only has two environments - Standard and Flex, but also a 2nd generation of Standard that is more up-to-date
- For mobile apps, use Firebase and for event-driver functions use Cloud FUnctions. If you need a specifyc OS or kernel, go with Compute Engine
- If you don't need hybrid or multi-cloud deployment or persistent disks, chose either App Engine Standard or App Engine Flex, depending on your scaling requirements
- GCP offers a number of services for containerized workloads cinluding Cloud Run and GKE
- When working with Compute Engine, remember that managed instance groups coupled with a cloud load balancer results in the fastest autoscaling response
- For high availability, the GKE node pool is best used with a minimum of three nodes for a production envinronment
- Cloud Run scales almost as fast as App Engine Standard Environment and you are only charged when a request is made
- The AI data lifecycle expands the traiditon one: ingest, store, transform, train, model, evaluate, deploy and predict
- Vertex AI is Google Cloud's AI platform, incorporating all machine learning APIs, such as Vision API, it's AutoML services and even related hardware, like Cloud TPU
- Be sure to use the proper GCP service for the various stages in the AI data lifecycle, such as using BigQuery for storing and process tabular data and Dataflow for processing unstructured data
- IoT Core is a global fully-managed service designed to connect, managed and ingest data from internet-connected devices and a primary source for streaming data
- Cloud Pub/Sub is a global messaging and ingestion service that supports both push and pull modes with exactly-once-processing for many GCP services
- Cloud BigQuery is a serverless , multi-regional, multi-cloud, SQL column-store data warehouse used for data analytics and ML capable of scaling to petabytes in minutes
