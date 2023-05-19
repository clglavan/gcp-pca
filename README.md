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
| You can add more storage space, throughput and IOPS | Only storage space can be resized, throughput and IOPS cannot |

- Managing file-based storage: Filestore
  - Fully-managed, Similar to network attached storage
  - Provision Filestore instance in zone, Access via VPC using NFSv3 protocol
  - Consistently fast performance, great for lift-and-shift migration
  - Backups are fully supported, snapshots (read-only) are supported
  - 3 Filestore tier levels, Basic, Enterprise and High Scale
    - Basic - best for file sharing, GKE, software dev and web hosting, HDD 1-63 TiB, SSD 2.5-63 TiB
    - Enterprise - best for critical applications, GCE, and GKE workloads, 1-10 TiB
    - High Scale - best for high-performance computing e.g. genome sequencing, 10-100 TiB
- Keeping Objects in Cloud Storage
  - Infinitely scalable, fully managed, highly durable object storage service
  - For mutable, unstructured data such as images, videos and documents
  - All objects are stored in buckets
    - buckets can be regional or multi regional
    - buckets support folders and subfolders
    - supports versioning per bucket, as well as maintaining a live object version and noncurrent versions
  - Permissions granted by bucket or by object and limited to specific teams or people, or fully public

| Standard | Nearline | Coldline | Archive |
| --- | --- | --- | --- |
| For your most frequently accessed data or stored for a brief time | ideal for data you plan to read or modify on average once per month or less | Best for objects or data you plan to access at most once every 90 days | Least expensive choice for objects that you plan to access less than once a year |

Use lifecycle Management rules to move objects between classes

- Do you need block storage ? 
  - yes: Do you need to store your data briefly ?
    - yes: Local SSD
    - no: persistent Disk
  - no: Do you need file-based storage?
    - yes: Cloud Filestore
    - no: Cloud Storage
- Do your objects need to be frequently accessed? Hot objects
  -  yes: Use Standard Class
  -  no: Are objects acceed at most once a month?
    - yes: Use Nearline Class
    - no: Are objects accessed at most once a quarter?
      - yes: Use Coldline CLass
      - no: Use Archive Class

## Saving your Data on GCP

### Cloud SQL
- Regional, fully-managed relational database service for SQL Server, MySQL, and PostgreSQL
- Automatic replication wiht automatic failover, backup and point-in-time recovery
- scale manually up to 96 processor cores, more than 624 GB of RAM and add read replicas as needed
- Features include:
  - built-in high availability
  - automatically scale storage up to 30 TB
  - connects with GAE, GCE, GKE and BigQuery among other services

### Cloud Spanner
- Fully managed relational database, up to 99.999% availability and unlimited scale
- Create a Spanner instance by defining instance configuration and compute capacity
- Use query parameters to increase efficiency and lower costs
- Features include:
  - Automatic sharding
  - External consistency
  - Backup/restore and point-in-time recovery

### Cloud Bigtable
- Fully managed, scalable NoSQL database service for large analytical and operational workloads
- Handles large amounts of data in a key-value store and supports high read and write at low latency
- Tables stored in instances that contain up to 4 nodes, located in different zones
- Use cases:
  - Time-series data
  - Marketing and/or financial data
  - IoT data

### Firestore
- Fully managed, scalable, serverless document database service
- Live synchronization and offline mode allow multi-user, collaborative application on mobile web
- Supports Datastore databases and Datastore API
- possible workloads include:
  - live asset and activity tracking
  - real-time analytics
  - media and product catalogs
  - social user profiles and gaming leaderboards

### Datastream
- Serverless Change data capture(CDC) and replication service
- Synchronizez data across heterogeneous databases and applications reliably

### Firebase Realtime Database
- serverless NoSQL databas for storing and syncing data
- enhances collaboration among users across devices and web in real time

### MemoryStore
- In-memory service for Redis and Memcached
- Provides low latency access and high throughput for heavily accessed data

### Deciding on the best database solution

- Is your data structured ?
  - no: Do you need mobile SDKs ?
    - yes: Cloud Storage for Firebase
    - no: Cloud Storage
  - yes: Is your workload analytics?
    - no: Is your data relational?
      - no: Do you need mobile SDKs ?
        - yes: Cloud Firestore for Firebase
        - no: Cloud firestore
      - yes: Do your need horizontal scalability ?
        - yes: Cloud Spanner
        - no: Cloud SQL
    - yes: Do you need low latency and NoSQL ?
      - yes: Cloud Bigtable
      - no: BigQuery

## Networking

### Cloud Domain
- Global registrar for domain names using Google Domains
- Uses build-in DNS or allows custom nameservers
- Supports DNSSEC and private Whois records
- Integration features:
  - managed as a GCP project, including billing
  - automatic domain verification wiht Search Console, App Engine, Cloud Run, etc
  - works with Cloud IAM for access management

### Mapping the Web with Cloud DNS
- Global, scalable, fully-managed authoritative domain name service
- Structural redundancies allow 100% uptime
- Offers both public and private managed zones
- features include
  - Cloud IAM and Cloud Logging integration
  - DNS peering and DNS forwarding
  - anycast nameservers
  - DNSSEC support

