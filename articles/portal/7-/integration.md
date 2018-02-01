
## API文档:集成第三方系统

### API接口

### 企业门户集成第三方系统

#### 描述

企业门户集成第三方系统，包括保存，删除，更新，查询集成第三方系统具体信息和请求参数等

#### 请求方法

integration/system/save

#### 请求方式

post

#### 请求参数说明



参数字段   必选   类型    长度限制   说明  

name   true   String    100   系统名称
 
i18n   false  String    50   -
  
code   true   String    50   系统编码

setting   true   Json   -   第三方系统设置信息，具体见下表

tag   true   String   50   版本戳


<table>

   <tr>
      <td>参数字段   </td>
      <td>必选   </td>
      <td>类型    </td>
      <td>长度限制  </td>
      <td>说明  </td>
   </tr>

   <tr>
      <td>name   </td>
      <td>true  </td>
      <td>String   </td>
      <td>100   </td>
      <td>系统名称</td>
   </tr>

   <tr>
      <td>i18n  </td>
      <td>false  </td>
      <td>String </td>
      <td>50  </td>
      <td>-</td>
   </tr>
 
   <tr>
      <td>code  </td>
      <td>true  </td>
      <td>String  </td>
	  <td>  50   </td>
      <td>系统编码</td>
   </tr>

   <tr>
      <td>setting </td>  
       <td>true   </td>
       <td>Json </td>
       <td>-    </td>
      <td> 第三方系统设置信息，具体见下表</td>
   </tr>
  
   <tr>
      <td>tag  </td>
       <td>true </td>
       <td>String </td>
       <td>50   </td>
      <td> 版本戳</td>
   </tr>
</table>





setting内容格式

参数字段   必选   类型    长度限制   说明  

code    true   String     50     系统编码

name   true   String  100  系统名称

gateway  false   String  -   网关

underController   boolean  -  需要授权

userAssociate   false  boolean   -   用户自行管理

supportfw   false    -          -   支持轻量化

model   true    String  50   是否信任模式

secretkey  true   String  50  密钥

verify  true   Json  -  见下表    

ipmapping  true  Json  -   见下表   

extendAttributes  false   Json -  扩展选项

tag   false   String   50    标签

<table>
   <tr>
      <td>参数字段 </td>
      <td>必选  </td>
      <td>类型   </td>
      <td>长度限制 </td>  
      <td>说明  </td>
   </tr>
  
   <tr>
      <td>code   </td>
     <td> true  </td>
      <td>String  </td>
      <td>50    </td>
      <td>系统编码</td>
   </tr>
  
   <tr>
      <td>name  </td>
        <td>true  </td>
        <td>String  </td>
        <td>100  </td>
       <td> 系统名称</td>
   </tr>

   <tr>
      <td>gateway </td>
        <td>false  </td>
        <td>String  </td>
        <td>-   </td>
        <td>网关</td>
   </tr>

   <tr>
      <td>underController   </td>
      <td> boolean</td>
      <td> -  </td>
      <td> 需要授权</td>
   </tr>
 
   <tr>
      <td>userAssociate </td>
      <td> false </td>
      <td> boolean</td>
      <td> -   用户自行管理</td>
   </tr>
   
   <tr>
      <td>supportfw </td>
      <td>false  </td>
      <td> -       </td>
     <td>  -   </td>
	<td>     支持轻量化</td>
   </tr>
 
   <tr>
      <td>model<td>   
      <td>true <td>
      <td>String <td>
      <td>50   <td>
     <td> 是否信任模式</td>
   </tr>
 
   <tr>
      <td>secretkey <td>
     <td> true  <td>
      <td>String  <td>
      <td>50  <td>
      <td>密钥</td>
   </tr>

   <tr>
      <td>verify  <td>
      <td>true<td>
      <td>Json  <td>
      <td>-  <td>
      <td>见下表    </td>
   </tr>
  
   <tr>
      <td>ipmapping <td>
      <td>true <td>
      <td>Json<td>
      <td>-   <td>
      <td>见下表   </td>
   </tr>
   
   <tr>
      <td>extendAttributes <td>
      <td>false <td>
      <td>Json <td>
      <td>-  <td>
      <td>扩展选项</td>
   </tr>

   <tr>
      <td>tag<td>
      <td>false <td>
      <td>String<td>
      <td>50   <td>
      <td>标签</td>
   </tr>
</table>



verify 内容格式

参数字段   必选   类型    长度限制   说明 

interfaceURL  false  String -   验证界面URL

verifyURL  false  String   -    验证URL

authorURL  false  String  -    认证URL

verifyItem  false  Json  -     验证参数和值

resultValidator  false  Json  -    -


