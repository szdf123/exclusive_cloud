# 环境配置要求

##中间件版本依赖

- elasticsearch：2.4.2
- kafka：2.12-1.0.0
- redis：2.8.3
- jdk：1.8
- 数据库:mysql5.7以上
- os:CentOS7以上

##端口占用

	es:9200 9300
	mysql: 3306
	kafka:9092
	redis:6379
	tomcat:8080
	eureka:8076
	zookeeper:2181
	请保持端口通畅


#安全配置

为了提高安全性，用户可以使用iptables对一些端口的访问进行限制，以下配置统一修改/etc/sysconfig/iptables-config文件，修改完成后执行systemctl restart iptables

##elasticsearch限制
elasticsearch使用9200 9300端口我们对这两个端口进行限制,然后对192.168.1.0/24网段开放访问
	
	 iptables -I INPUT -p tcp --dport 9200 -j DROP 
	 iptables -I INPUT -s 192.168.1.0/24 -p tcp --dport 9200 -j ACCEPT
	
	 iptables -I INPUT -p tcp --dport 9300 -j DROP 
	 iptables -I INPUT -s 192.168.1.0/24 -p tcp --dport 9300 -j ACCEPT

##kafka限制
	kafka使用9092端口但是需要注意的是，微服务客户端需要对kafka进行访问，因此对kafka进行限制要谨慎，保证部署中间件和客户机都能够连接

##redis
	redis使用6379端口，我们可以仿照elasticsearch的限制方式进行安全配置

	 iptables -I INPUT -p tcp --dport 6379 -j DROP 
	 iptables -I INPUT -s 192.168.1.0/24 -p tcp --dport 6379 -j ACCEPT

##tomcat
	tomcat的8080端口对外提供服务，该端口不要进行限制

##eureka
	eureka类似kafka，谨慎限制。使用8076和8080

##zookeeper	
	zookeeper使用2181，谨慎限制

