## oracle

### 三种数据库读数问题和四种隔离级别

脏读：一个事务读取另一个事务未提交的数据

不可重复读（虚读）：一个事务在另一个事务提交前后读取的记录数值不一样（update）

幻读：一个事务在另一个事务提交前后读取的记录个数不一样（insert delete）

| 隔离级别                   | 脏读（dirty read） | 不可重复读（noRepeatable read） | 幻读（phantom read） |
| ---------------------- | -------------- | ------------------------ | ---------------- |
| 未提交读（read uncommitted） | 可能             | 可能                       | 可能               |
| 已提交读（read committed）   | 不可能            | 可能                       | 可能               |
| 可重复读（repeatable read）  | 不可能            | 不可能                      | 可能               |
| 可串行化（serializable）     | 不可能            | 不可能                      | 不可能              |

### 取消connect权限

revoke connect from user

### oracle客户端+pl/sql developer的安装

### plsql设置快捷键

Tools-》Editor-》AutoReplace-》Edit

## mysql

### 授权，撤销权限

授权

GRANT privilege(privilege = select, update, delete, insert, rule , all) ON database.table TO ’username@host‘

```
GRANT SELECT, INSERT ON test.user TO 'pig'@'%'; 
GRANT ALL ON *.* TO 'pig'@'%'; // 给pig用户授权所有数据库所有表的所有权限
```

撤销权限

REVOKE privilege ON database.table FROM 'username@host'

```
REVOKE SELECT ON *.* FROM 'pig'@'%';
```

### mysql两种引擎的区别InnoDB和MyIASM

MyIASM是mydql默认的引擎; InnoDB是事务安全的，MyIASM是非事务安全的；InnoDB锁的粒度是行级的，MyIASM是表级的；InnoDB不支持全文索引，MyIASM支持全文索引；MyIASM相对简单，效率低，适合小型应用，MyIASM保存成文件形式，跨平台更方便

### mysql information_schema数据库的一些用途

该库中有tables表存着	所有的表信息 包括其他库的表的信息 所有可以通过下面的语句读取表信息

```
SELECT 
    table_name
FROM
    information_schema.tables
```

### 根据特定列比较两个表 找到不匹配的记录

思路： 将两个表做一次union all 操作 然后根据特定列分组，计算每个分组的count 如果为2则是相同数据 如果为1则是不匹配数据，常用于数据库的迁移

```
select col_name1, col_name2
from (select col_name1, col_name2 from t1 union all select col_name1, col_name2 from t2 ) t group by t.col_name1, t.col_name2 having count(*) = 1 
```

### 使用delete join语句 删除重复的行 重复的行保留最大id

```
DELETE t1 
FROM contacts t1
INNER JOIN contacts t2 
WHERE  t1.id < t2.id AND t1.email = t2.email;
```

### mysql查看表的列信息

```
show columns from tablename
```

### linux下打开mysql服务

```
sudo service mysql start
```

### 数据库表重命名

```
// 三种方式 ，个人喜欢第二种
RENAME TABLE tablename TO newtablename
ALTER TABLE tablename RENAME newtablename
ALTER TABLE tablename RENAME TO newtablename
```

### 修改表结构

```
// 喜欢用第二种 ，使用first 可以将该列至于最前边
ALTER TABLE 表名 ADD COLUMN 列名字 数据类型 约束；
ALTER TABLE 表名 ADD 列名字 数据类型 约束；
```



### 加载外部sql文件

使用source关键字 和sql文件路径

```
mysql> source e://example/example.sql
```

### mysql的几种约束

1 主键：定义主键的方式有三种

```
// 第一种
create table employee(
	id int primary key,
	name varchar(255)
)
// 第二种
create table employee(
	id int,
	name varchar(255),
	constraint emp_pk primary key (id)
)
// 第三种 复合主键
create table employee(
	id int,
	name varchar(255),
	constraint emp_pk prinary key(id, name) // emp_pk 是主键的名字
)
```

2 默认值约束 使用default 关键字

3 唯一约束 unique

```
create table employee(
	id int primary key,
	name varchar(255),
	unique(name)
)
```

4 外键约束 foreign key

```
create table employee(
	id int primary key,
	name varchar(255),
	dept_id int,
	constraint dept_fk foreign key (dept_id) references dept(id) // dept(id)表示dept表的id字段
)
```

5 非空约束 not null