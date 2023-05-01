# ECE530 HW2 report
Name: Yie-Sheng Chen
ID: 
e-mail: 

## Abstract

## Introduction
This homework is to understand common IaaS/PaaS through crafting a business report. It's based on "A Comparative Taxonomy and Survey"[1]. Due to time constraint, the services are organized mainly in tabular forms with some haste comments and discussions. The tables are based on those in [1] but with key difference that here each piece of information come with reference.

## Background Work
### A. Cloud Vendors and Industry Market Share
A maybe surprising result from [4] is that Alibaba overtake ibm as the fourth biggest public cloud provider.

## Services

### COMPUTE SERVICES

I went through some related background knowledge on compute services: namely virtual machine papers from my CS587 course. Afterwards, I came across an summary paper [3] that described history of virtual machines and several of the important papers, for example, the disco project that became VMWare.

And another worth mentioning literature is a 2019 paper [173] from Turing award author David A. Patterson that explored serverless computing, including the pricing and also Patterson's signature "fallacy" discussion.

* TABLE II VIRTUAL MACHINES

|Virtual Machine Services&Features|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Service|Amazon EC2 |Azure Virtual Machines, Scale Sets[6] |Compute Engine |Virtual Server[43], Bare Metal |
|Hypervisor |xen-based, and others |Windows Hyper-V[18] |KVM-based[25,26]|xen-based, Citrix[37,38,39]| 
|Auto Scale Ability|v[13] |v[19,20] |v[27,28] |v[40,41]|
|Max vCPUs |128(x1), 192(r6a.metal)[15] |96(D96d_v5)[21] |416(M2)[29,30] |64(M1)[42]|
|Max Memory (GB) |1952(x1),1536(r6a.metal) |384(D96d_v5) |12 TB(M2) |512 GB(M1)|
|Max Attached Storage |64 TiB(EBS)[22] |32 disks[21] |257 TB[30] |10TB(SAN)[42]|
|Max Instance Storage (GB) |3840(x1;SSD) |3600(D96d_v5;SSD) |No Local SSD[30] |100 GB(SAN)[42]|
|Custom VMs | | |v[31,32] |x[42]|
|Dedicated Hosts |v[16] |v[23] |v[33,34]|v[44,45,46]|
|Bare Metal|v[17] |v[24] |v[35,36]|v[47]|



* TABLE III SERVERLESS COMPUTING

|Serverless computing Services&Features|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Service |AWS Lambda |Azure Functions |Cloud Functions|IBM Cloud Functions/ OpenWhisk [75, 77]| 
|Supported Languages |natively: Java, Go, PowerShell, Node.js, C#, Python, and Ruby code, and Runtime API: any[48,49] |C#, JavaScript, F#, Java, PowerShell, Python, TypeScript(4.x) [60] |Node.js, Python, Go, Java, Ruby, PHP, .NET Core [70]| Node.js, Python, PHP, Go, Ruby, Java, .NET Core ; other languages using Docker actions[76, 78]|
|Max Execution Time / Request |15m [50] |unlimited (premium plan), 230s (http-triggered) [61,62] |60m (http, 2nd gen) [72] |10 m [76]|
|Scalability |automatic scaling [51] |automatic scaling [64] |automatic scaling [70]|automatic scaling [79]|
|HTTP Invocation |AWS Lambda Function URL, API Gateway[54,55] |HTTP trigger [65] |HTTP triggers [69]|IBM Cloud® Functions web action [80, 81]|
|Log Management  |CloudWatch[56,57,58,59] |Azure Monitor Logs with Kusto query language[66], Application Insights [67], view/stream log [68] |Cloud Logging [73], Google Cloud CLI [74] |view: IBM Log Analysis [82] |
|Concurrent Executions |1000 (default) [51,52,53] |20- 100 (premium;linux)[61,63] |100 (http, 2nd gen)[71]|1000 [83]|

### STORAGE SERVICES

There are some unfamiliar keywords. One of them is "egress", and [105] is a good source to understand it and it also explains scenarios that egress cost can occur. According to [105], the egress cost is not straight-forward to understand: it depends on the source and destination of the data and the source and destination may depend on cloud software's architecture.

As can be seen from AWS official S3 pricing page[106], there are several tiers of storage, and not only storing data costs money per the length of time, accessing the data also sometimes costs money. And on top of those, AWS S3 also provides "intelligent tier" to help customer save money if access pattern is unknown. 


* TABLE IV STORAGE SERVICES

