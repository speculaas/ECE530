# ECE530 HW2
* https://arxiv.org/pdf/1710.01476.pdf
* 

## extra materials

* ContinuousDeliveryWithSpinnaker.pdf
* Betsy Beyer, Chris Jones, Jennifer Petoff, Niall Richard Murphy - Site Reliability Engineering_ How Google Runs Production Systems-O’Reilly Media (2016)
* Cloud Programming Simplified: A Berkeley View on Serverless Computing
  * https://arxiv.org/abs/1902.03383
  * Table 6: Characteristics of storage services by cloud providers to the serverless ideal.
  * 
* 

## II. CLOUD DEPLOYMENT SCENARIOS AND VENDORS
* 
### A. Cloud Vendors and Industry Market Share
* Amazon’s AWS [16]
* Forrester [17],
* Synergy [18]
* Google [20] is a very interesting case

### B. Other Major Cloud Providers
* Joyent
* Salesforce

## III. COMPUTE SERVICES
* towards serverless computing [24].
  * zero costs for idle time
  * https://arxiv.org/pdf/1902.03383.pdf
    * https://arxiv.org/abs/1902.03383
    * [v1] Sat, 9 Feb 2019 07:25:09 UTC 
    * Cloud Programming Simplified: A Berkeley View on Serverless Computing
    * Fallacy Since serverless computing programming is in high-level languages like Python, it’s easy to port applications between serverless computing providers.
    * 

### A. Virtual Machines
* Microsoft Azure
  * Azure Virtual Machine Scale Sets
  * 
* Google Cloud Service Engine 
  * live migration
  * Google Slackdriver
  * 
* IBM’s SoftLayer

### B. Container Services
* https://ieeexplore.ieee.org/document/7922500
* https://www.sciencedirect.com/science/article/pii/S0167739X16303041
* despite being an old technology
* AWS EC2 Container Service (ECS)
  * AWS Elastic Container Service for Kubernetes (EKS)
* Microsoft offers Azure Container Service (ACS)
  * Windows container
  * 
* Google Container Engine (GCE)
* Bluemix Container Service

### C. Serverless Compute
* Amazon Lambda
  * can be triggered by HTTP endpoints, in-app activity of mobile apps or through the AWS services, such as S3, Dynamo DB, Kinesis SNS or CloudWatch.
  * Node.js, Python, and Java
  * organizationally independent 
* Microsoft ; Azure Functions
  * May 2016
  * C#, JavaScript, Python, and PHP
  * grouped locally in an ”application”
* Google Cloud Functions
  * February 2016
  * JavaScript
  * event triggering by internal Google Cloud Storage events, Google Cloud Pub/Sub or HTTP invocations
* IBM Open-Whisk
  * February of 2016
  * Node.js, Python, Swift, and Docker.
  * Docker allows the implementation of actions in any language
  * missing features including HTTP customization, ...
* 

## IV. STORAGE SERVICES

### A. Object Storage
* AWS Simple Storage Service (S3) ; buckets
  * standard service level: 99.99% availability on year basis and 11 nines durability
  * infrequent service level:  99.9% availability;  same 11 nines durability, and lower storage costs as a counterweight for high ingress/egress costs
  * AWS Glacier:
  * formal specifications ; TLA+
* Azure ; Blob Storage ; containers
  * service levels
  * Azure Cool Blob
* Google Cloud Storage service
  * differences lie in their availability, storage duration, cost for storage, and access 
* Bluemix Cloud Object Storage service
  * https://www.ibm.com/cloud-computing/object-storage
  * https://www.ibm.com/cloud/object-storage
  * OpenStack Swift platform
  * smaller limit per object equal to 5 GB when uploaded thought the API
  * 11 nines durability with regional and cross-regional options.
  * https://www.trustradius.com/products/ibm-cloud-object-storage/reviews#comparisons
    * IBM Cloud Object Storage Technical Details
    * Operating Systems	Unspecified
  *  four different configurations for the Object Storage service
* Table V compares cost, availability, and region support in the public cloud object stores

### B. Block Storage
* AWS Elastic Block Storage (EBS)
  * service design, similarly to S3, was verified using TLA+ and formal specifications [33].
