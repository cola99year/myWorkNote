

# 1. 数据库概述

### 英文简写

DB**：数据库（**Database**）**

DBMS**：数据库管理系统（**Database Management System**）**==**NoSQL**

SQL**：结构化查询语言（**Structured Query Language**）**



### MySQL历史

MySQL5.5发布，InnoDB存储引擎MySQL的默认存储引擎。

MySQL社区版免费就是开源，还有收费版。

Oracle收购sun，sun收购MySQL。



### 为什么用数据库？

内存断电即失，数据库可以持久化！

因此为什么不直接用128GB的内存，应用无时无刻都在内存中打开，还要硬盘作甚？

### DB与DBMS

数据库（存放数据的仓库）与数据管理系统（管理仓库的软件）

我的DB就在data文件夹里边

<img src="https://i0.hdslb.com/bfs/album/271209fd841b92704319b93815beed011cbde017.png" alt="image-20220519004219898" style="zoom:50%;" />



### RDBMS 与 非RDBMS

即关系型数据库与非关系型数据库

MySQL与redis（键值对）、MongoDB（文档型）

即   “数据类似表格的关系型数据库”	与 “键值对的关系的非关系型数据库”



### E-R模型、E-R关系

> E-R（entity-relationship，实体-联系）模型中有三个主要概念是： 实体集 、 属性 （字段）、 联系集 。

- 一个实体集（class）对应于数据库中的一个表（table），
- 一个实体（instance）则对应于数据库表中的一行（row），也称为一条记录（record），即Java的一个new对象。
- 一个属性（attribute）对应于数据库表中的一列（column），也称为一个字段（field）。



实体联系

一对一：用户的常用信息对应其不常用的信息

一对多：一个部门有多个员工

多对多：一个学生可以选多门课，一门课可以被多个学生选。

自我引用：员工对应老板，老板也是员工，老板的老板就是自己

### 💕ORM思想体现：

Object Relational Mapping 	对象关系映射

1. 数据库中的一个表 <---> Java或Python中的一个类 

2. **表中的一条数据 <---> 类中的一个对象（或实体）** 
3. 表中的一个列 <----> 类中的一个字段、属性(field)




# 2. 安装与登录命令

### 1、Windows登录MySQL命令

cmd以管理员形式，执行下图命令：

