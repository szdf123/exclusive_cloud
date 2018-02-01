# 卸载及常见问题

1.Redis 服务器最好不要与其他系统公用。

2.对于 Oracle 用户，删除安装时所指定的用户的所有表和视图即可。
对于其他数据库用户，删除 Portal 应用的数据库即可。

3.对于使用 tomcat 中间件用户，停止中间件的所有服务，删除 webapps/portal、integration、uitemplate_web 目录即可。