|Service type|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Object Storage  |Amazon S3, 11 9s durability [84] |Azure Blob Storage [85] |Cloud Storage [86] |Cloud Object Storage ; max obj. size: 10T [87]|
|Virtual Machine Disk (Block) Storage |Amazon EBS  [88] |Azure Disk Storage [89] |Persistent Disk [90] |IBM Cloud Block Storage [91]|
|Long Term Cold Storage |S3 Glacier storage classes [92] |Blob Storage(cool)[93] |Coldline [94], Archive storage [94,95,96]|Cold vault [97]|
|File Storage  |Amazon EFS, Amazon FSx for Lustre/ NetApp ONTAP/ OpenZFS/ Windows File Server[98] |Azure Files[99] |Filestore [100, 101, 102] |IBM Cloud File Storage[103, 104]|

* TABLE VI DATABASE SERVICES

|Service Type|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Relational Database Management |Amazon RDS with 7 engines:Amazon Aurora with MySQL/ PostgreSQL compatibility, MySQL, MariaDB, PostgreSQL, Oracle, and SQL Server [107] |SQL Server, Azure SQL Managed Instance, Azure SQL Database, MySQL, PostgreSQL, and MariaDB [108] |Cloud SQL, Cloud Spanner and AlloyDB for PostgreSQL [109] |IBM Db2 on Cloud, IBM Cloud Databases for PostgreSQL, IBM Cloud Hyper Protect DBaaS, EDB Postgres Enterprise and Standard with IBM[110] |
|Non Relational Database Management |DynamoDB [111, 112] |Azure Cosmos DB, Azure Cosmos DB for Apache Cassandra, Azure Cosmos DB for Table, Azure Cache for Redis, Azure Table Storage, Azure Cosmos DB Graph API, Azure Time Series Insights, OpenTSDB with HBase on HDInsight, Azure Search [113] |Firestore, Cloud Bigtable, Memorystore[115], Cloud Datastore [114, 116], MongoDB Atlas[114, 117]|IBM Cloud Databases for MongoDB [118, 119, 120], IBM Cloud Databases for DataStax/ Cassandra [121], IBM solidDB [118], IBM Cloud Databases for Elasticsearch [118, 123], IBM Cloudant/CouchDB [122]|
|In-Memory Data Store |Amazon MemoryDB for Redis, Elasticache for Redis, ElastiCache for Memcached [124] |Azure SQL Database, Azure SQL Managed Instance [125], Azure Cache for Redis [126, 127] |Memorystore/ for Redis and Memcached [128]|IBM Cloud Databases for Redis [129]|
|Cloud Extract Transform, Load (ETL) |AWS Glue [130, 131], Data Pipeline's range of supported data sources and Batch's asynchronous operations [132] |Azure Data Factory and Azure Synapse Analytics [133, 134] |Cloud Data Fusion, Dataflow, and Dataproc [135] |IBM Cloud Pak for Data [136, 137, 138]|

### BIG DATA AND ANALYTICS

One interesting note from the MIT 2020 distributed course is that Map/Reduce is being replaced at Google by Flume / FlumeJava, Colossus and BigTable [174, 175].

* TABLE VII BIG DATA, ANALYTICS, AND DATA PIPELINE SERVICES

|Service Type|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Hadoop |Amazon EMR [139] |Azure HDInsight [140, 141] |Dataproc [142]|Apache Hadoop [143] |
|Data Warehousing |Amazon Redshift [144, 145] |SMP: Azure SQL Database, SQL Server in a virtual machine, MPP: Azure Synapse Analytics (formerly Azure Data Warehouse), Apache Hive on HDInsight, Interactive Query (Hive LLAP) on HDInsight [146] |BigQuery [147, 148]|Data warehouse solutions[149, 151], Db2 Warehouse on Cloud [150, 151]|
|Data Streaming |Amazon Kinesis Data Streams/Data Firehose, Amazon Managed Streaming for Apache Kafka (Amazon MSK), Other streaming solutions on Amazon EC2 [152] |Azure Stream Analytics [153] |Datastream [154], Dataflow [155]|IBM Streams [156] |
|Data Queuing |Amazon SQS [157] |Azure Queue Storage [158], Storage queues, Service Bus queues [159] |Pub/Sub[160, 161] |IBM MQ [162] |

### MACHINE LEARNING AND ARTIFICIAL INTELLIGENCE SERVICES

* TABLE IX MACHINE LEARNING AND ARTIFICIAL INTELLIGENCE SERVICES