<table>
   <tr>
      <td>参数字段  </td>
       <td>必选  </td>
       <td>类型   </td>
       <td>长度限制</td>
      <td> 说明 </td>
   </tr>

   <tr>
      <td>interfaceURL  </td>
      <td> false </td>
      <td> String</td>
     <td>  -   </td>
      <td> 验证界面URL</td>
   </tr>

   <tr>
      <td>verifyURL</td> 
      <td> false</td>
      <td> String </td>
     <td>  -  </td>
     <td>  验证URL</td>
   </tr>

   <tr>
      <td>authorURL</td>
      <td> false</td>
      <td> String</td>
      <td> -   </td>
      <td> 认证URL</td>
   </tr>

   <tr>
      <td>verifyItem </td>
      <td> false</td>
       <td>Json </td>
      <td> -   </td>
      <td> 验证参数和值</td>
   </tr>

   <tr>
      <td>resultValidator</td>
      <td> false </td>
       <td>Json </td>
       <td>-</td> 
      <td> -</td>
   </tr>
</table>


ipmapping 内容格式 

参数字段   必选   类型    长度限制   说明 

enableMapping  true boolean  -   是否IP映射

ipMapping   false   Json    -    -


<table>
   <tr>
      <td>参数字段</td>   
        <td>必选 </td>
        <td>类型   </td>
        <td>长度限制</td>
        <td>说明 </td>
   </tr>
  
   <tr>
      <td>enableMapping </td>
        <td>true </td>
        <td>boolean </td>
       <td> -   </td>
        <td>是否IP映射</td>
   </tr>

   <tr>
      <td>ipMapping</td> 
        <td>false </td>
        <td>Json  </td>
        <td>-</td>   
        <td>-</td>
   </tr>
 
</table>


http://pressbin.com/tools/excel_to_html_table/index.html


返回参数说明 

参数字段   必选   类型    长度限制   说明 

status  true    String   1     成功与失败状态

message false  String -   返回具体信息

data   false  String  -  返回具体数据


<table>
   <tr>
      <td>参数字段 </td>  
      <td>必选  </td>
      <td>类型  </td>
      <td>长度限制 </td>
      <td>说明 </td>
   </tr>

   <tr>
      <td>status </td>
     <td> true   </td>
      <td>String </td>
    <td>  1  </td>
    <td>  成功与失败状态</td>
   </tr>
   <tr>
      <td>message</td>
      <td>false </td>
      <td>String</td>
     <td> -  </td>
      <td>返回具体信息</td>
   </tr>

   <tr>
      <td>data </td>
      <td>false  </td>
      <td>String </td>
      <td>-  </td>
      <td>返回具体数据</td>
   </tr>
</table>


### 根据系统编码删除第三方系统集成信息

#### 描述

删除第三方系统集成信息

#### 请求方法

/integration/system/delete/jira?r=0.7300665230450025&_=1517449633197

#### 请求方式

GET

#### 请求参数说明

参数字段   必选   类型    长度限制   说明 
{code}    true   String   50   系统编码




<table>
   <tr>
      <td>参数字段 </td>  
      <td>必选  </td>
      <td>类型  </td>
      <td>长度限制 </td>
      <td>说明 </td>
   </tr>

    <tr>
      <td>{code}</td>  
      <td>true  </td>
      <td>String  </td>
      <td>50 </td>
      <td>系统编码</td>
   </tr>
</table>


#### 返回参数说明 

参数字段   必选   类型    长度限制   说明 

status  true    String   1     成功与失败状态

message false  String -   返回具体信息

data   false  String  -  返回具体数据

<table>
   <tr>
      <td>参数字段 </td>  
      <td>必选  </td>
      <td>类型  </td>
      <td>长度限制 </td>
      <td>说明 </td>
   </tr>

   <tr>
      <td>status </td>
     <td> true   </td>
      <td>String </td>
    <td>  1  </td>
    <td>  成功与失败状态</td>
   </tr>
   <tr>
      <td>message</td>
      <td>false </td>
      <td>String</td>
     <td> -  </td>
      <td>返回具体信息</td>
   </tr>

   <tr>
      <td>data </td>
      <td>false  </td>
      <td>String </td>
      <td>-  </td>
      <td>返回具体数据</td>
   </tr>
</table>



### 查询第三方系统集成信息

#### 描述

查询第三方系统集成信息

#### 请求方法

/integration/system/query

#### 请求方式

POST

#### 请求参数说明

参数字段   必选   类型    长度限制   说明 

pageIndex   true   int    -     页数 

pageSize  true   int  -  每页条数

key   false   String    查询关键字

