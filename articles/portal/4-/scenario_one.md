## 如何开发widget


### 开发widget需具备的知识

Widget 开发人员需要熟悉js、react、uui、comonjs等主流前端开发技术，编写代码时要遵循AMD等大众规范，具体代码编写参考
Google JavaScript 编码规范指南：<http://alloyteam.github.io/JX/doc/specification/google-javascript.xml>

 一个widget xml定义结构如下：

	<?xml version="1.0" encoding="UTF-8"?>
	<Module><ModulePrefs title="待办-任务"></ModulePrefs>
	<Content type="html">
	<![CDATA[
	          Css引入  
	          Js引入
	          Js编写
	          Css编写
	          Html编写
	         系统变量
	]]>
	</Content>
	</Module>

### 各块具体介绍如下

1、Css引入 

	require('css!./indexlink.css'); 
	require('css!../../font/mehecofont/iconfont.css');
    
   通过require加载好处：加载一次，减少网络流量

2、Js 引入

	require(["/portal/widget/CommonLink6/linkTask.js"],function(task){
	    var hei = getWidgetAttr(‘height’);
	    task.init(hei);
	});

3、Js编写

	define(function(require, exports, module ){
	    var styles = require('css!./indexvision.css');
	    var icon = require('css!../../font/mehecofont/iconfont.css');
	    var viewModel={
	        pageInit:function(){
	
	        }
	    };
	    return {
	        init: function(){
	            viewModel.pageInit();
	        }
	    }
	});


4、Css编写

模板：

	.框架class  widget皮肤class  业务class{
	     ….
	}

示例：

	.commonlink .u-panel-heading{
	    background: #eeeeef;
	    border-radius: 10px;
	    height: 40px;
	    line-height: 40px;
	} 

说明：

	1：框架class会在页面主题切换时联动
    2：widget 皮肤class 会在布局个性化时编辑小部件皮肤时跟随联动
    3：业务class，具体widget业务含义

5、Html编写

Html编写要遵循uui 控件要求，html数据绑定、事件、

示例：

	<html>
	    <head>
	        <title></title>
	    </head>
	    <body>
	        <div class="oa-task width-full oaApprove">
	            <div class="u-panel">
	                <div class="u-panel-heading clearfix">
	                    <span class="pull-left"><strong>OA待办审批</strong></span>
	                    <ul class="pull-right height-full OAsc">
	                        <li class="pull-left title">
	                            <a href="javaScript:void(0)" searchtype="unread" data-bind="click:$root.search">待办审批</a>
	                        </li>
	                        <li class="pull-left title">
	                            <a href="javaScript:void(0)" searchtype="incoming" data-bind="click:$root.search">收文审批</a>
	                        </li>
	                    </ul>
	                </div>
	                <div class="u-panel-body">
	                    <div u-meta='{"id":"oaGrid","data":"dataTable","type":"grid","onBeforeClickFun":"onClickFun"}'>
	                        <div options='{"field":"title","dataType":"String","editType":"string","sortable":true,"canSwap":true}'></div>
	                        <div options='{"field":"sender","dataType":"String","editType":"string" ,"renderType":"timeRender","sortable":true}'></div>
	                        <div options='{"field":"senddate","dataType":"String","editType":"string","sumCol":true}'></div>
	                    </div>
	                </div>
	            </div>
	        </div>
	    </body>
	</html>


6、系统变量

在开发widget过程中，会涉及到系统级变量的获取，如：context(/portal、/integration)、widgetid等。
系统目前提供如下系统变量的注入：

(1).${context}，应用上下文
使用示例如下：

![](/articles/portal/4-/images/4-1.png)
<p align="center">图 1</p>
 
(2).${widgetId}, 小部件标识
使用示例如下：

![](/articles/portal/4-/images/4-2.png)
<p align="center">图 2</p>


### Widget实战

轮播图案例

1、autoplay.xml如下

	<?xml version="1.0" encoding="UTF-8"?>
	<Module>
	    <ModulePrefs title="首页轮播图" description="autoplay">
	    </ModulePrefs>
	    <UserPref status="1" name="height" display_name="高度" datatype="string" default_value="240" required="true" />
	    <UserPref status="1" name="number" display_name="图片数量" datatype="string" default_value="3" required="true" />
	    <Content type="html" inline="true">
	        <![CDATA[
	        <div class="swiper-container width-full"  id="${widgetId}">
	            <div class="swiper-wrapper">
	
	            </div>
	        </div>
	            <script type="text/javascript">
	                require(["./widget/autoplay/autoplay.js"],function(task){
	                    var count=getWidgetAttr("${widgetId}",'number');
	                    var height=getWidgetAttr("${widgetId}",'height');
	                    task.init("${widgetId}",count,height);
	                })
	            </script>
	        ]]>
	    </Content>
	</Module>

2、autoplay.js如下

	define(function(require, exports, module ){
	    var html = require('text!./index.html');
	    var styles = require('css!./index.css');
	    var viewModel={
	        pageInit:function(widgetId,count,height){
	            $('#'+widgetId).css('height',height);
	            for(var i=1;i<=count;i++){
	                var str='<div class="swiper-slide swiper-no-swiping" ><img src="./widget/autoplay/images/'+i+'.jpg" class="img-responsive"> </div>';
	                $('#'+widgetId).children().append(str);
	            }
	            var mySwiper = new Swiper ('#'+widgetId, {
	                loop:'true',
	                autoplay:3000,
	                speed:1000,
	                direction:'horizontal',
	                autoplayDisableOnInteraction:'false'
	            })
	        }
	    };
	    return {
	        init: function(widgetId,count,height){
	            viewModel.pageInit(widgetId,count,height);
	        }
	    }
	});

3、效果图如下


![](/articles/portal/4-/images/4-3.png)
<p align="center">图 3</p>