* Azure: Managed Disks service
* Google: Persistent Disk, ”PD”
  * https://cloud.google.com/persistent-disk
  * leader concerning the IOPS
    * SSD: 
      * 40,000 IOPS for reads and 30,000 for writes
      * 800 MB/s for reading and 400 MB/s for writing
    * Standard persistent disk: 
      * IOPs per-volume at 3,000 for reads and 15,000 for writes
      * maximum throughput per instance is 180 MB/s for reading and 120 MB/s for writing
    * https://blogs.oracle.com/cloud-infrastructure/post/300000-iops-per-volume-with-ultra-high-performance-oracle-cloud-infrastructure-block-volumes
  * 
* SoftLayer/Bluemix Block Storage service
  * 20GB to 12TB
* 

### C. File Storage
* also known as shared filesystem. 
* The shared filesystem protocols used today are the Network File System (NFS) and the Server Message Block (SMB).
* AWS Elastic File System (EFS)
  * utilizes EC2 instances and the NFS 4.1 protocol
  * 
* Azure File Storage
  * SMB 3.0
  * stored data are also accessible using a REST API for better integration
* Google: standard Cloud Storage service
  * custom Compute Engine instances that can be utilized as dedicated file servers
* Bluemix’s File Storage

## V. DATABASE SERVICES
* http://nil.csail.mit.edu/6.824/2020/notes/l-spanner.txt

|Service Type |Amazon |Microsoft |Google |IBM|
|----|----|----|----|----|
|Relational Database|AWS RDS,Aurora |Azure SQL Database, Database for PostgreSQL |Cloud SQL, spanner |dashDB for Transactions SQL Database,|
|In-Memory Data Services |Amazon |Microsoft |Google |IBM|
|Cloud ETL |Amazon |Microsoft |Google |IBM|

### A. Relational Database Management Services (RDBMS)
* AWS Relational Database Service (RDS)
  * provides a number of database types, including Amazon Aurora .. Oracle, PostgreSQL, MariaDB, MySQL, and Microsoft SQL Server
  * attractive alternative to running an owned instance in EC2 as it takes care of provisioning, patching, and maintenance
  * http://nil.csail.mit.edu/6.824/2020/notes/l-aurora.txt
    * LEC 10: Cloud Replicated DB, Aurora
    * http://nil.csail.mit.edu/6.824/2020/schedule.html
    * 
  * 
* Azure: SQL Database ; 
  * based on SQL Server
  * Stretch Database
* Google: Cloud SQL
  * up to 16 vCPUs available
  * Cloud Spanner
  * Python, Go, Java, Node.js along with Java Database Connectivity (JDBC)
* IBM: multiple Bluemix services
  * DashDB for Transactions SQL Database
    * supports all native DB2 drivers, SQL, PureData, .NET, Open Database Connectivity (ODBC), Java Database Connectivity (JDBC), Netezza, and Oracle
    * either dedicated instances with 8GB RAM, 2 vCPUs, 500 GB of data and logs space, 
    * or dedicated bare metal instances with 128GB RAM and 1.4 TB of SSD storage.
  * DB2 on Cloud service
    * a database on SoftLayer infrastructure
  * 
* 

### B. Non Relational Database Management Services
* DynamoDB
  * DAX ; in-memory, write through cache
  * Global Tables service
  * 
* Azure ; Cosmos DB
  * variety of APIs, including JavaScript, MongoDB, DocumentDB, SQL, Gremlin, and Azure Table storage for data query. 
  * graph, keyvalue, and document data 
* Google
  * Cloud Datastore service
    * strong consistency, and ACID transactions
    * charges for read/write operations, storage and bandwidth
    * Go, Java, JavaScript (Node.js), PHP, Python, and Ruby
  * BigTable
    * Apache HBase API
    * charges for ’nodes’, storage and bandwidth
    * Go and Java programming
  * 
* IBM ; Cloudant NoSQL DB
  * text, JSON, and geospatial
  * bulk or individually
  * Java, Node.js, Python, Swift and Mobile Platforms 
* 

### C. In-Memory Data Services
* AWS ElastiCache
  * compatibility with two different opensource engines: Memcached [57] and Redis [58].
    * http://nil.csail.mit.edu/6.824/2020/notes/l-memcached.txt
  * 
* Microsoft ; Redis Cache service
* Google ; App Engine service with App Engine Memcache
* IBM ; Bluemix Redis Cloud


## VI. BIG DATA AND ANALYTICS

