# 如何快速的开发应用

## 创建基础Maven工程

**1：创建基础的Maven结构的spring依赖的Web工程**

**2：具体请参考实例提供的test-server工程**


## 配置修改

### maven依赖(pom文件)
1. 增加mwclient的依赖

```
<dependency>
	<groupId>com.yonyou.cloud.middleware</groupId>
	<artifactId>middleware</artifactId>
	<version>3.0.1-SNAPSHOT</version>
</dependency>
```

 2.artifactId(影响访问路径)，finalname要与应用编码保持一致

### 属性文件配置

**application.properties**

1. access.key和access.secret与申请的Access Key中内容保持一致
2. spring.profiles.active为应用的环境(开发：dev，测试：test，灰度：stage，生产：online)
3. spring.application.name为应用的编码


## 接口开发
用例中的test-server为服务提供方，可以定义接口，并实现（接口可以抽取到服务提供方和调用方共同依赖的工程中，详细步骤可以参考demo工程pt-pubapi依赖相关文档），接口的定义和实现可以参考示例工程中pt-pubapi的IMsMiddleService和pt-server的MsMiddleService

**1：IMsMiddleService**

```
@RemoteCall("ms-middle@c87e2267-1001-4c70-bb2a-ab41f3b81aa3")
public interface IMsMiddleService {
    @ApiOperation(value = "获取随机数字", response = String.class)
    public String getDigit();
}

```

**2：MsMiddleService**

```
@Service
public class MsMiddleService implements IMsMiddleService{
    @Override
    public String getDigit() {
        return UUID.randomUUID().toString();
    }
}
```
**自动化创建**
后端开发人员可以通过更改@RemoteCall中的appcode来自动创建应用，无需界面操作


