# Hadoop-Mini-Project
Post-Sale Automobile Report
```
(base) khalids-iMac:~ raniabadr$ cd docker-hadoop

(base) khalids-iMac:docker-hadoop raniabadr$ docker-compose up -d
[+] Running 6/6
 ⠿ Network docker-hadoop_default  Creat...                                 0.4s
 ⠿ Container resourcemanager      Started                                  9.6s
 ⠿ Container nodemanager          Started                                  9.6s
 ⠿ Container historyserver        Started                                  9.5s
 ⠿ Container datanode             Started                                  9.5s
 ⠿ Container namenode             Started                                  9.6s

(base) khalids-iMac:docker-hadoop raniabadr$ docker ps
CONTAINER ID   IMAGE                                                    COMMAND                  CREATED         STATUS                   PORTS                                            NAMES
968a416be4f7   bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8   "/entrypoint.sh /run…"   4 minutes ago   Up 4 minutes (healthy)   8088/tcp                                         resourcemanager
9394cac54c9f   bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8          "/entrypoint.sh /run…"   4 minutes ago   Up 4 minutes (healthy)   9864/tcp                                         datanode
9ab2cbddfff8   bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8          "/entrypoint.sh /run…"   4 minutes ago   Up 4 minutes (healthy)   0.0.0.0:9000->9000/tcp, 0.0.0.0:9870->9870/tcp   namenode
3fe583b517bb   bde2020/hadoop-historyserver:2.0.0-hadoop3.2.1-java8     "/entrypoint.sh /run…"   4 minutes ago   Up 4 minutes (healthy)   8188/tcp                                         historyserver
f05e77263693   bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8       "/entrypoint.sh /run…"   4 minutes ago   Up 4 minutes (healthy)   8042/tcp                                         nodemanager
```
