# gcp-pca

# Processing Data

## Compute
---

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

---
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

### Autoscaling considerations

| Service     | Absolute Minimum | High availability | How | Speed |
| ----------- | ---------------- | ----------------- | --- | ----- |
| Compute Engine      | 1 instance | 2 instances | MIG or MIG + Load Blaancer | Moderate/better | 
| GKE Pods   | 1 pod        | 2 pod deployment | Load-based Internal Kubernetes | Decent |
| GKE Node Pool   | 1 instance        | 3 instances | Kubenretes pod back-pressure | Slow |
| App Engine Standard   | 0        | 0 | Request-based | Almost instantaneous |
| Cloud Run   | 0        | 0 / Adjustable | Request-based | Extremely fast |
| Cloud Functions   | 0        | 0 / Optional | Request-based | Almost instantaneous |


## Big Data
---

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
---
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

# Google Kubernetes Engine

## General 
---
### Coordinating Clusters
- a cluster is at least one control plane and multiple worker machines, aka nodes
- you can create zonal or regional clusters
- private clusters are VPC-native clusters dependent on internal IP addresses
- for highly available apps, distribute your workload using multi-zonal node pools
- a horizontal pod autoscaler (HPA) checks the workload's metrics against target thresholds
- configure horizontal pod autoscaling on deployment rather than replicaset

### Workloads
- custom and external metrics use HPA to scale based on conditions besides the workload
- configuring limits for Pods, based on workload is highly recommended
- ConfigMaps bind non-sensitive configuration artifacts to your Pod containers at runtime
- Deployments are best for stateless apps with ReadOnlyMany or ReadWriteMany volumes
- DaemonSets are good for ongoing background tasks that do not require user intervention
- StatefulSets are pods with unique persistent identities and hostnames

### Networking Pods,Services and External Clients
- with kubernetes, think about how Pods, Services and external clients communicate, instead of how your hosts or VMs are connected
- VPC-native clusters scale better than routes-based clusters and are needed for private clusters.
- Shared VPC networks are best for organizations with a centralized management team
- GKE Ingress(internal or external) implements Ingress resources as Google Cloud load balancers for HTTP(S) workloads
- Workloads Identity links Kubernetes service accounts to Google service accounts to safely access other Google services

### Operations
- monitoring and logging can be enabled for both new and existing clusters
- GKE containers logs are removed when the host Pod is removed, when their disk on runs out of space or when replaced by newer logs
- GKE generated two types of metrics:
  - system metrics - metrics from essential system componenets
  - Workload metrics - metrics exposed by any GKE workload

## Anthos 
---

### Anthos
- application deployment anywhere: on GCP, on-premises, hybrid and multicloud (AWS and Azure)
- supports Kubernetes Engine clusters, serverless Cloud Run and Compute Engine VMs
- use Migrate for Anthos to migrate and modernize existing workloads to containers
- enhance app development and delivery with up-to-date CI/CD automated pipelines
- enabled defense-in-depth security strategy with comprehensive security controls across all deployments
- fully integrated with Google Cloud Monitoring and Logging, including hybrid and on-prem configurations
### Anthos Service Mesh
- Anthos Service Mesh (ASM) enabled managed, observable and secure communication across microservices, on-remises and on GCP
- Powered by open-source Istio, ASM is one or more control planes and a data plane which monitors all traffic through a proxy
- Anthos Service Mesh controls traffic flow between services as well as ingress and egress:
 - supports canary and blue-green deployments
 - configure load balancing between services
 - provides in-depth telemetry with Cloud Monitoring, Logging and Trace
### Kubernetes Engine Connection
- Anthos clusters provide a unified way to work with Kubenretes clusters as part of Anthos, extending GKE to work in multiple environments
- Anthos on GCP uses "traditional" GKE, while on-premises uses VMWare and Bare Metal
- Logically group and normalize mutliple clusters via Fleets to manage multi-cluster capabilities and apply consistent policies
- Anthos config Management creates a common configuration across all infrastructure, including custom policies applied both on-premises and in the cloud
- Binary Authorization configures a validation policy enforced when deploying a container image
### Cloud Run for Anthos
- Cloud Run for Anthos is managed with Knative, which enabled serverless workloads on Kubernetes
- Streamlines operational needs with advanced workload autoscaling and automatic networking
- Scale idle workloads to zero instances or set a minimum instance count for baseline availability
- Out-of-the-box integration with Cloud Monitoring, Cloud Logging and Error Reporting
- Easily perform A/B tests with traffic splitting and quickly roll back to known working services

## Bare Metal
---

### Anthos Bare Metal
- Anthos clusters on bare metal allow you to directly deploy applications on your own hardware
- Anthos bare metal managed app deployments and health across existing data centers for more efficient operation
- Control system security without compatibility issues for vitual machines and operating systems
- Manage containers on a variety of performance-optimized hardware with direct access to hardware
- Scale up application while mainting reliability regardless of fluctuations in workload and network traffic thanks to advnaced monitoring
- Security can be customized with minimal connections to outside resources

### Deployment options for Anthos on Bare Metal

| Standalone | Multi-cluster | Hybrid |
| ---------- | ------------- | ------ |
| A single cluster serves as both user cluster and admin cluster | one admin cluster plus one or more clusters | specialized multi-cluster that runs user workloads on admin |
| Best for single teams and single workload types | Works well for fleet of clusters with centralized management | Create from standalone by adding more user clusters |
| Separate admin cluster not needed | Provides separation between different teams | Use only if no security concerns with user workloads on admin | 
| Works well for clusters in edge locations | Isolates development and production workloads | |

### Operating Bare metal Clusters
- use Connect to associate your bare metal clusters to Google Cloud
- access is enabled for workload management features and unified UI or Cloud COnsole
- Cloud Console displays health of all connected workloads and allows modifications to all
- put nodes into maintenance mode to drain Pods/workloads and exclude them from Pod scheduling


## Storing Data
---

### Storing your objects and files
- Local SSD
  - Very fast zonal resource, 375GB solid state disks directly attached to server hosting VM instance
  - Expandable to 3, 6, and 9 TB with increasing performance: up to 2.400.000 read and 1.200.000 write IOPS
  - All data encrypted at rest, lost when VM stops but can survive live migration
  - Best for transient data ( use case: media rendering, data analytics and high-performance computing ) 
- Persevering with persistent disks
  - Major benefit: Persistence, available even after VM shutdown
  - Independent of VMs where data is distributed across disks for redundancy
  - Highly durable (up to six 9s!) and secure: data encrypted at rest and in transit

| Zonal | Regional | 
| ---------- | ------------- | 
| Data in a single zone | Data in two zones in the same region |
| 4 types available: Standard, Balanced, SSD, and Extreme | 3 Types avaialble: Standard Blanaced and SSD |
| Can be used for both snapshot and boot disks | Snapshots are okay, but cannot be used for boot disks |
| You can add more storage space, throughput and IOPS | |








