## 配置向导

### 安装流程

1.安装 license server

见 iuap 开发平台 3.1_安装指南


2.安装 solr

3.安装 zookeeper

4.安装 redis

### 安装前的系统配置

设置机器名，不要用 localhost，不同的机器不要设置相同的机器名。
Linux 机器上将 ip 和机器名写到/etc/hosts 里。如果配置集群有多台机器，将所有机器的 ip 和机器名都写到
/etc/hosts 里，并保证时间一致。
关闭防火墙或开通所有需要用到的端口，如 tomcat 的 8080 或其他自定义端口。
使用 tomcat 或 weblogic 中间件时需要 oracle 的 jdk，从 oracle 官网下载安装 64 位的 jdk 1.7 或 1.8，并配置
为 JAVA_HOME 环境变量，

Linux 配置 JAVA_HOME

在/etc/profile 文件最后添加

```
export JAVA_HOME=/home/jdk1.7.0_51
ulimit -n 65535
echo 1 > /proc/sys/vm/overcommit_memory
echo 511 > /proc/sys/net/core/somaxconn
```

在/etc/sysctl.conf 文件最后添加

vm.overcommit_memory=1

然后执行

source /etc/profile

sysctl -p

Linux 上用 oraclejdk 还需要修改/home/jdk1.7.0_51/jre/lib/security/java.security

securerandom.source=file:/dev/./urandom

windows 配置 JAVA_HOME


### 文件配置

解压 portal.war、integration.war 和 uitemplate_web。

#### 配置数据库

修改 portal\WEB-INF\classes\application.properties

![](/articles/portal/3-/images/3-g-1.png)

原则是使用某种数据库时将其他数据库相关的内容注释掉，再修改相关配置，主要修改数据库 ip、端
口、数据库名、用户名和密码；

修改 integration\WEB-INF\classes\application.properties
![](/articles/portal/3-/images/3-g-2.png)

原则是使用某种数据库时将其他数据库相关的内容注释掉，再修改相关配置，主要修改数据库 ip、端口、
数据库名、用户名和密码；

#### 配置 redis 

修改 portal\WEB-INF\classes\application.properties，如

```
#业务缓存适用
redis.url=direct://20.12.6.191:6379?poolSize=50&poolName=mypool&password=ufsoft
#session 缓存使用
redis.session.url=direct://20.12.6.191:6379?poolSize=50&poolName=mypool&password=ufsoft
```

注意：此处配置的 redis 最好不要与其他系统共用。
修改 integration\WEB-INF\classes\application.properties，如

```
#业务缓存适用
redis.url=direct://20.12.6.191:6379?poolSize=50&poolName=mypool&password=ufsoft
#session 缓存使用
redis.session.url=direct://20.12.6.191:6379?poolSize=50&poolName=mypool&password=ufsoft
```

注意：此处配置的 redis 最好不要与其他系统共用。

#### 配置 zookeeper

修改 portal\WEB-INF\classes\application.properties
![](/articles/portal/3-/images/3-g-3.png)

#### 配置 licenseserver

修改 portal\WEB-INF\classes\licence.properties 例如如下
![](/articles/portal/3-/images/3-g-4.png)

#### 配置日志路径

修改 portal\WEB-INF\classes\logback.xml 和 integration\WEB-INF\classes\logback.xml

```
<appender name="rollingFile" class="ch.qos.logback.core.rolling.RollingFileAppender">
 <file>/tmp/logs/iportal.log</file>
 <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">
 <fileNamePattern>/tmp/logs/iportal.%d{yyyy-MM-dd}.log</fileNamePattern>
 </rollingPolicy>
 <encoder>
 <pattern>%date{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
 </encoder>
</appender>
```

默认日志是/tmp/logs/iportal.log，可根据情况修改

#### 配置 uitemplate_web

配置 WEB-INF\conf\uitemplate\datasource.properties 文件

a.配置数据库
![](/articles/portal/3-/images/3-g-5.png)

主要修改数据库 ip、端口、数据库名、用户名和密码；

b.配置 redis

![](/articles/portal/3-/images/3-g-6.png)

配置 WEB-INF\conf\uitemplate\ uitemplate.properties 文件

参照服务地址配置，环境启动的 ip 和 port

![](/articles/portal/3-/images/3-g-7.png)

备注：uitemplate_web 支持 mysql 数据库，不支持 ora11g

