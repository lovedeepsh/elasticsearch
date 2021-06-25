### **Elastic Search**
___________
- Elasticsearch is an open-source search server written in Java and built on top of Apache Lucene.
- It is a NO-SQL, distributed database.
- ES is a document-oriented database designed to store, retrieve, and manage document-oriented or semi-structured data.
- When you use Elasticsearch, you store data in JSON document form. Then, you query them for retrieval.
- It is schema-less, using some defaults to index the data unless you provide mapping as per your needs.
- Elasticsearch uses Lucene StandardAnalyzer for indexing for automatic type guessing and for high precision.
- It provides a distributed, full-text search engine suitable for enterprise workloads.
- While not a Time Series Database per se, Elasticsearch employs Lucene’s column indexes, which are used to aggregate numeric values.
- Combined with query-time aggregations and the ability to index on time-stamp fields (which is also important for storing and retrieving log data), Elasticsearch provides the primitives for storing and querying time series data.
- When coupled with Kibana, a visualization tool, Elasticsearch can be used to provide near-real time analytics using large volumes of log data.


**How does Elastic Search works**

- You can send new data, called documents, to Elasticsearch using the API or ingestion tools such as Logstash and Amazon Kinesis Firehose.
- Elasticsearch automatically stores the original document and adds a searchable reference to the document in the cluster’s index.
- You can then search and retrieve the document using the Elasticsearch API.
- You can also use Kibana, an open-source analytics and visualization tool, to search, analyze, and dashboard your data.

**Elastic Search Benefits**
- **Fast :** You can also use Kibana, an open-source analytics and visualization tool, to search, analyze, and dashboard your data.
- **Easy-to-use API's :** Elasticsearch offers simple REST based APIs, a simple HTTP interface, and uses schema-free JSON documents making it easy to index, search, and query your data.
- **Complimentry tooling & plugins :** Elasticsearch comes integrated with Kibana, a popular visualization and reporting tool. It also offers built-in integration with Logstash to easily transform source data using pre-defined templates and load it data into your index. In addition, you can use a number of open-source Elasticsearch plug-ins such as language analyzers and suggesters to readily add rich functionality to your applications.
- **Near real-time Index updates :** Elasticsearch index updates such as adding a new document to the index usually take one second or less before the updated data is available for search. This lets you use Elasticsearch for near real-time use cases such as application monitoring and anomaly detection.

**Elastic Search Use cases**

- Log Analytics 
- Full text search
- Distributed document store
- Real-time application monitoring

**Basic concepts of Elastic Search**

Let's take a look at the basic concepts of Elasticsearch: clusters, near real-time search, indexes, nodes, shards and more.

- **Cluster :** A cluster is a collection of one or more servers that together hold entire data and give federated indexing and search capabilities across all servers. For relational databases, the node is DB Instance. There can be N nodes with the same cluster name.
- **Near-Real-Time (NRT) :** Elasticsearch is a near-real-time search platform. There is a slight from the time you index a document until the time it becomes searchable.
- **Index :** The index is a collection of documents that have similar characteristics. For example, we can have an index for customer data and another one for a product information. An index is identified by a unique name that refers to the index when performing indexing search, update, and delete operations. In a single cluster, we can define as many indexes as we want. Index = database schema in an RDBMS (relational database management system) — similar to a database or a schema. Consider it a set of tables with some logical grouping. In Elasticsearch terms: index = database; type = table; document = row.
- **Node :** A node is a single server that holds some data and participates on the cluster’s indexing and querying. A node can be configured to join a specific cluster by the particular cluster name. A single cluster can have as many nodes as we want. A node is simply one Elasticsearch instance. Consider this a running instance of MySQL. There is one MySQL instance running per machine on different a port, while in Elasticsearch, generally, one Elasticsearch instance runs per machine. Elasticsearch uses distributed computing, so having separate machines would help, as there would be more hardware resources.
- **Shards :** A shard is a subset of documents of an index. An index can be divided into many shards. 

____
### **Influx DB**
____

