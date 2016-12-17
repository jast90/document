### tar zookeeper-3.4.9.tar.gz
    tar -xf zookeeper-3.4.9.tar.gz 
### 创建data和log目录
    zhiwen@ubuntu:~/zookeeper-3.4.9$ mkdir data
    zhiwen@ubuntu:~/zookeeper-3.4.9$ mkdir log

### 添加编辑zoo.cfg
	zhiwen@ubuntu:~/zookeeper-3.4.9/conf$ cp zoo_sample.cfg  zoo.cfg

	zhiwen@ubuntu:~/zookeeper-3.4.9$ vim conf/zoo.cfg 
	添加或修改如下内容：
	dataDir=/home/zhiwen/zookeeper-3.4.9/data
	dataLogDir=/home/zhiwen/zookeeper-3.4.9/log
	server.1=ubuntu:2888:3888

### 在data目录下创建myid
	zhiwen@ubuntu:~/zookeeper-3.4.9$ cd data/
	zhiwen@ubuntu:~/zookeeper-3.4.9/data$ vim myid
	输入如下内容：
	1

### zhiwen用户下修改vim /home/zhiwen/.bash_profile 增加zookeeper配置
	#keeper env
	export ZOOKEEPER_HOME=/home/zhiwen/zookeeper-3.4.9
	export PATH=$ZOOKEEPER_HOME/bin:$PATH

	生效.bash_profile
	zhiwen@ubuntu:~/zookeeper-3.4.9/bin$ source /home/zhiwen/.bash_profile


### 启动并测试zookeeper
启动zookeeper
	zhiwen@ubuntu:~/zookeeper-3.4.9/bin$ ./zkServer.sh start
查看进程
	zhiwen@ubuntu:~$ jps
	4601 Jps
	4476 QuorumPeerMain

	zhiwen@ubuntu:~/zookeeper-3.4.9/bin$ ps -ef | grep java
	tomcat     1237      1  0 21:50 ?        00:00:03 /usr/lib/jvm/java-8-oracle/bin/java -Djava.util.logging.config.file=/home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djdk.tls.ephemeralDHKeySize=2048 -classpath /home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5/bin/bootstrap.jar:/home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5/bin/tomcat-juli.jar -Dcatalina.base=/home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5 -Dcatalina.home=/home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5 -Djava.io.tmpdir=/home/zhiwen/Desktop/tomcat8/apache-tomcat-8.5.5/temp org.apache.catalina.startup.Bootstrap start
	zhiwen     1490      1  0 21:50 ?        00:00:01 /usr/lib/jvm/java-8-oracle/bin/java -Dzookeeper.log.dir=. -Dzookeeper.root.logger=INFO,CONSOLE -cp /home/zhiwen/zookeeper-3.4.9/bin/../build/classes:/home/zhiwen/zookeeper-3.4.9/bin/../build/lib/*.jar:/home/zhiwen/zookeeper-3.4.9/bin/../lib/slf4j-log4j12-1.6.1.jar:/home/zhiwen/zookeeper-3.4.9/bin/../lib/slf4j-api-1.6.1.jar:/home/zhiwen/zookeeper-3.4.9/bin/../lib/netty-3.10.5.Final.jar:/home/zhiwen/zookeeper-3.4.9/bin/../lib/log4j-1.2.16.jar:/home/zhiwen/zookeeper-3.4.9/bin/../lib/jline-0.9.94.jar:/home/zhiwen/zookeeper-3.4.9/bin/../zookeeper-3.4.9.jar:/home/zhiwen/zookeeper-3.4.9/bin/../src/java/lib/*.jar:/home/zhiwen/zookeeper-3.4.9/bin/../conf: -Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.local.only=false org.apache.zookeeper.server.quorum.QuorumPeerMain /home/zhiwen/zookeeper-3.4.9/bin/../conf/zoo.cfg


### 查看日志
	zhiwen@ubuntu:~$ tail /home/zhiwen/zookeeper-3.4.9/bin/zookeeper.out 

### 配置zookeeper开机使用zhiwen用户启动
	编辑/etc/rc.local 文件，加入：
	su - zhiwen -c '/home/zhiwen/zookeeper-3.4.9/bin/zkServer.sh start'