![image-20220519013303497](https://i0.hdslb.com/bfs/album/aaa5cd401f52fbc67131ef29a2f39bba30598834.png)

如果你电脑还安装了5版本的MySQL，想登录5版本的可以这样：

```shell
#root就是MySQL的用户名
mysql -u root -P13306 -p
```

因为5版本的mysql端口号不同



### 连接远程的MySQL

原来远程的数据库也是直接可视化连接，我真是瓜怂啊，哈哈哈。



### Linux安装MySQL教程

https://blog.csdn.net/weixin_40614372/article/details/106518993；注意看评论区，我有更正

**Linux的MySQL配置信息**

```ini
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
socket=/tmp/mysql.sock
 
[mysqld]
# skip-name-resolve
 
# 设置3306端口
port=3306
socket=/tmp/nysql.sock
 
# 是否需要密码登录
# skip-grant-tables
 
# 设置mysq1的安装目录
basedir=/usr/local/mysql
 
# 设置mysq1数据库的数据的存放目录
datadir=/usr/local/mysql/data
 
# 允许最大连接数
max_connections=200
 
# 服务端使用的字符集默认为8比特编码的Iatin1字符秀
character-set-server=utf8
default-time-zone='+08:00'
# 创建新表时将使用的默认存储引随
default-storage-engine=INNODB
 
# lover_case_table_name=1
max_allowed_packet=16M
default-authentication-plugin=mysql_native_password
```

1



# 3. 查询入门

## 3.0 概念

### SQL是门语言

不同的SQL，他们大多数的基本语句是遵循美国标准局规定的SQL语句。

但是还是会有小部分特色的语句，所有SQL语句相当于一通百通咯。



**SQL也是一门语言。与java、C语言并列**。





### DDL、DML、DCL、DQL、TCL

即SQL功能的分类，主要三大类DDL、DML、DCL

> **DDL**（Data Definition Languages、**数据定义语言**）

这些语句定义了不同的数据**库、表、视图、触发器、用户、索引**等==数据库对象==，还可以用来创建、删除、修改数据库和数据表的结构。主要的语句关键字包括 **CREATE 、 DROP 、 ALTER** 等。



> **DML**（Data Manipulation Language、**数据操作语言**）

操作表里的记录，重中之重！

用于增、删、更新和查数据库记录，并检查数据完整性。主要的语句关键字包括 INSERT 、 DELETE 、 UPDATE 、 SELECT 等。SELECT是SQL语言的基础，最为重要。



> **DCL**（Data Control Language、**数据控制语言**）

访问权限和安全级别

用于定义数据库、表、字段、用户的访问权限和安全级别。主要的语句关键字包括 **GRANT 、 REVOKE 、 COMMIT 、 ROLLBACK 、 SAVEPOINT** 等。



> **DQL**（Data Query Language、**数据查询语言**）

最频繁的操作，把他从DML分离出来

因为查询语句使用的非常的频繁，所以很多人把查询语句单拎出来作为DQL一类。



> **TCL** （Transaction Control Language，**事务控制语言**）

把他从DCL分离出来的，将 COMMIT 、 ROLLBACK 取出来



## 3.1 开始前，先学规则

### 单双引号

- use my_databse；限相当于你点击哪一个数据库选中的操作。
- 字符串型和日期时间类型的数据可以使用**单引号**（' '）表示，如：'张三'
- **字段**尽量使用**双引号**（""），而且不建议省略as ，如：字段起中文别名select age as "年龄"

### 大小写敏感问题

- MySQL **在** Windows **环境下是大小写不敏感的**

  MySQL **在** Linux **环境下是大小写敏感的**
  
  数据库名、表名、表的别名、变量名是严格区分大小写的
  
  关键字、函数名、列名(或字段名)、列的别名(字段的别名) 是忽略大小写的。
  
  **推荐采用统一的书写规范：**
  
  数据库名、表名、表别名、字段名、字段别名等都小写
  
  SQL 关键字、函数名、绑定变量等都大写

### SQL语句\G与分号

> 每条命令以 ; 或 \g 或 \G 结束，分号等同于 \g 或 \G

作用：**在终端中**，你没分号或者\G，他就以为你没写完SQL语句，与下一句的拼接起来了，就报错。

呈现效果不同：

<img src="https://i0.hdslb.com/bfs/album/15527c331249e7e03509c54c4ad00c2c8e8cd5b8.png" alt="image-20220525114608260" style="zoom:67%;" />



### 三种注释

单行注释：#注释文字(MySQL特有的方式) 

单行注释：-- 注释文字(--后面必须包含一个空格。) 

多行注释：/* 注释文字 */ 

## 3.2 Source命令执行sql文件

方式1：命令导入，不能有分号

> source 文件绝对路径

![image-20220519152035652](https://i0.hdslb.com/bfs/album/6167e1745d52095e8aaaf25bd127d6579e8e66a2.png)

方式2：可视化软件导入

执行sql脚本文件



## 3.3 Select查询

### 0、单双引号问题

别名最好别漏as，全称alias

**列名**的别名规定**双引号**，真正的数据信息规定**单引号**！

MySQL可能不介意单双引号，但是以后工作可能用Oracle，不按规则那就会错！

### 1、查询入门

```sql
use atguigudb;
-- 伪表dual，凑句子用；
select 1 from dual; 

SELECT * from employees;

select employee_id,last_name,salary
from employees;

```

### 2、字段起别名as

全称alias

别名不能在where中使用，可在order by使用。

因为语句的执行顺序是from→where→select→order by，分清先后顺序

```sql
-- 别名
select employee_id as emp_id,last_name,salary as "工资"
from employees;
```

### 3、数据去重distinct

注意：DISTINCT 需要放到**所有列名的前面**，如果写成 SELECT salary, DISTINCT department_id FROM employees 会出现语法逻辑错误，前面又没去重，后面又去重了，数据不就矛盾了

```sql
# distinct
SELECT distinct department_id
from employees;
```





### 4、空值不可参与运算💕IFNULL(x，y)函数

**空值**不可参与加减乘除的运算中，因为谁跟空值运算都会变成null值！

使用==IFNULL(x，y)函数==，就可以避免该情况：如果x不为NULL，则返回x，否则返回y 

```sql
-- 反例
-- 利率commission_pct为空，年收入跟他运算，年收入都为空了
SELECT salary,salary*12*(1+commission_pct) as "年收入",commission_pct
from employees;

-- 正例
-- 添加IFNULL，就可以避免该情况
SELECT salary,salary*12*(1+IFNULL(commission_pct,0)) as "年收入",commission_pct
from employees;
```

### 5、着重号``

表名等名称与数据库关键字冲突，但是建表时候，不要与之冲突，实在坚持冲突，就加着重号``

```sql
SELECT * from `order`;
```

### 6、查询常数

给表填入不存在的常数列，相当于java定义静态常量

```sql
-- 随便写入常量
SELECT "可乐公司的员工",first_name from employees;
```

![image-20220519214814230](https://i0.hdslb.com/bfs/album/9134a4d3a563244b7808509643470f2782ec2980.png)

### 7、显示表结构

```sql
desc employees;
```



![image-20220519215203528](https://i0.hdslb.com/bfs/album/94b1962c0bdfcd0f017e5d29d036b462bb8bfb43.png)





### 8、where查询英文：大小写不区分问题

查询King，由于MySQL在Windows不分大小写，King写为king小写，竟然也能查询到！！

实在**是MySQL的不严谨**！！！在Linux区分大小写，注意！！

```sql
-- 查询部门id为90的人
SELECT * from employees where department_id=90;

SELECT * from employees where last_name='King';
```





# 4. 运算符查询

### 1、SQL的加号只表示加法运算

> 在SQL中，+没有连接的作用，==只表示加法运算==。此时，会将字符串转换为数值（隐式转换）

```sql
# 在SQL中，+没有连接的作用，就表示加法运算。此时，会将字符串转换为数值（隐式转换）
SELECT 100 + '1'  # 在Java语言中，结果是：1001。 
FROM DUAL;
# 结果为101；

SELECT 100 + 'a' #此时将'a'看做0处理
FROM DUAL;
# 结果100；
```

### 2、除号默认带浮点

```sql
SELECT  100 / 2, 100 DIV 0     # 分母如果为0，则结果为null
FROM DUAL;
```

结果为50.0000，null；

### 3、取模运算（求余数）

```sql
# 取模运算： % mod
SELECT 12 % 3,12 % 5, 12 MOD -5,-12 % 5,-12 % -5
FROM DUAL;
```

余数是正是负，由被除数决定！

![image-20220519222347238](https://i0.hdslb.com/bfs/album/66b43840780c154121ef3d916b50563c0b801726.png)

### 4、取模之求id为偶数员工

```sql
SELECT employee_id 
from employees 
where employee_id%2=0;
```

### 5、=号的原理

salary = 6000;	系统去找为6000的则为真标志1，不是6000则假为0，然后返回全部判断为1的结果！

commission_pct = NULL;  **NULL参与运算都是NULL，没有真也没有假，返回值就是为空了**

```sql
SELECT last_name,salary,commission_pct
FROM employees
#where salary = 6000;
WHERE commission_pct = NULL;  #此时执行，不会有任何的结果
```

### 6、<=>  "安全等于"

**为NULL而生**！等于空的意思

```sql
#查询表中commission_pct为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct <=> NULL;
```

### 7、IS NULL、ISNUL()、IS NOT NULL

**ISNULL()是一个函数**：如下练习2

```sql
# 练习1：查询表中commission_pct为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct IS NULL;
# 练习2
SELECT last_name,salary,commission_pct
FROM employees
WHERE ISNULL(commission_pct);

# 练习3：查询表中commission_pct不为null的数据有哪些
SELECT last_name,salary,commission_pct
FROM employees
WHERE commission_pct IS NOT NULL;
```

### 8、least、greatest

找最大值、最小值，

LENGTH是字节数长度

```SQL
SELECT LEAST('g','b','t','m'),GREATEST('g','b','t','m')
FROM DUAL;
-- ASCI最小是b，最大是t

-- 下面同理，LEAST(first_name,last_name)是比较ASCI，LEAST(LENGTH(first_name),LENGTH(last_name))是长度谁长谁短，输出短的字符数是多少
SELECT LEAST(first_name,last_name),LEAST(LENGTH(first_name),LENGTH(last_name))
FROM employees;
```

ascii码对照表：

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg.doc.docsou.com%2Fpic%2F4d8c5f9a49406d95b4647265%2F1-728-jpg_6_0_______-715-0-0-715.jpg&refer=http%3A%2F%2Fimg.doc.docsou.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=auto?sec=1664984400&t=3c78457120893537b3ed32212fd8d9f2)





### 9、BETWEEN AND 闭区间

- **BETWEEN** xx **AND** xx	**包含边界**
- **NOT BETWEEN** xx **AND** xx
- xx **&&** xx       salary >= 6000 && salary <= 8000
- xx **or** xx

查询工资6000到8000

```sql
#查询工资在6000 到 8000的员工信息
SELECT employee_id,last_name,salary
FROM employees
where salary between 6000 and 8000;
#WHERE salary >= 6000 && salary <= 8000;

#查询工资不在6000 到 8000的员工信息
SELECT employee_id,last_name,salary
FROM employees
WHERE salary NOT BETWEEN 6000 AND 8000;
#where salary < 6000 or salary > 8000;
```

### 10、IN、NOT IN

IN就是或的意思，有满足的都列出来。

查询部门id是10,20,30的

```sql
SELECT last_name,department_id
from employees
-- 反例
-- where department_id=10 or 20 or 30;
-- 正例
#where department_id=10 or department_id=20 or department_id=30;
where department_id in(10,20,30);
```

### 11、LIKE模糊查询

_代表一个不确定的字符，两个就`__`

```sql
#练习：查询last_name中包含字符'a'的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%';

#以字符'a'开头的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE 'a%';

#练习：查询last_name中包含字符'a'且包含字符'e'的员工信息
#写法1：
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%' AND last_name LIKE '%e%';
#写法2：
SELECT last_name
FROM employees
WHERE last_name LIKE '%a%e%' OR last_name LIKE '%e%a%';

# _ ：代表一个不确定的字符，两个就__

#练习：查询第3个字符是'a'的员工信息
SELECT last_name
FROM employees
WHERE last_name LIKE '__a%';

#练习：查询第2个字符是_且第3个字符是'a'的员工信息
#需要使用转义字符: \ 
SELECT last_name
FROM employees
WHERE last_name LIKE '_\_a%';
```

查询第2个字符是_且第3个字符是'a'

![image-20220520004214487](https://i0.hdslb.com/bfs/album/bd3fa542a3e6af288d8f1794749c9da9ff8f4e02.png)

### 12、regexp正则表达式（略）

REGEXP、RLIKE :正则表达式

REGEXP运算符用来匹配字符串，语法格式为： expr REGEXP 匹配条件 。如果expr满足匹配条件，返回

![image-20220520005646284](https://i0.hdslb.com/bfs/album/58ae4077a84758af0382b2305f20254cad054d20.png)

```sql
-- 小荷才露尖尖角
-- $结尾
-- .
-- [ab]
SELECT 'shkstart' REGEXP '^shk', 'shkstart' REGEXP 't$', 'shkstart' REGEXP 'hk'
FROM DUAL;

SELECT 'atguigu' REGEXP 'gu.gu','atguigu' REGEXP '[ab]'
FROM DUAL;
```

### 13、XOR逻辑运算符^

<img src="https://i0.hdslb.com/bfs/album/af5ed9dfffb4549a4beb4d47c0f62449cdc63255.png" alt="image-20220520010354519" style="zoom: 67%;" />

> 注意：
>
> AND和OR可以同时使用，先运算AND的，最后才运算OR

即查询  **“id为50，工资不大于6000的” 和   “id不为50，工资大于6000的”**；

```sql
# XOR :追求的"异"
SELECT last_name,salary,department_id
FROM employees
WHERE department_id = 50 XOR salary > 6000;
```

### 14、位运算符

位运算符是在二进制数上进行计算的运算符。位运算符会先将操作数变成二进制数，然后进行位运算，最后将计算结果从二进制变回十进制数。

<img src="https://i0.hdslb.com/bfs/album/ba6062714e47f1e79b71e6d4ddfc5bc94bf99c90.png" alt="image-20220520011855385" style="zoom: 67%;" />

---



左移：下面整体往左移动！

---



<img src="https://i0.hdslb.com/bfs/album/02adb0b46caa5d7e8541fd5882ead4b2b12ecd07.png" alt="image-20220520012052636" style="zoom:67%;" />

---



# 5. 排序&分页查询

### 排序就用：order by

SQL如果没有用排序，**默认排序方式是我们的添加的顺序！**

ASC 升序，使用了排序`ORDER BY age`，**默认是升序**

DESC 降序

```sql
SELECT salary as sa
from employees
-- where不可用别名
where salary>4000
ORDER BY sa DESC;
```

**语句执行顺序：**查完结果再排序，排序完再分页

字段的别名不能在where中使用，可在order by使用。因为语句的执行顺序是from→where→select→order by，



### 二级排序

```sql
#4. 二级排序

-- 显示员工信息，按照department_id的降序排列，salary的升序排列
SELECT employee_id,salary,department_id
FROM employees
ORDER BY department_id DESC,salary ASC;
```



### limit分页

> 需求：每页显示pageSize条记录，此时显示第pageNo页：
> 公式：LIMIT (pageNo-1) * pageSize**,**pageSize;
>
> limit 第一个参数表示从第几条开始，第二参表示查几个
>
> **比如limit 1,2；表示从第2条数据开始查询，查询2条数据！**



> 若知道只想返回一条数据，**加limit 1可以提高性能**！

==同理，要几条就limit几条，limit 6；limit 5；==



```sql
# 需求1：每页显示20条记录，此时显示第1页
SELECT employee_id,last_name
FROM employees
LIMIT 0,20;  #逗号别漏！


# 需求2：每页显示20条记录，此时显示第2页
SELECT employee_id,last_name
FROM employees
LIMIT 20,20;  #逗号别漏！


# 需求3：每页显示20条记录，此时显示第3页
SELECT employee_id,last_name
FROM employees
LIMIT 40,20;  #逗号别漏！


```

关键字写的顺序

```sql
SELECT employee_id,last_name,salary
FROM employees
WHERE salary > 6000
ORDER BY salary DESC
#limit 0,10;
LIMIT 10;
```



> MySQL8新特性：OFFSET：limit参数的颠倒
>
> 有107条数据，我们只想要显示第 32、33 条数据怎么办呢？==LIMIT 2 OFFSET 31;==

```sql
#练习：表里有107条数据，我们只想要显示第 32、33 条数据怎么办呢？

SELECT employee_id,last_name
FROM employees
LIMIT 31,2;

#2.3 MySQL8.0新特性：LIMIT ... OFFSET ...

#练习：表里有107条数据，我们只想要显示第 32、33 条数据怎么办呢？

SELECT employee_id,last_name
FROM employees
LIMIT 2 OFFSET 31;
```

 LIMIT 可以使用在MySQL、PGSQL、MariaDB、SQLite 等数据库中使用，表示分页。

**不能使用在**SQL Server、DB2、Oracle！



# 6. 多表查询&连接查询

###  6.0 多表查询的概念

> **多表查询，也称为关联查询**，指两个或更多个表一起完成查询操作。别和子查询搞混

前提条件：这些一起查询的表之间是**有关系的**（一对一、一对多），它们之间**一定是有关联字段**，这个

关联字段**可能建立了外键**，也可能没有建立外键。比如：员工表和部门表，这两个表依靠“部门编号”进

行关联。

**有n个表实现多表的查询，则需要至少n-1个连接条件**

<img src="https://i0.hdslb.com/bfs/album/badb3b2fb516b85415474bdf988fbb8fb7bd639e.png" alt="image-20220520211328761" style="zoom: 50%;" />

---



### 6.1 两张表做连接时用不用join的区别？

> 都是多表查询、关联查询，返回结果和性能都**没区别**，SQL是对不用join的情况进行优化了！

前提：存在student（sid，sname，cid）和class（cid，cname）两表
 查询：选出所有学生，同时返回班级名称
不用join：

```sql
 SELECT sid，sname，cid, cname
 FROM student，class
 WHERE student.cid=class.cid;
```

 用join：

```sql
 SELECT sid，sname，cid, cname
 FROM student
 INNER JOIN class
 ON student.cid=class.cid;
```





### 6.2 两表相同字段连接——多表查询

查询员工对应的部门名字，涉及员工表、部门表。

```sql
-- 反例出现笛卡尔积的错误
#错误的原因：缺少了多表的连接条件
#错误的实现方式：每个员工都与每个部门匹配了一遍。
SELECT employee_id,department_name
FROM employees,departments;  #查询出2889条记录


-- 多表查询的正确方式：需要有连接条件，增加where连接条件

SELECT employee_id,department_name
FROM employees,departments
#两个表的连接条件,这里会忽略有NULL的情况
WHERE employees.department_id = departments.department_id;
```

### 6.3 SQL优化：指明字段所在表

**从sql优化的角度**，建议多表查询时，每个**字段前都指明其所在的表**。

```sql
SELECT employees.employee_id,departments.department_name,employees.department_id
FROM employees,departments
WHERE employees.`department_id` = departments.department_id;
```

### 6.4 表起别名

from给表起别名后，在SELECT和WHERE中使用表的别名，且**不能再使用表的原名了**。

```sql
-- 因为执行顺序是from→where→select→order by
SELECT emp.employee_id,dept.department_name,emp.department_id
FROM employees emp,departments dept
WHERE emp.`department_id` = dept.department_id;
```



参照字段起别名：[2、给列名起别名](###2、给列名起别名)



### 6.5 两表无相同字段的多表查询——非等值连接

上文都是等值连接，下面是**非等值连接**，两表之间没有任何相同或者有关联的字段。

```sql
SELECT e.last_name,e.salary,j.grade_level
FROM employees e,job_grades j
where e.`salary` between j.`lowest_sal` and j.`highest_sal`;
```



### 6.6 自连接——自己连自己

上面的例子都是非自连接，**自连接就是E-R的自我引用**

如图所示：因为字段无老板对应的名字，因为老板名字也在员工名字列。因此通过id的自连接，查询出老板的名字

---

<img src="https://i0.hdslb.com/bfs/album/5539552ae60dbe5d0afa8495cb8d6d98e9bdc30e.png" alt="image-20220520214338227" style="zoom:67%;" />

---



```sql
-- 查询员工id,员工姓名及其管理者的id和姓名
SELECT emp.employee_id,emp.last_name,mgr.employee_id,mgr.last_name
FROM employees emp ,employees mgr
WHERE emp.`manager_id` = mgr.`employee_id`;
```



### 6.7 内连接与外连接

#### 概念

例如：员工通过部门id，查询他的部门名字是什么。

---

![image-20220520215623993](https://i0.hdslb.com/bfs/album/2784ee22aa81bddf3d43572a1e6c1a4a5837cff1.png)

---



**内连接**【`INNER JOIN`，可省略inner】：通过部门id查询得到部门名字的，返回的查询结果就是内连接；而部门id为null的员工，不符合查询结果就无法返回！

<img src="https://i0.hdslb.com/bfs/album/7f09d6ccb76d2574a5f8abdf99324b8a06f5c70e.png" alt="image-20220906203400015" style="zoom:50%;" />

**外连接**：

1. 左外连接：把**部门id为null的员工**，与内连接合并到查询结果一并返回！`left join`

<img src="https://i0.hdslb.com/bfs/album/7ab444fcdfd37980dfeafc2c21893c6286b893e4.png" alt="image-20220906203502908" style="zoom:50%;" />

2. 右外连接：把**没有员工的部门**，与内连接合并到查询结果一并返回！`right join`

3. 满外连接：左右外连接一同返回！











#### 代码例子

[问题1]()：测试内连接

**join**就是用到哪个表，**on**就是两表之间的等值连接条件！

```sql
-- 阿里巴巴不允许三个表以上连表查询！
SELECT last_name,department_name,city
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`
JOIN locations l
ON d.`location_id` = l.`location_id`;
```



[问题2]()：查询**所有的**员工的last_name,department_name,city信息 

​		注意：看到**所有**，你都必须打起精神，所以**要考虑==表关联字段==为空的员工的情况，**也就是外连接查询！！

左外连接：

```sql
--查询所有的员工的last_name,department_name信息
SELECT last_name,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;
```

右外连接：

```sql
SELECT last_name,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;
```

满外连接：**mysql不支持**FULL OUTER JOIN，说到Oracle时可以谈到这个！

```sql
SELECT last_name,department_name
FROM employees e FULL OUTER JOIN departments d
ON e.`department_id` = d.`department_id`;
```









# ✅实现7种joins

## 1、三表禁止join

> 【强制】**超过三个表禁止 join**。且需要 join 的字段，**数据类型必须一致**， 被关联的字段**必须有索引**。
>
> 也就是说：双表 join 也要注意表索引、SQL 性能； 

**评论：以空间换时间，表字段冗余就行，阿里有钱，硬盘想加多大就多大**；

SELECT last_name,department_name,city
FROM employees e **JOIN** departments d
**ON** e.`department_id` = d.`department_id`
**JOIN** locations l
**ON** d.`location_id` = l.`location_id`;



## 2、union和union all

Union：并集去重

**Union all：并集不去重**

---

<img src="https://i0.hdslb.com/bfs/album/6320172f88699a912abe0db830d4a633345a6f3d.png" alt="image-20220520223838720" style="zoom: 80%;" />

---



## 3、7种Joins



![image-20220520225402903](https://i0.hdslb.com/bfs/album/d7228a080813a4d715b2580fa79e3c086a5e17ab.png)

> SQL实现7种joins

易错：右外-内连接

SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;

-- 是e.`department_id` IS NULL;	而不是 = null；
-- 而且是e，为什么是e的，看上面的图，空白的部分是不是属于A的

```sql
# 中图：内连接
SELECT employee_id,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`;

# 左上图：左外连接
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`;

# 右上图：右外连接
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;

# 左中图：左外-内连接
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL;

-- 左中图：找的是员工表中，员工里部门为空的部分，e.`department_id` is null也可以哦
-- 右中图：找的是部门表中，部门里没有员工的部分，若d.`department_id` is null，找的就是部门号为空的部分了

# 右中图：右外-内连接
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;


# 左下图：满外连接
# 方式1：左外 UNION ALL 右外-内连接
-- 注意只有一个分号，是一条语句

SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;


# 方式2：左外-内连接 UNION ALL 右外

SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`;



# 右下图：左中图  UNION ALL 右中图
SELECT employee_id,department_name
FROM employees e LEFT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE d.`department_id` IS NULL
UNION ALL
SELECT employee_id,department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;
```







## 4、natural join与using

### 自然连接

帮你自动查询两张连接表中`所有相同的字段`，然后进行`等值连接`

```sql
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.`department_id` = d.`department_id`
AND e.`manager_id` = d.`manager_id`;

# NATURAL JOIN : 它会帮你自动查询两张连接表中`所有相同的字段`，然后进行`等值连接`。
-- 等同上面的SQL
SELECT employee_id,last_name,department_name
FROM employees e NATURAL JOIN departments d;
```

### using

对指定的一个字段就行的等值连接

```sql
新特性2:USING
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
ON e.department_id = d.department_id;

-- 即
SELECT employee_id,last_name,department_name
FROM employees e JOIN departments d
USING (department_id);
```



# 7. SQL的函数

## 7.1、单行函数

1. 只对一行进行变换，每行**返回一个**结果。
2. 单行函数**可以嵌套使用**，参数是一列或一个值。
3. 类似传一个或几个参数，过滤后只返回一个结果

单行函数可嵌套：

```sql
#单行函数可以嵌套：四舍五入保留2位，再截断位0位的小数，直接截断不是四舍五入
SELECT TRUNCATE(ROUND(3.1415926,2),0)
FROM DUAL;
```



### 数值函数☆

![image-20220521235958765](https://i0.hdslb.com/bfs/album/976294fad9f6d70043d92ef15df1786c4ec9121e.png)



### 进制转换

![image-20220522000301866](https://i0.hdslb.com/bfs/album/bd66fa42cd10d502076f5d2cf4bac86caae2e4b1.png)

### 三角函数与指数

略

### 字符串函数☆

①对字符串的操作！

![image-20220522001305007](https://i0.hdslb.com/bfs/album/1bd529a09ce392b865985b4671bca33ef9b359e0.png)

②`NULLIF`

![image-20220522002141044](https://i0.hdslb.com/bfs/album/762c283e5362086c3d0ece6a52922d121fff7bfe.png)

③

略了，太多了。。。。



### 日期时间函数😍

时间戳、from_unixtime

> ①返回日期时间：如SELECT NOW();

![image-20220522003854278](https://i0.hdslb.com/bfs/album/bc320a0d71381842be3d49852e1c43479ee8e256.png)

> ②日期与时间戳转换
>
> mysql处理的时间戳是十位的，为秒级别的。java获取的是毫秒级13位的，要÷1000，才能交给mysql的from_unixtime函数处理

| 函数                     | 用法                                                |
| ------------------------ | --------------------------------------------------- |
| UNIX_TIMESTAMP()         | 返回10位数的当前时间戳，即：SELECT UNIX_TIMESTAMP() |
| UNIX_TIMESTAMP(date)     | 传入指定的时间后，返回时间戳，如传入NOW()           |
| FROM_UNIXTIME(timestamp) | 传入10位数时间戳，转换为普通格式时间                |

例子：

<img src="https://i0.hdslb.com/bfs/album/62d5f15958e574443dd6b6413ec683207b7c27cc.png" alt="image-20220906213552413" style="zoom: 67%;" />

更多内容看pdf：07章4.3开始。



### case流程控制函数

> 先想明白，什么时候会用到case，就是相当于java的if else、Switch case的情况！

即类似java的if else、Switch case……	增加了一个修饰条件的列，本质并没有改动原来的数据。

属于**分支语**句，循环语句的流程控制呢？MySQL本身就是循环，把数据一条条循环读取出来。

![image-20220522132855472](https://i0.hdslb.com/bfs/album/81080ccf1ca2016033744fe109c7497234ddb02a.png)

注意：

CASE WHEN ... THEN ...WHEN ... THEN ... ELSE ... END   ：类似于java的if ... else if ... else if ... else

CASE ... WHEN ... THEN ... WHEN ... THEN ... ELSE ... END  ：类似于java的swich ... case...

```sql
#4.1 IF(VALUE,VALUE1,VALUE2)
-- "details" 相当于起别名，否则，用你的整个流程语句来当列名
SELECT last_name,salary,IF(salary >= 6000,'高工资','低工资') "details"
FROM employees;

SELECT last_name,commission_pct,IF(commission_pct IS NOT NULL,commission_pct,0) "details",
salary * 12 * (1 + IF(commission_pct IS NOT NULL,commission_pct,0)) "annual_sal"
FROM employees;

#4.2 IFNULL(VALUE1,VALUE2):看做是IF(VALUE,VALUE1,VALUE2)的特殊情况
SELECT last_name,commission_pct,IFNULL(commission_pct,0) "details"
FROM employees;

#4.3 CASE WHEN ... THEN ...WHEN ... THEN ... ELSE ... END
# 类似于java的if ... else if ... else if ... else
SELECT last_name,salary,CASE WHEN salary >= 15000 THEN '白骨精' 
			     WHEN salary >= 10000 THEN '潜力股'
			     WHEN salary >= 8000 THEN '小屌丝'
			     ELSE '草根' END "details",department_id
FROM employees;

SELECT last_name,salary,CASE WHEN salary >= 15000 THEN '白骨精' 
			     WHEN salary >= 10000 THEN '潜力股'
			     WHEN salary >= 8000 THEN '小屌丝'
			     END "details"
FROM employees;

#4.4 CASE ... WHEN ... THEN ... WHEN ... THEN ... ELSE ... END
# 类似于java的swich ... case...
/*
查询部门号为 10,20, 30 的员工信息, 
若部门号为 10, 则打印其工资的 1.1 倍, 
20 号部门, 则打印其工资的 1.2 倍, 
30 号部门,打印其工资的 1.3 倍数,
其他部门,打印其工资的 1.4 倍数

*/
SELECT employee_id,last_name,department_id,salary,CASE department_id WHEN 10 THEN salary * 1.1
								     WHEN 20 THEN salary * 1.2
								     WHEN 30 THEN salary * 1.3
								     ELSE salary * 1.4 END "details"
FROM employees;
```



### 加密与解密函数

次要知识，因为都在java后端加密，不需要MySQL加密



### 查询MySQL配置信息

![image-20220522123003111](https://i0.hdslb.com/bfs/album/bb8f654780ecb1694757c0608e4b9bf3d46f895b.png)

### 其他函数

挑两个不错的，详情看pdf

![image-20220522123029766](https://i0.hdslb.com/bfs/album/b14c0f266b8dedfff23213bea09ad9d79a202e26.png)

## 7.2、聚合函数

> （**多行参数、分组函数**）：即传一个字段，字段里是**多个**、**多行**参数，如AVG(salary），只返回一个结果。
>
> MySQL不支持聚合函数嵌套使用，**Oracle可以**。



### 常用的聚合函数类型

- AVG()    #会剔除NULL的行数，即107条数据中有NULL值，底层求平均就不是÷107了，
- SUM() 
- MAX() 
- MIN() 
- COUNT()    #数数，也是不计算null值，也就是说AVG = SUM / COUNT

```sql
#③ 公式：AVG = SUM / COUNT  永远成立，因为AVG就是不要NULL！
SELECT AVG(salary),SUM(salary)/COUNT(salary),
AVG(commission_pct),SUM(commission_pct)/COUNT(commission_pct),
SUM(commission_pct) / 107
FROM employees;

#需求：查询公司中平均奖金率
#错误的！
-- 奖金率为空值的人，你不应该把他们剔除了，他们为NULL他们的奖金率不就是0，人头数也要计算在内！！
SELECT AVG(commission_pct)
FROM employees;

#正确的：
SELECT SUM(commission_pct) / COUNT(IFNULL(commission_pct,0)),
AVG(IFNULL(commission_pct,0))
FROM employees;
```



>**问题：用**count(*)**，**count(1)**，**count(**列名**)**谁好呢**?
>
>MyISAM引擎的表：是没有区别的。这种引擎内部有一计数器在维护着行数。
>
>Innodb引擎的表：用count(*)，count(1)直接读行数，复杂度是O(n)，因为innodb真的要去数一遍。但好于具体的count(列名)。具体解释在：MySQL高级篇
>
>count(**列名**)：列中有空值的话，就不算记录数了，行数计算就会算少！



### group by分组

> FROM ...,...-> ON -> (LEFT/RIGNT  JOIN) -> WHERE -> **GROUP BY** -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT
>
> **理解：**
>
> 按照性别字段分组，group by sex，即男、女分成一组了，
>
> select 中除了sex字段，就不能带有其他字段了，因为那个字段不止一个值，**除非那个字段也分组**：GROUP BY sex,hobby;
>
> ![image-20220627211551736](https://i0.hdslb.com/bfs/album/061d589ffd685016695a43446c601caefc18695b.png)
>
> ```sql
>SELECT sex,hobby,count(*)
> FROM grouptest
>GROUP BY sex,hobby;  #注意
> ```





①单个分组

```sql
#需求：查询各个部门的平均工资，最高工资
SELECT department_id,AVG(salary),SUM(salary)
FROM employees
GROUP BY department_id
```

**②组里边再分组**☆

两种方式顺序是一样的：

![image-20220522140655978](https://i0.hdslb.com/bfs/album/5884f400267058fcb327a6e61bd9dbd5782ceeb8.png)

```sql
#需求：查询各个department_id,job_id的平均工资
#方式1：
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY  department_id,job_id;
#方式2：
SELECT job_id,department_id,AVG(salary)
FROM employees
GROUP BY job_id,department_id;


#错误的！
SELECT department_id,job_id,AVG(salary)
FROM employees
GROUP BY department_id;

#结论1：SELECT中出现的非组函数的字段必须声明在GROUP BY 中。
#      反之，GROUP BY中声明的字段可以“不出现”在SELECT中。
```





with rollup（了解）：统计所有分组的数量。参考：[一张图搞懂with rollup](https://blog.csdn.net/m5776775/article/details/103687585)

```sql
MySQL中GROUP BY中使用WITH ROLLUP

SELECT department_id,AVG(salary)
FROM employees
GROUP BY department_id WITH ROLLUP;

#需求：查询各个部门的平均工资，按照平均工资升序排列
SELECT department_id,AVG(salary) avg_sal
FROM employees
GROUP BY department_id
ORDER BY avg_sal ASC;

#说明：当使用ROLLUP时，不能同时使用ORDER BY子句进行结果排序，即ROLLUP和ORDER BY是互相排斥的。
#错误的：
SELECT department_id,AVG(salary) avg_sal
FROM employees
GROUP BY department_id WITH ROLLUP
ORDER BY avg_sal ASC;
```



### having

FROM ...,...-> ON -> (LEFT/RIGNT  JOIN) -> WHERE -> **GROUP BY** -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT

我们知道，多表连接条件和过滤条件是用where。但是当**过滤条件中有聚合函数时候，那么where就要用having代替**！

聚合函数不能写在where中，如果过滤条件不是聚合函数的，就写到where中，**where与having分工合作，效率更高！**

聚合函数用了**having，必须连着group by用**，否则出的结果将没有意义，为什么（看下文）？

区分出：

- 过滤出数据的最大值MAX()>1000的数据

- 过滤出数据的值>1000的数据

  ```java
  这样的当然不需要跟group by，where都可以替代
  SELECT salary
  FROM employees
  HAVING salary>10000;
  
  这样用having配合group by 才有意义
  SELECT MAX(salary)
  FROM employees
  GROUP BY department_id
  HAVING MAX(salary)>10000;
  ```

  

```sql
练习：查询各个部门中最高工资比10000高的部门信息
#错误的写法：聚合函数不能写在where中
SELECT department_id,MAX(salary)
FROM employees
WHERE MAX(salary) > 10000
GROUP BY department_id;


#要求1：如果过滤条件中使用了聚合函数，则必须使用HAVING来替换WHERE。否则，报错。
#要求2：HAVING 必须声明在 GROUP BY 的后面。

#正确的写法：
SELECT department_id,MAX(salary)
FROM employees
GROUP BY department_id
HAVING MAX(salary) > 10000;

#要求3：开发中，我们使用HAVING的前提是SQL中使用了GROUP BY。


#练习：查询部门id为10,20,30,40这4个部门中最高工资比10000高的部门信息
#方式1：推荐，执行效率高.  不要全部放在having
SELECT department_id,MAX(salary)
FROM employees
WHERE department_id IN (10,20,30,40)
GROUP BY department_id
HAVING MAX(salary) > 10000;

```





# 😀SQL底层执行顺序😀

由于执行顺序因此，非聚合函数的过滤条件要写在where，前期就把大部分的数据过滤了，后期处理更复杂的一些过滤，执行效率不就高了！

也解释了having为什么写在group by后的原因了！

```sql
#sql99语法：
SELECT ....,....,....(存在聚合函数)


FROM ... (LEFT / RIGHT)JOIN ....ON 多表的连接条件 
(LEFT / RIGHT)JOIN ... ON ....
WHERE 不包含聚合函数的过滤条件
GROUP BY ...,....
HAVING 包含聚合函数的过滤条件


ORDER BY ....,...(ASC / DESC )
LIMIT ...,....


每走一步，都会生成一个虚拟表，即一个处在中间过程不是最终结果的表，I一步一步地执行，最终才生成一个结果表，返回给我们！

#4.2 SQL语句的执行过程：
分页再排序只会更复杂……
#FROM ...,...-> ON -> (LEFT/RIGNT  JOIN) -> WHERE -> GROUP BY -> HAVING -> SELECT -> DISTINCT -> ORDER BY -> LIMIT

```

记忆：在校（FROM）男生（WHERE）不同姓氏身高（GROUP BY）的最大值（HAVING）查询（SELECT），最后从高到低排序（ORDER BY）、分页

# 8. 子查询

> 结论：在SELECT中，除了`GROUP BY` 和 `LIMIT`之外，**其他位置都可以声明子查询！**

## 8.1、子查询小试牛刀

需求：谁的工资比Abel的高？

先查出Abel的工资，再拿Abel的工资为过滤条件，得出工资比他高的人。

```sql
#1. 由一个具体的需求，引入子查询
#需求：谁的工资比Abel的高？

#自连接
SELECT e2.last_name,e2.salary
FROM employees e1,employees e2
WHERE e2.`salary` > e1.`salary` #多表的连接条件
AND e1.last_name = 'Abel';

#子查询
--  括号内为内查询，相对的就是外查询
SELECT last_name,salary
FROM employees
WHERE salary > (
		SELECT salary
		FROM employees
		WHERE last_name = 'Abel'
		);

#2. 称谓的规范：外查询（或主查询）、内查询（或子查询）

/*
- 子查询（内查询）在主查询之前一次执行完成。
- 子查询的结果被主查询（外查询）使用 。
- 注意事项
  - 子查询要包含在括号内
  - 将子查询放在比较条件的右侧，如上文例子
  - 单行操作符对应单行子查询，多行操作符对应多行子查询
*/
```

## 8.2、单行子查询

单行子查询，**内查询返回的结果只有一个数据**，即为单行子查询。

**空值问题**：若返回的这个数据为空值NULL，则返回的表也是NULL表，0行

> **不等于**的比较符号：<> 
>
> 空值专属---**安全等于**：<=>

### 1、普通

```sql
#题目1：返回job_id与141号员工相同，salary比143号员工多的员工姓名，job_id和工资

SELECT last_name,job_id,salary
FROM employees
WHERE job_id = (
		SELECT job_id
		FROM employees
		WHERE employee_id = 141
		)
AND salary > (
		SELECT salary
		FROM employees
		WHERE employee_id = 143
		);


#题目2：查询与141号员工的manager_id和department_id相同的其他员工
#的employee_id，manager_id，department_id。
#方式1：
SELECT employee_id,manager_id,department_id
FROM employees
WHERE manager_id = (
		    SELECT manager_id
		    FROM employees
		    WHERE employee_id = 141
		   )
AND department_id = (
		    SELECT department_id
		    FROM employees
		    WHERE employee_id = 141
		   )
AND employee_id <> 141;-- 排除141员工自己，因为要的是其他员工。
```

### 2、having单行子查询

```sql
#题目：查询最低工资大于110号部门最低工资的部门id和其最低工资

SELECT department_id,MIN(salary)
FROM employees
WHERE department_id IS NOT NULL
GROUP BY department_id
HAVING MIN(salary) > (
			SELECT MIN(salary)
			FROM employees
			WHERE department_id = 110
		     );
```

### 3、 case单行子查询

先想明白，什么时候会用到case，就是相当于java的if else、Switch case的情况！

```sql
#题目：显式员工的employee_id,last_name和location。
#若员工的department_id跟【location_id=1800的department_id】相同，则location为’Canada’，其余则为’USA’。

SELECT employee_id,last_name,CASE department_id 
							WHEN (SELECT department_id
                                  	 FROM departments
                                  	 WHERE location_id = 1800)
                               THEN 'Canada'
							ELSE 'USA' END as "location"	#location字段名，结果即为then后的Canada、else后的USA
FROM employees;

```

## 8.3、多行子查询

**内查询返回的结果为多个、多行的数据**，即为多行子查询。

也是要注意，多行数据中，有一行存在空值的问题



**多行操作符**

![image-20220522190830126](https://i0.hdslb.com/bfs/album/ed6814a2e6ed5f14d377137e80bc040387c05c1a.png)

**任一**就是满足其一便可

```sql
#5.多行子查询
#5.1 多行子查询的操作符： IN  ANY ALL SOME(同ANY)

#5.2举例：
# IN:
SELECT employee_id, last_name
FROM   employees
WHERE  salary IN
                (SELECT   MIN(salary)
                 FROM     employees
                 GROUP BY department_id); 
                 
# ANY / ALL:
#题目2：返回其它job_id中比job_id为‘IT_PROG’部门 任一工资  低的员工的员工号、
#姓名、job_id 以及salary

SELECT employee_id,last_name,job_id,salary
FROM employees
WHERE job_id <> 'IT_PROG'
AND salary < ANY (
		SELECT salary
		FROM employees
		WHERE job_id = 'IT_PROG'
		);

#题目3：返回其它job_id中比job_id为‘IT_PROG’部门所有工资低的员工的员工号、
#姓名、job_id 以及salary
SELECT employee_id,last_name,job_id,salary
FROM employees
WHERE job_id <> 'IT_PROG'
AND salary < ALL (
		SELECT salary
		FROM employees
		WHERE job_id = 'IT_PROG'
		);
		
-- 最难的一题		
#题目4：查询平均工资最低的部门id
#MySQL中聚合函数是不能嵌套使用的。
#方式1：
SELECT department_id
FROM employees
GROUP BY department_id
HAVING AVG(salary) = (
			SELECT MIN(avg_sal)
			FROM(
				SELECT AVG(salary) avg_sal
				FROM employees
				GROUP BY department_id
				) as t_dept_avg_sal
			);

#方式2：小于等于所有部门的平均工资
SELECT department_id
FROM employees
GROUP BY department_id
HAVING AVG(salary) <= ALL(	
			SELECT AVG(salary) avg_sal
			FROM employees
			GROUP BY department_id
			) 
#5.3 空值问题
```



## 8.4、相关子查询

### 概念

一句话：内查询用到了外查询的表

子查询的执行依赖于外部查询，通常情况下都是因为**子查询中的表用到了外部的表**，并进行了条件关联，因此**每执行一次外部查询，子查询都要重新计算一次**，这样的子查询就称之为 **关联子查询** 。相关子查询按照一行接一行的顺序执行，主查询的每一行都执行一次子查询

### 案例：

```sql
#题目：查询员工中工资大于本部门平均工资的员工的last_name,salary和其department_id
#方式1：使用相关子查询
SELECT last_name,salary,department_id
FROM employees e1
WHERE salary > (
		SELECT AVG(salary)
		FROM employees e2
		WHERE department_id = e1.`department_id`
		);

#方式2：在FROM中声明子查询
SELECT e.last_name,e.salary,e.department_id
FROM employees e,(
		SELECT department_id,AVG(salary) avg_sal
		FROM employees
		GROUP BY department_id) as t_dept_avg_sal
WHERE e.department_id = t_dept_avg_sal.department_id
AND e.salary > t_dept_avg_sal.avg_sal


#题目：查询员工的id,salary,按照department_name 排序
-- order by 写子查询
SELECT employee_id,salary
FROM employees e
ORDER BY (
	 SELECT department_name
	 FROM departments d
	 WHERE e.`department_id` = d.`department_id`
	) ASC;

#结论：在SELECT中，除了GROUP BY 和 LIMIT之外，其他位置都可以声明子查询！

#题目：若employees表中employee_id与job_history表中employee_id相同的数目不小于2，
#输出这些相同id的员工的employee_id,last_name和其job_id

SELECT *
FROM job_history;

SELECT employee_id,last_name,job_id
FROM employees e
WHERE 2 <= (
	    SELECT COUNT(*)
	    FROM job_history j
	    WHERE e.`employee_id` = j.`employee_id`
		)
```

## 8.5、exist与not exist

> 使用EXISTS，相关子查询，exist与in对比的优化问题见MySQL高级或文章末尾！

-- MySQL底层是一行一行执行表的信息对比
-- 第一个表第一行与第二个表第一行对比是否存在`e1.employee_id = e2.manager_id`，如果存在，直接返回这个id；
-- 否则第一个表第一行继续对比第二个表第二行的id，一直找到结束都没有，

-- 开始找第一个表的第二行的id，与第二个表的第一行。

>not exsit就是同理了！！！

案例：

```sql

#6.2 EXISTS 与 NOT EXISTS关键字

#题目：查询公司管理者的employee_id，last_name，job_id，department_id信息
#方式1：自连接
-- 需要去重，很多员工的管理者相同
SELECT DISTINCT mgr.employee_id,mgr.last_name,mgr.job_id,mgr.department_id
FROM employees emp JOIN employees mgr
ON emp.manager_id = mgr.employee_id;

#方式2：子查询

SELECT employee_id,last_name,job_id,department_id
FROM employees
WHERE employee_id IN (
			SELECT DISTINCT manager_id
			FROM employees
			);

#方式3：使用EXISTS，相关子查询
-- MySQL底层是一行一行执行表的信息对比
-- 第一个表第一行与第二个表第一行对比是否存在e1.`employee_id` = e2.`manager_id`，如果存在，直接返回这个id；
-- 否则继续对比第二个表第二行的id，一直找到结束都没有，开始找第一个表的第二行。
SELECT employee_id,last_name,job_id,department_id
FROM employees e1
WHERE EXISTS (
	       SELECT *
	       FROM employees e2
	       WHERE e1.`employee_id` = e2.`manager_id`
	     );

#题目：查询departments表中，不存在于employees表中的部门的department_id和department_name
-- 也就是说，哪些部门没有员工，即部门的右外-内连接
#方式1：
SELECT d.department_id,d.department_name
FROM employees e RIGHT JOIN departments d
ON e.`department_id` = d.`department_id`
WHERE e.`department_id` IS NULL;

#方式2：
SELECT department_id,department_name
FROM departments d
WHERE NOT EXISTS (
		SELECT *
		FROM employees e
		WHERE d.`department_id` = e.`department_id`
		);
```



# 9. 创建库和管理表

## 9.1、库的DDL

创建数据库推荐下面的方法，要写字符集，因为企业可能5.7版本，默认字符集就不是utf8！

#1.3 修改数据库
#更改数据库字符集

```sql
CREATE DATABASE mytest3 ;
-- 建议
#如果要创建的数据库不存在，则创建成功.已经存在，则创建不成功，但不会报错。
CREATE DATABASE IF NOT EXISTS mytest3 CHARACTER SET 'utf8';

SHOW DATABASES;

#1.2 管理数据库
#查看当前连接中的数据库都有哪些
SHOW DATABASES;

#切换数据库
USE atguigudb;

#查看当前使用的数据库
SELECT DATABASE() FROM DUAL;

#查看当前数据库中保存的数据表
SHOW TABLES;

#查看指定数据库下保存的数据表
SHOW TABLES FROM mysql;



#1.3 修改数据库
#更改数据库字符集
SHOW CREATE DATABASE mytest2;

ALTER DATABASE mytest2 CHARACTER SET 'utf8';

#1.4 删除数据库
#方式2：推荐。 如果要删除的数据库存在，则删除成功。如果不存在，则默默结束，不会报错。
DROP DATABASE IF EXISTS mytest1;

```



## 9.2、创建表的两种方式

**数据最后一行不要加逗号！**

1. 白手起家创建表
2. 基于现有的表，同时导入数据：除了非空约束，其他主键约束等都无法复制过来。
2. **创建临时表：**create的时候，在table面前加 temporary

```sql
#方式1："白手起家"的方式
CREATE TABLE IF NOT EXISTS myemp1(   #需要用户具备创建表的权限。
id INT,
emp_name VARCHAR(15), #使用VARCHAR来定义字符串，必须在使用VARCHAR时指明其长度。
hire_date DATE
);
#查看表结构
DESC myemp1;
#查看创建表的语句结构
SHOW CREATE TABLE myemp1; #如果创建表时没有指明使用的字符集，则默认使用表所在的数据库的字符集。


#方式2：基于现有的表，同时导入数据
-- 除了非空约束，其他主键约束等都无法复制过来。
CREATE TABLE myemp2
AS
SELECT employee_id,last_name,salary
FROM employees;

-- 复制其他库的表
create table emp_copy 
as
SELECT employee_id,last_name
from atguigudb.employees
ORDER BY employee_id desc;

#说明1：查询语句中字段的 “ 别名 ”，可以作为新创建的表的字段的名称。
#说明2：此时的查询语句可以结构比较丰富，使用前面章节讲过的各种SELECT
CREATE TABLE myemp3
AS
SELECT e.employee_id emp_id,e.last_name lname,d.department_name
FROM employees e JOIN departments d
ON e.department_id = d.department_id;

SELECT *
FROM myemp3;

DESC myemp3;


#练习：创建一个表employees_blank，实现对employees表的复制，不包括表数据
CREATE TABLE employees_blank
AS
SELECT *
FROM employees
WHERE 1 = 2; #山无陵，天地合，乃敢与君绝。

```



## 9.3、表的DDL

修改AlTER（增加字段add、修改字段modify、重命名字段change、删除字段**drop column**）；

删除DROP（删除字段、删除表）；

重命名RENAME（重命名表）；

清空truncate、delete from

```sql
#3. 修改表  --> ALTER TABLE 

-- 3.1 添加一个字段
ALTER TABLE myemp1
ADD salary DOUBLE(10,2); #默认添加到表中的最后一个字段的位置

ALTER TABLE myemp1
ADD phone_number VARCHAR(20) FIRST;

ALTER TABLE myemp1
ADD email VARCHAR(45) AFTER emp_name;

-- 3.2 修改一个字段：数据类型、长度、默认值（略）
ALTER TABLE myemp1
MODIFY emp_name VARCHAR(25) ;

ALTER TABLE myemp1
MODIFY emp_name VARCHAR(35) DEFAULT 'aaa';

-- 删除主键自增
alter table 表名  modify 字段   类型;

-- 3.3 重命名一个字段，还得必须跟上他对应的varchar，或者修改他的长度。
ALTER TABLE myemp1
CHANGE salary monthly_salary DOUBLE(10,2);

ALTER TABLE myemp1
CHANGE email my_email VARCHAR(50);

# 3.4 删除一个字段
ALTER TABLE myemp1
DROP COLUMN my_email;

#4. 重命名表
#方式1：
RENAME TABLE myemp1 TO myemp11;

#方式2：
ALTER TABLE myemp2
RENAME TO myemp12;

#5. 删除表
#不光将表结构删除掉，同时表中的数据也删除掉，释放表空间
DROP TABLE IF EXISTS myemp12;

#6. 清空表
#清空表，表示清空表中的所有数据，但是表结构保留。

TRUNCATE TABLE employees_copy;
-- 或者
delete from employees_copy;

```

## 9.4、事务回滚问题

> DCL 中 COMMIT 和 ROLLBACK

COMMIT:提交数据。一旦执行COMMIT，则数据就被永久的保存在了数据库中，意味着数据**不可以回滚**。

ROLLBACK:**回滚数据**。一旦执行ROLLBACK,则可以实现数据的回滚。回滚到最近的一次COMMIT之后。

为了避免事故，占用写资源又如何，尽量delete from，TRUNCATE不能回滚

```
阿里开发规范：
【参考】TRUNCATE TABLE 比 DELETE 速度快，且使用的系统和事务日志资源少，但 TRUNCATE 无事务且不触发 TRIGGER，有可能造成事故，故不建议在开发代码中使用此语句。
```

> 对比 TRUNCATE TABLE 和 DELETE FROM 

相同点：都可以实现对表中所有数据的删除，**同时保留表结构**。

不同点：

TRUNCATE TABLE：一旦执行此操作，表数据全部清除。同时，数据是**不可以回滚的**。

DELETE FROM：一旦执行此操作，表数据可以全部清除（**不带WHERE的时候**）。同时，数据是**可以实现回滚**的。

> DDL 和 DML 的说明

① DDL的操作一旦执行，就**不可回滚**。指令`SET autocommit = FALSE`对DDL操作失效。(因为在执行完DDL操作之后，底层会执行一次COMMIT。而此COMMIT操作不受SET autocommit = FALSE影响的。)  

② DML的操作默认情况，一旦执行，也是不可回滚的。但是，如果在**执行DML之前**，执行了  `SET autocommit = FALSE`，则执行的DML操作**就可以实现回滚**。就比如delete from



```sql
# 演示：DELETE FROM 
#1)
COMMIT;
#2)还有数据
SELECT *
FROM myemp3;
#3)设置不要自动commit
SET autocommit = FALSE;
#4)
DELETE FROM myemp3;
#5)
SELECT *
FROM myemp3;
#6)回滚
ROLLBACK;
#7)数据还在！
SELECT *
FROM myemp3;

# 演示：TRUNCATE TABLE
#1)
COMMIT;
#2)
SELECT *
FROM myemp3;
#3)
SET autocommit = FALSE;
#4)
TRUNCATE TABLE myemp3;
#5)
SELECT *
FROM myemp3;
#6)回滚
ROLLBACK;
#7)数据没了
SELECT *
FROM myemp3;

```

## 9.5、DDL的原子化

在**MySQL 8.0版本**中，InnoDB表的**DDL支持事务完整性**，即 DDL操作要么成功要么回滚 。

MySQL5版本，不支持原子化，同时删除两个表，即使有一个表不存在而报错，另外一个表都会被成功删除。





# 10、DML数据增删改

## 10.1、插入表数据

- **如果id自增，还是写出列名吧，不然可能报错。**

1. 没指明字段插入：一定要按照声明的字段的先后顺序添加
2. 表名字段插入：没有赋值没约束，默认会是null值
3. 把另外一张表的数据插入到新表：新表字段的长度要 **>=** 原有的表字段长度

```sql
#方式1：一条一条的添加数据

#没有指明添加的字段
#正确的
INSERT INTO emp1
VALUES (1,'Tom','2000-12-21',3400); #注意：一定要按照声明的字段的先后顺序添加


#指明要添加的字段 （推荐）
INSERT INTO emp1(id,hire_date,salary,`name`)
VALUES(2,'1999-09-09',4000,'Jerry');
# 说明：没有进行赋值的hire_date 的值为 null
INSERT INTO emp1(id,salary,`name`)
VALUES(3,4500,'shk');

#同时插入多条记录 （推荐）
INSERT INTO emp1(id,NAME,salary)
VALUES
(4,'Jim',5000),
(5,'张俊杰',5500);




#方式2：把另外一张表的数据插入到新表


INSERT INTO emp1(id,NAME,salary,hire_date)
SELECT employee_id,last_name,salary,hire_date  # 查询的字段一定要与添加到的表的字段一一对应
FROM employees
WHERE department_id IN (70,60);




DESC emp1;
DESC employees;

#说明：emp1表中要添加数据的字段的长度不能低于employees表中查询的字段的长度。
# 如果emp1表中要添加数据的字段的长度低于employees表中查询的字段的长度的话，就有添加不成功的风险。

```

## 10.2、更新和删除

**DML**操作**默认**情况下，执行完以后都**会自动提交**数据。

如果希望执行完以后不自动提交数据，则需要使用 `SET autocommit = FALSE;`

```sql
#2. 更新数据 （或修改数据）
# UPDATE .... SET .... WHERE ...
# 可以实现批量修改数据的。

UPDATE emp1
SET hire_date = CURDATE()
WHERE id = 5;

#同时修改一条数据的多个字段
UPDATE emp1
SET hire_date = CURDATE(),salary = 6000
WHERE id = 4;

#题目：更新姓名中包含字符a的提薪20%
UPDATE emp1
SET salary = salary * 1.2
WHERE NAME LIKE '%a%';


#3. 删除数据 DELETE FROM .... WHERE....
-- id为1的一行被删除
DELETE FROM emp1
WHERE id = 1;

```

## 10.3、新特性计算列

MySQL8新特性，什么叫计算列呢？简单来说就是某一列的值是通过别的列计算得来的。例如，a列值为1、b列值为2，c列

不需要手动插入，定义a+b的结果为c的值，那么c就是计算列，是通过别的列计算得来的。

```sql
CREATE TABLE test1(
a INT,
b INT,
c INT GENERATED ALWAYS AS (a + b) VIRTUAL  #字段c即为计算列
);

INSERT INTO test1(a,b)
VALUES(10,20);

SELECT * FROM test1;
-- c列的值自动变成30

UPDATE test1
SET a = 100;
-- c列的值自动变成120
```



# 11、数据类型精讲

都在12章pdf文件中！

<img src="https://i0.hdslb.com/bfs/album/911e329d0bb495306b7c2614b3ee037920658686.png" alt="image-20220906224044153" style="zoom: 80%;" />







# 12、数据完整性与约束

主键、域完整性、外键、自定义

![image-20220524162738984](https://i0.hdslb.com/bfs/album/b98b67b2af495555cead15581970aa18454b7f6a.png)

## 12.1、约束的增删查

### ①查看表中的约束

```sql
#2. 如何查看表中的约束
SELECT * FROM information_schema.table_constraints 
WHERE table_name = 'test1';

-- 或者
desc test1;
```

### ②增、删约束

CONSTRAINT：约束

> 对not nul这种就可以改为null删除

```sql
-- 增加约束
-- 这种添加不能漏他的类型：varchar
ALTER TABLE test1
MODIFY email VARCHAR(25) NOT NULL;

#方式2：添加主键约束
ALTER TABLE test2
ADD PRIMARY KEY(salary);

-- ADD CONSTRAINT添加约束：名为uk_test2_sal，唯一约束
ALTER TABLE test2
ADD CONSTRAINT uk_test2_sal UNIQUE(salary);

#3.3 在ALTER TABLE时删除约束
ALTER TABLE test1
MODIFY email VARCHAR(25) NULL;

```

## 12.2、唯一性约束

### ③唯一性约束：列级、表级

唯一性：如id唯一，手机号唯一。。

```sql
#4.1 在CREATE TABLE时添加约束
CREATE TABLE test2(
id INT UNIQUE, --列级约束添加方式：无约束名
last_name VARCHAR(15) ,
email VARCHAR(25),
salary DECIMAL(10,2),
--表级约束添加方式：有约束名
    -- 约束名是uk_test2_email
    -- 用于删除约束的时候会用到！
CONSTRAINT uk_test2_email UNIQUE(email)
    
-- 不起约束名是这样
UNIQUE(email)
-- 在创建唯一约束的时候，如果不给唯一约束命名，就默认和列名相同。
);

-- 修改表的方式添加约束
ALTER TABLE test2
ADD CONSTRAINT uk_test2_sal UNIQUE(salary);
```

### ④复合的唯一性约束，即多字段

多列一起约束，多个字段只要有一个字段不同便可唯一性了！

```sql
#4.3 复合的唯一性约束
CREATE TABLE USER(
id INT,
`name` VARCHAR(15),
`password` VARCHAR(25),

#表级约束
CONSTRAINT uk_user_name_pwd UNIQUE(`name`,`password`)
);

INSERT INTO USER
VALUES(1,'Tom','abc');
#可以成功的：
INSERT INTO USER
VALUES(1,'Tom1','abc');
```

### ⑤如何删除唯一性约束

![image-20220524162359306](https://i0.hdslb.com/bfs/album/01114ced5946069d7859169d6a14219d15f3cd1d.png)

```sql
#4.4 删除唯一性约束
-- 添加唯一性约束的列上也会自动创建唯一索引。
-- 删除唯一约束只能通过删除唯一索引的方式删除。
-- 删除时需要指定唯一索引名，唯一索引名就和唯一约束名一样。
-- 唯一约束若未指定名称，如果是单列，就默认和列名相同；如果是组合列，那么默认和()中排在第一个的列名相同。也可以自定义唯一性约束名。


SELECT * FROM information_schema.table_constraints 
WHERE table_name = 'test2';

#如何删除唯一性索引:指定索引名
ALTER TABLE test2
DROP INDEX uk_test2_sal;
```



## 12.3、主键约束

**主键特点：**primary key

1. 主键约束=not null + unique；
2. 一个表只能有一个主键！
3. MySQL的主键名总是**PRIMARY**，就算自己命名了主键约束名也没用。不用起约束名！就是**PRIMARY**

原理基于B+树的底层

```sql
ALTER TABLE test2
ADD PRIMARY KEY(salary);
```

也可以多个字段

## 12.4、设置自增列

**要求：**

1. 一个表只能一个自增列：主键；
2. 字段必须是数整型
3. 会在当前最大值的基础上自增；如果自增列手动指定了具体值，直接
4. 赋值为具体值

```sql
-- 建表时
create table employee(
    eid int primary key auto_increment,
    ename varchar(20) );
    
-- 建表后
alter table employee
modify eid int auto_increment;
-- 删除自增
alter table employee modify eid int;#去掉auto_increment相当于删除
```

> 5.7与8.0的自增特点

- 在MySQL 5.7系统中，对于自增主键的分配规则，是由InnoDB数据字典内部一个 计数器来决定的，而**该计数器只在内存中维护** 【内存断电即失】，并不会持久化到磁盘中。当数据库重启时，该计数器会被初始化。重启前删除id5，重启后，再次添加id仍是5，而不是6。
- MySQL 8.0将自增主键的计数器持久化到 重做日志中。每次计数器发生改变，都会将其写入**重做日志中**。如果数据库重启，InnoDB会根据重做日志中的信息来初始化计数器的内存值。重启后，再次添加id是6，而不是5。





## 12.5、外键约束

**主表：**被引用的表，也叫父表。

**从表：**引用别的表，也叫子表。

>注意:
>
>1.通常先创建主表，再创建从表
>
>2.插入数据时，先插入主表，再插入从表，插入从表时必须保证在外键数据在主表中是存在的，否则失败。（因为完整性约束）
>
>3.删除数据时，先删除从表，再删除主表
>
>4.删表时，先删除外键约束，再删除从表，再删除主表，否则及其容易表锁死的情况，一直在转圈，而卡死了。

- 外键必须是引用别人的主键，可以建立多个外键约束；

- **创表时，**先创主表的，再创从表的；**删表时，**先删从表的，再删主表的。否则，增删改操作都会失败。
- 创建外键约束，约束名默认不是你的字段列名，而是自动产生一个，因此**你可以指定一个外键约束名**；索引名得自己去看了
- 外键列的名字可以两表列名都不同，但**类型必须一样！**

### 创建、删除、测试约束

```sql
#①先创建主表
CREATE TABLE dept1(
dept_id INT PRIMARY key,
dept_name VARCHAR(15)
);
#②再创建从表
CREATE TABLE emp1(
emp_id INT PRIMARY KEY AUTO_INCREMENT,
emp_name VARCHAR(15),
department_id INT,

#表级约束,fk_emp1_dept_id 为自定义的约束名
CONSTRAINT fk_emp1_dept_id FOREIGN KEY (department_id) REFERENCES dept1(dept_id)

);

-- 虽然有外键约束，但是null值可以存的！
-- 其他的得主表有了，才能操作！
INSERT into emp1 VALUES 
(8,'tomoo',null);

-- DELETE删除不了，TRUNCATE可以。
-- 还是别搞这么花，先搞好主表，再搞从表吧
TRUNCATE emp1;


-- 创建后添加约束：

ALTER TABLE emp2
ADD CONSTRAINT fk_emp2_dept_id FOREIGN KEY(department_id) REFERENCES dept2(dept_id);



#删除外键约束
#ALTER TABLE 从表名 DROP FOREIGN KEY 外键约束名;
ALTER TABLE emp1
DROP FOREIGN KEY fk_emp1_dept_id;

#再手动的删除外键约束对应的普通索引
SHOW INDEX FROM emp1;

#ALTER TABLE 从表名 DROP INDEX 索引名;
ALTER TABLE emp1
DROP INDEX fk_emp1_dept_id;

```

### 约束等级❤️

-- `Cascade方式`：在父表上update/delete记录时，同步update/delete掉子表的匹配记录 

-- `Set null方式`：在父表上update/delete记录时，将子表上匹配记录的列设为null，但是要注意子表的外键列不能为not null  

-- `No action方式`：如果子表中有匹配的记录，则**不允许对父表**对应候选键进行update/delete操作  

-- `Restrict方式`：同no action， 都是立即检查外键约束

-- `Set default方式`（在可视化工具SQLyog中可能显示空白）：父表有变更时，子表将外键列设置成一个默认的值，但Innodb不能识别

比如：

on update cascade on delete cascade 	把修改操作设置为级联修改等级，把删除操作也设置为级联删除等级 

on update set null on delete cascade      把修改操作设置为set null等级，把删除操作设置为级联删除等级 

❤️**结论**：对于外键约束，**最好是**采用: `ON UPDATE CASCADE ON DELETE RESTRICT` 的方式。就是能更新，但是不能删除。

```sql

#演示：
# on update cascade on delete set null
CREATE TABLE dept(
    did INT PRIMARY KEY,		#部门编号
    dname VARCHAR(50)			#部门名称
);

CREATE TABLE emp(
    eid INT PRIMARY KEY,  #员工编号
    ename VARCHAR(5),     #员工姓名
    deptid INT,		  #员工所在的部门
    FOREIGN KEY (deptid) REFERENCES dept(did)  ON UPDATE CASCADE ON DELETE SET NULL
    #把修改操作设置为级联修改等级，把删除操作设置为set null等级
);

INSERT INTO dept VALUES(1001,'教学部');
INSERT INTO dept VALUES(1002, '财务部');
INSERT INTO dept VALUES(1003, '咨询部');


INSERT INTO emp VALUES(1,'张三',1001); #在添加这条记录时，要求部门表有1001部门
INSERT INTO emp VALUES(2,'李四',1001);
INSERT INTO emp VALUES(3,'王五',1002);


UPDATE dept
SET did = 1004
WHERE did = 1002;

DELETE FROM dept
WHERE did = 1004;


SELECT * FROM dept;

SELECT * FROM emp;
```

### 阿里巴巴规范

**阿里开发规范** ：外键所实现的功能，在java后端去实现，不要在MySQL！

【 强制 】不得使用外键与级联，一切外键概念必须在应用层解决。

说明：（概念解释）学生表中的 student_id 是主键，那么成绩表中的 student_id 则为外键。如果更新学生表中的 student_id，同时触发成绩表中的 student_id 更新，即为级联更新。

**外键与级联更新适用于单机低并发 ，不适合分布式 、高并发集群 ；级联更新是强阻塞，存在数据库更新风暴的风险；外键影响数据库的插入速度 。** （面试）

解释2：

在 MySQL 里，外键约束是有成本的，需要消耗系统资源。对于大并发的 SQL 操作，有可能会不适合。比如大型网站的中央数据库，可能会 因为外键约束的系统开销而变得非常慢 。所以，MySQL 允许你不使用系统自带的外键约束，在 应用层面完成检查数据一致性的逻辑。也就是说，即使你不用外键约束，也要想办法通过应用层面的附加逻辑，来实现外键约束的功能，确保数据的一致性。



## 12.6、check约束

> 设置一个check的条件，添加的数据若不符合这个条件时，就无法添加。MySQL 8.0才支持这个check约束。

![image-20220524223400825](https://i0.hdslb.com/bfs/album/8361ea8ee7734aa4f6c6153bb2d03cc882334dd3.png)

## 12.7、default约束

如果此字段没有显式赋值，则赋值为默认值。

```sql
create table employee( 
    eid int primary key, ename varchar(20) not null,
    gender char default '男',
    tel char(11) not null default '' #默认是空字符串
);

-- 删除默认约束
alter table employee modify tel char(11) not null;		#删除tel字段默认值约束，保留非空约束
```

# 13、视图VIEW

### 概念

> 为什么需要视图？

想让员工管理一下那个表，但是又不想让他看到表的所有的数据。针对一个公司的销售人员，我们只想给他看部分数据，而某些敏感的数据，比如采购的价格，则不会提供给他。

> 视图概念

1. 视图是一种虚拟表 ，本身是 不具有数据 的，占用很少的内存空间，它是 SQL 中的一个重要概念。
2. **视图建立在已有表的基础上**, 视图赖以建立的这些表称为**基表**。
3. 视图的创建和删除只影响视图本身，不影响对应的基表。但是当对视图中的数据进行增加、删除和修改操作时，数据表中的数据会相应地发生变化，反之亦然。
4. 视图，可以看做是一个虚拟表，本身是不存储数据的。
5. 视图的本质，**就可以看做是存储起来的SELECT语句**，我们执行每一步关键字的时候，不也会生成虚拟表。

- 视图的应用场景：针对于小型项目，不推荐使用视图。针对于大型项目，可以考虑使用视图。

- 视图的优点：简化查询，控制数据的访问
- 缺点：**如果实际数据表的结构变更了，我们就需要及时对相关的视图进行相应的维护*，真麻烦。

> 视图最主要的作用？

虽然可以更新视图数据，但总的来说，**视图作为 虚拟表 ，主要用于 方便查询 ，**不建议更新视图的数据。**对视图数据的更改，都是通过对实际数据表里数据的操作来完成的。**

### 针对单表创建视图

有as的，数据库对象的特点，创建表也有as

```sql
-- 2.1 针对于单表
#情况1：视图中的字段与基表的字段有对应关系
CREATE VIEW vu_emp1
AS
SELECT employee_id,last_name,salary
FROM emps;

SELECT * FROM vu_emp1;

#起视图中字段名的别名方式1：
CREATE VIEW vu_emp2
AS
SELECT employee_id emp_id,last_name lname,salary #查询语句中字段的别名会作为视图中字段的名称出现
FROM emps
WHERE salary > 8000;

#起视图中字段名的别名方式2：
CREATE VIEW vu_emp3(emp_id,NAME,monthly_sal) #小括号内字段个数与SELECT中字段个数相同
AS
SELECT employee_id,last_name,salary 
FROM emps
WHERE salary > 8000;

SELECT * FROM vu_emp3;

#情况2：视图中的字段在基表中可能没有对应的字段
-- 搞一个聚合函数列，若修改、删除此字段就会失败！
CREATE VIEW vu_emp_sal
AS
SELECT department_id,AVG(salary) avg_sal
FROM emps
WHERE department_id IS NOT NULL
GROUP BY department_id;

SELECT * FROM vu_emp_sal;

```



### 针对多表创建视图

```sql
#2.2 针对于多表

CREATE VIEW vu_emp_dept
AS
SELECT e.employee_id,e.department_id,d.department_name
FROM emps e JOIN depts d
ON e.`department_id` = d.`department_id`;

SELECT * FROM vu_emp_dept;
```



### 基于视图创建视图

```sql
#2.3 基于视图创建视图

CREATE VIEW vu_emp4
AS
SELECT employee_id,last_name
FROM vu_emp1;

SELECT * FROM vu_emp4; 
```

### 查看视图

```sql
#3. 查看视图
# 语法1：列出一列数据：所有表和所有视图
SHOW TABLES;
1
#语法2：查看视图的结构
DESCRIBE vu_emp1;

#语法3：查看视图的属性信息
SHOW TABLE STATUS LIKE 'vu_emp1';

#语法4：查看视图的详细定义信息
SHOW CREATE VIEW vu_emp1;

```

### 更新视图数据

```sql
#4."更新"视图中的数据
#4.1 一般情况，可以更新视图的数据
SELECT * FROM vu_emp1;

SELECT employee_id,last_name,salary
FROM emps;
#更新视图的数据，会导致基表中数据的修改
UPDATE vu_emp1
SET salary = 20000
WHERE employee_id = 101;

#同理，更新表中的数据，也会导致视图中的数据的修改
UPDATE emps
SET salary = 10000
WHERE employee_id = 101;

#删除视图中的数据，也会导致表中的数据的删除
DELETE FROM vu_emp1
WHERE employee_id = 101;

SELECT employee_id,last_name,salary
FROM emps
WHERE employee_id = 101;

#4.2 不能更新视图中的数据

SELECT * FROM vu_emp_sal;

#更新失败
UPDATE vu_emp_sal
SET avg_sal = 5000
WHERE department_id = 30;

#删除失败
DELETE FROM vu_emp_sal
WHERE department_id = 30;
```

### 修改、删除视图

```sql
#5. 修改视图

DESC vu_emp1;

#方式1:增加一个字段，多一个or replace即可
CREATE OR REPLACE VIEW vu_emp1
AS
SELECT employee_id,last_name,salary,email
FROM emps
WHERE salary > 7000;

#方式2：用alter
ALTER VIEW vu_emp1
AS 
SELECT employee_id,last_name,salary,email,hire_date
FROM emps;

#6. 删除视图
SHOW TABLES;

DROP VIEW vu_emp4;

DROP VIEW IF EXISTS vu_emp2,vu_emp3;
```



# 14、存储过程与存储函数

## 14.1 存储过程

### 1、为什么要存储过程？

​		把存储过程看成是一些 SQL 语句的集合，中间加了点逻辑控制语句。存储过程在业务比较复杂的时候是非常实用的，比如很多时候我们完成一个操作可能需要写一大串 SQL 语句，写有一个存储过程，方便了我们下一次的调用。

> 存储过程优点：

1. 存储过程一旦调试完成通过后就能稳定运行，减少了 SQL 语句暴露在网上的风险，也提高了数据查询的安全性。
2. 使用**存储过程比单纯 SQL 语句执行要快，因为存储过程是预编译过的**。

> 存储过程缺点：

存储过程**难以调试和扩展**，而且**没有移植性，还会消耗数据库资源**。

### 2、带 OUT类型

```sql
#类型2：带 OUT
#举例4：创建存储过程show_min_salary()，查看“emps”表的最低薪资值。并将最低薪资
#通过OUT参数“ms”输出

DESC employees;

DELIMITER //

CREATE PROCEDURE show_min_salary(OUT ms DOUBLE)
BEGIN
	SELECT MIN(salary) INTO ms
	FROM employees;
END //

DELIMITER ;

#调用

CALL show_min_salary(@ms);

#查看变量值
SELECT @ms;

```

### 3、带 IN类型

```sql
#类型3：带 IN
#举例5：创建存储过程show_someone_salary()，查看“emps”表的某个员工的薪资，
#并用IN参数empname输入员工姓名。

DELIMITER //

CREATE PROCEDURE show_someone_salary(IN empname VARCHAR(20))
BEGIN
	SELECT salary FROM employees
	WHERE last_name = empname;
END //

DELIMITER ;

#调用方式1
CALL show_someone_salary('Abel');
#调用方式2
SET @empname := 'Abel';
CALL show_someone_salary(@empname);

```

### 4、带 IN 和 OUT

```sql
#类型4：带 IN 和 OUT
#举例6：创建存储过程show_someone_salary2()，查看“emps”表的某个员工的薪资，
#并用IN参数empname输入员工姓名，用OUT参数empsalary输出员工薪资。

DELIMITER //

CREATE PROCEDURE show_someone_salary2(IN empname VARCHAR(20),OUT empsalary DECIMAL(10,2))
BEGIN
	-- into 就是把结果输出到empsalary
	SELECT salary INTO empsalary
	FROM employees
	WHERE last_name = empname;
END //

DELIMITER ;

#调用
SET @empname = 'Abel';
CALL show_someone_salary2(@empname,@empsalary);

SELECT @empsalary;
```



## 14.2 存储函数



# 15、变量+流程控制+游标

> 评价：不重要，而且阿里巴巴禁止存储过程和存储函数，这一系列的功能都能在java实现。
>
> 但**游标挺重要的**！

系统变量与用户变量：MySQL 8.0版本新增了 SET PERSIST 命令，全局系统变量设置后永久生效，而不是重启就没了。

程序出错的定义封装：相当于java的各种异常错误的封装类。

if：多种变量条件and、or

case ：只对一个变量的多种情况分支就用case

LOOP循环、repeat：循环体，像do while

while：Java的while

leave：相当于java的break。可以leave begin存储体名，退出存储体了；还可以 leave 循环体名leave while_label，退出循环体；

iterate：相当于java的continue

游标：在循环体中一条条的取数据，如同鼠标一行一行去复制内容的步骤一样，部分独特的场景题目就会用到。十分简洁。操作步骤十分清晰。容易造成内存不足，一定要关闭

1. 声明一个游标: declare 游标名称 CURSOR for table;(这里的table可以是你查询出来的任意集合)
2. 打开定义的游标:open 游标名称;
3. 获得下一行数据:FETCH  游标名称 into    **取游标中的值存入到变量中**
4. 需要执行的语句(增删改查):这里视具体情况而定
5. 关闭游标:CLOSE 游标名称;

> 案例：创建存储过程，使用游标

![在这里插入图片描述](https://img-blog.csdnimg.cn/4afbd568004f4351ab70d95f7f3706b5.png)

![image-20220525203900583](https://i0.hdslb.com/bfs/album/24ba44abc83789f99d39ad058d8473769d340f3f.png)

调用：

![在这里插入图片描述](https://img-blog.csdnimg.cn/9c008a9da58a4cb682f4e4e59f13272f.png)





# 16、触发器

## 对DML操作监视的触发器

应用：太帅了！

> NEW.employee_id,NEW.last_name,NEW.salary
>
> 
>
> OLD.employee_id,OLD.last_name,OLD.salary

**复制空表也很帅！**

```sql
#第17章_触发器的课后练习

#练习1：

#0. 准备工作

CREATE DATABASE test17_trigger;

USE test17_trigger;

CREATE TABLE emps
AS
SELECT employee_id,last_name,salary
FROM atguigudb.`employees`;

SELECT * FROM emps;

#1. 复制一张emps表的空表emps_back，只有表结构，不包含任何数据

CREATE TABLE emps_back
AS
SELECT * FROM emps
WHERE 1 = 2;


#2. 查询emps_back表中的数据
SELECT * FROM emps_back;


#3. 创建触发器emps_insert_trigger，每当向emps表中添加一条记录时，同步将这条记录
#添加到emps_back表中

DELIMITER //

CREATE TRIGGER emps_insert_trigger
AFTER INSERT ON emps
FOR EACH ROW #每行受影响触发器都执行
BEGIN
	#将新添加到emps表中的记录添加到emps_back表中
	INSERT INTO emps_back(employee_id,last_name,salary)
	VALUES(NEW.employee_id,NEW.last_name,NEW.salary);
END //

DELIMITER ;

#show triggers;


#4. 验证触发器是否起作用
SELECT * FROM emps;

SELECT * FROM emps_back;

INSERT INTO emps(employee_id,last_name,salary)
VALUES(301,'Tom1',3600);


#练习2：
#0. 准备工作：使用练习1中的emps表

#1. 复制一张emps表的空表emps_back1，只有表结构，不包含任何数据

CREATE TABLE emps_back1
AS
SELECT * 
FROM emps
WHERE 1 = 2;


#2. 查询emps_back1表中的数据

SELECT * FROM emps_back1;


#3. 创建触发器emps_del_trigger，每当向emps表中删除一条记录时，同步将删除的这条记录添加到emps_back1表中

DELIMITER //

CREATE TRIGGER emps_del_trigger
BEFORE DELETE ON emps
FOR EACH ROW
BEGIN
	#将emps表中删除的记录，添加到emps_back1表中。
	INSERT INTO emps_back1(employee_id,last_name,salary)
	VALUES(OLD.employee_id,OLD.last_name,OLD.salary);
END //

DELIMITER ;


#4. 验证触发器是否起作用

DELETE FROM emps
WHERE employee_id = 101;


DELETE FROM emps;

SELECT * FROM emps;


SELECT * FROM emps_back1;

```

















# End





# 总结

### SQL优化总结

1. **分页查询**中的limit 1；【05章，limit分页】
2. **多表查询**时，每个**字段前都指明其所在的表**。【6.3】
3. 禁止使用 SELECT * ，必须使用 SELECT <字段列表> 查询！
4. 非聚合函数的过滤条件都写在where，因为where在having前面。where早早就过滤了大部分数据，再执行having性能就更好了！  【见[😀SQL底层执行顺序😀](#😀SQL底层执行顺序😀)，这也是为什么面试官问的原因】
5. <img src="https://i0.hdslb.com/bfs/album/e603ae3bf3ccfd8c81eabfaa5c5a39843aa60b89.png" alt="image-20221013114023396" style="zoom:80%;" />



### Oracle与MySQL区别

1. Oracle满外连接：full outer join
2. 聚合函数：Oracle可以嵌套使用！
3. Oracle没有limit？



### MySQL8与MySQL5.7区别

1、MySQL 8.0支持check约束。

![image-20220524223400825](https://i0.hdslb.com/bfs/album/8361ea8ee7734aa4f6c6153bb2d03cc882334dd3.png)



2、字符集不同：5.7的默认字符集不是utf，为 `latin1`，MySQL8改为`utf8mb4`。

3、在**MySQL 8.0版本**中，InnoDB表的**DDL支持事务完整性**，即 DDL操作要么成功要么回滚 。

MySQL5版本，不支持原子化，同时删除两个表，即使有一个表不存在而报错，另外一个表都会被成功删除。

4、老版本mysl5.5以前的存储引擎都不是*InnoDB*






### 面试

> 面试1、为什么建表时，加 not null default '' 或 default 0?

答：不想让表中出现null值。

> 面试2、为什么不想要null的值?

答:（1）不好比较。null是一种特殊值，比较时只能用专门的is null 和 is not null来比较。碰到运算符，通常返回null。 

​     （2）效率不高。影响提高索引效果。因此，我们往往在建表时 not null default '' 或 default 0

> 面试3、带AUTO_INCREMENT约束的字段值是从**1**开始的吗？

在MySQL中，**默认AUTO_INCREMENT的初始值是1**，但是你插入一条不是1的，name就不是1开始的了！每新增一条记录，字段值自动加1。设置自增属性（AUTO_INCREMENT）的时候，还可以指定第一条插入记录的自增字段的值，这样新插入的记录的自增字段值从初始值开始递增，如在表中插入第一条记录，同时指定id值为5，则以后插入的记录的id值就会从6开始往上增加。添加主键约束时，往往需要设置字段自动增加属性。

> 面试4、并不是每个表都可以任意选择存储引擎？**外键约束（FOREIGN KEY）不能跨引擎使用。**

MySQL支持多种存储引擎，**每一个表都可以指定一个不同的存储引擎**，需要注意的是：外键约束是用来保证数据的参照完整性的，如果表之间需要关联外键，却指定了不同的存储引擎，那么这些表之间是不能创建外键约束的。所以说，存储引擎的选择也不完全是随意的。

sa
