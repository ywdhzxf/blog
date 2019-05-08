
---
title: Mysql的基础学习
date: 2019-05-06 12:36:15
tags: 数据库
---


## MySQL

### 概念

```
   数据： data
   数据库： DB
   数据库管理系统：DBMS
   数据库系统：DBS
   MySQL：数据库  
   mysql：客户端命令（用来连接服务或发送sql指令）
   SQL：结构化查询语言 ，其中MySQL支持这个。
   SQL语言分为4个部分：DDL（定义）、DML（操作）、DQL（查询）、DCL（控制）
   
   MySQL->库->表->数据
   
   SQL语句中的快捷键
   \G 格式化输出（文本式，竖立显示）
   \s 查看服务器端信息
   \c 结束命令输入操作
   \q 退出当前sql命令行模式
   \h 查看帮助
```

### 授权

```
格式：grant 允许操作 on 库名.表名 to 账号@来源 identified by '密码';
	
	--实例：创建zhangsan账号，密码123，授权lamp61库下所有表的增/删/改/查数据,来源地不限
	mysql> grant select,insert,update,delete on lamp61.* to zhangsan@'%' identified by '123';
	mysql> grant all on *.* to zhangsan@'%' identified by '123';
	Query OK, 0 rows affected (0.00 sec)
```

### 连接数据库

```
常用   mysql -u 用户名 -p密码  
mysql -h 主机名 -u 用户名  -p密码  库名
   
   C:\>mysql  --采用匿名账号和密码登陆本机服务
   C:\>mysql -h localhost -u root -proot   --采用root账号和root密码登陆本机服务
   C:\>mysql -u root -p   --推荐方式默认登陆本机
	 Enter password: ****

   C:\>mysql -u root -p lamp61  --直接进入lamp61数据库的方式登陆
```

### 数据类型和运算符

```
MySQL的数据类型分为四大类：数值类型、字串类型、日期类型、NULL。
	
	5.1 数值类型：
		*tinyint(1字节) 0~255  -128~127
		smallint(2字节)
		mediumint(3字节)
		*int(4字节)
		bigint(8字节)
		*float(4字节)   float(6,2)
		*double(8字节)  
		decimal(自定义)字串形数值
		
	 5.2 字串类型
		普通字串
		*char  定长字串   	 char(8)  
		*varchar 可变字串 varchar(8)
		
		二进制类型
		tinyblob
		blob
		mediumblob
		longblob
		
		文本类型
		tinytext
		*text      常用于<textarea></textarea>
		mediumtext
		longtext
		
		*enum枚举
		set集合
		
	5.3 时间和日期类型：
		date  年月日
		time  时分秒
		datetime 年月日时分秒
		timestamp 时间戳
		year 年
	
	5.4 NULL值
		NULL意味着“没有值”或“未知值”
		可以测试某个值是否为NULL
		不能对NULL值进行算术计算
		对NULL值进行算术运算，其结果还是NULL
		0或NULL都意味着假，其余值都意味着真

	MySQL的运算符：
		算术运算符：+ - * / % 
		比较运算符：= > < >= <= <> != 
		数据库特有的比较：in，not in, is null,is not null,like, between and 
		逻辑运算符：and or not
```

### 表的字段约束

```
!!! 有先后顺序的关系
		
		unsigned 无符号(正数)
		zerofill 前导零填充
		auto_increment  自增
		default	默认值
		not null  非空
		PRIMARY KEY 主键 
（非null并不重复） (包括非空,写主见就不用写非空)
		unique 唯一性   （可以为null但不重复）
		index 常规索引	
```

### 建表格式

```
 create table 表名(
	   字段名 类型 [字段约束],
	   字段名 类型 [字段约束],
	   字段名 类型 [字段约束],
	   ...
	  );

create table stu(
	-> id int unsigned not null auto_increment primary,
	-> name varchar(8) not null unique,
	-> age tinyint unsigned,
	-> sex enum('m','w') not null default 'm',
	-> classid char(6)
	-> );
```



## 数据库的基本操作

### 数据库

