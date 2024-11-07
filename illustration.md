# Hand Over CIB session :

## Main points :
1. [Know About confluent](#What-is-confluent-platform)
2. [Confluent Services and their fucntionalities](#core-services-in-confluent-platform-and-their-functionalities)
3. [Ports](#ports-of-services)
4. [Order of Starting and Stopping services](#order-of-starting-and-stopping-services)


## What is confluent platform?
  it aims at enabling reliable data streaming, processing, and integration across various systems.


  ## Core services in Confluent Platform and their functionalities:

<span style="color:lightblue; font-size:20px;">1. Kafka Brokers </span>

    A Kafka broker’s primary function is to : 
    - manage and store the data streams
    -  facilitate client interactions (producers and consumers)
    - ensure fault tolerance and high availability within the Kafka cluster.

    It is the central server component that keeps Kafka highly scalable, distributed, and reliable.

<span style="color:lightblue; font-size:20px;">1.1 Metadata Service (MDS) </span>

  It handles authorization by storing and managing ACLs, defining who can access Kafka resources, It can integrate with LDAP servers.

 ### Example Flow of an Authorization Request
1. Client Authentication:
 A client (producer/consumer) authenticates with a Kafka broker using SSL, SASL, or other security mechanisms.
2. Authorization Check: After authentication, the broker consults the Metadata Service to check if the client has the appropriate credentials&authorization(role) to access the requested Kafka resource.
3. Access Granted/Denied: Based on the Authorization(role) retrieved from ZooKeeper, the broker either allows or denies the client's request.

<span style="color:lightblue; font-size:20px;">2. Zookeeper

</span>
It handles:

- Cluster Metadata Management:

   ZooKeeper stores metadata about Kafka brokers, topics, and partitions. Kafka brokers register themselves with ZooKeeper, which then keeps track of active brokers and partition assignments.
- Leader Election:

  When a broker (server) goes down, ZooKeeper helps elect a new leader for the affected partitions.
- Configuration Management:

  ZooKeeper manages certain configurations and settings across brokers, including broker quotas, user configurations, and security settings.

   <span style="color:lightblue; font-size:20px;">3. Confluent Control Center</span>

   Functionality:
   
    Control Center provides   <span style="color:green;"> a graphical </span>
 interface to monitor and manage Kafka clusters. It tracks broker and topic performance, schema validation, and other Kafka components.

   Capabilities:
   - Monitor real-time throughput, lag, and partition distribution.
   - Configure and monitor consumer groups. 

   <span style="color:lightblue; font-size:20px;">4. Kafka Connect</span>

   Functionality:
   
    Kafka Connect is a framework for integrating Kafka with other data systems using connectors. It can pull data into Kafka from external systems (sources) or push data from Kafka to external systems (sinks).

   Use Cases:
  - Connect relational databases, NoSQL databases, file systems, and cloud storage with Kafka.
  - Perform ETL (Extract, Transform, Load) with streaming data.

  <span style="color:lightblue; font-size:20px;">5. Confluent Schema Registry</span>

   Functionality:
   
   Schema Registry stores and enforces data schemas for Kafka messages, ensuring data compatibility and quality across services.

   Key Features: 
  - Supports versioned schemas, typically in Avro, JSON Schema, or Protobuf format.
  - Ensures compatibility between producers and consumers using schema evolution.

  
 <span style="color:lightblue; font-size:20px;"> 6. ksqlDB
</span>

Functionality:

 ksqlDB is a SQL-based stream processing service that allows users to write continuous queries on Kafka topics, transforming streams of data in real time.

Capabilities:
- Perform filtering, aggregation, and joining of data streams.
- Enables real-time analytics, ETL processing, and materialized views directly on Kafka.
- Simplifies stream processing with SQL queries rather than complex coding.

 <span style="color:lightblue; font-size:20px;">7. Confluent REST Proxy

</span>

Functionality:

 REST Proxy enables RESTful HTTP access to a Kafka cluster, allowing applications that don’t support Kafka’s native protocol to interact with it.

Use Cases:

- Integrate Kafka with web-based applications and microservices.
- Perform producer and consumer operations via HTTP endpoints.

<span style="color:lightblue; font-size:20px;">8. Zookeeper

</span>


## Ports of services

You will find the file attached : 
[Confluent communication matrix file](./CommunicationMatrix.xlsx)

## Order of Starting and Stopping services:

Starting Order: (and vice versa)
1. ZooKeeper
2. Kafka Brokers
3. Schema Registry
4. Kafka Connect
5. ksqlDB & kafka rest proxy(they depend on Brokers & Schema-registry)
6. Confluent Control Center 

