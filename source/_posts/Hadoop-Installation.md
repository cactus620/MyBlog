title: Hadoop on 64-bit Ubuntu
date: 2014-12-04 17:19:16
categories: Programming
tags:
---
Finally I managed to install Hadoop and start it correctly. Although at first I plan to setup one master node and three slaves as the data nodes. At last there's only one master node and one data node running on the same machine.
<!--more-->

I'm using Ubuntu 14.04.1 and Hadoop 2.5.2. Actually all went smoothly at first, as there're lots of tutorials and articles about this, for example this one [here](http://www.bogotobogo.com/Hadoop/BigData_hadoop_Install_on_ubuntu_single_node_cluster.php). The main problem which really bothered me is that I'm using the 64-bit Ubuntu system, while the Hadoop installation only contain 32-bit libraries.

There's only a warning saying:
``` sh
 ...WARN util.NativeCodeLoader: Unable to load native-hadoop library for your platform... using builtin-java classes where applicable
```
But actually, this caused the data nodes not really started for me. After running start-all.sh the status report shows there's no data node running and the capacity is all 0.
``` sh
 $ jps
 20501 SecondaryNameNode
 20296 NameNode
 21032 Jps
 20651 ResourceManager
 $ bin/hdfs dfsadmin -report
 Configured Capacity: 0 (0 B)
 Present Capacity: 0 (0 B)
 DFS Remaining: 0 (0 B)
 DFS Used: 0 (0 B)
 DFS Used%: NaN%
 Under replicated blocks: 0
 Blocks with corrupt replicas: 0
 Missing blocks: 0
 
 -------------------------------------------------
 Datanodes available: 0 (0 total, 0 dead)
```
The problem is solved after building the 64-bit library following the instructions [here](http://beadooper.com/?p=144).

Next, I'd like to still setup the three slave machines as planned. And then get something to run on it.
