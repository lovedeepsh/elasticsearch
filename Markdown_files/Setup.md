### **Configuring Elastic Search, Telegraf, Influxdb and Kafka** 

**Theory** 

The main Objective of this Proof Of Concept is to setup a DEMO environment through which we can monitor :-

- Elastic Search Data
- System Data
- Metrics

Basically Data is Time Series, So we are using Telegraf to fetch the Data using its Input Plugin and Pus the Time-Series Data inside the InfluxDB and also using Kafka to Visualize that data.

This is a DEMO Proof Of Concept for a Live environment (Having multiple elasticsearch nodes inside a cluster and monitoring its Time-Series data).

We will Use only one Elastic Search node inside this DEMO.
And perform various Operations step-by-step define below :-
___
### **Step 1** **Installing and Configuring JAVA**
____
**For UBUNTU**

```
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
sudo apt-get install oracle-java8-set-default
```

**Set JAVA_HOME & JRE_HOME**

Edit **/etc/environment** file and add the following lines at the end.

```
JAVA_HOME=/usr/lib/jvm/java-8-oracle  
JRE_HOME=/usr/lib/jvm/java-8-oracle-jre
```
----
**For CENTOS**

```
sudo yum install java-1.8.0-openjdk-devel
sudo yum install java-1.8.0-openjdk
```

Edit **/etc/environment** file and add the following lines at the end.

```
JAVA_HOME=/usr/lib/jvm/java-8-oracle  
JRE_HOME=/usr/lib/jvm/java-8-oracle-jre
```
----


### **Step 2 Installing Elastic Search**
_____
**For Ubuntu**

- Import the Elastic Search PGP key
 
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```

- Installing from the APT repository

You may need to install the apt-transport-https package on Debian before proceeding:

```
sudo apt-get install apt-transport-https
```

Save the repository definition to **/etc/apt/sources.list.d/elastic-6.x.list**:

```
echo "deb https://artifacts.elastic.co/packages/6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
```

You can install the Elasticsearch Debian package with:

```
sudo apt-get update && sudo apt-get install elasticsearch
```
____
**For CENTOS**

- Import the Elastic Search PGP key

```
rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch
```

- Create and Edit **/etc/yum.repos.d/elasticsearch.repo**

```
[elasticsearch-6.x]
name=Elasticsearch repository for 6.x packages
baseurl=https://artifacts.elastic.co/packages/6.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md
```

- Follow these commands to Install Elastic Search manually.

```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.4.0.rpm
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.4.0.rpm.sha512
sudo rpm --install elasticsearch-6.4.0.rpm
```
____
### **Step 3 Installing and Configuring InfluxDB Server**
____

**InfluxDB is an open source time series database with no external dependencies. It's useful for recording metrics, events, and performing analytics.**

- **For UBUNTU**

```
wget https://dl.influxdata.com/influxdb/releases/influxdb_1.6.1_amd64.deb
sudo dpkg -i influxdb_1.6.1_amd64.deb
```
____

- **For CENTOS**

```
wget https://dl.influxdata.com/influxdb/releases/influxdb-1.6.1.x86_64.rpm
sudo yum localinstall influxdb-1.6.1.x86_64.rpm
```

- **Starting the InfluxDB service**

```
service influxdb start
```

- **CONFIGURING**

Create your First DATABASE:

```
curl -XPOST "http://localhost:8086/query" --data-urlencode "q=CREATE DATABASE mydb"
```

Insert some data:

```
curl -XPOST "http://localhost:8086/write?db=mydb" \
-d 'cpu,host=server01,region=uswest load=42 1434055562000000000'

curl -XPOST "http://localhost:8086/write?db=mydb" \
-d 'cpu,host=server02,region=uswest load=78 1434055562000000000'

curl -XPOST "http://localhost:8086/write?db=mydb" \
-d 'cpu,host=server03,region=useast load=15.4 1434055562000000000'
```

Query that data:

```
curl -G "http://localhost:8086/query?pretty=true" --data-urlencode "db=mydb" \
--data-urlencode "q=SELECT * FROM cpu WHERE host='server01' AND time < now() - 1d"
```
____
### **Step 4 Installing and Configuring Kafka Server**
____

**Pre-reqisites**
- Docker

**Installing Docker First**

- For Ubuntu

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update
apt-cache policy docker-ce
sudo apt-get install -y docker-ce
sudo systemctl status docker
sudo usermod -aG docker ${USER}
su - ${USER}
sudo usermod -aG docker username
```

- For Centos

```
sudo yum check-update
curl -fsSL https://get.docker.com/ | sh
sudo systemctl start docker
sudo systemctl status docker
sudo systemctl enable docker
sudo usermod -aG docker $(whoami)
sudo usermod -aG docker username
```

### **Now Installing Kafka**

```
docker run -d -p 2181:2181 -p 9092:9092 \
    --env ADVERTISED_HOST=localhost \
    --env ADVERTISED_PORT=9092 spotify/kafka
```
____
### **Step 5 Installing and Configuring Telegraf**
____

**Using Ansible Role:**

Ansible role: https://github.com/rossmcdonald/telegraf
____

**Through Source**

Telegraf requires golang version 1.9 or newer, the Makefile requires GNU make. - 
- Install Go >=1.9
- Install dep ==v0.5.0
- Download Telegraf source:
    go get -d github.com/influxdata/telegraf

- Run make from the source directory
```  
    cd "$HOME/go/src/github.com/influxdata/telegraf"
    make
```
___

**For UBUNTU manually**

```
wget https://dl.influxdata.com/telegraf/releases/telegraf_1.7.3-1_amd64.deb
sudo dpkg -i telegraf_1.7.3-1_amd64.deb
```
___

**For CENTOS manually**

```
wget https://dl.influxdata.com/telegraf/releases/telegraf-1.7.3-1.x86_64.rpm
sudo yum localinstall telegraf-1.7.3-1.x86_64.rpm
```
___
**How to use it**

- See usage with:

```
./telegraf --help
```

- Generate a telegraf config file:

```
./telegraf config > telegraf.conf
```

- Generate config with only cpu input & influxdb output plugins defined:

```
./telegraf --input-filter cpu --output-filter influxdb config
```

- Run a single telegraf collection, outputing metrics to stdout:

```
./telegraf --config telegraf.conf --test
```

- Run telegraf with all plugins defined in config file:

```
./telegraf --config telegraf.conf
```

- Run telegraf, enabling the cpu & memory input, and influxdb output plugins:

```
./telegraf --config telegraf.conf --input-filter cpu:mem --output-filter influxdb
```

- For Advance Configuration please follow the link below:


https://github.com/influxdata/telegraf/blob/master/docs/CONFIGURATION.md
___









