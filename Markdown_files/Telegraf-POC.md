### **_TELEGRAF_**

**For configuring the Telegraf with elasticsearch, Follow the given link**

https://docs.wavefront.com/elasticsearch.html

**POC QUESTIONS**

- What is Telegraph?
- How it works & How to use?
- Configuration of Telegraph?
- How to export matrix using Telegraph?
- Integration with ElasticSearch?

## 1. What is Telegraph?

Telegraf is part of the TICK Stack and is a plugin-driven server agent for collecting and reporting metrics.

```
What is TICK Stack?
The TICK Stack is a collection of associated technologies which combine to deliver a platform for storing, capturing, monitoring and visualizing data that is in time series. 
```

- Telegraf has integrations to source a variety of metrics, events, and logs directly from the containers and systems it’s running on, pull metrics from third-party APIs, or even listen for metrics via a StatsD and Kafka consumer services.

- It also has output plugins to send metrics to a variety of other datastores, services, and message queues, including InfluxDB, Graphite, OpenTSDB, Datadog, Librato, Kafka, MQTT, NSQ, and many others.

## Properties Of Telegraf

**Agent**

- Telegraf is a metric collection daemon that can collect metrics from a wide array of inputs and write them into a wide array of outputs.
- It is plugin-driven for both collection and output of data so it is easily extendable.
- It is written in Go, which means that it is a compiled and standalone binary that can be executed on any system with no need for external dependencies, no npm, pip, gem, or other package management tools required.


**Coverage**

- With over 200 plugins already written by subject matter experts on the data in the community, it is easy to start collecting metrics from your end-points.
- Even better, the ease of plugin development means you can build your own plugin to fit with your monitoring needs.
- You can even use Telegraf to parse the input data formats into metrics. These include: InfluxDB Line Protocol, JSON, Graphite, Value, Nagios, and Collectd.


**Flexible**

- The Telegraf plugin architecture supports your processes and does not force you to change your workflows to work with the technology.
- Whether you need it to sit on the edge, or in a centralized manner, it just fits with your architecture instead of the other way around.
- Telegraf’s flexibility makes it an easy decision to implement.


## 2. How it works?

**Telegraf Input Plugin**
Use this plugin to gather Elasticsearch health statistic clusters. The Elasticsearch Telegraf plugin queries endpoints to obtain node and optionally cluster-health or cluster-stats metrics:
- The **cluster nodes stats API** allows to retrieve one or more (or all) of the cluster nodes statistics.
- The **cluster health API** allows to get a very simple status on the health of the cluster.
- The **Cluster Stats API** allows to retrieve statistics from a cluster wide perspective.

**URL** - https://github.com/influxdata/telegraf/tree/master/plugins/inputs/elasticsearch

**Telegraf Output Plugin**
- This plugin writes to Elasticsearch via HTTP using Elastic, an Elasticsearch client for the Go programming language. 
- Currently it only supports Elasticsearch 5.x series.
- This plugin can manage indexes per time-frame, as commonly done in other tools with Elasticsearch. The timestamp of the metric collected will be used to decide the index destination.

**URL** - https://github.com/influxdata/telegraf/tree/release-1.4/plugins/outputs/elasticsearch


### **There are basically 3 types of Plugins used by Telegraf**
- Input Plugin - Services that Telegraf can collect data from.
- Output Plugin - Services that Telegraf can push data to.
- Service Plugin - Services that can push data to Telegraf.

**For a complete list see**
https://docs.influxdata.com/telegraf/v0.13/

**To Install Please follow the GIT Link below and FInd the Ansible Role for the Installation of Telegraf**
```
```


**To Generate the Telegraf.conf file, Use the following command**
```
$ telegraf -sample-config > telegraf.conf
```










