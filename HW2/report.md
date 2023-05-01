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
|Log Management  |CloudWatch [56, 57, 58, 59] |Azure Monitor Logs with Kusto query language [66], Application Insights [67], view/stream log [68] |Cloud Logging [73], Google Cloud CLI [74] |view: IBM Log Analysis [82] |
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

## references
```
[1] D. Sikeridis, I. Papapanagiotou, B. Prasad Rimal, and M. Devetsikiotis, “A Comparative Taxonomy and Survey of Public Cloud Infrastructure Vendors.”
[2] Amazon EC2. Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/ec2/
[3] ALLISON RANDAL, "The Ideal Versus the Real: Revisiting the History of Virtual Machines and Containers" Available: https://dl.acm.org/doi/fullHtml/10.1145/3365199
[4] Felix Richter, "Big Three Dominate the Global Cloud Market" Accessed on Apr. 30, 2023. [Online]. Available: https://www.statista.com/chart/18819/worldwide-market-share-of-leading-cloud-infrastructure-service-providers/
[5] Azure Virtual Machines. Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/free/virtual-machines/
[6] "What are Virtual Machine Scale Sets?" Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/overview
[7] Compute Engine. Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute
[8] IBM Cloud Virtual Server for VPC. Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/virtual-servers
[9] IBM Cloud Bare Metal Servers. Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/bare-metal-servers
[10] David Clinton, "AWS announced a move from Xen towards KVM. So what is KVM?" Accessed on Apr. 30, 2023. [Online]. Available: https://www.freecodecamp.org/news/aws-just-announced-a-move-from-xen-towards-kvm-so-what-is-kvm/
[11] "What is a hypervisor?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/what-is/hypervisor/
[12] Amazon EC2 FAQs. Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/ec2/faqs/
[13] Amazon EC2 Auto Scaling. Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/ec2/autoscaling/
[14] "What is Amazon EC2 Auto Scaling?". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/autoscaling/ec2/userguide/what-is-amazon-ec2-auto-scaling.html
[15] "Amazon EC2 Instance Types - Amazon Web Services". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/ec2/instance-types/
[16] "Amazon EC2 Dedicated Hosts". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/ec2/dedicated-hosts/
[17] "Introducing two new Amazon EC2 bare metal instances". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/about-aws/whats-new/2021/11/amazon-ec2-bare-metal-instances/
[18] "Hypervisor security on the Azure fleet". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/security/fundamentals/hypervisor
[19] "Overview of autoscale in Azure". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-monitor/autoscale/autoscale-overview
[20] "Overview of autoscale with Azure Virtual Machine Scale Sets". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-autoscale-overview
[21] "Ddv5 and Ddsv5-series". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/virtual-machines/ddv5-ddsv5-series
[22] "Constraints on the size and configuration of an EBS volume". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/volume_constraints.html
[23] "Azure Dedicated Hosts". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/virtual-machines/dedicated-hosts
[24] "What is BareMetal Infrastructure on Azure?". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/baremetal-infrastructure/concepts-baremetal-infrastructure-overview
[25] Andy Honig, Nelly Porter, "7 ways we harden our KVM hypervisor at Google Cloud: security in plaintex". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/blog/products/gcp/7-ways-we-harden-our-kvm-hypervisor-at-google-cloud-security-in-plaintext
[26] "About nested virtualization". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/instances/nested-virtualization/overview
[27] "Load balancing and scaling". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/load-balancing-and-autoscaling
[28] "Autoscaling groups of instances". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/autoscaler
[29] "Machine families resource and comparison guide". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/machine-resource
[30] "feedbackMemory-optimized machine family". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/memory-optimized-machines
[31] "Create a VM with a custom machine type". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/instances/creating-instance-with-custom-machine-type
[32] "Custom machine types". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/custom-machine-types
[33] "Sole-tenancy overview". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/compute/docs/nodes/sole-tenant-nodes
[34] Manish Dalwadi, Bryan Nairn, "Introducing sole-tenant nodes for Google Compute Engine — when sharing isn’t an option". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/blog/products/gcp/introducing-sole-tenant-nodes-for-google-compute-engine
[35] "Bare Metal Solution". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/bare-metal/docs
[36] Gurmeet Goindi, "Bare Metal Solution: Enabling specialized workloads in Google Cloud". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/blog/products/compute/bare-metal-solution-enabling-specialized-workloads-in-google-cloud
[37] "Getting started with virtual servers". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/virtual-servers?topic=virtual-servers-getting-started-tutorial
[38] "Technical overview | Citrix Hypervisor 8.2". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.citrix.com/en-us/citrix-hypervisor/technical-overview.html
[39] "What is Citrix XenServer?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/virtualization?topic=virtualization-what-is-citrix-xenserver
[40] "Enabling Auto scale for better capacity and resiliency". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/ha-infrastructure?topic=ha-infrastructure-ha-auto-scale
[41] "FAQs for auto scale". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/vpc?topic=vpc-faqs-auto-scale
[42] "Profiles | IBM Cloud Docs". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/virtual-servers?topic=virtual-servers-about-virtual-server-profiles
[43] "IBM Cloud Virtual Server for VPC | IBM". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/virtual-servers
[44] "Creating dedicated hosts and groups". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/vpc?topic=vpc-creating-dedicated-hosts-instances&interface=ui
[45] "About dedicated virtual servers". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/virtual-servers?topic=virtual-servers-dedicated-virtual-servers
[46] "ibm-cloud-docs/virtual-servers: Documentation repository for virtual-servers". Accessed on Apr. 30, 2023. [Online]. Available: https://github.com/ibm-cloud-docs/virtual-servers
[47] "IBM Cloud Bare Metal Servers | IBM". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/bare-metal-servers
[48] "AWS Lambda – FAQs". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/lambda/faqs/
[49] "Lambda runtimes - AWS Lambda". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html
[50] "AWS Lambda enables functions that can run up to 15 minutes". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/about-aws/whats-new/2018/10/aws-lambda-supports-functions-that-can-run-up-to-15-minutes/
[51] "Lambda function scaling". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/dg/lambda-concurrency.html
[52] Julian Wood, "Understanding AWS Lambda scaling and throughput". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/blogs/compute/understanding-aws-lambda-scaling-and-throughput/
[53] "Scaling and concurrency in Lambda". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/operatorguide/scaling-concurrency.html
[54] "AWS Lambda Function URL vs API Gateway – When to Use What". Accessed on Apr. 30, 2023. [Online]. Available: https://www.beabetterdev.com/2022/04/06/aws-lambda-function-url-vs-api-gateway-when-to-use-what/
[55] "Invoking Lambda function URLs". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/dg/urls-invocation.html
[56] "Accessing Amazon CloudWatch logs for AWS Lambda". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/dg/monitoring-cloudwatchlogs.html
[57] "awsdocs/aws-lambda-developer-guide: The AWS Lambda Developer Guide". Accessed on Apr. 30, 2023. [Online]. Available: https://github.com/awsdocs/aws-lambda-developer-guide
[58] "Monitoring and troubleshooting Lambda functions". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/lambda/latest/dg/lambda-monitoring.html
[59] "Logging and metrics for AWS Lambda". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/prescriptive-guidance/latest/implementing-logging-monitoring-cloudwatch/lambda-logging-metrics.html
[60] "Supported languages in Azure Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/supported-languages
[61] "Azure Functions hosting options". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale
[62] "What is the maximum execution time for an Azure Function which run under Consumption plan". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/answers/questions/1185604/what-is-the-maximum-execution-time-for-an-azure-fu
[63] "Event-driven scaling in Azure Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/event-driven-scaling
[64] "Do Azure Functions Actually Scale?". Accessed on Apr. 30, 2023. [Online]. Available: https://medium.com/fastapi-tutorials/do-azure-functions-actually-scale-2a34648dac8d
[65] "Azure Functions HTTP trigger". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger?pivots=programming-language-csharp&tabs=python-v2%2Cin-process%2Cfunctionsv2
[66] "Monitoring Azure Functions with Azure Monitor Logs". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitor-log-analytics?tabs=csharp
[67] "Monitor executions in Azure Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitoring
[68] "Enable streaming execution logs in Azure Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-functions/streaming-logs
[69] "Write Cloud Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/docs/writing
[70] "Cloud Functions execution environment". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/docs/concepts/execution-environment#runtimes
[71] "Using maximum instances". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/docs/configuring/max-instances
[72] "Quotas". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/quotas
[73] "Monitoring Cloud Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/docs/monitoring
[74] "Writing, Viewing, and Responding to Logs". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/functions/docs/monitoring/logging
[75] "IBM Cloud Functions". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/functions/
[76] "FAQ | IBM Cloud Docs". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-faq
[77] "Apache OpenWhisk - Resources and Tools - IBM Developer - IBM Developer". Accessed on Apr. 30, 2023. [Online]. Available: https://developer.ibm.com/components/apache-openwhisk/
[78] "Runtimes  | IBM Cloud Docs". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-runtimes
[79] "Function as a Service architecture". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-faas
[80] "Creating web actions". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-actions_web
[81] openwhisk. Accessed on Apr. 30, 2023. [Online]. Available: https://github.com/ibm-cloud-docs/openwhisk
[82] "Viewing logs". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-logs
[83] "System details and limits". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/openwhisk?topic=openwhisk-limits
[84] "What is Object Storage? - Object Storage Explained - AWS". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/what-is/object-storage/
[85] "Introduction to Azure Blob Storage". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blobs-introduction
[86] "Cloud Storage  |  Google Cloud". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/storage
[87] "IBM Cloud Object Storage | IBM ". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/object-storage
[88] "What Is Block Storage?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/what-is/block-storage/
[89] "Azure Disk Storage – Block Storage | Microsoft Azure". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/storage/disks
[90] "Persistent Disk". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/persistent-disk
[91] "IBM Cloud Block Storage". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/block-storage
[92] "Amazon S3 Glacier storage classes". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/s3/storage-classes/glacier/
[93] "Hot, cool, and archive access tiers for blob data". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/storage/blobs/access-tiers-overview
[94] "Storage classes". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/storage/docs/storage-classes
[95] MIKE WHEATLEY, "Google launches new storage option for long-term data". Accessed on Apr. 30, 2023. [Online]. Available: https://siliconangle.com/2020/01/09/google-launches-new-storage-option-long-term-data/
[96] Geoffrey Noer, "Put your archive data on ice with new storage offering". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/blog/products/storage-data-transfer/archive-storage-class-for-coldest-data-now-available
[97] "Flexible storage classes". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/object-storage/storage-class-tiers-archive
[98] "What Is Cloud File Storage?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/what-is/cloud-file-storage/
[99] "Azure Files". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/storage/files
[100] "Filestore". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/filestore
[101] "Storage Options in Google Cloud: Block, Network File, and Object Storage". Accessed on Apr. 30, 2023. [Online]. Available: https://bluexp.netapp.com/blog/object-storage-block-and-shared-file-storage-in-google-cloud
[102] "Cloud File Sharing Services: Google Cloud File Storage". Accessed on Apr. 30, 2023. [Online]. Available: https://bluexp.netapp.com/blog/nfs-cloud-file-storage-on-google-cloud
[103] "IBM Cloud File Storage". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/file-storage
[104] "What is file storage?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/topics/file-storage
[105] "Understanding AWS Egress Costs and How to Avoid Them". Accessed on Apr. 30, 2023. [Online]. Available: https://www.nops.io/aws-egress-costs-and-how-to-avoid/
[106] "Amazon S3 pricing". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/s3/pricing/?p=pm&c=s3&z=4
[107] "Amazon RDS". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/rds/
[108] "What is a relational database?". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/resources/cloud-computing-dictionary/what-is-a-relational-database/#examples
[109] "What is a relational database?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/learn/what-is-a-relational-database
[110] "What is a relational database?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/topics/relational-databases
[111] "What is NoSQL?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/nosql/
[112] "Amazon DynamoDB". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/dynamodb/
[113] "Non-relational data and NoSQL". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/architecture/data-guide/big-data/non-relational-data
[114] "Google Cloud NoSQL: Firestore, Datastore, and Bigtable". Accessed on Apr. 30, 2023. [Online]. Available: https://bluexp.netapp.com/blog/gcp-cvo-blg-google-cloud-nosql-firestore-datastore-and-bigtable
[115] "Your Google Cloud database options, explained". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/blog/topics/developers-practitioners/your-google-cloud-database-options-explained
[116] "Datastore". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/datastore
[117] "MongoDB Atlas on Google Cloud". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/mongodb
[118] "What are NoSQL databases?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/topics/nosql-databases
[119] "Getting Started". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.ibm.com/docs/databases-for-mongodb?topic=databases-for-mongodb-getting-started
[120] "IBM Cloud Databases for MongoDB". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/databases-for-mongodb
[121] "IBM Cloud Databases for DataStax". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/databases-for-datastax
[122] "IBM Cloudant". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/cloudant
[123] "IBM Cloud Databases for Elasticsearch". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/databases-for-elasticsearch
[124] "What Is an In-Memory Database?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/nosql/in-memory/
[125] "Optimize performance by using in-memory technologies in Azure SQL Database and Azure SQL Managed Instance". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-sql/in-memory-oltp-overview?view=azuresql
[126] "About Azure Cache for Redis". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/azure-cache-for-redis/cache-overview
[127] "Types of Databases on Azure". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/category/databases/
[128] "Memorystore". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/memorystore
[129] "IBM Cloud Databases for Redis". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/databases-for-redis
[130] "AWS Glue". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/glue/
[131] "What Is ETL (Extract Transform Load)?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/what-is/etl/
[132] "Evaluate AWS Glue vs. Data Pipeline for cloud-native ETL". Accessed on Apr. 30, 2023. [Online]. Available: https://www.techtarget.com/searchaws/tip/Evaluate-AWS-Glue-vs-Data-Pipeline-for-cloud-native-ETL
[133] "Extract, transform, and load (ETL)". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/architecture/data-guide/relational-data/etl
[134] "Pipelines and activities in Azure Data Factory and Azure Synapse Analytics". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/data-factory/concepts-pipelines-activities?tabs=data-factory
[135] "What is ETL?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/learn/what-is-etl
[136] Ronald Miller, "IBM Bluemix Data Connect Deprecation Announcement". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/blogs/cloud-archive/2017/12/ibm-bluemix-data-connect-deprecation-announcement/
[137] "ELT vs. ETL: What’s the Difference?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/blog/elt-vs-etl-whats-the-difference
[138] "IBM Cloud Pak for Data". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/products/cloud-pak-for-data
[139] "What is Hadoop?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/emr/details/hadoop/what-is-hadoop/
[140] "Azure HDInsight". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/hdinsight
[141] "What is Apache Hadoop in Azure HDInsight?". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/hdinsight/hadoop/apache-hadoop-introduction
[142] "What is Apache Hadoop?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/learn/what-is-hadoop
[143] "Apache Hadoop". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/analytics/hadoop
[144] "Free Data Lakes and Analytics on AWS". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/free/analytics/?trk=34c2d7cd-1420-4f9a-8661-56d00cb2d36c&sc_channel=ps&ef_id=EAIaIQobChMIhZHBsKPT_gIVjwytBh2iWwkWEAAYASAAEgIVpfD_BwE:G:s&s_kwcid=AL!4422!3!651751059021!e!!g!!aws%20data%20warehouse%20architecture!19852662158!145019246817
[145] "Amazon Redshift". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/redshift/?p=ft&c=aa&z=3
[146] "Data warehousing in Microsoft Azure". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/architecture/data-guide/relational-data/data-warehousing
[147] "What is a Data Warehouse?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/learn/what-is-a-data-warehouse
[148] "Cloud data warehouse to power your data-driven innovation". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/bigquery
[149] "Data warehouse solutions". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/data-warehouse
[150] "IBM Db2 Warehouse". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/products/db2/warehouse
[151] "What is a data warehouse?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/topics/data-warehouse
[152] "What is streaming data?". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/streaming-data/
[153] "Azure Stream Analytics". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/stream-analytics
[154] "Datastream". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/datastream
[155] "Dataflow". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/dataflow
[156] "IBM Streams". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/streaming-analytics
[157] "Amazon SQS". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/sqs/
[158] "What is Azure Queue Storage?". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/storage/queues/storage-queues-introduction
[159] "Storage queues and Service Bus queues - compared and contrasted". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted
[160] "What is Pub/Sub?". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/pubsub/docs/overview
[161] "Event-driven architecture with Pub/Sub". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/solutions/event-driven-architecture-pubsub
[162] "What is a message queue?". Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/topics/message-queues
[163] "Machine Learning on AWS". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/machine-learning/
[164] "Azure Machine Learning". Accessed on Apr. 30, 2023. [Online]. Available: Machine Learning azure
[165] "What is Azure Machine Learning?". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/machine-learning/overview-what-is-azure-machine-learning?view=azureml-api-2
[166] "AI and machine learning products". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/products/ai
[167] "Amazon Rekognition". Accessed on Apr. 30, 2023. [Online]. Available: https://aws.amazon.com/rekognition/
[168] "Azure Cognitive Services". Accessed on Apr. 30, 2023. [Online]. Available: https://azure.microsoft.com/en-us/products/cognitive-services/
[169] "What is Amazon VPC?". Accessed on Apr. 30, 2023. [Online]. Available: https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
[170] "What is Azure Virtual Network?". Accessed on Apr. 30, 2023. [Online]. Available: https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-overview
[171] "Virtual Private Cloud (VPC)". Accessed on Apr. 30, 2023. [Online]. Available: https://cloud.google.com/vpc
[172] network-appliances. Accessed on Apr. 30, 2023. [Online]. Available: https://www.ibm.com/cloud/network-appliances
[173] "Cloud Programming Simplified: A Berkeley View on Serverless Computing". Accessed on Apr. 30, 2023. [Online]. Available: https://arxiv.org/abs/1902.03383
[174] "6.824 Schedule: Spring 2020". Accessed on Apr. 30, 2023. [Online]. Available: http://nil.lcs.mit.edu/6.824/2020/schedule.html
[175] "6.824 2020 Lecture 1: Introduction". Accessed on Apr. 30, 2023. [Online]. Available: http://nil.lcs.mit.edu/6.824/2020/notes/l01.txt
[176] James Kurose, Keith Ross, "Computer Networking: A Top-Down Approach 8th". Accessed on Apr. 30, 2023. [Online]. Available: http://gaia.cs.umass.edu/kurose_ross/online_lectures.htm
```

