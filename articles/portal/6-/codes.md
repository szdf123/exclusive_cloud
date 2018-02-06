## 代码示例

### widget开发代码示例

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



具体见developWidget