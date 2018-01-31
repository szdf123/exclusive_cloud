## 场景六：消息中心

### 业务需求

消息推送主要用户提升用户体验，避免用户刷新页面从服务器端拉取数据。例如邮件提醒，重要通知能即时推送给用户，提高用户体验。

### 功能说明

iuap-message组件提供了向手机发送短信、发送电子邮件、向APP推送消息的功能。

1.提供了向手机发送短信
2.提供了发送电子邮件
3.电子邮件支持抄送、密送
4.电子邮件支持附件发送
5.提供了向APP推送消息的功能
6.可扩展的消息发送方式；

## 整体设计

### 依赖环境

组件采用Maven进行编译和打包发布，其对外提供的依赖方式如下：

1
<dependency>
2
  <groupId>com.yonyou.iuap</groupId>
3
  <artifactId>iuap-message</artifactId>
4
  <version>${iuap.modules.version}</version>
5
</dependency>

${iuap.modules.version} 为平台在maven私服上发布的组件的version。

### 功能说明

iuap-message组件提供了向手机发送短信、发送电子邮件、向APP推送消息的功能。

1.消息推送 

在公司现有的消息推送平台的基础上，利用此平台的REST服务，将业务数据包装成符合要求的格式，发送到平台上，完成APP的推送。（用户的移动端也需要安装平台提供的SDK）

2.发送短信 

发送短信的功能是基于公司的短信推送平台，通过此平台的提供的REST服务，按照平台的要求，将数据封装提交到平台，完成短信发送任务。目前支持国内的移动、联通和电信三大网络。

3.发送邮件 

电子邮件服务，是基于JavaMail实现的邮件发送服务，使用JDK原生的javax.mail组件来完成发送邮件的服务。

主要工作流程如下：

1.验证登录权限Authenticator

2.根据设置的Properties和Authenticator创建一个Session

3.创建一个MimeMessage实例，设置这个message的收信人、主题、内容等

4.发送邮件Transport.send(message);

## 使用说明

### 组件包说明

iuap-message组件提供了向手机发送短信、发送电子邮件、向APP推送消息的功能。

### 组件配置

将配置文件message-senderInfo.xml(可在上文示例工程拿到)放到工程的classpath下，如果是maven工程，放在src/main/resources目录下即可

### 工程样例

消息推送组件提供有示例工程iuap-message-example，用户可从maven库上下载，示例工程中有较为完整的对iuap-message组件的使用示例代码。

### 开发步骤

可直接参考以下示例工程：

1.添加配置文件：

将配置文件message-senderInfo.xml(可在上文示例工程拿到)放到工程的classpath下，如果是maven工程，放在src/main/resources目录下即可

2.调用消息服务的接口方法，发送消息:

1
// 创建消息接收者
2
MessageReceiver emailReceivers = new EmailReceiver("username1@domain.com,username2@domain.com");
3
 
4
// 创建消息内容
5
MessageContent emailContent = new EmailContent("我是标题1", "测试内容1");
6
 
7
// 发送消息
8
List<MessageResponse> responseList = new MessageSend(emailReceivers, emailContent).send(); 


### 常用接口

#### 描述 

短信、邮件和APP消息推送接口

#### 请求方法 

new MessageSend(msgReceivers, msgContent).send();

请求参数说明

<table>
   <tr>
      <td>参数字段</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>必选</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>类型</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>长度</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>说明</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>msgReceivers</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>MessageReceiver</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息的接收者，有多个的时候，按照英文”,”分割</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>msgContent</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>MessageContent</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息内容，包含消息标题，消息内容，发送时间。其中消息标题和发送时间非必填</td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>

1.msgReceivers消息接收者。可以是邮件地址，或者是电话号码，或者是APP ID。

2.msgContent消息内容，可以设置消息标题、文本内容。

####描述

短信、邮件和APP通过消息通道发送接口

####请求方法

new MessageSend(msgReceivers, msgContent, channel).send();

####请求参数说明

<table>
   <tr>
      <td>参数字段</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>必选</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>类型</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>长度</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>说明</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>msgReceivers</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>MessageReceiver</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息的接收者，有多个的时候，按照英文”,”分割</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>msgContent</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>MessageContent</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息内容，包含消息标题，消息内容，发送时间。其中消息标题和发送时间非必填</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>channel</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息通道编码</td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>


1.msgReceivers 消息接收者。可以是邮件地址，或者是电话号码，或者是APP ID。

2.msgContent 消息内容，可以设置消息标题、文本内容。

3.channel 消息通道编码，需要注册消息通道，具体参考消息通道相关文档。

支持消息通道的扩展，扩展步骤如下： 

