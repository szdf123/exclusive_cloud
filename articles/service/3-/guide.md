# 配置向导
专属云配置都存在安装盘/script/env/envset.txt文件下，以下为配置项含义的介绍

- 必须修改的配置项

		#下面几个ip不能填localhost,因为portal的配置会将这ip交个浏览器直接调用
		
		##zookeeper中间件，安装盘自带请修改localhost为部署机地址（下同）
		zookeeper_url=localhost:2181
		##友互通服务url端口号为tomcat服务端口号
		yht_url=http://localhost:8080
		##portal登录成功跳转页面
		portal_loginUrl=http://localhost:8080/portal/sso/login.jsp
		##sdk服务url
		sdk_servername=http://localhost:8080
		##跳转服务ip
		sdk_ip=localhost
		##跳转服务端口
		sdk_port=8080
		#kafka地址
		kafka_ip=localhost:9092		
		
		#结束
		

- 部署机相关配置：
		
		#不需要改动，但是可以改为部署机iP
		##部署机tomcat服务地址
		tomcat_url=http://localhost:8080
		##部署tomcat服务地址（无访问协议）
		tomcat_ip=localhost:8080
		##微服务控制台服务端口，请设置为tomat服务端口
		msconsole_server_port=8080
		##数据权限服务端口（请设置为tomat服务端口）
		data_authority_server_port=8080
		##eureka服务url
		eureka_url=http://localhost:8080/registry

- elasticsearch配置:

		##es服务ip 
		es_ip=127.0.0.1
		##es服务集群名称 
		es_cluster=elasticsearch-private
		##es服务用户名
		es_username=mwadmin
		##es服务密码
		es_password=mwadmin*20170728
		##es服务管理员用户名
		es_admin_username=esadmin
		##es服务管理员密码
		es_admin_password=esadmin
		##es服务severmeta工程相关索引名称
		severmeta_index=yycloud-basedoc-mw-servmeta-private
		##es服务severmeta工程相关索引下属type名称
		severmeta_type=meta
		##es服务zipking相关索引名称
		zipkin_index=zipkin
		##es服务ip带端口
		es_ip_port=127.0.0.1:9300
		##es服务友互通工程相关索引名称
		es_tenantuser_index=yycloud-basedoc-marketuser
		##es服务友互通工程相关索引名称
		es_appuser_index=yycloud-basedoc-yhtapp
		##es服务友互通索引type
		es_tenantuser_type=user
		##es服务友互通索引type
		es_appuser_type=user
		
- 数据库地址密码
		
		#数据库地址密码
		jdbc_ip=localhost:3306
		jdbc_username=root
		jdbc_password=Ufsoft*123
		
		cas_jdbc_ip=localhost:3306
		cas_jdbc_username=gYO2C6VZvGaqExuL0COILw==
		cas_jdbc_password=9jHwKjvp5nCSPGLKn9mw+w==
		
		tenantauth_jdbc_ip=localhost:3306
		tenantauth_jdbc_username=6eLJVbeWA/E=
		tenantauth_jdbc_password=UpQrX6rH9uYdDW1DqX5JpQ==


- redis缓存		
		
		#redis
		redis_ip=localhost:6379
		redis_ip_noport=localhost
		redis_password=Ufsoft123

- 邮件发送配置

		mail_ip=192.168.210.160
		mail_password=wLjBXUhNUg40g+RaUyTYrQ==
		mail_sender=iuap_admin@yonyou.com
		mail_subject=yht
		mail_username=iuap_admin
		mail_smtpport=25

- 平台用户校验配置
		
		#平台用户校验配置
		access_key=50iZDhyAoXtfguLR
		access_secret=g2MWT3PVMEOiuCo9F6IWjJzEiNEw60
		conf_providerid=c87e2267-1001-4c70-bb2a-ab41f3b81aa3
		apiLink_provider=35568e76-1ef1-4d77-b5cf-8fb66d2c8002
		protal_key=9TaCKkCH8AYBv1Ki
		protal_secret=gbpbeQcXzwGbYYMAZbfmhpOK8HZ5lF
		servmeta_key=hgWiiAtTSiR6A8w0
		servmeta_secret=qK3UQzaG1Aw57n6zPpiQC8xZIC2oA2

- auth校验文件存储地址
		
		authfile_path=/etc/config/microservice/authfile.properties
