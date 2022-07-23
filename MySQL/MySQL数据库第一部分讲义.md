[TOC]

###  MySQL数据库第一部分讲义

#### 一 动手做（TODO重点任务六个）：
##### 任务1. 掌握MySQL数据库的安装及配置(参考安装文档)
##### 任务2. 会MySQL数据库常用基本操作命令
  以管理员身份打开cmd窗口，然后看mysql服务是否启动，如果没有启动，输入启动服务命令：
>net start mysql
>
>备注：mysql是服务名称
```
     1. 登录数据库系统命令  
      输入mysql -u root -p 然后回车
      再输入密码，即可登录。
      
     2. 查看现有的数据库
      show databases;
     
     3. 创建数据库
      create database [if not exists] 数据库名;
      --if no exists是可选参数
     
     4. 选择使用一个数据库
      use 数据库名;
      
     5. 查看当前数据库下所有的表
      show tables;  
      
     6. 查看表结构
      desc  数据表名;
      
     7. 查看表详细结构：
      show create table 表名;
     
     8. 删除一个数据库
      drop database [if exists]  数据库名;
      --if exists 是可选参数
```
> 如果要关闭服务，在以管理员打开的cmd窗口里输入net stop mysql


##### 任务3. 会安装和使用MySQL数据库的图形化工具SQLYog和Navicat 
##### 任务4. 查看当前有哪些数据库，使用DDL语句创建school数据库并使用该数据库
##### 任务5. 使用DDL语句创建一个用户数据表t_user。
>备注：用户表字段：用户ID、用户名(3-15 个字符)、密码（MD5加密）、真实姓名(必须是汉字，2-4个汉字 )、性别、手机号码(最初建表时取名为tel，数据类型为int)、职务(必须是汉字，2-10个汉字 )、备注。