|Service Type |Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Machine Learning  |AWS machine learning [163] |Azure Machine Learning [164, 165] |AI and machine learning products, Vertex AI, Vertex AI Workbench, AutoML, Timeseries Insights API (Preview), Deep Learning Containers, Deep Learning VM Image, GPUs, TensorFlow Enterprise, TPUs [166] ||
|Language Processing & Speech Recognition AIs |Amazon |Microsoft |Cloud Natural Language, Dialogflow, Media Translation (Beta), Speech-to-Text, Text-to-Speech, Translation AI, Contact Center AI, Document AI, Product Discovery [166]||
|Image Recognition AI |Amazon Rekognition [167] |Azure Cognitive Services [168] |Video AI, Vision AI [166] ||

### NETWORKING SERVICES

Another interesting note and comparison is that the computer network textbook [176] from James Kurose and Keith Ross also discussed CDN. It compared youtube against Netflix which are two different cases: Youtube needs to handle videos from user. On the other hand, the source of Netflix videos are more centralized. And of course [176] also discussed the two main philosophy of CDN.

|Networking Services|Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Virtual Networking |Amazon VPC [169] |VNet [170] |Virtual Private Cloud (VPC) [171]|Gateway appliances [172]|
|DNS Services |Amazon |Microsoft |Google|IBM|
|Private Connectivity |Amazon |Microsoft |Google|IBM|
|Content Delivery Network |Amazon |Microsoft |Google|IBM|
|Load Balancing |Amazon |Microsoft |Google|IBM|

## X. ADDITIONAL SERVICES

The following comes directly from my own draft study note of [1]. So the references numbers are from [1] and the information are not update.

### A. Internet of Things
* AWS IoT Platform
  * Device communications (publish and receive messages) are handled over HTTP, Message Queue Telemetry Transport (MQTT) [94] or MQTT over WebSockets.
  * provides SDKs for Embedded C, JavaScript, Python, iOS, and Android
  * messages are processed in 512 byte blocks (= single message up to max 128 KB)
  * offers a strong security design
  * highly integrated with Amazon’s internal authentication engine - Identity and Access Management (IAM).
  * AWS Greengrass
    * local gateway to IoT devices
    * primary routing, data caching, and message processing.
  * lightweight enough to be supported by ARM-based System on Chip (SoC) devices
  * M2M exposure through MQTT endpoints
  * developers can utilize custom Lambda functions
* Azure ; 
  * IoT Platform and the 
  * IoT Hub
    * keeps track of devices via a dedicated registry and provides reliable communication between them.
  * supports AMQP, MQTT, and HTTP protocols while supported SDKs include JavaScript, .NET, Java, Python, and C.
  * Blob Storage handles received data for archiving or offline processing.
  * alternative of transferring data to an Event Hub instance for real-time processing, monitoring or diagnostics.
  * Messages are sent in 4 KB blocks, while the service has 4-tiers which can support up to 300,000,000 messages per day.
  * edge computing deployments
  * by launching the IoT Edge, a software able to run on both Linux and Windows also supporting x86 and ARM architectures. 
    * Azure IoT Edge enables the local deployment of Azure services with the language support of Java, C, C#, Python, and Node.js.
    * various supported modules (including Machine Learning, Stream Analytics or IoT Hub) are packed and deployed as Docker containers on top of IoT Edge.
  * Communications are implemented through MQTT and AMQT protocols
* Google ; IoT PaaS
  * Cloud IoT Core
  * device manager service
    * initially registering each IoT instance establishing identity, along with an authentication mechanism
  * messaging bridge
    * collect data from customer devices and deliver them to Google’s Cloud Pub/Sub service.
    * The Pub/Sub service messages in high volume over HTTP or gRPC [95], while supported languages include Java, Go, .NET, JavaScript, C, Python, Ruby, and PHP.
  * highly integrated with Cloud Functions(serverless capabilities), Cloud Dataflow (real-time or batch data processing), and Cloud Machine Learning (predictive analytics), while datasets can be stored in BigQuery.
* IBM ; Watson IoT Platform
  * connections through the MQTT messaging protocol including a maximum of 500 connected devices, with data exchange and analysis limit of 200 MB for each.
  * variety of solutions carefully mapped to the need of different industries including Automotive, Electronics, Banking, and Retail.
  * deeply empowered by the cloud-cognitive capabilities

## conclusion
There are so much interesting and promising topics in this homework. In the process, I spent much time going through "A Comparative Taxonomy and Survey" [1], and in the end, didn't have enough time to organize the materials I went through into this report. I wish I could have more time to update all the categories from [1] and also organize related material I came through. It will be nice if this can become precursor to my PhD research.