<table>
   <tr>
      <td>参数字段 </td>
	 <td>必选 </td>
	 <td>类型  </td>
	 <td>长度限制  </td>
	<td> 说明 </td>
   </tr>
   
   <tr>
      <td>pageIndex</td>   
      <td>true </td>
      <td>int </td>
      <td>-    </td>
      <td>页数 </td>
   </tr>
   
   <tr>
      <td>pageSize</td> 
      <td>true </td>
      <td>int  </td>
      <td>- </td>
      <td>每页条数</td>
   </tr>
   
   <tr>
      <td>key   </td>
     <td> false  </td>
     <td> String  </td>
     <td> 查询关键字</td>
   </tr>
</table>


#### 返回参数说明

参数字段   必选   类型    长度限制   说明 

status  true   int   -   返回状态

message  false  String   -  返回信息

data   false   Json      -    返回数据 

<table>
   <tr>
      <td>参数字段</td>
      <td>必选  </td>
      <td>类型 </td>
      <td>长度限制</td>
     <td> 说明 </td>
   </tr>

   <tr>
      <td>status</td>  
     <td> true </td>
      <td>int </td>
      <td>-   </td>
      <td>返回状态</td>
   </tr>

   <tr>
      <td>message</td>
     <td> false</td>
     <td> String </td> 
    <td>  - </td>
     <td>返回信息</td>
   </tr>

   <tr>
      <td>data  </td>
      <td>false  </td>
     <td> Json  </td>
      <td>-    </td>
      <td>返回数据 </td>
   </tr>
</table>

data具体内容格式说明 


参数字段   必选   类型    长度限制   说明 

content  false   String  -   具体内容 

last   true   boolean   -   -

totalElements   int   -   总共元素 

totalPages   int  -   总页数 

size  int  -    每页大小  

number  int  -  第几页 

numberOfElements int -   元素位置

sort  Json    -   类别 

first boolean  -   -

<table>
      <tr>
      <td>参数字段   </td>
      <td>必选   </td>
      <td>类型    </td>
      <td>长度限制  </td>
      <td>说明  </td>
   </tr>

   <tr>
      <td>content </td>
      <td>false</td>
  <td>String </td>
  <td>-   </td>
  <td>具体内容</td>
   </tr>
   
   <tr>
      <td>last  </td>
     <td> true  </td>
     <td> boolean  </td>
     <td> -  </td>
    <td>  -</td>
   </tr>
  
   <tr>
      <td>totalElements  </td>
     <td> int </td>
      <td>-  </td>
    <td>  总共元素</td>
   </tr>
   
   <tr>
      <td>totalPages</td>
      <td>int</td>
      <td>- </td>
      <td>总页数 </td>
   </tr>
  
   <tr>
      <td>size </td>
     <td> int </td>
    <td>  -   </td>
     <td> 每页大小  </td>
   </tr>
  
   <tr>
      <td>number </td>
     <td> int</td>
     <td> - </td>
     <td> 第几页 </td>
   </tr>
  
   <tr>
      <td>numberOfElements </td>
     <td> int </td>
    <td>  -  </td>
     <td> 元素位置</td>
   </tr>
   
   <tr>
      <td>sort </td>
      <td>Json</td>
      <td>-   </td>
      <td>类别 </td>
   </tr>
   
   <tr>
      <td>first </td>
      <td>boolean</td> 
      <td>- </td>  
      <td>-</td>
   </tr>
</table>


sort 具体内容格式说明

参数字段   必选   类型    长度限制   说明 

direction  true  String  -    排序方式

property  true   String -   -

ignoreCase  true  boolean   -  忽略大小写

nullHandling   true   String -   - 

ascending   true   boolean   -   - 

<table>
   <tr>
      <td>参数字段   </td>
      <td>必选   </td>
      <td>类型    </td>
      <td>长度限制  </td>
      <td>说明  </td>
   </tr>

   <tr>
      <td>direction </td>
     <td> true</td>
      <td>String </td>
     <td> -    </td>
      <td>排序方式</td>
   </tr>

   <tr>
      <td>property </td>
      <td>true </td>
      <td>String </td>
     <td> - </td>
     <td> -</td>
   </tr>

   <tr>
      <td>ignoreCase</td>
      <td>true </td>
     <td> boolean</td>  
     <td> - </td>
     <td> 忽略大小写</td>
   </tr>
 
   <tr>
      <td>nullHandling  </td>
     <td> true   </td>
     <td> String</td>
     <td> -  </td>
     <td> - </td>
   </tr>

   <tr>
      <td>ascending</td>
  <td>true  </td>
 <td> boolean</td>
 <td> - </td> 
  <td>- </td>
   </tr>

</table>