```
show databases;                    	   查看当前所有数据库信息
create database  库名;       			 创建数据库
create if not exists 库名;			 尝试创建数据库,若已存在则不创建
drop database 库名;					删除数据库
drop database if exists 库名;	 		 尝试删除数据库
show create database 库名\G;			  查看数据库的sql语句
use 库名;								进入当前数据库
select database();					   查看当前所在数据库位置
```

### 数据表

```
show tables;						查看当前所有的表
create table  [if not exists ] 表名(字段1 类型,字段2 类型,...)	
创建数据表,指定字段并指定类型 [尝试创建]

desc  表名;						  查看表结构
show create table 表名;				查看表的见表语句
show create table 表名\G				格式化查看建表语句
drop table 表名;						删除数据表dd;
drop table if exists 表名;			尝试删除表;
```

### 表的数据(增删改查 DML)

```
-- 表的数据操作（增insert 删delete 改update 查select）
--========================================
  ! uu  是表名
-- 标准添加（指定所有表字段，给定所有字段值进行添加）
insert into uu(id,name,age) values(1,'zhangsan',20); 

-- 标准添加（不同之处是字段顺序）
insert into uu(age,id,name) values(22,2,'lisi');

-- 指定部分字段添加值
insert into uu(id,name) values(3,'wangwu');

-- 不指定字段信息添加值，注意字段值得顺序和个数要和表结构一致
insert into uu values(4,'zhaoliu',25);

-- 批量添加值
insert into uu values(5,'u01',21),(6,'u02',22),(7,'u03',23);

-- 查看所有字段所有值
select * from uu;

-- 修改uu表的id值为3的信息，将age改为18
update uu set age=18 where id=3; 

-- 修改id为6的信息，将age改为28，name改为uu04
update uu set age=28,name='uu04' where id=6;

-- 删除id值为100的信息
delete from uu where id=100;

-- 删除id值大于50的所有信息
 delete from uu where id>50;

```

### 修改表结构

```
 格式： alter table 表名 action（更改选项）;
     更改选项：
  1. 添加字段：alter table 表名 add 字段名信息
-- 在user表的最后追加一个num字段 设置为int not null
       mysql> alter table user add num int not null;
                
-- 在user表的email字段后添加一个age字段，设置int not null default 20；
         mysql> alter table user add age int not null default 20 after email;
 -- 在user表的最前面添加一个aa字段设置为int类型
        mysql> alter table user add aa int first;

 2. 删除字段：alter table 表名 drop 被删除的字段名
      例如：-- 删除user表的aa字段
       mysql> alter table user drop aa;
	
  3. 修改字段：alter table 表名 change[modify] 被修改后的字段信息  (修改记得必须要写属性值)
  其中：change可以修改字段名， modify 不修改

 -- 修改user表中age字段信息（类型），（使用modify关键字的目的不修改字段名）
       mysql> alter table user modify age tinyint unsigned not null default 20;
            -- 修改user表的num字段改为mm字段并添加了默认值（使用change可以改字段名）
            mysql> alter table user change num mm int not null default 10;
        
4. 添加和删除索引
  -- 为user表中的name字段添加唯一性索引，索引名为uni_name;
        mysql> alter table user add unique uni_name(name);
  -- 为user表中的email字段添加普通索引，索引名为index_eamil
        mysql> alter table user add index index_email(email);
   -- 将user表中index_email的索引删除
        mysql> alter table user drop index index_email;
	
5. 更改表名称：
      ALTER TABLE 旧表名 RENAME AS 新表名

 6. 更改AUTO_INCREMENT初始值:
      ALTER TABLE 表名称 AUTO_INCREMENT=1
        
 7. 更改表类型：
        ALTER TABLE 表名称 ENGINE="InnoDB"
        
    MySQL数据库中的表类型一般常用两种：MyISAM和InnoDB
    区别：MyISAM类型的数据文件有三个frm(结构)、MYD（数据）、MYI（索引）
    MyISAM类型中的表数据增 删 改速度快，不支持事务，没有InnoDB安全。
          
   InnoDB类型的数据文件只有一个 .frm
   InnoDB类型的表数据增 删 改速度没有MyISAM的快，但支持事务，相对安全。
```

### 数据DQL 操作:数据查询