- InfluxDB is an open source Time Series Database written in Go.
- At its core is a custom-built storage engine called the Time-Structured Merge (TSM) Tree, which is optimized for time series data.
- Controlled by a custom SQL-like query language named InfluxQL, InfluxDB provides out-of-the-box support for mathematical and statistical functions across time ranges and is perfect for custom monitoring and metrics collection, real-time analytics, plus IoT and sensor data workloads.
- InfluxDB is used as a data store for any use case involving large amounts of time-stamped data, including DevOps monitoring, log data, application metrics, IoT sensor data, and real-time analytics.
- Conserve space on your machine by configuring InfluxDB to keep data for a defined length of time, automatically expiring & deleting any unneeded data from the system.
- InfluxDB also offers a SQL-like query language for interacting with data.

**Benefits of Influx DB**

- **High Performance :** InfluxDB is a high-performance data store written specifically for time series data. It allows for high throughput ingest, compression and real-time querying of that same data. InfluxDB is written entirely in Go and it compiles into a single binary with no external dependencies. It provides write and query capabilities with the command line interface, the built-in HTTP API, a set of client libraries (like Go, Java, and Javascript to name a few) and with plugins for common data formats such as Telegraf, Graphite, Collectd, and OpenTSDB.
- **SQL-Like Queries :** nfluxDB provides InfluxQL as a SQL-like query language for interacting with your data. It has been lovingly crafted to feel familiar to those coming from other SQL or SQL-like environments while also providing features specific to storing and analyzing time series data. InfluxQL also supports regular expressions, arithmetic expressions, and time series specific functions to speed up data processing.
- **Downsampling & Data Retention :** InfluxDB can handle millions of data points per second. Working with that much data over a long period of time can create storage concerns. InfluxDB will automatically compact the data to minimize your storage space. In addition, you can easily downsample the data; keeping the high precision raw data for only a limited time, and storing the lower precision, summarized data for much longer or forever. InfluxDB offers two features—Continuous Queries (CQ) and Retention Policies (RP)—that help you automate the process of downsampling data and expiring old data.


**Organizations using InfluxDB**

- BBOX
- CISCO
- CITRIX
- COUPA
- EBAY
- IBM

____
### **Time Series Data**
____

- It is used to analyze historical data to make predictions about market prices in the perspect of time.
- Time series data is evanescent and voluminous, which is to say, it comes and goes quickly and in great number.
- A time series is a series of data points indexed (or listed or graphed) in time order.
- Most commonly, a time series is a sequence taken at successive equally spaced points in time.
- Time series are very frequently plotted via line charts.

____
### **Telegraf**
____

- Telegraf is the Agent for Collecting and Reporting Metrics & Data
- Telegraf is part of the TICK Stack and is a plugin-driven server agent for collecting and reporting metrics.
- Telegraf has integrations to source a variety of metrics, events, and logs directly from the containers and systems it’s running on, pull metrics from third-party APIs, or even listen for metrics via a StatsD and Kafka consumer services.
- It also has output plugins to send metrics to a variety of other datastores, services, and message queues, including InfluxDB, Graphite, OpenTSDB, Datadog, Librato, Kafka, MQTT, NSQ, and many others.


**Concepts of Telegraf**

- **AGENT :** Telegraf is a metric collection daemon that can collect metrics from a wide array of inputs and write them into a wide array of outputs. It is plugin-driven for both collection and output of data so it is easily extendable. It is written in Go, which means that it is a compiled and standalone binary that can be executed on any system with no need for external dependencies, no npm, pip, gem, or other package management tools required.
- **Coverage :**With over 200 plugins already written by subject matter experts on the data in the community, it is easy to start collecting metrics from your end-points. Even better, the ease of plugin development means you can build your own plugin to fit with your monitoring needs. You can even use Telegraf to parse the input data formats into metrics. These include: InfluxDB Line Protocol, JSON, Graphite, Value, Nagios, and Collectd.
- **Flexible :** The Telegraf plugin architecture supports your processes and does not force you to change your workflows to work with the technology. Whether you need it to sit on the edge, or in a centralized manner, it just fits with your architecture instead of the other way around. Telegraf’s flexibility makes it an easy decision to implement.





