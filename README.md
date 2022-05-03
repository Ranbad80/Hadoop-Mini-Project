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

(base) khalids-iMac:docker-hadoop raniabadr$docker cp /Users/raniabadr/Documents/Hadoop_mini_project/final_mapper.py namenode:final_mapper.py
(base) khalids-iMac:docker-hadoop raniabadr$docker cp /Users/raniabadr/Documents/Hadoop_mini_project/final_reducer.py namenode:final_reducer.py
(base) khalids-iMac:docker-hadoop raniabadr$docker cp /Users/raniabadr/Documents/Hadoop_mini_project/final_reducer2.py namenode:final_reducer2.py
(base) khalids-iMac:docker-hadoop raniabadr$docker cp /Users/raniabadr/Documents/Hadoop_mini_project/final_mapper2.py namenode:final_mapper2.py
(base) khalids-iMac:docker-hadoop raniabadr$ docker exec -it namenode bash
root@9ab2cbddfff8:/# ls
KEYS  bin  boot  dev  entrypoint.sh  etc  final_mapper.py  final_mapper2.py  final_reducer.py  final_reducer2.py  hadoop  hadoop-data  home  lib  lib64  media	mnt  opt  proc	root  run  run.sh  sbin  srv  sys  tmp	usr  var
root@9ab2cbddfff8:/# hdfs dfs -mkdir -p /user/root/input
root@9ab2cbddfff8:/# exit
exit
(base) khalids-iMac:docker-hadoop raniabadr$ docker cp /Users/raniabadr/docker-hadoop/data.csv namenode:data.csv
(base) khalids-iMac:docker-hadoop raniabadr$ docker exec -it namenode bash
root@9ab2cbddfff8:/# hdfs dfs -put data.csv /user/root/input
put: `/user/root/input/data.csv': File exists
root@9ab2cbddfff8:/# hadoop jar /opt/hadoop-3.2.1/share/hadoop/tools/lib/hadoop-streaming-3.2.1.jar \
> -file final_mapper.py -mapper final_mapper.py \
> -file final_reducer.py -reducer final_reducer.py \
> -file final_mapper2.py -mapper final_mapper2.py \
> -file final_reducer2.py -reducer final_reducer2.py \
> -input input -output output
2022-05-03 02:04:44,963 WARN streaming.StreamJob: -file option is deprecated, please use generic option -files instead.
packageJobJar: [final_mapper.py, final_reducer.py, final_mapper2.py, final_reducer2.py, /tmp/hadoop-unjar6110838956766672237/] [] /tmp/streamjob3833710192428772920.jar tmpDir=null
2022-05-03 02:04:46,162 INFO client.RMProxy: Connecting to ResourceManager at resourcemanager/172.18.0.2:8032
2022-05-03 02:04:46,375 INFO client.AHSProxy: Connecting to Application History server at historyserver/172.18.0.3:10200
2022-05-03 02:04:46,408 INFO client.RMProxy: Connecting to ResourceManager at resourcemanager/172.18.0.2:8032
2022-05-03 02:04:46,409 INFO client.AHSProxy: Connecting to Application History server at historyserver/172.18.0.3:10200
2022-05-03 02:04:46,684 INFO mapreduce.JobResourceUploader: Disabling Erasure Coding for path: /tmp/hadoop-yarn/staging/root/.staging/job_1651542637195_0001
2022-05-03 02:04:46,942 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:47,774 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:47,830 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:48,267 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:48,329 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:48,841 INFO mapred.FileInputFormat: Total input files to process : 1
2022-05-03 02:04:48,885 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:48,918 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:48,946 INFO mapreduce.JobSubmitter: number of splits:2
2022-05-03 02:04:49,260 INFO sasl.SaslDataTransferClient: SASL encryption trust check: localHostTrusted = false, remoteHostTrusted = false
2022-05-03 02:04:49,282 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1651542637195_0001
2022-05-03 02:04:49,283 INFO mapreduce.JobSubmitter: Executing with tokens: []
2022-05-03 02:04:49,496 INFO conf.Configuration: resource-types.xml not found
2022-05-03 02:04:49,497 INFO resource.ResourceUtils: Unable to find 'resource-types.xml'.
2022-05-03 02:04:49,890 INFO impl.YarnClientImpl: Submitted application application_1651542637195_0001
2022-05-03 02:04:50,016 INFO mapreduce.Job: The url to track the job: http://resourcemanager:8088/proxy/application_1651542637195_0001/
2022-05-03 02:04:50,018 INFO mapreduce.Job: Running job: job_1651542637195_0001
2022-05-03 02:05:27,911 INFO mapreduce.Job: Job job_1651542637195_0001 running in uber mode : false
2022-05-03 02:05:27,920 INFO mapreduce.Job:  map 0% reduce 0%
2022-05-03 02:06:25,552 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000001_0, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000003/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:25,608 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000000_0, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000002/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:35,227 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000001_1, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000004/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:36,319 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000000_1, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000005/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:42,660 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000001_2, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000007/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:43,692 INFO mapreduce.Job: Task Id : attempt_1651542637195_0001_m_000000_2, Status : FAILED
Error: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapTask.runOldMapper(MapTask.java:462)
	at org.apache.hadoop.mapred.MapTask.run(MapTask.java:349)
	at org.apache.hadoop.mapred.YarnChild$2.run(YarnChild.java:174)
	at java.security.AccessController.doPrivileged(Native Method)
	at javax.security.auth.Subject.doAs(Subject.java:422)
	at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1730)
	at org.apache.hadoop.mapred.YarnChild.main(YarnChild.java:168)
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 9 more
Caused by: java.lang.RuntimeException: Error in configuring object
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:113)
	at org.apache.hadoop.util.ReflectionUtils.setConf(ReflectionUtils.java:79)
	at org.apache.hadoop.util.ReflectionUtils.newInstance(ReflectionUtils.java:137)
	at org.apache.hadoop.mapred.MapRunner.configure(MapRunner.java:38)
	... 14 more
Caused by: java.lang.reflect.InvocationTargetException
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.apache.hadoop.util.ReflectionUtils.setJobConf(ReflectionUtils.java:110)
	... 17 more
Caused by: java.lang.RuntimeException: configuration exception
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:222)
	at org.apache.hadoop.streaming.PipeMapper.configure(PipeMapper.java:66)
	... 22 more
Caused by: java.io.IOException: Cannot run program "/tmp/hadoop-root/nm-local-dir/usercache/root/appcache/application_1651542637195_0001/container_e11_1651542637195_0001_01_000008/./final_mapper.py": error=2, No such file or directory
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1048)
	at org.apache.hadoop.streaming.PipeMapRed.configure(PipeMapRed.java:209)
	... 23 more
Caused by: java.io.IOException: error=2, No such file or directory
	at java.lang.UNIXProcess.forkAndExec(Native Method)
	at java.lang.UNIXProcess.<init>(UNIXProcess.java:247)
	at java.lang.ProcessImpl.start(ProcessImpl.java:134)
	at java.lang.ProcessBuilder.start(ProcessBuilder.java:1029)
	... 24 more

2022-05-03 02:06:48,758 INFO mapreduce.Job:  map 100% reduce 100%
2022-05-03 02:06:49,773 INFO mapreduce.Job: Job job_1651542637195_0001 failed with state FAILED due to: Task failed task_1651542637195_0001_m_000001
Job failed as tasks failed. failedMaps:1 failedReduces:0 killedMaps:0 killedReduces: 0

2022-05-03 02:06:49,956 INFO mapreduce.Job: Counters: 14
	Job Counters 
		Failed map tasks=7
		Killed map tasks=1
		Killed reduce tasks=1
		Launched map tasks=8
		Other local map tasks=6
		Rack-local map tasks=2
		Total time spent by all maps in occupied slots (ms)=499996
		Total time spent by all reduces in occupied slots (ms)=0
		Total time spent by all map tasks (ms)=124999
		Total vcore-milliseconds taken by all map tasks=124999
		Total megabyte-milliseconds taken by all map tasks=511995904
	Map-Reduce Framework
		CPU time spent (ms)=0
		Physical memory (bytes) snapshot=0
		Virtual memory (bytes) snapshot=0
2022-05-03 02:06:49,957 ERROR streaming.StreamJob: Job not successful!
Streaming Command Failed!
 


```