```
 格式：
        select [字段列表]|* from 表名
        [where 搜索条件]
        [group by 分组字段 [having 子条件]]
        [order by 排序 asc|desc]
        [limit 分页参数]
 
    1. where条件查询
    1. 查询班级为lamp138期的学生信息
    mysql> select * from stu where classid='lamp138';
    
    2. 查询lamp138期的男生信息（sex为m）
    mysql> select * from stu where classid='lamp138' and sex='m';
    
    3. 查询id号值在10以上的学生信息
    mysql> select * from  stu where id>10;
    
    4. 查询年龄在20至25岁的学生信息
    mysql> select * from stu where age>=20 and age<=25;
    mysql> select * from stu where age between 20 and 25;
    
    5. 查询年龄不在20至25岁的学生信息
    mysql> select * from stu where age not between 20 and 25;
    mysql> select * from stu where age<20 or age>25;
    
    6. 查询id值为1,8,4,10,14的学生信息
    select * from stu where id in(1,8,4,10,14);
    mysql> select * from stu where id=1 or id=8 or id=4 or id=10 or id=14;
    
    7. 查询lamp138和lamp94期的女生信息
    mysql> select * from stu where classid in('lamp138','lamp94') and sex='w';
    mysql> select * from stu where (classid='lamp138' or classid='lamp94') and sex='w
    
```

#### 查询

```
 where条件查询
--========================================================
--1. 查询id为3的学生信息
mysql> select * from stu where id=3;

--2. 查询性别sex为m的所有信息
mysql> select * from stu where sex='m';

--3. 查询年龄大于25岁的所有学生信息
mysql> select * from stu where age>25;

--4. 查询学生年龄是22~27岁的所有信息
mysql> select * from stu where age>=22 and age<=27;
mysql> select * from stu where age between 22 and 27;

--5. 查询学生年龄在20~25岁之外的所有信息
mysql> select * from stu where age<20 or age>25;
mysql> select * from stu where age not between 20 and 25;

--6. 查询性别sex为w，并且年龄大于22岁的所有信息
mysql> select * from stu where sex='w' and age>22;

--7. 查询classid不为null的所有信息
mysql> select * from stu where classid  is not null;

--8. 查询id值为1,3,5,9,12的学员信息
mysql> select * from stu where id in(1,3,5,9,12);

--9. 查询name字段值是以zh开头的所有信息
mysql> select * from stu where name like "zh%";
mysql> select * from stu where name regexp  "^zh"; --正则写法

--10.查询姓名name中含有ang子串的所有信息
mysql> select * from stu where name like "%ang%";
mysql> select * from stu where name regexp  "ang";
-11. 查询姓名是任意四位字符构成的信息。
mysql> select * from stu where name like "____";
mysql> select * from stu where name regexp "^[a-z0-9]{4}$";
```

#### 统计函数

```
MySQL的统计函数（聚合函数）：
max() min() count()  sum()  avg()

- 分组 group by 字段名[,字段名]
	统计班级classid值为2的男女生各多少人？
select sex,count(*) from stu where classid=2 group by sex;

- 排序：order by 字段名[,字段名] desc|asc
-- asc 默认升序  desc 降序
	获取每个班级的平均年龄，并按平均年龄降序，
  select classid,avg(age) from stu group by classid order by avg(age) desc;
  select classid,avg(age) anum from stu group by classid order by anum desc;
  
-- limit 关键字 查询部分数据 
-- 例如： .... limit m; 查询数据只显示前m条  
-- 例如： .... limit m,n; 排除前m条，然后再查询出前n条 
	统计每个班级的人数，按人数从大到小排序，取前3条。
	select classid,count(*) num from stu group by classid order by num desc limit 3;

分页公式：.... (页号-1)*页大小, 页大小;
```
#### 多表查询

```
表之间的关系有：1对1  1对多  多对多

1. 嵌套查询， 一个查询的结果是另外sql的条件
2. where关联查询  
3. join连接查询（左联，右联，内联）

-- 查询年龄最大的所有学生信息
mysql> select * from stu where age=(select max(age) from stu);
+----+---------+------+-----+---------+
| id | name    | age  | sex | classid |
+----+---------+------+-----+---------+
|  9 | xiaoli  |   29 | w   |       2 |
| 14 | zhangle |   29 | m   |       5 |
+----+---------+------+-----+---------+

-- 查询python02期的所有学生信息
mysql> select * from stu where classid=(select id from classes where name='python02');
mysql> select * from stu where classid in(select id from classes where name='python02');
```

