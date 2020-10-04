### MySQL与SQLServer的语法区别

1、MySQL支持enum,和set类型，SQL Server不支持
2、MySQL不支持nchar,nvarchar,ntext类型
3、MySQL的递增语句是AUTO_INCREMENT，而MS SQL是identity(1,1)
4、MS SQL默认到处表创建语句的默认值表示是((0)),而在MySQL里面是不允许带两括号的
5、MySQL需要为表指定存储类型
6、MS SQL识别符是[],[type]表示他区别于关键字，但是MySQL却是 `，也就是按键1左边的那个符号
7、MS SQL支持getdate()方法获取当前时间日期，但是MySQL里面可以分日期类型和时间类型，获取当前日期是current_date ()，当前完整时间是 now()函数
8、MS SQL不支持replace into 语句，但是在最新的sql20008里面，也支持merge语法
9、MySQL支持insert into table1 set t1 = „‟, t2 = „‟ ,但是MS SQL不支持这样写
10、MySQL支持insert into tabl1 values (1,1), (1,1), (1,1), (1,1), (1,1), (1,1), (1,1)
11、MySQL在创建表时要为每个表指定一个存储引擎类型，而MS SQL只支持一种存储引擎
12、MySQL不支持默认值为当前时间的datetime类型（MS SQL很容易做到），在MySQL里面 是用timestamp类型
13、MS SQL里面检查是否有这个表再删除，需要这样：if exists (select * from dbo.sysobjects where id = object_id(N’uc_newpm’) and OBJECTPROPERTY(id,N’IsUserTable’)=1) 但是在MySQL里面只需要 DROP TABLE IF EXISTS cdb_forums;
14、MySQL支持无符号型的整数，那么比不支持无符号型的MS SQL就能多出一倍的最大数 存储
15、MySQL不支持在MS SQL里面使用非常方便的varchar(max)类型，这个类型在MS SQL里 面既可做一般数据存储，也可以做blob数据存储
16、MySQL创建非聚集索引只需要在创建表的时候指定为key就行，比如：KEY displayorder (fid,displayorder) 在MS SQL里面必须要：create unique nonclustered index index_uc_protectedmembers_username_appid on dbo.uc_protectedmembers (username asc,appid asc)
17、MySQL text字段类型不允许有默认值
18、MySQL的一个表的总共字段长度不超过65XXX。
19、一个很表面的区别就是MySQL的安装特别简单，而且文件大小才110M（非安装版），相 比微软这个庞然大物，安装进度来说简直就是…
20、MySQL的存储过程只是出现在最新的版本中，稳定性和性能可能不如MS SQL。
21、同样的负载压力，MySQL要消耗更少的CPU和内存，MS SQL的确是很耗资源。
22、MySQL的ifnull()函数对应sql的isnull()函数;
23、MySQL的存储过程中变量的定义去掉@;
24、MySQL的每句结束要用";"
25、SQLServer存储过程的AS在MySql中需要用begin …end替换
26、字符串连接用concat()函数;如 SQLServer: Temp=‟select * from ‟+‟tablename‟+…+… MySql:Temp=concat(‟select * from‟, ‟tablecname‟,…,…)
27、MySQL的uuid()对应mssql的GUID();
28、MySql的out对应SQLServer的output,且mysql 的out要放在变量的前面，SQLServer 的output放在变量后面
29、MySql out,in,inout的区别——MySQL 存储过程 “in” 参数：跟 C 语言的函数参 数的值传递类似， MySQL 存储过程内部可能会修改此参数，但对 in 类型参数的修改，对调用者（caller）来说是不可见的（not visible）。MySQL 存储过程 “out” 参数：从存储过程内部传值给调用者。在存储过程内部，该参数初始值为 null，无论调用者是否给存储过程参数设置值。MySQL 存储过程 inout 参数跟 out 类似，都可以从存储过程内部传值给调用者。不同的是：调用者还可以通过 inout 参数传递值给存储过程。
30、MySQL的if语句为 if (条件) then end if; 或者 If (条件) then Else End if 或者 If（条件）then Elseif (注意不能写成 Else if ) Elseif … End if
31、Mysql的Execute对应SqlServer的exec; (注意：必须想下面这样调用) Set @cnt=‟select * from 表名‟; Prepare str from @cnt; Execute str;
32、MySql存储过程调用其他存储过程用call Call 函数名（即SQLServer的存储过程名）（‟参数1‟,‟参数2‟,……）
33、mysql的日期
```
1) 获得当前日期函数：curdate()，current_date()

2) 获得当前时间函数：curtime();

3) 获得当前日期+时间：now();

4) MySQL dayof... 函数：dayofweek(), dayofmonth(), dayofyear()分别返回日期参 数，在一周、一月、一年中的位置。 

5) (注：周日=1，周一=2，周二=3，……)

6) 返回本月的天数：select day(last_day(now()));

7) MySQL 为日期增加一个时间间隔：date_add() 

8) select date_add(CURRENT_DATE(),interval „要增加的天数‟ day) as Fdate

9) MySQL 为日期减去一个时间间隔：date_sub() 

10) select date_sub('1998-01-01 00:00:00', interval '1 1:1:1' day_second);

11) MySQL 日期、时间相减函数：datediff(date1,date2), timediff(time1,time2)

12) MySQL 拼凑日期、时间函数：makdedate(year,dayofyear),  maketime(hour,minute,second) 

13) 例：select makedate(2001,31); -- '2001-01-31'

14) select makedate(2001,32); -- '2001-02-01'

15) 本周时间（起始） 

