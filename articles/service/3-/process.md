# 配置流程

##中间件版本依赖

- elasticsearch：2.4.2
- kafka：2.12-1.0.0
- redis：2.8.3
- jdk：1.8
- 数据库:mysql5.7以上
- os:CentOS7以上

端口占用

	es:9200 9300
	mysql: 3306
	kafka:9092
	redis:6379
	tomcat:8080
	eureka:8076
	zookeeper:2181
	请保持端口通畅


## 启动准备

###申请授权
请参见文档 \doc\授权文档\授权文档.md

###准备mysql数据库

	script\sql

启动微服务治理平台之前需要安装mysql数据库并且导入位于上方路径的sql脚本.


### 修改配置变量

- 直接配置

- /script/env/envset.txt配置文件有一些配置变量需要修改

		#必改项
		#下面几个ip不能填localhost,因为portal的配置会将这ip交个浏览器直接调用
		yht_url=http://localhost:8080
		portal_loginUrl=http://localhost:8080/portal/sso/login.jsp
		sdk_servername=http://localhost:8080
		sdk_ip=localhost
		sdk_port=8080
		#结束
		这些配置项的localhost请改成您的本机ip
		
		根据您搭建的mysql数据库信息，将该配置文件内数据库相关配置替换成您的mysql数据库配置

- 为了增加安全性，可以参见/done/doc/安全配置 的安全配置文档

- 图形化配置(与直接配置二选一)
	
	双击exclusive_cloud_installer.jar启用图形化配置器

![](image/fig1.jpg)
	依次填入相关配置后点击保存配置



## 启动微服务治理平台

- 一键启动
	
		linux
		先赋予脚本可执行权限  chmod 755 ./startup.sh  ./shutdown.sh
		运行startup.sh脚本
</br>

		windows
		运行startup.bat脚本

- 分步启动
	
		linux
		执行/script/bin/linux内的脚本顺序如下
		init_conf.sh
		zookeeper_start.sh
		kafka_start.sh
		redis_start.sh
		elasticsearch_start.sh
		zipkin-client_start.sh
		esImportTimer_start.sh
		tomcat_start.sh
</br>

		windows
		执行\script\bin\win内的脚本顺序如下
		init_conf.bat
		zookeeper_start.bat
		kafka_start.bat
		redis_start.bat
		elasticsearch_start.bat
		zipkin-client_start.bat
		esImportTimer_start.bat
		tomcat_start.bat
## 访问

这里部署机ip为172.20.28.31，请您根据您自己的部署机ip替换

部署成功以后可以通过以下三个页面进行验证：

门户页面 portal_url ： http://172.20.28.31:8080/portal

注册中心 eureka ： http://172.20.28.31:8080/registry/

搜索引擎 elasticsearch ：http://172.20.28.31:9200/_plugin/head/


测试主账号

		admin  yonyou@2018   c87e2267-1001-4c70-bb2a-ab41f3b81aa3    AZlWmAET34W3uwxA    Qr3L3gsig1bO8kud3pRyI8PNTO6Zkl	

		user 111111     Vxj4S5h1spZo2gnn / QLfLD4QQM3sPwN9mi7kUaYQxLvkEbd

##微服务开发测试用例

测试用例位于：./demo文件夹
测试用例使用文档位于./doc/测试文档