```
where关联查询

已知：员工personnel表和部门department表，其中员工表中的did字段为部门表id主键关联。
	  查询所有员工信息，并显示所属部门名称
要求：显示字段：员工id  部门 姓名
mysql> select p.id,d.name,p.name from personnel p,department d where p.did = d.id;
	+----+-----------+-----------+
	| id | name      | name      |
	+----+-----------+-----------+
	|  2 | 人事部    | 李玉刚    |
	| 10 | 人事部    | 阿杜      |
	|  4 | 市场部    | 刘欢      |
```

```
连接join查询

左联：left join
右联：right join
内联：inner join

查询新闻信息，并补齐新闻类别信息
mysql> select n.id,n.title,t.name from news n,ntype t where n.ntid=t.id;
mysql> select n.id,n.title,t.name from news n inner join ntype t on n.ntid=t.id;
同上，但采用的是左联查询left join
mysql> select n.id,n.title,t.name from news n left join ntype t on n.ntid=t.id;

统计每个新闻类别下的新闻数量，采用where关联统计
mysql> select t.name,count(n.id) from ntype t,news n where t.id=n.ntid group by t.id;

统计每个新闻类别下的新闻数量，采用左联统计
mysql> select t.name,count(n.id) from ntype t left join news n on t.id=n.ntid group by t.id;
```

#### 1对1

```
已知如下表所示，商品类别信息表（具有两层类别关系，通过pid表示，0表示一级类别）
mysql> select * from type;
+----+-----------+------+
| id | name      | pid  |
+----+-----------+------+
|  1 | 服装      |    0 |
|  2 | 数码      |    0 |
|  3 | 男装      |    1 |
|  4 | 手机      |    2 |
|  5 | 相机      |    2 |
|  6 | 电脑      |    2 |
|  7 | 女装      |    1 |
|  8 | 童装      |    1 |
|  9 | 食品      |    0 |
| 10 | 零食      |    9 |
| 11 | 特产      |    9 |
| 12 | 休闲装    |    1 |
+----+-----------+------+


-- 查询二级类别信息，并关联出他们的父类别名称
mysql> select  t1.id,t1.name,t2.name  from type t1,type t2 where t1.pid!=0 and t1.pid=t2.id;
+----+-----------+--------+
| id | name      | name   |
+----+-----------+--------+
|  3 | 男装      | 服装   |
|  4 | 手机      | 数码   |
|  5 | 相机      | 数码   |
|  6 | 电脑      | 数码   |
|  7 | 女装      | 服装   |
|  8 | 童装      | 服装   |
| 10 | 零食      | 食品   |
| 11 | 特产      | 食品   |
| 12 | 休闲装    | 服装   |
+----+-----------+--------+
9 rows in set (0.01 sec)

--统计每个一级类别下都有多少个子类别。
mysql> select t1.id,t1.name,count(t2.id) from type t1,type t2 where t1.pid=0 and t1.id=t2.pid group by t1.id;
+----+--------+--------------+
| id | name   | count(t2.id) |
+----+--------+--------------+
|  1 | 服装   |            4 |
|  2 | 数码   |            3 |
|  9 | 食品   |            2 |
+----+--------+--------------+
3 rows in set (0.00 sec)
```

### 数据库的备份和导入

```
-- 数据库mydb备份
[root@localhost mnt]# mysqldump -u root -p mydb > mydb.sql
password：

-- 备份 mydb库中的stu表
[root@localhost mnt]# mysqldump -u root -p mydb stu > stu.sql
password：

-- 恢复数据（导入）注：mydb库要存在
[root@localhost mnt]# mysql -u root -p mydb < mydb.sql
[root@localhost mnt]# mysql -u root -p mydb < stu.sql
```

### 数据库日志的备份和导入