### A. Big Data Managed Cluster-as-a-Service
* AWS Elastic MapReduce (EMR)
  * Hadoop, Spark [43], HBase, Flink, and Presto solution that supports an underlying EC2 cluster with the combination of AWS services such as S3 and DynamoDB. 
  * Core nodes
  * Ruby, Perl, Python, Java, R, C++, and PHP
  * https://medium.com/empathyco/success-story-from-aws-emr-to-kubernetes-2135387d7e25
* Azure ; HDInsight service
  * supports Apache Hadoop, Spark, HBase, Microsoft R Server, and Kafka in the Azure cloud
  * store data directly in Azure Blob storage
  * Java and Python
  * Hive, Pig, and Storm applications
    * https://learn.microsoft.com/en-us/azure/hdinsight/hadoop/apache-hadoop-hive-pig-udf-dotnet-csharp
    * https://pig.apache.org/ ; Pig's infrastructure layer consists of a compiler that produces sequences of Map-Reduce programs
  * plugins for both IntelliJ IDEA and Eclipse
  * PowerShell, Bash, and Windows command inputs
* Google ; Cloud DataProc
  * can host MapReduce, Spark, SparkSQL, Hive, and Pig jobs
  * Python, Java, Scala, and R.
  * Hadoop Distributed File System compliant connector
  * On-demand clusters are not supported initially
  * full control over the cluster: Google Cloud Platform Console (gcloud cli), Cloud Datapro REST API or Google Cloud SDK
* IBM ; BigInsights for Apache Hadoop
  * open source Hadoop with a number of tools and capabilities, including Big SQL, BigSheets, Java MapReduce, Big R (R Language integration in Hadoop), and In-Hadoop Analytics.
  * supports Pig, HBase, Hive, and integration with Spark through a separate service Bluemix Apache Spark.
  * integration with the rest Bluemix services offering interfaces for advanced data analytics, social media analytics and extraction/analysis of text
* 

### B. Data Warehouse

* Amazon ; Redshift
  * based on a SQL data warehouse
  * Java Database Connectivity (JDBC), Open Database Connectivity connections (ODBC)
  * integration with other AWS services
  * load data and information in parallel to each node from AWS DynamoDB, S3 or EC2.
  * can add AWS Kinesis, Elastic MapReduce, Data Pipeline, and Lambda.
* Azure ; SQL Data Warehouse
  * composed of Storage (data are stored in Azure Blob storage), Compute Nodes and Data Movement Service
  * only have to pay for the query performance they require
  * while other vendors force customers to delete the existing cluster, backup the existing data and restore them later.
* Google ; BigQuery
  * serverless
  * manage projects and datasets in the Google Cloud Platform
  * quick scaling to petabytes and requires no provision to scale a cluster
  * load their data via a streaming API for real-time analytics or transfer data towards other regions of the Google infrastructure
* IBM ; dashDB for Analytics
  * IBM’s BLU Acceleration technology
  * comes with embedded Netezza analytics, linear regression capabilities, decision tree clustering, K-means clustering, IBM Watson, and R support for predictive analytics
* 

## VII. DATA PIPELINES

### A. Streaming Services
* AWS ; Kinesis Streams
  * for processing information pipelines
  * using the Connector Library and Kinesis Client Library
  * and up to 5 read transactions per second
* Azure ; Stream Analytics
  * ability to process Blob storage data or information streamed through Event Hubs/IoT Hub.
  * SQL-based language is utilized to perform queries
  * Event Hubs stream capacity: throughput unit
  * Event publishing: HTTPS or AMQP 1.0
  * https://learn.microsoft.com/en-us/azure/stream-analytics/stream-analytics-introduction
* Google ; Cloud Dataflow service
  * AWS and Azure: delegates processing to adjacent services such as Hadoop
  * supports a fully programmable (Python, Java) framework and a distributed computing platform.
  * batch and streaming workers
  * https://cloud.google.com/learn/what-is-streaming-analytics
* IBM ; Streaming Analytics
  * a programming language, an API, an IDE for applications, and a runtime system that can run the applications on a single or distributed set of resources. 
  * Java, Python, and Scala
  * standard: 4-core virtual server nodes with 12GB of RAM and 1Gbits/second Network
  * premium: 16-core virtual server with 256GB of RAM, 2TB of disk and unlimited public bandwidth at 100 Mbps
  * https://www.ibm.com/cloud/streaming-analytics
    * ? https://cloud.google.com/learn/what-is-streaming-analytics
  * 
* 

