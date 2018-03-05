## 场景六：消息中心

### API接口

#### 描述 

短信、邮件和APP消息推送接口

#### 请求方法 

new MessageSend(msgReceivers, msgContent).send();

请求参数说明
<table> 
   <tbody>
    <tr> 
     <th><br> 参数字段<br> </th> 
     <th><br> 必选<br> </th> 
     <th><br> 类型<br> </th> 
     <th><br> 长度<br> </th> 
     <th><br> 说明<br> </th> 
    </tr> 
    <tr> 
     <td><br> msgReceivers<br> </td> 
     <td><br> True<br> </td> 
     <td><br> MessageReceiver<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息的接收者，有多个的时候，按照英文”,”分割<br> </td> 
    </tr> 
    <tr> 
     <td><br> msgContent<br> </td> 
     <td><br> True<br> </td> 
     <td><br> MessageContent<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息内容，包含消息标题，消息内容，发送时间。其中消息标题和发送时间非必填<br> </td> 
    </tr> 
   </tbody>
  </table>

1.msgReceivers消息接收者。可以是邮件地址，或者是电话号码，或者是APP ID。

2.msgContent消息内容，可以设置消息标题、文本内容。

#### 描述

短信、邮件和APP通过消息通道发送接口

#### 请求方法

new MessageSend(msgReceivers, msgContent, channel).send();

#### 请求参数说明

<table> 
   <tbody>
    <tr> 
     <th><br> 参数字段<br> </th> 
     <th><br> 必选<br> </th> 
     <th><br> 类型<br> </th> 
     <th><br> 长度<br> </th> 
     <th><br> 说明<br> </th> 
    </tr> 
    <tr> 
     <td><br> msgReceivers<br> </td> 
     <td><br> True<br> </td> 
     <td><br> MessageReceiver<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息的接收者，有多个的时候，按照英文”,”分割<br> </td> 
    </tr> 
    <tr> 
     <td><br> msgContent<br> </td> 
     <td><br> True<br> </td> 
     <td><br> MessageContent<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息内容，包含消息标题，消息内容，发送时间。其中消息标题和发送时间非必填<br> </td> 
    </tr> 
    <tr> 
     <td><br> channel<br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息通道编码<br> </td> 
    </tr> 
   </tbody>
  </table>


1.msgReceivers 消息接收者。可以是邮件地址，或者是电话号码，或者是APP ID。

2.msgContent 消息内容，可以设置消息标题、文本内容。

3.channel 消息通道编码，需要注册消息通道，具体参考消息通道相关文档。

支持消息通道的扩展，扩展步骤如下： 

(1)默认支持sms,messagepush,email，用户可扩展自己的消息通道，若要扩展消息通道，需在配置文件message-senderInfo.property中增加自己的消息通道,仿照下面的示例设置参数

<div class="lines"><div class="line alt1"><table><tbody><tr><td class="number"><code>01</code></td><td class="content"><code class="plain">&lt;msconfig&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>02</code></td><td class="content"><code class="plain">&lt;!-- 短信服务参数配置&nbsp; START--&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>03</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;sms&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>04</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;corpId&gt;&lt;/corpId&gt;&lt;!-- 账户ID --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>05</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;secretKey&gt;&lt;/secretKey&gt;&lt;!-- 接口调用秘钥 --&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>06</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;url&gt;http:</code><code class="comments">//umessage.yyuap.com/remote/sendSms.do&lt;/url&gt;&lt;!-- 短信服务器URL --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>07</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;/sms&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>08</code></td><td class="content"><code class="plain">&lt;!-- 短信服务参数配置&nbsp; END--&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>09</code></td><td class="content">&nbsp;</td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>10</code></td><td class="content"><code class="plain">&lt;!-- 消息推送参数配置&nbsp; START--&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>11</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;messagepush&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>12</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;userName&gt;&lt;/userName&gt;&lt;!-- 账户名(即控制台登录名) --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>13</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;userKey&gt;&lt;/userKey&gt;&lt;!-- 远程接口秘钥 --&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>14</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;url&gt;http:</code><code class="comments">//upush.yyuap.com/remote/req.do&lt;/url&gt;&lt;!-- 消息推送服务器URL --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>15</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;/messagepush&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>16</code></td><td class="content"><code class="plain">&lt;!-- 消息推送参数配置&nbsp; END--&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>17</code></td><td class="content">&nbsp;</td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>18</code></td><td class="content"><code class="plain">&lt;!-- 邮件服务发送参数配置&nbsp; START--&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>19</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;mail&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>20</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;userName&gt;&lt;/userName&gt;&lt;!-- 账户名(发件人邮箱账户的账号) --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>21</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;password&gt;&lt;/password&gt;&lt;!-- 密码(发件人邮箱账户的密码) --&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>22</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;hostName&gt;mail.yonyou.com&lt;/hostName&gt;&lt;!-- 邮件发送服务器SMTP地址URL --&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>23</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;&nbsp;&nbsp;</code><code class="plain">&lt;port&gt;</code><code class="value">25</code><code class="plain">&lt;/port&gt;&lt;!-- 邮件发送服务器SMTP端口号 --&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>24</code></td><td class="content"><code class="spaces">&nbsp;&nbsp;</code><code class="plain">&lt;/mail&gt;</code></td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>25</code></td><td class="content"><code class="plain">&lt;!-- 邮件服务参数配置&nbsp; END--&gt;</code></td></tr></tbody></table></div><div class="line alt2"><table><tbody><tr><td class="number"><code>26</code></td><td class="content">&nbsp;</td></tr></tbody></table></div><div class="line alt1"><table><tbody><tr><td class="number"><code>27</code></td><td class="content"><code class="plain">&lt;/msconfig&gt;</code></td></tr></tbody></table></div></div>