```
mysql日志
	vim /etc/my.cnf       产看下面这句话56行
	开启日志： 在mysql配置文件中开启：log-bin=mysql-bin
	
	查看bin-log日志:
	mysql>show binary logs;
	查看最后一个bin-log日志:
	mysql>show master status;
	
	此时就会多一个最新的bin-log日志
	mysql>flush logs;
	查看最后一个bin日志.
	mysql>show master status;

	mysql>reset master;
	清空所有的bin-log日志
	执行查看bin-log日志

	备份数据:
	mysqldump -u 用户名 -p 库名 -l -F 库名> 库名.sql
	其中：-F即flush logs，可以重新生成新的日志文件，当然包括log-bin日志 

	// Linux关闭MySQL的命令
	$mysql_dir/bin/mysqladmin -uroot -p shutdown
	// linux启动MySQL的命令
	$mysql_dir/bin/mysqld_safe &
```

### MySql的其他操作

```
1 表复制    		2表的索引			3视图
4 内置函数		   5 事务处理		    6 触发器
7 日志			8 有关慢查询操作	   9 数据库的恢复
```

```
1. MySQL的表复制
	复制表结构
	mysql> create table 目标表名 like 原表名;
	
	复制表数据
	mysql> insert into 目标表名 select * from 原表名; 

create table stu2 like stu;
复制stu 名为stu2 ;  只复制结构不复制内容

insert into stu2 select * from stu limit 5;
赋值stu数据前五条添加到 stu2;
```

```
2. 数据表的索引
	创建索引
	CREATE INDEX index_name ON table_name (column_list)
	CREATE UNIQUE INDEX index_name ON table_name (column_list)
	
	删除索引
	DROP INDEX index_name ON talbe_name
```

```
3. mysql视图
	创建视图:
	mysql> create view v_t1 as select * from t1 where id>4 and id<11;
	Query OK, 0 rows affected (0.00 sec)
	
	view视图的帮助信息:
	mysql> ? view
	ALTER VIEW
	CREATE VIEW
	DROP VIEW
	
	查看视图:
	mysql> show tables;
	
	删除视图v_t1:
	mysql> drop view v_t1;
```

```
4. MySQL的内置函数
	字符串处理函数
	---------------------------------------------
	*concat(s1,s2,…Sn) 连接s1,s2..Sn为一个字符串
	insert(str,x,y,instr)将字符串str从第xx位置开始，y字符串的子字符串替换为字符串str
	lower(str)将所有的字符串变为小写
	upper(str)将所有的字符串变为大写
	left(str,x)返回字符串中最左边的x个字符
	rigth(str,y)返回字符串中最右边的x个字符
	lpad(str,n,pad)用字符串pad对str最左边进行填充，直到长度为n个字符串长度
	rpad(str,n,pad)用字符串pad对str最右边进行填充，直到长度为n个字符串长度
	trim(str)  去掉左右两边的空格
	ltrim(str) 去掉字符串str左侧的空格
	rtrim(str) 去掉字符串str右侧的空格
	repeat(str,x)   返回字符串str重复x次
	replace(str,a,b)将字符串的的a替换成b
	strcmp(s1,s2)   比较字符串s1和s2
	substring(s,x,y)返回字符串指定的长度
	*length(str)  返回值为字符串str 的长度    

	数值函数
	-----------------------------------------------------
	*abs(x)    返回x的绝对值
	ceil(x)   返回大于x的最小整数值
	floor(x)  返回小于x的最大整数值
	mod(x,y)  返回x/y的取余结果
	rand()    返回0~1之间的随机数
	*round(x,y)返回参数x的四舍五入的有y位小数的值
	truncate(x,y) 返回x截断为y位小数的结果

	日期和时间函数
	---------------------------------------------------
	curdate()  返回当前日期,按照’YYYY-MM-DD’格式
	curtime()  返回当前时间,当前时间以'HH:MM:SS' 
	*now()      返回当前日期和时间,
	*unix_timestamp(date) 返回date时间的unix时间戳
	from_unixtime(unix_timestamp[,format])	返回unix时间的时间
	week(date)		返回日期是一年中的第几周
	year(date)      返回日期的年份
	hour(time)      返回time的小时值
	minute(time)    返回日time的分钟值
	monthname(date) 返回date的月份
	*date_fomat(date,fmt) 返回按字符串fmt格式化日期date值
	date_add(date,INTERVAL,expr type) 返回一个日期或者时间值加上一个时间间隔的时间值
	*datediff(expr,expr2)   返回起始时间和结束时间的间隔天数

	//统计时间戳647583423距离当前时间相差天数（生日天数（不考虑年份））
	mysql> select datediff(date_format(from_unixtime(647583423),"2017-%m-%d %h:%i:%s"),now());

	其他常用函数
	------------------------------------------------------
	*database() 返回当前数据库名
	version()   返回当前服务器版本
	user()		返回当前登陆用户名
	inet_aton   返回当前IP地址的数字表示 inet_aton("192.168.80.250");
	inet_ntoa(num) 返回当前数字表示的ip   inet_ntoa(3232256250);
	*password(str)  返回当前str的加密版本
	*md5(str)      返回字符串str的md5值
```

