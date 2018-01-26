# 代码示例

完整示例包含三个工程，分别为公共的SDK（rpc-sdk），前端和客户端工程（rpc-client）、服务提供方工程（rpc-provider），下述文档列出部分关键配置和示例代码，更加详细的源码请参考安装盘中的源码工程。

## 前端图表页面和js代码

### 静态页

	<!DOCTYPE html>
	<html>
	<head>
	<meta content='text/html;charset=utf-8' http-equiv='content-type'>
	<title>Echarts图表Demo</title>
	<script src="js/esl/esl.js"></script>
	<script src="js/jquery.js"></script>
	</head>
	
	<body>
		<div id="link" style="margin:0 auto; margin-top:50px; width: 800px; height:20px;">
			<a href="#" onclick="toBar()">柱状图示例</a>
			<a href="#" onclick="toPie()">饼状图示例</a>
		</div>
		<div id="line" style="margin:0 auto; margin-top:20px; width: 800px; height: 600px;"></div>
	</body>
	</html>


### javascript 代码

	<script type="text/javascript">
	
		var fileLocation ='js/echarts';
		require.config({
		    paths:{ 
				echarts: fileLocation,
		        'echarts/chart/line': fileLocation,
		        'echarts/chart/bar': fileLocation,
		        'echarts/chart/pie': fileLocation
		    }
		});
	
		// 作为入口
		require(
		    [
		        'echarts',
		        'echarts/chart/line'
		    ], 
			displayChart
		);
	
		function displayChart(ec) {
	        //折线图
	        var lineChart = ec.init(document.getElementById('line'));
			$.get('/rpc-client/options/line', function (data) {
				var obj = eval('(' + data + ')');
				lineChart.setOption(obj);
			});
	    }
		
		function toBar(){
			window.location.href = "/rpc-client/bar.html";
		}
		
		function toPie(){
			window.location.href = "/rpc-client/pie.html";
		}
	</script>

## SDK接口声明代码

### 注解方式声明示例

	@RemoteCall(AppInfoConstant.APP_INF_SERVER)
	public interface IChartDataService {
		
		/**
		 * 远程获取echart的各种图表的json数据
		 * 
		 * @param type line/pie/bar
		 * @return echarts的json数据
		 */
		@ApiOperation("根据类型获取各种echarts图表的数据")
		public @ApiReturnValue(name="json 数据", description="echarts 需要的option数据，详情请参考echarts官网文档") String getChartDataByType(@ApiParam(name="图表类型", required=true, description="图表类型数据文件前缀，如bar、pie、line等", exampleValue="line") String type) throws Exception;
	}

### 配置文件方式声明示例

	/**
	 * 获取图表类型列表服务<br>
	 * 此示例不使用RemoteCall注解，使用spring配置文件的方式配置远程的bean
	 * 
	 * @author Administrator
	 */
	public interface IChartTypeService {
		
		/**
		 * 远程获取echart图表类型列表
		 * 
		 * @return echarts的图表类型list
		 */
		public @ApiReturnValue(name="图表类型列表", description="示例中支持的 echarts demo的图表类型") List<String> getChartTypes() throws Exception;
	}

配置文件：

	<bean id="chartTypeService" class="com.yonyou.cloud.middleware.rpc.RPCBeanFactory">
	    <constructor-arg value="${remote.server.name}"></constructor-arg>
	    <constructor-arg value="${remote.server.providerid}"></constructor-arg>
	    <constructor-arg>
	    	<list>
	        	<value>com.yonyou.cloud.ms.service.IChartTypeService</value>
	        </list>
	    </constructor-arg>
	</bean>

## 客户端代码示例

### Controller 示例

	@RestController
	@RequestMapping(value = "/options")
	public class ChartOptionsController {
		
		private static final Logger LOGGER = LoggerFactory.getLogger(ChartOptionsController.class);
	
		@Autowired
		private MsClientService clientService;
		
		@RequestMapping(value = "/line")
		public String getLineOption(HttpServletRequest request) {
			String json = "";
			try {
				json = clientService.getRemoteChartData("line");
			} catch (Exception e) {
				LOGGER.error("获取line的图表初始化数据失败!", e);
			}
			return json;
		}
		
		@RequestMapping(value = "/pie")
		public String getPieOption(ServletRequest request) {
			String json = "";
			try {
				json = clientService.getRemoteChartData("pie");
			} catch (Exception e) {
				LOGGER.error("获取饼图初始化数据失败!", e);
			}
			return json;
		}
		
		@RequestMapping(value = "/bar")
		public String getBarOption(ServletRequest request) {
			String json = "";
			try {
				json = clientService.getRemoteChartData("bar");
			} catch (Exception e) {
				LOGGER.error("获取柱状图初始化数据失败!", e);
			}
			return json;
		}
	
	}


### 客户端配置

	
	#私有测试环境
	access.key=50iZDhyAoXtfguLR
	access.secret=g2MWT3PVMEOiuCo9F6IWjJzEiNEw60
	
	spring.application.name=rpc-client
	spring.profiles.active=dev
	
	#针对consumer bean的额外配置
	remote.server.name=rpc-provider
	remote.server.providerid=35568e76-1ef1-4d77-b5cf-8fb66d2c8002
	
	#针对指定IP调用的额配置，默认配置未false
	client.usemock=false

### 远程调用示例

	@Service
	public class MsClientService {
	
		@Autowired
		private IChartDataService remoteDataService;
		
		@Autowired
		private IChartTypeService remoteTypeService;
		
		public String getRemoteChartData(String type) throws Exception {
			return remoteDataService.getChartDataByType(type);
		}
	
		public List<String> getRemoteChartType() throws Exception {
			return remoteTypeService.getChartTypes();
		}
	}

## 服务提供端代码示例

### 服务提供方工程配置示例
	
	#私有测试环境
	access.key=50iZDhyAoXtfguLR
	access.secret=g2MWT3PVMEOiuCo9F6IWjJzEiNEw60
	
	spring.application.name=rpc-provider
	spring.profiles.active=dev
	
	#针对consumer bean的额外配置
	remote.server.name=rpc-provider
	remote.server.providerid=35568e76-1ef1-4d77-b5cf-8fb66d2c8002

### 远程服务接口的实现

	@Service
	public class ChartDataServiceImpl implements IChartDataService {
	
		@Override
		public String getChartDataByType(String type) throws Exception {
			String ctxPath = CustomServletContextListener.CTX_REAL_PATH;
			String json = FileUtils.readFileToString(new File(ctxPath + File.separator + "data" + File.separator + type + ".json"),"utf-8");
			return json;
		}
	    
	}

listener:

	public class CustomServletContextListener implements ServletContextListener {
		
		public static String CTX_REAL_PATH = null;
	
	    public void contextDestroyed(ServletContextEvent sce) {
	    }
	
		public void contextInitialized(ServletContextEvent event) {
			String realContextPath = event.getServletContext().getRealPath("/");
			CTX_REAL_PATH = realContextPath;
		}
	
	}
