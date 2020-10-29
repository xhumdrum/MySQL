1、服务类型不是Network Service。打开配置管理器-->SQL Server服务-->SQL Serve，右键-->属性-->内置账户，选择Network Service，然后重启SQL Server服务。

2、TCP/IP协议未启用。打开配置管理器-->SQL Server 网络配置-->（实例名称）的协议-->TCP/IP，右键-->属性-->IPALL，TCP端口填默认的端口：1433，然后重启SQL Server服务。

3、远程访问未启用。启动Microsoft SQL Server Management Studio，连接数据库后，在对象资源管理器中，点击右键选择方面-->服务器配置-->RemoteAccessEnabled改为True。

4、未开启SQL Server身份认证。启动Microsoft SQL Server Management Studio，连接数据库后，在对象资源管理器中，点击右键选择属性-->安全性-->服务器身份认证，选择SQL Server和Windows身份认证模式。