```
5. MySQL的事务处理
	关闭自动提交功能（开启手动事务）
	mysql> set autocommit=0;
	从表t1中删除了一条记录
	mysql> delete from t1 where id=11;
	此时做一个p1还原点:
	mysql> savepoint p1;
	再次从表t1中删除一条记录:
	mysql> delete from t1 where id=10;
	再次做一个p2还原点:
	mysql> savepoint p2;
	此时恢复到p1还原点，当然后面的p2这些还原点自动会失效: 
	mysql> rollback to p1;
	退回到最原始的还原点:
	mysql> rollback;
	回滚
	
	开启自动事务提交（关闭手动事务）
	mysql> set autocommit=1;
```

```
6. MySQL的触发器
	格式：1、触发器的定义：
	  CREATE TRIGGER trigger_name trigger_time trigger_event
		ON tbl_name FOR EACH ROW trigger_stmt
	  
	  说明：
	  # trigger_name：触发器名称
	  # trigger_time:触发时间，可取值：BEFORE或AFTER
	  # trigger_event：触发事件，可取值：INSERT、UPDATE或DELETE。
	  # tb1_name：指定在哪个表上
	  # trigger_stmt：触发处理SQL语句。
  
	示例：
		mysql> delimiter $$
		mysql> create trigger del_stu before delete on stu for each row
			-> begin
			->  insert into stu_bak values(old.id,old.name,old.sex,old.age,old.addtime);
			-> end;
			-> $$
		Query OK, 0 rows affected (0.05 sec)

		mysql> delimiter ;
```

```
7. mysql日志
	进入 /usr/my.cnf
	开启日志： 在mysql配置文件中开启：log-bin=mysql-bin
	
	查看bin-log日志:
	mysql>show binary logs;
	
	查看最后一个bin-log日志:
	mysql>show master status;
	
	此时就会多一个最新的bin-log日志
	mysql>flush logs;

	查看最后一个bin日志.
	mysql>show master status;

	mysql>reset master;
	清空所有的bin-log日志
	执行查看bin-log日志

	备份数据:
	mysqldump -uroot -pwei test -l -F '/tmp/test.sql'
	其中：-F即flush logs，可以重新生成新的日志文件，当然包括log-bin日志 

	// Linux关闭MySQL的命令
	$mysql_dir/bin/mysqladmin -uroot -p shutdown
	// linux启动MySQL的命令
	$mysql_dir/bin/mysqld_safe &
```

```
8、有关慢查询操作：
	开户和设置慢查询时间:
	vi /etc/my.cnf
	log_slow_queries=slow.log
	long_query_time=5
	查看设置后是否生效
	mysql> show variables like "%quer%"; 
	慢查询次数:
	mysql> show global status like "%quer%";
```

```
9 数据库的恢复
	1. 首先恢复最后一次的备份完整数据
	[root@localhost mnt]# mysql -u root -p mydemo<mydemo_2017-7-26.sql 
	Enter password: 
	
	2. 查看bin-log日志
	[root@localhost data]# mysqlbinlog --no-defaults mysql-bin.000009;
	  查找到恢复的节点
	  
	3. 执行bin-log日志文件，恢复最后一块的增量数据。 
	[root@localhost data]# mysqlbinlog --no-defaults --stop-position="802" mysql-bin.000009|mysql -u root -p123456 mydemo;

```

### Python3 Mysql数据库连接