### Static External IP Addresses
Reserve static external IP addresses in projects and assign them to resources. GCP supports two types of static external ip addresses: regional and global
- Regional IP addresses can be assigned to Compute Engine VMs and network load balancers
- Global IP addresses are assigned to Anycast IPs and global load balancers (HTTP/S, SSL and TCP proxies)
- Static IP addresses can be assigned through the console, gcloud command line, API or Terraform
- No charge except for IP addresses that are reserved but not used

### Cloud Load Balancing
- Fully distributed, software-defined managed service that spreads network traffic across multiple instances of your apps
- Layer 4 and Layer 7 load balancing with Cloud CDN integration and automatic scaling
- Regional load balancing features:
  - health checks
  - session affinity
  - IPv4 only
- Global load balancing features:
  - multi-region failover
  - connects to closest region for lowest latency
  - IPv4 and IPv6

### Cloud CDN
- Cloud Content Delivery Network (CDN) relies on Google Cloud's global edge network
- Cloud CDN works with external GCP HTTPS load balancing
- Manage cache rules with cache control header or allow Cloud CDN to automatically cache static content
- Content sources include:
  - Instance groups
  - Zonal network endpoint groups (NEGs)
  - Serverless NEGs like GAE and Cloud Functions

### Virtual Private Cloud (VPC)
- Global IPv4 unicast software-defined network
- Automatic or custom creation (configure subnets, firewall rules, routes, VPNs, and BGP)
- VPC is global, but subnets are regional
- Options include:
  - shared VPC
  - VPC peering
  - Bring your own IP addresses
  - Packet mirroring

### Cloud Interconnect
Extends on-premises network to VPC through high available, low-latency connection
| Dedicated Interconnect | Partner Interconnect | 
| --- | --- |
| Direct connection to GCP | Connects to GCP via partner |
| Best for high bandwidth needs | Better for lower bandwidth needs | 
| 10-Gbps or 100Gbps circuits | Dependent on partner capabilities |
| Capacities from 50 Mbps - 50 Gbps | Capacities from 50 Mbps - 50 Gbps |
| Traffic not encrypted, but can be added | Traffic not encrypted, but can be added | 

Can't use Cloud VPN with interconnect

### Cloud VPN
- Securely connects peer network to VPC
- Traffic is ecnrypted by one IPsec VPN gateway and decrypted by another gateway
- Requires static IP address for persistence and does not support dynamic, e.g. "dial-in" VPN
- Best practices:
  - Keep Cloud VPN resources in own project
  - use dynamic routing and BGP
  - Establish secure firewall rules for VPN
  - Generated strong pre-shared keys

### Cloud router
- Provides dynamic routing for hybrid networks linking VPCs to external networks via BGP
- Works with Cloud VPN and Dedicated Interconnect
- Automatically learns subnets in VPC and announces them to on-premises network
- Works with router appliances

### CDN Interconnect
- Direct low-latency connectivity to certain CDN providers, with lower egress fees
- Works for both pull and push cache fills
- Best for high-volume egress traffic (lower costs) and frequent content updates (lower latency)

### Load balancing

#### Dealing with Global web traffic
- External, Internet-to-GCP Traffic
  - HTTP or HTTPS Traffic -> HTTP(S) Load Balancing
  - TCP Traffic
    - SSL Offload
      - yes: SSL Proxy
      - no: Global LB or IPV6 (no ssl) ?
        - yes: TCP Proxy
        - no: Preserve Client IPs ?
          - yes: Network TCP/UDP Load Balancing
          - no: TCP Proxy
  - UDP Traffic
    - IPv6 Clients? Global LB?
      - No: Network TCP/UDP Load Balancing
      - yes: None
- Internal IPv4 Clients, GCP Instance-to-Instance RFC 1918 Traffic
  - TCP/UDP Traffic - Internal TCP/UDP Load Balancing

## Security

### Cloud IAM
- Who, principals
  - Google Account
  - Service Account
  - Google Group
  - Google Workspace account
  - Cloud Identity domain
  - All authenticated users
  - All users
- Access, roles
  - Billing Account Administrator
  - Billing account User
  - Storage Object creator
  - Storage Object Viewer
  - Cloud SQL Editor
  - Cloud SQL instance user
  - Security Admin
  - etc
- Which, resources
  - VM instance
  - GKE cluster
  - Storage bucket
  - Pub/Sub topic
  - Organization
  
#### Roles
- Primitive roles pre-date Cloud IAM and are the broadest with the most permissions: Owner, Editor and Viewer.
- Predefined roles target specific rsources with specific actions at a granular level:
  - Billing accounts Administrator (roles/billing.admin)
  - Kubernetes Engine Developer (roles/container.developer)
- Custom Roles Collect a unique set of permissions in order to ensure that the role has only the permissions needed, which enforces the principle of least privilege.

#### IAM
- Globally managed access control for organizations
- Resource access is granted to roles( collection of permissions) and roles are granted to principals
- Recommender helpls identify excess or needed permissions from principals
- Grants IAM access to external identities (eg, AWS, Azure Active Directory, on-prem AD) with workload identity federation.