(1)默认支持sms,messagepush,email，用户可扩展自己的消息通道，若要扩展消息通道，需在配置文件message-senderInfo.property中增加自己的消息通道,仿照下面的示例设置参数

<msconfig>
02
<!-- 短信服务参数配置  START-->
03
  <sms>
04
    <corpId></corpId><!-- 账户ID -->
05
    <secretKey></secretKey><!-- 接口调用秘钥 -->
06
    <url>http://umessage.yyuap.com/remote/sendSms.do</url><!-- 短信服务器URL -->
07
  </sms>
08
<!-- 短信服务参数配置  END-->
09
 
10
<!-- 消息推送参数配置  START-->
11
  <messagepush>
12
    <userName></userName><!-- 账户名(即控制台登录名) -->
13
    <userKey></userKey><!-- 远程接口秘钥 -->
14
    <url>http://upush.yyuap.com/remote/req.do</url><!-- 消息推送服务器URL -->
15
  </messagepush>
16
<!-- 消息推送参数配置  END-->
17
 
18
<!-- 邮件服务发送参数配置  START-->
19
  <mail>
20
    <userName></userName><!-- 账户名(发件人邮箱账户的账号) -->
21
    <password></password><!-- 密码(发件人邮箱账户的密码) -->
22
    <hostName>mail.yonyou.com</hostName><!-- 邮件发送服务器SMTP地址URL -->
23
    <port>25</port><!-- 邮件发送服务器SMTP端口号 -->
24
  </mail>
25
<!-- 邮件服务参数配置  END-->
26
 
27
</msconfig>


（2）完成消息通道的实现类，实现接口com.yonyou.uap.service.IMessageSendChannelExt，并配置到文件message-channelExt.xml中。

view sourceprint?
1
<MessageSendChannelExt>
2
    <mail>com.yonyou.uap.service.impl.mail.EMailSend</mail>
3
    <sms>com.yonyou.uap.service.impl.sms.SMSSend</sms>
4
    <messagepush>com.yonyou.uap.service.impl.messagepush.MessagePush</messagepush>
5
</MessageSendChannelExt>


(3)消息具体参数配置可以通过以下方式获取：

1
ISenderInfoFetch getEmailSenderInfo = new SenderInfoFetchByXML();
2
Map<String, Object> channelInfoMap = getEmailSenderInfo.getSenderInfo(“消息通道编码”);

(4)需要在引用组件的war包aplication.xmk中配置以下两个bean

1
<bean id="senderInfoFetch" class="com.yonyou.uap.message.service.impl.SenderInfoFetchByDB" />
2
<bean id="senderInfoFetcher" class="com.yonyou.uap.service.SenderInfoFetcher" />

###扩展机制

1.发送HTML内容的电子邮件： 

在设置邮件发送内容时，可以直接编写HTML代码，如下：

1
StringBuffer htmlContent = new StringBuffer();
2
htmlContent.append("<h1>我是标题</h1>");
3
htmlContent.append("<h3>企业互联网运营支撑平台</h3>");
4
htmlContent.append("<div><img src='http://img4.3lian.com/sucai/img6/230/29.jpg'></div>");
5
htmlContent.append("<a href='http://iuap.yonyou.com/'>用友开放平台</a>");
6
MessageContent mailContent = new EmailContent("HTML Mail测试", htmlContent.toString());

这样就可以发送HTML格式的邮件。

1.支持邮件抄送，密送，发送附件

MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFiles);

<table>
   <tr>
      <td>参数字段</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>必选</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>类型</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>长度</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>说明</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>title</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>邮件的标题</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>content </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息内容</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>copyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>抄送人（多个抄送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>blindCopyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>密送人（多个密送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>attachFiles </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String[]</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>附件的本地路径名 </td>
   </tr>
</table>

1
MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFileBytesMap)


<table>
   <tr>
      <td>参数字段</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>必选</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>类型</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>长度</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>说明</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>title</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>邮件的标题</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>content </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息内容</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>copyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>抄送人（多个抄送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>blindCopyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>密送人（多个密送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>attachFileBytesMap </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>Map </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>附件支持二进制发送,Map 表示<文件名,对应的文件二进制流> </td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>

1
MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFileUrls)


<table>
   <tr>
      <td>参数字段</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>必选</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>类型</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>长度</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>说明</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>title</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>邮件的标题</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>content </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>True</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>消息内容</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>copyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>抄送人（多个抄送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>blindCopyReceivers </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>String</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>密送人（多个密送人时，用半角英文逗号分隔）</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>attachFileUrls </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>false </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>List </td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>-</td>
   </tr>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>通过url地址的形势发送附件 </td>
   </tr>
   <tr>
      <td></td>
   </tr>
</table>
