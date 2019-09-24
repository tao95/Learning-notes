#一.	数据库的基本概念
	1.数据库的英文名称：DataBase,简称：DB
	2.什么是数据库？
		*用来存储和管理数据的仓库
	3.数据库的特点
		*持久化存储数据，其实数据库就是一个文件系统
		*方便存储和管理数据
		*使用统一的方式来管理数据库 --SQL语言
	4.常用的数据库软件
		*Oracle: 收费的大型数据库，Oracle公司的产品，收购了sun公司，收购了MYSQL。
		*MYSQL: 开源免费的数据库。小型的数据库，已经被Oracle公司收购，MYSQL6.x版本也开始收费。
		*SQLServer: 微软公司的收费的中型数据库，C#,.NET等语言常用。
		*DB2: IBM公司收费的数据库，常用在银行系统中。
		*SyBase：已经退出历史舞台，但该公司提供了一个非常专业的数据建模工具PowerDesigner。
		*SQLite: 嵌入式的小型数据库，应用于手机端，Android开发。
		*Mongodb:
	在Web应用中，使用最多的是MYSQL数据库，原因如下：
		1）开源、免费
		2）功能足够强大，可以应付web应用开发(最高支持千万级别的并发访问)


#二.	MySQL数据库软件
	1.安装
		参考百度上各个版本的安装教程，这儿就不做过多说明。
	2.卸载
		a.首先去mysql的安装目录找到my.ini配置文件，复制出"datadir=C:/ProgramData/MySQL/MySQL Server 5.7/Data"。
		b.然后通过控制面板卸载MySQL。
		c.最后删除C:/ProgramData目录下的MySQL文件夹。
	3.配置
		*MySQL服务启动
			a. 手动
			b. 通过cmd 输入命令services.msc 打开服务的窗口
			c. 使用管理员打开cmd
				*输入net start mysql 5.7 :启动mysql服务
				*输入net stop mysql 5.7 :关闭mysql服务
	4.MySQL登录
		*mysql -u用户名 -p密码，eg：mysql -uroot -proot
		*mysql -hIP地址 -uroot -p连接目标的密码，eg:mysql -h127.0.0.1 -uroot -proot
		*mysql --host=ip -user=root --password=连接目标的密码
	5.MySQL目录
		*安装目录
		*数据目录

#三.	SQL语言的学习
	1.什么是SQL?
		Structured Query Language: 结构化查询语言
		其实就是定义了操作所有关系型数据库的规则。每一种数据库操作的方式存在不一样的地方，称为“方言”。
	2.SQL通用的语法
		a. SQL语句可以单行或多行进行书写，以分号结尾。
		b. 可以使用空格和缩进增强语句的可读性。
		c. MySQL数据库的SQL语句不区分大小写，关键字建议使用大写。
		d. 3种注释
			* 单行注释：-- 注释内容 或 # 注释内容（MySQL特有）
			* 多行注释：/* 注释内容 */
	3.SQL分类
		1）DDL(Data Definition Language)数据定义语言
			用来定义数据库对象：数据库、表、列等。关键字：create,drop,alter等
		2) DML(Data Manipulation Language)数据操作语言
			用来对数据库中表的数据进行增删改。关键字：insert,delete,update等。
		3) DQL(Data Query Language)数据查询语言
			用来查询数据库中表的记录(数据)。关键字：select,where等
		4）DCL(Data Control Language)数据库控制语言(了解)
			用来定义数据库的访问权限和安全级别，及创建用户。关键字：GRANT、REVOKE等。

#四.DDL:操作数据库、表
	1.操作数据库：CRUD
		1)C(Create):创建
			*创建数据库
				*create database 数据库名称;
			*创建数据库，判断不存在，再创建;
				*create database if not exists 数据库名称
			*创建数据库，并指定字符集
				*create database 数据库名称 character set 字符集名;
			*创建数据库，判断是否存在，并制定字符集为gbk
				*create database if not exists 数据库名称 character set gbk;
		2)R(Retrieve):查询
			*查询所有的数据库名称;
				*show databases;
			*查询某个数据库的字符集：查询某个数据库的创建语句
				*show create database 数据库名称;
		3)U(Update):修改、更新
			*修改数据库的字符集
				*alter database 数据库名称 character set 字符集名称;
		4)D(Delete):删除
			*删除数据库
				*drop database 数据库名称;
			*判断数据库存在，存在再删除
				*drop database if exists 数据库名称;
		5)使用数据库
			*查询当前正在使用的数据库名称
				*select database();
			*使用数据库
				*use 数据库名称;


	2.操作表
		1) C(Create):创建
			语法：
				create table 表名(
					列名1 数据类型1，
					列名2 数据类型2，
					列名3 数据类型3，
					...
					列名n 数据类型n
				);
				*注意：最后一列，不需要加逗号(,)
			数据库类型：
				*int:整数类型
				*double:小数类型
				*date:日期，只包含年月日，yyyy-MM-dd
				*datetime:日期，只包含年月日时分秒  yyyy-MM-dd HH:mm:ss
				*timestamp:时间错类型 包含年月日时分秒  yyyy-MM-dd HH:mm:ss
					如果将来不给这个字段赋值，或赋值为null，则默认使用当前的系统时间，来自动赋值
				*varchar:字符串
			创建表：
				create table student(
					id int,
					name varchar(32),
					age int,
					socre double(4,1),
					birthday date,
					insert_time timestamp
				);
			复制表：
				*create table 表名 like 被复制的表名;
		2) R(Retrieve):查询
			*查询某个数据库中所有的表名称
				*show tables;
			*查询表的结构
				*desc 表名;
		3) U(Update):修改
			*修改表名:
				alter table 表名 rename to 新的表名;
			*修改字符集:
				首先查看原表的字符集
					show create table 表名;
				然后进行修改
					alter table 表名 character set 字符集名称;
			*添加一列:
				alter table 表名 add 列名 数据类型;
			*修改列的名称和类型:
				alter table 表名 change 列名 新列名 新数据类型;
				alter table 表名 modify 列名 新数据类型;
			*删除列:
				alter table 表名 drop 列名;
		4) D(Delete):删除
			*drop table 表名;
			*drop table if exists 表名;
			