（2）完成消息通道的实现类，实现接口com.yonyou.uap.service.IMessageSendChannelExt，并配置到文件message-channelExt.xml中。

```
<MessageSendChannelExt>
    <mail>com.yonyou.uap.service.impl.mail.EMailSend</mail>
    <sms>com.yonyou.uap.service.impl.sms.SMSSend</sms>
    <messagepush>com.yonyou.uap.service.impl.messagepush.MessagePush</messagepush>
</MessageSendChannelExt>
```

(3)消息具体参数配置可以通过以下方式获取：

```
ISenderInfoFetch getEmailSenderInfo = new SenderInfoFetchByXML();
Map<String, Object> channelInfoMap = getEmailSenderInfo.getSenderInfo(“消息通道编码”);
```

(4)需要在引用组件的war包aplication.xmk中配置以下两个bean

```
<bean id="senderInfoFetch" class="com.yonyou.uap.message.service.impl.SenderInfoFetchByDB" />
<bean id="senderInfoFetcher" class="com.yonyou.uap.service.SenderInfoFetcher" />
```

### 扩展机制

1.发送HTML内容的电子邮件： 

在设置邮件发送内容时，可以直接编写HTML代码，如下：

```
StringBuffer htmlContent = new StringBuffer();
htmlContent.append("<h1>我是标题</h1>");
htmlContent.append("<h3>企业互联网运营支撑平台</h3>");
htmlContent.append("<div><img src='http://img4.3lian.com/sucai/img6/230/29.jpg'></div>");
htmlContent.append("<a href='http://iuap.yonyou.com/'>用友开放平台</a>");
MessageContent mailContent = new EmailContent("HTML Mail测试", htmlContent.toString());
```

这样就可以发送HTML格式的邮件。

1.支持邮件抄送，密送，发送附件

MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFiles);

<table> 
   <tbody>
    <tr> 
     <th><br> 参数字段<br> </th> 
     <th><br> 必选<br> </th> 
     <th><br> 类型<br> </th> 
     <th><br> 长度<br> </th> 
     <th><br> 说明<br> </th> 
    </tr> 
    <tr> 
     <td><br> title<br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 邮件的标题<br> </td> 
    </tr> 
    <tr> 
     <td><br> content <br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息内容<br> </td> 
    </tr> 
    <tr> 
     <td><br> copyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 抄送人（多个抄送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> blindCopyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 密送人（多个密送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> attachFiles <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String[]<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 附件的本地路径名 <br> </td> 
    </tr> 
   </tbody>
  </table>
<pre>1 MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFileBytesMap)</pre>


<table> 
   <tbody>
    <tr> 
     <th><br> 参数字段<br> </th> 
     <th><br> 必选<br> </th> 
     <th><br> 类型<br> </th> 
     <th><br> 长度<br> </th> 
     <th><br> 说明<br> </th> 
    </tr> 
    <tr> 
     <td><br> title<br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 邮件的标题<br> </td> 
    </tr> 
    <tr> 
     <td><br> content <br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息内容<br> </td> 
    </tr> 
    <tr> 
     <td><br> copyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 抄送人（多个抄送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> blindCopyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 密送人（多个密送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> attachFileBytesMap <br> </td> 
     <td><br> false<br> </td> 
     <td><br> Map
      <string, object="">
       <br> 
      </string,></td> 
     <td><br> -<br> </td> 
     <td><br> 附件支持二进制发送,Map
      <string,byte[]>
       表示&lt;文件名,对应的文件二进制流&gt; 
       <br> 
      </string,byte[]></td> 
    </tr> 
   </tbody>
  </table>

<pre>1 MessageContent mailContent = new EmailContent(title, content, copyReceivers, blindCopyReceivers, attachFileUrls)</pre>


<table> 
   <tbody>
    <tr> 
     <th><br> 参数字段<br> </th> 
     <th><br> 必选<br> </th> 
     <th><br> 类型<br> </th> 
     <th><br> 长度<br> </th> 
     <th><br> 说明<br> </th> 
    </tr> 
    <tr> 
     <td><br> title<br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 邮件的标题<br> </td> 
    </tr> 
    <tr> 
     <td><br> content <br> </td> 
     <td><br> True<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 消息内容<br> </td> 
    </tr> 
    <tr> 
     <td><br> copyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 抄送人（多个抄送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> blindCopyReceivers <br> </td> 
     <td><br> false<br> </td> 
     <td><br> String<br> </td> 
     <td><br> -<br> </td> 
     <td><br> 密送人（多个密送人时，用半角英文逗号分隔）<br> </td> 
    </tr> 
    <tr> 
     <td><br> attachFileUrls <br> </td> 
     <td><br> false <br> </td> 
     <td><br> List
      <string> 
       <br> 
      </string></td> 
     <td><br> -<br> </td> 
     <td><br> 通过url地址的形势发送附件 <br> </td> 
    </tr> 
   </tbody>
  </table>