### B. Queuing Services
* AWS Simple Queue Service (SQS)
  * Java, Ruby, Python, .NET, PHP, and Java Script/Node.js.
  * Standard Queues: best-effort policy for ordering
  * First-In First-Out (FIFO) Queues
  * message size: 256 KB of text data (XML, JSON or unformated)
  * queue sizes:
  * latencies
* MS ; Storage Queues and Service Bus Queues
  * Storage Queues
    * Azure Storage family and provides reliable message exchange between services
    * offers no guarantees regarding ordering and an at-least-once delivery policy
    * queue size
    * unlimited number of queues
    * maximum size of a message is 64 KB
  * Service Bus Queues 
    * part of Azure’s messaging infrastructure offering FIFO ordering guarantee with an addition of at-most-once delivery policy. 
    * number of queues is limited to 10000
    * maximum queue size
    * message size
  * REST, HTTPS
  * APIs for .NET, C++, Java, PHP, and Node.js.
  * Service Bus Topics and Subscriptions
    * a message is broadcasted to multiple resources in a publish/subscribe fashion
    * scale the queuing functionalities to many recipients, as it resembles a virtual queue where messages are sent to a specific topic and are received to one or more associated subscriptions
* Google ; cloud PUB/SUB service
  * an engine that allows message exchange between individual entities.
  * using a single topic and subscription logic
  * at-least-once delivery policy is implemented and a FIFO (in-order) guarantee is not supported.
  * GO, C#, Node.js, Java, PHP, Python, and Ruby
* IBM ; does not support such functionality through a dedicated cloud service inside Bluemix
* 

## VIII. MACHINE LEARNING AND ARTIFICIAL INTELLIGENCE

* AWS
  * AWS Lex
    * English language with 15 seconds speech input of either Linear Pulse Code Modulation (LPCM) or Opus [73] format.
  * AWS Polly
    * text-to-speech conversion
  * AWS Rekognition
    * image processing applications
  * Amazon Rekognitionm supports a variety of image labels used to extract common categories and supports facial analysis, comparison, and recognition with the ability to detect 12 different facial attributes.
  * AWS Machine Learning
    * real-time predictions within 100 ms
  * APIs that include Java, .NET, Node.js, PHP, Python, Ruby, Go, C++, Android, and iOS.
* Azure Cognitive Services
  * APIs for different AI functionalities
  * language processing
    * Language Understanding Intelligent Service (LUIS)
      * application with HTTP endpoints that provide written language understanding capabilities
    * Translator Text API and the Text Analytics API (V 2.0)
      * key phrase extraction (for 5 languages) and sentiment analysis (for 15 languages)
      * data limits
    * Translator Speech API, the Custom Speech Service
      * processing spoken language
      * speech-to-text transcriptions
      * Speaker Recognition API for speaker identification
  * Emotion API and Face API ; face recognition capabilities
  * Computer Vision API
    * General image processing needs
    * Input image formats include JPEG, GIF, BMP, and PNG
    * C#, Java, PHP, JavaScript, Python, and Ruby.
  * Machine Learning service
    * general ML applications with dataset support of up to 10 GB (multiple inputs)
    * Scripting modules include the support of SQL, R, and Python, while for new custom modules the customers can only use R.
* Google
  * Cloud Machine Learning Engine
  * Cloud Natural Language API
    * packing label, syntax analysis, and sentiment extraction
    * Cloud Client Libraries for developers working with the Natural Language API include Java, PHP, Ruby, Python, Node.js, C#, and Go
  * Cloud Vision API
    * face, logo, landmark and any custom content detection on the input image
    * JPEG, PNG, GIF, BMP, WEBP, and ICO
  * custom Tensor Processing Units (TPUs)
  * TensorFlow
    * opportunity for the customer to integrate ML accelerations directly to their existing product
* Watson Machine Learning service
  * main powerhouse behind cognitive application development.
  * set of REST APIs called from any programming language
  * allows integration with the IBM SPSS Modeler
    * a data mining and text analysis workbench
  * free plan with the ability to deploy up to 5 models with 5000 predictions per month and a 5 hour per month restriction in compute time
  * fully optimized professional plan offers 2000000 predictions and 1000 compute hours with extra billing for any extra hour or any extra 1000 predictions
  * language processing and text reckognition applications
    * Natural Language Classifier
      * understands and processes text that can be provided in CSV format, UTF-8 encoded and with maximum 15000 rows or 1024 characters
      * supports 9 different languages
      * Node.js, Python or Java APIs
    * 
  * 
* 