```

	Python3 MySQL 数据库连接
======================================================

1. 什么是 PyMySQL？
	PyMySQL 是在 Python3.x 版本中用于连接 MySQL 服务器的一个库，Python2中则使用mysqldb。
	PyMySQL 遵循 Python 数据库 API v2.0 规范，并包含了 pure-Python MySQL 客户端库。
	
2. PyMySQL安装

	PyMySQL下载地址：https://github.com/PyMySQL/PyMySQL。
	
	2.1 使用pip命令进行安装：
	$ pip install PyMySQL
	
	2.2 使用 git 命令下载安装包安装(你也可以手动下载)：
	$ git clone https://github.com/PyMySQL/PyMySQL
	$ cd PyMySQL/
	$ python3 setup.py install
	
3. 数据库连接
    
   通过如下代码测试数据库连接
----------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","123456","mydb" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # 使用 execute()  方法执行 SQL 查询 
    cursor.execute("SELECT VERSION()")

    # 使用 fetchone() 方法获取单条数据.
    data = cursor.fetchone()

    print ("Database version : %s " % data)

    # 关闭数据库连接
    db.close()
    
    
4. 执行数据查询：
-------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","","mydemo" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # SQL 查询语句
    sql = "select * from stu limit %d" % (3)
    #sql = "select * from stu"

    try:
       # 执行SQL语句
       cursor.execute(sql)
       # 获取所有记录列表
       results = cursor.fetchall()
       for row in results:
          id = row[0]
          name = row[1]
          sex = row[2]
          age = row[3]
          classid = row[4]
           # 打印结果
          print ("id=%d,name=%s,sex=%s,age=%d,classid=%s" % (id,name,sex,age,classid))
    except:
       print ("Error: unable to fetch data")

    # 关闭数据库连接
    db.close()
 
5. 执行数据添加
---------------------------------------------------------------------
#!/usr/bin/python3

import pymysql

# 打开数据库连接
db = pymysql.connect("localhost","root","","mydemo" )

# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()

# SQL 插入语句
sql = "INSERT INTO stu(name,sex,age,classid) values('%s','%c','%d','%s')" % ('uu142','m',22,'lamp180') 

try:
   # 执行sql语句
   cursor.execute(sql)
   # 执行sql语句
   db.commit()
   print("ok: %d " % (cursor.rowcount))
except:
   # 发生错误时回滚
   db.rollback()

# 关闭数据库连接
db.close() 
    
6. 执行删除操作
---------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","","mydemo" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # SQL 删除语句
    sql = "delete from stu where id = '%d'" % (13)
    try:
       # 执行SQL语句
       cursor.execute(sql)
       # 提交修改
       db.commit()
    except:
       # 发生错误时回滚
       db.rollback()

    # 关闭数据库连接
    db.close()
    
    
数据库查询操作：  
    Python查询Mysql使用 fetchone() 方法获取单条数据, 使用fetchall() 方法获取多条数据。
        fetchone(): 该方法获取下一个查询结果集。结果集是一个对象
        fetchall(): 接收全部的返回结果行.
        rowcount: 这是一个只读属性，并返回执行execute()方法后影响的行数。
        
        
        
pip命令
------------------------------------------------------------
列出已安装的包：
    $ pip list
    $ pip freeze     # 查看自己安装的

安装软件（安装特定版本的package，通过使用==, &gt;=, &lt;=, &gt;, &lt;来指定一个版本号）**
    $ pip install SomePackage
    $ pip install 'Markdown<2.0'
    $ pip install 'Markdown>2.0,<2.0.3'
    
卸载软件pip uninstall SomePackage
    $ pip uninstall SomePackage
    
下载所需的软件包：
    $ pip download SomePackage -d directory 
    例如下载PyMySQL软件包
    $ pip download PyMySQL -d D:/pypackage

安装下载好的软件包文件
    $ pip install 目录/软件包文件名
    如安装PyMySQL软件包
    $ pip install D:/pypackage/PyMySQL-0.7.11-py2.py3-none-any.whl
```
### 修改完结符

```
\d  $$     把最后的完结符号由;改为$$ 用于写代码时用
```

### python3 Mysql数据库连接