#### Resource Manager
- Modifies Cloud IAM policies across an organization
- Cloud Asset Inventory monitors and analyzes all GCP assets, including IAM policies
- Organization Policy Service sets contraints on resources and helps orgs stay in compliance

#### Cloud Identity
- Fully managed Identity as a Service for provisioning and managing identity resources
- Each user and group is given a Cloud Identity account allowing Cloud IAM to manage Access.
- Can be configured to federate identities with other identity providers (eg Active Directory )
- Features include:
  - SSO with other apps
  - Multi-factor authentication
  - Device security with endpoint management

#### Cloud IAP
- establishes a central authorization layer for applications accessed by HTTPS. Also internally by HTTP
- enforces access cotnrol policies for apps and resources
- based on load balancer and IAM. Permits only authenticated requests

### Cloud Security Command Center
Comprehensive security management and risk platform. Two tiers are supported: Standard and Premium.
- designed to prevent, detect and respond to threats from a single pane of glass
- Integrates and monitors many security services on GCP as well as external services
- Identifies security compliance violations and misconfigurations in Google Cloud assets
- Exports SCC data to Splunk or other Security Information and Event Management (SIEMs)

| Standard | Premium |
| ---- | ---- |
| Security Health Analytics | Security Health Analytics - Standard plus compliance monitoring |
| Web security Scanner | Web Security Secanner - Standard plus managed scans | 
| Cloud Armor | Event Threat Detection | 
| Cloud DLP | Container Threat Detection | 
| Anomaly Detection | Continuous Exports to Pub/Sub | 

### Web Security Scanner
- Detects key vulnerabilities in App Engine, Compute Engine and Kubernetes Engine applications
- Crawler based, supports public URLs and IPs not behind a firewall
- Standard tier supports custom scans, Premium tier supports managed scans
- Security Scanner detects:
  - Cross-Site Scripting (XSS)
  - Flash injection
  - Mixed (HTTP/HTTPS) content
  - Outdated and insecure JavaScript libraries

### Cloud Armor
- Edge-level, enterprise-grade DDoS protection and web application firewall (WAF) 
- Leverages Google Cloud load balancing
- Mitigates OWASP's top ten risks including broken authentication, SQL injections, and XSS
- Features include:
   - Allow or deny traffic by IPs or CIDR ranges
   - Preview changes before pushing policy live
   - Configure WAF rules to reduce false positives
   - Reference named IP address lists from CDN partners Fastly, Cloudflare and Imperva

### Event Threat Detection
- Idenfity threats in near-real time by monitoring and analyzing Cloud Logging (audit,vpc flow, firewall, net logs, dns and linux cis)
- Threats are defined by rules, which specify the needed logs
- Create custom rules by running queries on log data exported to BigQuery
- Quickly detect many different types of attacks, including:
  - Malware
  - Crypto mining
  - Outgoing DDoS attacks
  - Port scanning
  - IAM anomalous grant
  - Brute-force SSH

### Cloud Data Loss Prevention
- Inspection, classification and de-identification platform to protect sensitive data
- Includes over 150 data detectors for personal identifiable information (PII))
- Connect DLP results to Cloud SCC, Data Catalog, or export to external SIEM or governance tool.
- Detects sensitive data in:
  - Streams of data or structured text
  - Files in Cloud Storage and BigQuery

## Encryption Keys

### Cloud key management Service
Highly available, low-latency service to generate, manage and apply cryptographic keys

Cloud KMS encrypts and decrypts - does not store secrets itself - and controls access to keys
- Supports both symmetrical (eg AES) and asymmetrical, like RSA or EC, algorithms
- Includes a 24-h delay for key material destruction, to prevent accidental or malicious data loss
- Supports regulatory compliance and adds optional variations: Cloud HSM, Cloud EKM, CMEK, and CSEK
- Google Cloud recommends the regular automatic rotation of symmetric keys

### Cloud Hardware, Security Module
- Hosts ecnryption keys and performs cryptographic actions in cluster of FIPS 140-2 Level 3 certifies devices
- Enables compliance with hardware requirements
- Cloud HSM keys are cryptographically bound to region, with support for multi-regions
- Cloud HSM properties:
  - Keys are non-exportable
  - Tamper resistant

### Cloud External Key Management
- Uses keys from supported external key management partners instead of GCP
- Works only with supported CMEK integration services like BigQuery, Compute Engine, Cloud Run, Cloud Spanner, Cloud Storage, GKE, Pub/Sub and Secret Manager
- Key ring should be created in same location as external key management partner
- Benefits include
  - key provenance
  - access control
  - centralized key management

### Secret Manager
- Fully managed service for storing, managing and accessing secrets as binary blobs or text strings
- used for storing sensitive runtime info such as database passwords, API keys, or TLS certificates
- Data of each secret is immutable and new versions are craeted each time value is modified
- Best practices:
  - follow the principle of least privilege
  - limit access with IAM conditions
  - Use the Secret Manager API instead of env vars
  - Reference secrets by version number, not "latest" 