16) select date_sub(CURRENT_DATE(),interval dayofweek(curdate())-2 day) as Fdate

17) 本周时间（结束） 

18) select date_add(CURRENT_DATE(),interval dayofweek(curdate())+3 day) as  Fdate 

19) 上周时间（起始） 

20) select date_sub(CURRENT_DATE(),interval dayofweek(curdate())+5 day) as Fdate 

21) 上周时间（结束） 

22) select date_sub(CURRENT_DATE(),interval dayofweek(curdate())-1 day) as Fdate

23) 本月时间(起始) 

24) select DATE_SUB(CURDATE(),INTERVAL DAY(CURDATE())-1 DAY) as Fdate

25) 本月时间（结束） 

26) Select date_add(current_date(),interval day(last_day(CURDATE()))  -day(CURDATE()) day) as Fdate

27) 上月时间（起始）

28) select DATE_SUB(DATE_SUB(CURDATE(),INTERVAL DAY(CURDATE())  DAY),interval day(last_day(DATE_SUB(CURDATE(),INTERVAL DAY(CURDATE()) DAY)))-    1 day) as Fdate

29) 上月时间（结束） 

30) select DATE_SUB(CURDATE(),INTERVAL DAY(CURDATE()) DAY) as Fdate

31) 今年时间（起始） 

32) select makedate(year(curdate()),1) as FDate

33) 今年时间（结束） 

34) select DATE_SUB(makedate(year(curdate())+1,1) ,INTERVAL 1 day) as Fdate

35) 去年时间（起始） 

36) select makedate(year(curdate())-1,1) as Fdate

37) 去年时间（结束） 

38) select DATE_SUB(makedate(year(curdate()),1) ,INTERVAL 1 day) as FDate

39) DATE_FORMAT(date,format)：根据format字符串格式化date值。下列修饰符 可以被用在format字符串中

40) %M     月名字(January……December)            %W     星期名字(Sunday……Saturday)            %D     有英语前缀的月份的日期(1st,   2nd,   3rd,   等等。）         %Y     年,   数字,   4   位         %y     年,   数字,   2   位          %a     缩写的星期名字(Sun……Sat)           %d     月份中的天数,   数字(00……31)           %e     月份中的天数,   数字(0……31)           %m     月,   数字(01……12)           %c     月,   数字(1……12)           %b     缩写的月份名字(Jan……Dec)           %j     一年中的天数(001……366)           %H     小时(00……23)           %k     小时(0……23)           %h     小时(01……12)           %I     小时(01……12)           %l     小时(1……12)           %i     分钟,   数字(00……59)            %r     时间,12   小时(hh:mm:ss   [AP]M)             %T     时间,24   小时(hh:mm:ss)           %S     秒(00……59)           %s     秒(00……59)           %p     AM或PM

41) %w     一个星期中的天数(0=Sunday   ……6=Saturday   ）          %U     星期(0……52),   这里星期天是星期的第一天         %u     星期(0……52),   这里星期一是星期的第一天         %%     一个文字“%”。      

42) 例：所有的其他字符不做解释被复制到结果中。         mysql>  select   DATE_FORMAT('1997-10-04   22:23:00',   '%W   %M   %Y');       ->'Saturday   October   1997'        mysql>select   DATE_FORMAT('1997-10-04   22:23:00',   '%H:%i:%s');   

43) ->   '22:23:00'    

44) mysql>select   DATE_FORMAT('1997-10-04   22:23:00',   '%D   %y   %a    %d   %m   %b   %j');    

45) ->'4th   97   Sat   04   10   Oct   277'    

46) mysql>select   DATE_FORMAT('1997-10-04   22:23:00',   '%H   %k   %I    %r   %T   %S    %w');    

47) ->'22   22   10   10:23:00   PM   22:23:00   00   6'
```
34、MySql存储过程中没有return函数，在MySql中可以用循环和out参数代替 If EXISTS(SELECT * FROM T_Chance WHERE FCustID=CostomerID) return 0 改写为： （在参数中定义一个out变量：out temp varchar(100);） BEGIN Loop1:loop SELECT count(*) FROM T_Chance WHERE FCustID=CostomerID int @cnt If @cnt>0 then begin set temp=0; leave loop1; end; end if end loop loop1;
35、select @a=count() from VW_Action 在mySql中修改为：select count() from VW_Action into @a;
36、MySQL中没有top关键字，需要用limit代替且放在后面 注意，在MySQL中的limit不能放在子查询内，limit不同与SQLServer,它可 以规定范围 limit a,b——范围a-b SQL SERVER : select top 8 * from table1 MYSQL: select * from table1 limit 5;
37、即使存储过程没有参数也要写括号“（）”
38、当一个存储过程中有创建临时表时 create procedure up_test () begin drop table if exists tb1; create TEMPORARY table tb1//注意添加TEMPORARY table ( id int, name varchar(20) );//注意最后加分号 insert tb1 values(‘1’,‘jim’); select * from tb1; end

39、建表中自增长问题： create table user ( Id varchar(10) primary key auto_increment not null, Name varchar(20) not null, Password varchar(20), create_date datetime ); auto_increment 自增长

40、“Unable to convert MySQL date/time value to System.DateTime"这是因为在日期 列中有"0000-00-00"数据值，要修正这个问题，你可以把这些数据设为null，或者在连接字符串中设置"Allow Zero Datetime=True” 。

41、MySQL视图的FROM子句不允许存在子查询，因此对于SQL Server中FROM 子句带有子查询的视图，需要手工进行迁移。可通过消除FROM子句中的子查询，或将FROM子句中的子查询重构为一个新的视图来进行迁移。