##### 任务6. 修改数据表t_user的结构
>备注：给用户表增加一个字段status(表示用户状态），将t_user的手机号码的字段名称由tel改为telephone,类型由原来的int改为varchar 。

#### 二 理解并掌握（技术要点及面试题）

##### 1.什么是SQL（Structured Query Language）？

> SQL指结构化查询语言，全称是 Structured Query Language。SQL 是用于访问和处理数据库的可以与数据库交互的计算机语言。
> SQL 是一种 ANSI（American National Standards Institute 美国国家标准化组织）标准的计算机语言。
> SQL属于非过程化语言。


##### 2. 支持SQL语言的RDBMS数据库有哪些？
> RDBMS 指关系型数据库管理系统，全称 Relational Database Management System。
> RDBMS 是 SQL 的基础，同样也是所有现代数据库系统的基础，支持SQL语言的RDBMS数据库有 MS SQL Server、IBM DB2、Oracle、MySQL 以及 Microsoft Access。
> RDBMS 中的数据存储在数据库对象数据表中。
> 数据表是相关的数据项的集合，它由列和行组成的二维表。

##### 3. SQL语言分类有哪些？(面试题)
###### (1)DDL（Data Define Language）数据定义语言
>       DDL是Data Define  Language 的简称，是数据定义语言，主要用于定义和管理数据库 的各种对象。如：数据表，视图，索引。
>       对数据表进行创建，修改，删除的操作使用的SQL语言属于DDL（Data Define Language）数据定义语言。
>       DDL针对的是数据表的结构，不是数据表里的数据。

###### (2)DML（Data Manipulation Language）数据操纵语言
>       DML(Data Manipulation Language)数据操作语言：用于插入或更新修改和删除数据。
>
>       - INSERT INTO...   
>
>       - UPDATE  ...SET...  
>
>       - DELETE FROM

###### (3)DQL（Data Query Language）数据查询语言
> DQL（Data Query Language）数据查询语言主要用于查询检索数据。
DQL数据查询语言用于检索数据库中的数据，主要是SELECT语句，它在操作数据库的过程中使用最为频繁。SELECT语句是数据库中非常重要的SQL语句，主要用于数据查询。

###### (4)DCL（Data Control Language）数据控制语言
> DCL(Data Control Language)数据控制语言： 用于定义数据库用户权限等。
> DCL数据控制语言用于执行权限授予和权限收回操作。
> 主要包括GRANT和REVOKE两条命令。其中，GRANT命令用于给用户或角色授予权限，而REVOKE命令则用于收回用户或角色所具有的权限。
>
>   - GRANT...TO..;
>   - REVOKE  ...FROM...;

###### (5)TCL(Transaction Control Language）事务控制语言
>   TCL(Transaction Control Language）事务控制语言用于维护数据的一致性，包括COMMIT、ROLLBACK和SAVEPOINT 语句。
>   其中，COMMIT语句用于提交对数据库的更改，ROLLBACK语句用于取消对数据库的更改，而SAVEPOINT语句则用于设置保存点。

###### 面试题1
> 1．数据定义语言是用于（ B ）的方法。
> A.确保数据的准确性	 	   B、定义和修改数据结构		
> C、查看数据		              D、删除和更新数据
> 2.操作数据库的过程中使用最为频繁的SQL是（D）。
> A.CREATE      B、DROP		
> C、SHOW       D、SELECT

##### 4. MySQL的数据类型有哪些？  

(1) 整数类型

![](G:\Java1018\02_数据库\图片\1.png)
> 备注：建表时如果定义整数类型int ,不指定长度，默认精度是11位，相当于int(11) 。

(2) 浮点类型和定点类型

![](G:\Java1018\02_数据库\图片\2.png)


> 备注：
>  float(m,d) 	单精度浮点型     8位精度(4字节)     m表示整数和小数的总位数，d小数位
> double(m,d) 	双精度浮点型    16位精度(8字节)   m表示整数和小数的总位数，d小数位
> 假设一个字段定义为double(6,3)，如果插入一个数123.45678,实际数据库里存的是123.457，但总个数还以实际为准，即6位。整数部分最大是3位，如果插入数12.123456，存储的是12.1235，如果插入12.12，存储的是12.1200.

(3) 时间日期类型

![](G:\Java1018\02_数据库\图片\3.png)

(4) 字符串类型

> CHAR：255 固定字符串   例如：char(5) 
> VARCHAR：65535 可变字符串     例如：varchar(5)
> TEXT 文本  （保存较大文本，字符串数据）
> TINYTEXT、MEDIUMTEXT、TEXT、LONGTEXT
> ENUM 单个值
> SET 多个值 

(5) 二进制类型

![](G:\Java1018\02_数据库\图片\4.png)

> 注意：常用的数据类型有int,char,varchar,date,datetime,text等

##### 6.MySQL中常见的约束条件有哪些？
> (1) 主键约束PRIMARY KEY（PK）
	唯一标识表中的某一条记录，相当于非空+唯一，用PRIMARY KEY表示
	一个表中只能有一个主键，可以由一个字段表示，也可以由多个字段联合(联合主键）组成
	如果采用联合主键时，每个字段都不能为空。
> (2) 非空约束
     非空约束（not null）要确保字段值不能为空。	
> (3) 唯一约束
     确保所在的字段不出现重复值，但是允许出现 NULL 值，UNIQUE表示。
> (4) 外键约束 FOREIGN KEY (FK)
     用 REFERENCES 表示参照，主要作用：确保相关的两个字段之间的参照关系,
	 被参照的表称为主表，参照主表的表被称之子表，子表中的参照字段可以为空或者来自主表,
     删除子表中的数据时，主表中的数据不被删除。
	 反之，删除主表中的数据时，如果子表中有参照记录，则主表记录不能删除。
> (5) auto_increment   自增 （放在主键上）
     在表中插入数据时，如果不对该字段赋值，会自动在已有最大值的基础上加1 。
> (6) default  默认值
     在表中插入数据时，如果不给有默认值的字段赋值，该字段将使用默认值。
> (7) unsigned - 无符号
     说明此字段为无符号整数类型。
> (8) zerofill   表示0填充
     定义了数据类型的长度，如果实际位数小于定义的长度，显示时会在左边用0填充。

###### 面试题2
> 在设计数据库时，要充分考虑数据的完整性或准确性。下面关于PRIMARY KEY和UNIQUE的描述错误的是（  　 ）〔选择二项）
> A.PRIMARY KEY用来在表中设置主键，主键列的值是可以重复的，用来唯一标识表中的每一条记录
> B.PRIMARY KEY列不可以有null值, 而UNIQUE列是可以有null的
> C.PRIMARY KEY列和UNIQUE列都不可以有null值
> D.设为UNIQUE的列的值是不能重复的，用来唯一区别UNIQUE列的值

##### 7.如何创建数据表？（面试，口述代码）
> (1) 数据库基本表的创建
> 语法格式：
```sql
  CREATE TABLE  [ IF NOT EXISTS] 表名(  
     字段1   数据类型1 主键，
     字段2   数据类型2，
     字段3   数据类型3，
     字段4   数据类型4 
  );
```
> 备注：IF NOT EXISTS是可选参数的。如果不指定if not exists语句,创建同名表的时候就会报错。
>
> 指定了if not exists语句来创建表,虽然表名是存在的,但是创建没有报错,但是存在警告信息,警告中信息是表已经存在了.
>
> 另:两次创建的表,如果字段不同,表名相同,还是不允许创建.

> 例如：
```sql
CREATE TABLE t_class(
    cno    int(4) primary key ，
    cname  varchar(15) 
);
--带IF NOT EXISTS参数
CREATE TABLE IF NOT EXISTS t_class(
    cno    int(4) primary key ，
    cname  varchar(15)
);
```
> (2) 带约束条件的数据表的创建
语法格式：
```sql
CREATE TABLE  表名(  
    字段1   数据类型1   约束条件1 约束条件2 ... ，
    字段2   数据类型2   约束条件，
    字段3   数据类型3，
    字段4   数据类型4 
)  ENGINE=InnoDB DEFAULT CHARSET=utf8;
```
> 注意：ENGINE=InnoDB 表示引擎是InnoDB,MySQL默认的，这个引擎支持事务。
> DEFAULT CHARSET=utf8 表示建表时默认编码为utf-8


> 示例1：
```sql
CREATE TABLE t_stu(
    sno    int(8) primary key  auto_increment，
    sname  varchar(30) not null，
    sex    char(4) default '男'，
    age    int(3) unsigned，
    cno    int(4) 
);
```
> 创建数据表时添加主键约束和外键约束
> 示例2：

```sql
CREATE TABLE t_stu(
    sno    int(8) not null auto_increment，
    sname  varchar(30) not null，
    sex    char(4) default '男'，
    age    int(3) unsigned，
    cno    int(4)，
    primary key(sno)，
    constraint fk_stu_cno foreign key(cno) references t_class(cno)  
);
```
> 备注：如果是联合主键，就把联合主键的字段写在primary key后面的括号里，
> 例如：primary key (sid,cid)

##### 8.如何修改数据表的结构？
######   1) 如何修改表名?
　语法：ALTER TABLE 旧表名 RENAME [TO] 新表名
  > 例如：
```sql
  ALTER TABLE t_stu RENAME TO t_student; 
```
######  2) 如何修改字段?
   语法：ALTER TABLE 表名 CHANGE 旧属性名 新属性名 新属性类型;
> 示例1：修改字段类型
```sql
ALTER TABLE t_student CHANGE stu_id stu_id int(6);
```
>  示例2：修改字段名和类型
```sql
ALTER TABLE t_student CHANGE stu_id sid int(5);
```
> 注意：MySQL中修改字段类型时用CHANGE或MODIFY都可以，但是MODIFY不能同时修改字段名和类型。Oracle中是使用关键字MODIFY，不能使用CHANGE。


######   3) 如何增加字段？
   语法：ALTER TABLE 表名 ADD 新属性名  新属性类型 [完整性约束] [first | after 原有字段];
> (1) 新增无完整性约束的字段示例：
```sql
ALTER TABLE t_student ADD email varchar(20);
```
> (2) 新增有完整性约束的字段示例：
```sql
ALTER TABLE t_student ADD age int not null;
```
> (3) 将字段添加到第一位示例：
```sql
ALTER TABLE t_student ADD sid int primary key first;
```
> (4) 将字段添加到某个字段之后示例：
```sql
ALTER TABLE t_student ADD address varchar(100) after telephone;
```
######   4) 如何删除字段？
语法：ALTER TABLE 表名 DROP 属性名;
> 示例：
```sql
ALTER TABLE t_student DROP address;
```
######  5) 如何给已创建好的表增加主键约束？
语法：
ALTER TABLE 表名1   ADD   PRIMARY KEY(主键列名) ；

> 示例：
```sql
ALTER TABLE t_class  ADD  PRIMARY KEY (cno);
```
######  6) 如何删除主键约束？
语法：
ALTER TABLE 表名1   DROP PRIMARY KEY；

> 示例：
```sql
ALTER TABLE t_class  DROP PRIMARY KEY;
```
######  7) 如何给已创建好的表增加外键约束？
语法：
ALTER TABLE 表名1   ADD CONSTRAINT  约束名  foreign key(外键列名)  REFERENCES 表名2（主键名）；

> 示例：
```sql
ALTER TABLE t_student ADD CONSTRAINT fk_t_stu_cno FOREIGN KEY(cno) REFERENCES t_class(cno);
```


######  8) 如何删除外键？
语法：ALTER TABLE 表名 DROP foreign key 外键名

> 示例：
```sql
ALTER TABLE t_student DROP foreign key fk_t_stu_cno;
```
> 注意：MYSQL在建外键后,会自动建一个同名的索引。所以要删除外键，需要同时删除这个同名索引。
> 删除索引：
```sql
ALTER TABLE t_student DROP index fk_t_stu_cno;
```

##### 9. 如何删除数据表？
语法：DROP TABLE [IF EXISTS] 表名;
> 示例：
```sql
DROP TABLE t_test;
-- 带IF EXISTS参数
DROP TABLE IF EXISTS t_test;
```
> ###### 注意：
> (1). 在删除表的时候要谨慎，以避免误删，导致数据丢失，所以在删除前最好做好备份工作
> (2). 在删除表时，如果当前表存在外键，则先删除外键，再删除该表
> (3). 在删除有关联外键表时，则先删除子表[存在外键的表]，再删除主表
> (4). 不带IF EXISTS参数删除不存在的表会报错说表不存在，带有参数IF EXISTS 不会报错。

##### 10.DROP TABLE 和TRUNCATE TABLE的异同？（面试题）
>  (1).DROP TABLE
>   - DDL语言
>   - 用于删除表（表的结构、属性以及索引也会被删除）
>   - 无法回退,彻底删除
>    
>  (2).TRUNCATE TABLE
>   -  DDL语言
>   -  默认所有的表内容都删除，表结构不会被删除
>   -  无法回退 
>   -  删除速度比delete快   

#### 三 课后任务（TODO 能够独立完成)
##### 任务一 创建好下面的数据表并且加上约束条件。（TODO 4个任务）

> 任务1、创建学生表t_student（学号sno，姓名sname，性别sex，出生日期birthday，电话号码tel，电子邮箱email, 班号cno） 
> 备注：添加约束：学号为主键，姓名：不为空， 性别 默认为“男” ，电子邮箱为唯一约束
> 
> 任务2 、创建课程表t_course（课程编号cno，课程名称cname，学分credit，学时hours,授课老师teacher）
> 备注：课程编号为主键，自增。
>
> 任务3、创建学生选课成绩表t_scgrade（学号sno，课程编号cno，成绩grade）
> 备注：学号和课程编号是联合主键，学号和课程表都是外键
>
> 任务4、创建班级表t_class（班号cno，班级名称cname），给上面建好的学生表的列cno添加外键约束。

##### 任务二  给上面创建好的数据表修改结构。（TODO 4个任务）

> 任务1 给学生表t_student（学号sid，姓名sname，性别sex，年龄age，电话号码tel，电子邮箱email）  增加一个字段（家庭地址address），然后修改家庭地址的字段。
>
> 任务2 给课程表t_course（课程编号cid，课程名称cname，学分credit，授课老师teacher）,增加一个上课地点的字段，删除这个字段
>
>
> 任务3 创建班级表t_class（班号cno，班级名称cname），给上面建好的学生表增加一列（班号），并给它添加外键约束。
>
>
> 任务4 有一个人创建了一张员工表myemp(员工号eno，员工姓名ename，工作职位job，工资sal)，要想知道每个员工在哪个部门，想知道给他们发了多少奖金， 该表需要如何修改。把表名修改成t_employee  ，把工资名称sal修改成salary , 并且把该字段的数据类型修改为double 。

##### 任务三 根据UOL联合开放实验室信息管理系统需求分析，手写用户表，角色表，角色_权限表，权限表的建表语句，添加约束。（TODO ）

