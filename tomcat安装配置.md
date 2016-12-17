### 下载tomcat
	wget http://mirrors.hust.edu.cn/apache/tomcat/tomcat-8/v8.5.6/bin/apache-tomcat-8.5.6.tar.gz
### 解压tomcat
	tar -zxvf apache-tomcat-8.5.6.tar.gz

### 删除webapps下的所有文件
	rm -rf *

### 将dubbo-admin.war文件解压到webapps下并修改/webapps/dubbo-admin/WEB-INF下的dubbo.properties
	dubbo.registry.address=zookeeper://192.168.187.128:2181
	dubbo.admin.root.password=zhiwen@123
	dubbo.admin.guest.password=zhiwen@123

### 启动tomcat
	zhiwen@ubuntu:~/duboo-admin-tomcat$ ./bin/startup.sh

### 监控日志
	tail -f /home/zhiwen/duboo-admin-tomcat/logs/catalina.out
