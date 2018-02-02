
## API文档:定时任务

### 简介
iuap-dispatch-service组件功能包括添加、删除、暂停、重启任务。不仅提供了外部调用的Rest服务，并且本身也有完整的任务配置界面，
包括任务调度，日志查询等功能。


### API接口

### 指定任务Beanid新增基于Cron表达式的定时任务

#### 描述

添加或覆盖基于Cron表达式的定时调度任务

#### 请求方法

/dispatchserver/add.do

#### 请求方式

post

#### 请求参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>recallConfig</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>回调信息配置，Json格式，具体参考下面说明</td>
   </tr>
   <tr>
      <td>taskConfig</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务执行配置，Json格式，具体参考下面说明</td>
   </tr>
   <tr>
      <td>replace</td>
      <td>True</td>
      <td>boolean</td>
      <td>无</td>
      <td>是否覆盖，为ture时，自动覆盖，为false时，如果存在会返回错误信息</td>
   </tr>
</table>

recallConfig内容格式：

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>recallType</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>回调方式，SOCKET/HTTP</td>
   </tr>
   <tr>
      <td>option</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>回调的方式地址，"recallType" = "HTTP"时，格式为{"url":"http://ip:port/XXX"} </td>
   </tr>
   <tr>
      <td>"recallType" = "SOCKET"时，格式为{"host":"ip","port"}</td>
   </tr>
   <tr>
      <td>data</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务附加数据，执行时传递给调用接口，建议为json格式</td>
   </tr>
</table>

taskConfig内容格式：

<table>
   <tr>
      <td>参数字段</td>
      <td>triggerType</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>triggerType</td>
      <td></td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>触发方式，SimpleTrigger/CronTrigger，下面参数根据类型不同变化， </td>
   </tr>
   <tr>
      <td>可参考sdk中的CronTaskConfig/SimpleTaskConfig两种配置类参数</td>
   </tr>
   <tr>
      <td>jobCode</td>
      <td>SimpleTrigger/CronTrigger</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务名称</td>
   </tr>
   <tr>
      <td>groupCode</td>
      <td>SimpleTrigger/CronTrigger</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>组名称</td>
   </tr>
   <tr>
      <td>priority</td>
      <td>SimpleTrigger/CronTrigger</td>
      <td>True</td>
      <td>int</td>
      <td>无</td>
      <td>优先级，数字大的优先执行</td>
   </tr>
   <tr>
      <td>endDate</td>
      <td>SimpleTrigger/CronTrigger</td>
      <td>True</td>
      <td>Date</td>
      <td>无</td>
      <td>任务结束始时间</td>
   </tr>
   <tr>
      <td>cronExpress</td>
      <td>CronTrigger</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>表达式，</td>
   </tr>
   <tr>
      <td>startDate</td>
      <td>SimpleTrigger</td>
      <td>True</td>
      <td>Date</td>
      <td>无</td>
      <td>任务开始时间</td>
   </tr>
   <tr>
      <td>timeConfig</td>
      <td>SimpleTrigger</td>
      <td>True</td>
      <td>Json</td>
      <td>无</td>
      <td>时间配置，json格式，参考TimeConfig类格式如下</td>
   </tr>
</table>

timeConfig内容格式：

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>interval</td>
      <td>True</td>
      <td>int</td>
      <td>无</td>
      <td>执行间隔时间，具体单位见intervalType</td>
   </tr>
   <tr>
      <td>intervalType</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>执行间隔时间单位：NULL/MILLISECOND/SECOND/MINUTE/HOUR</td>
   </tr>
   <tr>
      <td>isForever</td>
      <td>True</td>
      <td>boolean</td>
      <td>无</td>
      <td>是否重复执行，为true时会一直定时执行，直到暂停或删除任务</td>
   </tr>
   <tr>
      <td>repeatCount</td>
      <td>True</td>
      <td>int</td>
      <td>无</td>
      <td>重复次数，isForever为false时，任务仅执行指定的次数</td>
   </tr>
</table>

返回参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>success</td>
      <td>boolean</td>
      <td>true/false</td>
   </tr>
   <tr>
      <td>error</td>
      <td>String</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>resultValue</td>
      <td>String</td>
      <td>返回值，一般为null</td>
   </tr>
</table>

### 暂停任务

#### 描述

根据任务名称和组名称暂停任务

#### 请求方法

/dispatchserver/pause.do

#### 请求方式

post

#### 请求参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>jobName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务名称</td>
   </tr>
   <tr>
      <td>groupName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>组名称</td>
   </tr>
</table>

返回参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>success</td>
      <td>boolean</td>
      <td>true/false</td>
   </tr>
   <tr>
      <td>error</td>
      <td>String</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>resultValue</td>
      <td>String</td>
      <td>返回值，一般为null</td>
   </tr>
</table>

### 恢复任务

#### 描述

根据任务名称和组名称恢复任务

#### 请求方法

/dispatchserver/resumeTask.do

#### 请求方式

post

请求参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>jobName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务名称</td>
   </tr>
   <tr>
      <td>groupName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>组名称</td>
   </tr>
</table>

返回参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>success</td>
      <td>boolean</td>
      <td>true/false</td>
   </tr>
   <tr>
      <td>error</td>
      <td>String</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>resultValue</td>
      <td>String</td>
      <td>返回值，一般为null</td>
   </tr>
</table>

### 删除任务

#### 描述

根据任务名称和组名称删除任务

#### 请求方法

/dispatchserver/delete.do

#### 请求方式

post

#### 请求参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>jobName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务名称</td>
   </tr>
   <tr>
      <td>groupName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>组名称</td>
   </tr>
</table>

返回参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>success</td>
      <td>boolean</td>
      <td>true/false</td>
   </tr>
   <tr>
      <td>error</td>
      <td>String</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>resultValue</td>
      <td>String</td>
      <td>返回值，一般为null</td>
   </tr>
</table>

### 立即执行任务

#### 描述

根据任务名称和组名称立即执行任务

#### 请求方法

/dispatchserver/trigger.do

#### 请求方式

post

#### 请求参数说明

<table>
   <tr>
      <td></td>
   </tr>
   <tr>
      <td>参数字段</td>
      <td>必选</td>
      <td>类型</td>
      <td>长度限制</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>jobName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>任务名称</td>
   </tr>
   <tr>
      <td>groupName</td>
      <td>True</td>
      <td>String</td>
      <td>无</td>
      <td>组名称</td>
   </tr>
</table>


#### 返回参数说明

<table>
   <tr>
      <td>参数字段</td>
      <td>类型</td>
      <td>说明</td>
   </tr>
   <tr>
      <td>success</td>
      <td>boolean</td>
      <td>true/false</td>
   </tr>
   <tr>
      <td>error</td>
      <td>String</td>
      <td>错误信息</td>
   </tr>
   <tr>
      <td>resultValue</td>
      <td>String</td>
      <td>返回值，一般为null</td>
   </tr>
</table>
