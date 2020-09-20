
## 第一步、开启群晖 NAS 的 SSH 登录功能
1. 登录群晖 NAS
2. 打开 “控制面板”，找到最后面的 “终端机和 SNMP”
3. 勾选两项：“启动 Telnet 功能” 和 “启动 SSH 功能”，端口号可以是默认的 22

## 第二步、打开 SSH 终端 （Win10 中可以直接打开 cmd 命令行窗口，其他 OS 中可以下载 PuTTY 来连接 SSH）
4. 输入命令
> ssh -p 22 xiaxiang@192.168.0.111    ( 22:端口号 xiaxiang:登录的用户名 192.168.0.111:群晖 NAS 的IP ）
5. 屏幕上出现
> xiaxiang@192.168.0.111's password:  ( 输入登录密码 )
6. 屏幕上出现
> xiaxiang@xyHomeServer:~$            ( xyHomeServer:群晖 NAS 的主机名) 

## 第三步、进入 MariaDB 默认安装目录
7. 输入命令,进入/bin
> xiaxiang@xyHomeServer:~$ cd /usr/local/mariadb10/bin

## 第四步、以 root 用户登录 MariaDB10
8. /bin 目录下有 MySQL 可执行文件，输入命令
> xiaxiang@xyHomeServer:/usr/local/mariadb10/bin$ ./mysql -uroot -p
> Enter password: ( 输入 MariaDB10 的 root 用户登录密码)
9. 屏幕显示
> Welcome to the MariaDB monitor.  Commands end with ; or \g.
> Your MariaDB connection id is 14
> Server version: 10.3.21-MariaDB Source distribution
> 
> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
> 
> Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.
> 
> MariaDB [(none)]>
        
 ## 第五步、添加能从远程访问的 root 账号
10. 执行 SQL 命令
> MariaDB [(none)]> GRANT ALL PRIVILEGES ON *.* TO 'root'@'192.168.0.%' IDENTIFIED BY '密码' WITH GRANT OPTION;
> Query OK, 0 rows affected (0.227 sec)
11. 验证结果，输入命令
> MariaDB [(none)]> select user,host from mysql.user where host<>'localhost';
> +------+-------------+
> | user | host        |
> +------+-------------+
> | root | 127.0.0.1   |
> | root | 192.168.0.% |
> | root | ::1         |
> +------+-------------+
> 3 rows in set (0.022 sec)
          
  ## 第六步、打开 MySQL 图形客户端 SQLYog，新建连接，输入 IP：192.168.0.111，端口号 3307，以及root和登录密码，即可连接
  
  
  
          
          
    