```

	Python3 MySQL 数据库连接
======================================================

1. 什么是 PyMySQL？
	PyMySQL 是在 Python3.x 版本中用于连接 MySQL 服务器的一个库，Python2中则使用mysqldb。
	PyMySQL 遵循 Python 数据库 API v2.0 规范，并包含了 pure-Python MySQL 客户端库。
	
2. PyMySQL安装

	PyMySQL下载地址：https://github.com/PyMySQL/PyMySQL。
	
	2.1 使用pip命令进行安装：
	$ pip install PyMySQL
	
	2.2 使用 git 命令下载安装包安装(你也可以手动下载)：
	$ git clone https://github.com/PyMySQL/PyMySQL
	$ cd PyMySQL/
	$ python3 setup.py install
	
3. 数据库连接
    
   通过如下代码测试数据库连接
----------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","123456","mydb" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # 使用 execute()  方法执行 SQL 查询 
    cursor.execute("SELECT VERSION()")

    # 使用 fetchone() 方法获取单条数据.
    data = cursor.fetchone()

    print ("Database version : %s " % data)

    # 关闭数据库连接
    db.close()
    
    
4. 执行数据查询：
-------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","","mydemo" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # SQL 查询语句
    sql = "select * from stu limit %d" % (3)
    #sql = "select * from stu"

    try:
       # 执行SQL语句
       cursor.execute(sql)
       # 获取所有记录列表
       results = cursor.fetchall()
       for row in results:
          id = row[0]
          name = row[1]
          sex = row[2]
          age = row[3]
          classid = row[4]
           # 打印结果
          print ("id=%d,name=%s,sex=%s,age=%d,classid=%s" % (id,name,sex,age,classid))
    except:
       print ("Error: unable to fetch data")

    # 关闭数据库连接
    db.close()
 
5. 执行数据添加
---------------------------------------------------------------------
#!/usr/bin/python3

import pymysql

# 打开数据库连接
db = pymysql.connect("localhost","root","","mydemo" )

# 使用 cursor() 方法创建一个游标对象 cursor
cursor = db.cursor()

# SQL 插入语句
sql = "INSERT INTO stu(name,sex,age,classid) values('%s','%c','%d','%s')" % ('uu142','m',22,'lamp180') 

try:
   # 执行sql语句
   cursor.execute(sql)
   # 执行sql语句
   db.commit()
   print("ok: %d " % (cursor.rowcount))
except:
   # 发生错误时回滚
   db.rollback()

# 关闭数据库连接
db.close() 
    
6. 执行删除操作
---------------------------------------------------------------------
    #!/usr/bin/python3

    import pymysql

    # 打开数据库连接
    db = pymysql.connect("localhost","root","","mydemo" )

    # 使用 cursor() 方法创建一个游标对象 cursor
    cursor = db.cursor()

    # SQL 删除语句
    sql = "delete from stu where id = '%d'" % (13)
    try:
       # 执行SQL语句
       cursor.execute(sql)
       # 提交修改
       db.commit()
    except:
       # 发生错误时回滚
       db.rollback()

    # 关闭数据库连接
    db.close()
    
    
数据库查询操作：  
    Python查询Mysql使用 fetchone() 方法获取单条数据, 使用fetchall() 方法获取多条数据。
        fetchone(): 该方法获取下一个查询结果集。结果集是一个对象
        fetchall(): 接收全部的返回结果行.
        rowcount: 这是一个只读属性，并返回执行execute()方法后影响的行数。
```
### pip

```
      
pip命令
------------------------------------------------------------
列出已安装的包：
    $ pip list
    $ pip freeze     # 查看自己安装的

安装软件（安装特定版本的package，通过使用==, &gt;=, &lt;=, &gt;, &lt;来指定一个版本号）**
    $ pip install SomePackage
    $ pip install 'Markdown<2.0'
    $ pip install 'Markdown>2.0,<2.0.3'
    
卸载软件pip uninstall SomePackage
    $ pip uninstall SomePackage
    
下载所需的软件包：
    $ pip download SomePackage -d directory 
    例如下载PyMySQL软件包
    $ pip download PyMySQL -d D:/pypackage

安装下载好的软件包文件
    $ pip install 目录/软件包文件名
    如安装PyMySQL软件包
    $ pip install D:/pypackage/PyMySQL-0.7.11-py2.py3-none-any.whl
```
    