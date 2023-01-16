# Hadoop for Efficient Data Processing

<br/>

### Hadoop Docker (docker/)

> Code extracted from the last commit of the repository "https://github.com/big-data-europe/docker-hadoop" on Jun 29, 2020.

**Quick Start**

To deploy an example HDFS cluster, run:

```bash
  docker-compose up
```

Run example wordcount job:

```bash
  make wordcount
```

Or deploy in swarm:

```bash
docker stack deploy -c docker-compose-v3.yml hadoop
```

`docker-compose` creates a docker network that can be found by running `docker network list`, e.g. `dockerhadoop_default`.

Run `docker network inspect` on the network (e.g. `dockerhadoop_default`) to find the IP the hadoop interfaces are published on. Access these interfaces with the following URLs:

-   Namenode: http://<dockerhadoop_IP_address>:9870/dfshealth.html#tab-overview
-   History server: http://<dockerhadoop_IP_address>:8188/applicationhistory
-   Datanode: http://<dockerhadoop_IP_address>:9864/
-   Nodemanager: http://<dockerhadoop_IP_address>:8042/node
-   Resource manager: http://<dockerhadoop_IP_address>:8088/

<br/>

**Configure Environment Variables**

The configuration parameters can be specified in the hadoop.env file or as environmental variables for specific services (e.g. namenode, datanode etc.):

```
  CORE_CONF_fs_defaultFS=hdfs://namenode:8020
```

CORE_CONF corresponds to core-site.xml. fs_defaultFS=hdfs://namenode:8020 will be transformed into:

```
  <property><name>fs.defaultFS</name><value>hdfs://namenode:8020</value></property>
```

To define dash inside a configuration parameter, use triple underscore, such as YARN*CONF_yarn_log\*\*\_aggregation*\*\*enable=true (yarn-site.xml):

```
  <property><name>yarn.log-aggregation-enable</name><value>true</value></property>
```

The available configurations are:

-   /etc/hadoop/core-site.xml CORE_CONF
-   /etc/hadoop/hdfs-site.xml HDFS_CONF
-   /etc/hadoop/yarn-site.xml YARN_CONF
-   /etc/hadoop/httpfs-site.xml HTTPFS_CONF
-   /etc/hadoop/kms-site.xml KMS_CONF
-   /etc/hadoop/mapred-site.xml MAPRED_CONF

If you need to extend some other configuration file, refer to base/entrypoint.sh bash script.

<br/>

<br/>

### Reference

-   [Big Data Europe](https://www.big-data-europe.eu/) : Integrating Big Data, software & communicaties for addressing Europe's societal challenges
    -   GitHub : https://github.com/big-data-europe
    -   Docker Hub : https://hub.docker.com/u/bde2020
