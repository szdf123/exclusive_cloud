# API接口文档规范




## 接口名称

```
传递RPC上下文参数
```

## 接口说明

```
服务消费者向服务提供者发起RPC调用时, 除了可以向服务提供者传递业务参数外, 还可以向服务提供端传递上下文参数; 
如设置当前用户, 当前链路ID, 大事务ID等. 
```
```
注意: 服务消费者在RPC调用时, 因tomcat等web容器的线程是在线程池内的, 业务设置上下文参数在RPC调用前设置, 在调用后框架不会清理, 业务方要选择合适的时机进行清理, 如在调用后清理或线程使用完毕后清理(request范围), 以避免上下文参数被带入别的线程中. 服务提供者不用清理上下文参数, RPC框架会自动清理.
```

## 接口使用说明

* maven引入:
<pre>
&lt;groupId&gt;com.yonyou.iuap&lt;/groupId&gt;
&lt;artifactId&gt;iuap-generic&lt;/artifactId&gt;
&lt;version&gt;3.2.1-SNAPSHOT&lt;/version&gt;

&lt;groupId&gt;com.yonyou.cloud.middleware&lt;/groupId&gt;
&lt;artifactId&gt;iris-iuap-support&lt;/artifactId&gt;
&lt;version&gt;3.0.1-SNAPSHOT&lt;/version&gt;
</pre>

* **上下文参数API使用:**

	1. 服务消费者设置上下文参数
		<pre>com.yonyou.iuap.context.InvocationInfoProxy.setParameter("上下文参数键", "上下文参数值");</pre>
	1. 服务消费者清理上下文参数
		<pre>com.yonyou.iuap.context.InvocationInfoProxy.reset();</pre>
	3. 服务提供者获取上下文参数
		<pre>com.yonyou.iuap.context.InvocationInfoProxy.getParameter("上下文参数键");</pre>



## 接口名称

```
设置RPC序列化协议
```

## 接口说明

```
服务消费者向服务提供者发起RPC调用时, 默认使用hessian序列化协议; 可以在发起调用前动态设置传输协议,可选json/hessian两种协议. 生效周期为request范围, request结束后会自动清理自定义设置.
```

## 接口使用说明

* **设置上下文参数API使用:**

	1. 设置为hessian传输协议:
		<pre>com.yonyou.cloud.middleware.iris.RPCInvocationInfoProxy.setProto(com.yonyou.cloud.middleware.rpc.transport.CodecAdapterFactory.APPLICATION_OCTET_STREAM_VALUE)</pre>

	2. 设置为json传输协议:
		<pre>com.yonyou.cloud.middleware.iris.RPCInvocationInfoProxy.setProto(com.yonyou.cloud.middleware.rpc.transport.CodecAdapterFactory.APPLICATION_JSON_UTF8_VALUE)</pre>


## 接口名称

```
设置调用Zone
```

## 接口说明

```
服务消费者向服务提供者发起RPC调用时, 默认不使用zone过滤服务提供者; 可以在发起调用前动态设置调用zone, 选择在属于特定zone的服务提供者, 如果指定的zone内没有对应的服务提供者, 才会调用到没有zone的对应服务提供者. 生效周期为request范围, request结束后会自动清理自定义设置.
```

## 接口使用说明

* **筛选服务提供者API使用:**

	1. 设置筛选服务提供者的zone:
		<pre>com.yonyou.cloud.middleware.iris.RPCInvocationInfoProxy.setInstanceZone(String)</pre>


## 接口名称

```
获取当前环境参数:AppRuntimeEnvironment
```

## 接口说明

```
无论是服务提供者还是服务消费者, 在应用启动后会有一些环境参数, 如SevletContext,AppCode,ProviderId,Context,Profile, Port,Zone; 可以通过调用静态方法的方式获取环境参数.
```

## 接口使用说明

* **当前环境参数API使用:**

	1. 获取Servlet上下文:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getServlet_context()</pre>

	2. 获取应用Code:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getAppCode()</pre>
	
	3. 获取租户ID:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getProviderId()</pre>
	
	4. 获取应用上下文路径:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getContext()</pre>

	5. 获取部署环境(dev:开发,test:测试,stage:灰度,online:线上):
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getProfile()</pre>
	
	6. 获取应用端口:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getPort()</pre>
	
	7. 获取是否启用SSL:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.isSslEnabled()</pre>

	8. 获取当前服务的zone:
		<pre>com.yonyou.cloud.middleware.AppRuntimeEnvironment.getZone()</pre>


