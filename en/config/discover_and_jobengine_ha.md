

## Service Discovery and Job Engine HA

KAP supports service discovery from v2.0. Now KAP has a new implementation based on Apache Curator framework, which is more stable and flexible. To enable the service discovery, you need do the following configuration on each KAP instance:

 - Configure Zookeeper address in `kylin.properties`
 

 - Enable Curator based scheduler

```
```

 - Resart KAP

After restart, each KAP will register itself in Zookeeper, and each one will discover other instances from Zookeeper. 

By defaut, KAP will use `hostname -f` as the node name and the port in `tomcat/conf/server.xml` as the service port, and then broadcast this to cluster, for example: `salve1:7070`. This requires your cluster can resolve the hostname on each nodes. If not, it will cause connection error as they couldn't connect with each other. In this case, you needed manually specify the REST address when start KAP, for example:

```
export KYLIN_REST_ADDRESS=10.0.0.100:7070
$KYLIN_HOME/bin/kylin.sh start
```

### Job Engine HA


```
kylin.server.mode=query
```