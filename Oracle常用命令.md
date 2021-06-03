### 登录

```
 sqlplus system/password@orcl1234
 sqlplus username/password@servername
 sqlplus /as sysdba
 sqlplus username/passwrod@servername < filepath //将文件在oracle中一键执行
```

### 工作时登录（保护账户密码：不被记录）

1、(SQL>为标记 ，下同)

```
 sqlplus /nolog
 SQL> conn username/password@servername
```

2、

```
 sqlplus /nolog
 SQL> conn username
 SQL> password@servername
```

### 创建账户，赋予权限

```sql
 CREATE USER username IDENTIFIED BY password;
 GRANT connect,resourse,create any view TO username 
```

### 备份

```sql
 CREATE  TABLE tablename1 AS  SELECT * FROM tablename2 WHERE 1=1; --where成立建表加数据，不成立只有表没有数据
```

### 导入导出文件

```
 imp username/password@servername file=FILEPATH fromuser=hr touser=username
 exp username/password@servername file=FILEPATH 
 注释：username=system password=orcl1234 servername=seven
```

### 分页

```sql
SELECT * FROM (SELECT rownum rn,s.* FROM (SELECT * FROM stu_grade) s WHERE rownum<8) WHERE rn>=2;
```

### 自动追踪

```sql
 set autotrace on;
 set autotrace off;
```

### 查看系统资源

```sql
SELECT   resource_name,  
    current_utilization,  
    max_utilization,  
    LIMIT,  
    ROUND (max_utilization / LIMIT * 100) || '%' rate  
FROM   (SELECT   resource_name,  
                 current_utilization,  
                 max_utilization,  
                 TO_NUMBER (initial_allocation) LIMIT  
          FROM   v$resource_limit  
         WHERE   resource_name IN ('processes', 'sessions')  
                 AND max_utilization > 0); 
```

### 转义

```sql
两种比较常见的方式 ：1.用中括号[ ]转义。 2.用关键字ESCAPE 转义。

延展知识：

1.用中括号[]转义 。

例子：WHERE ColumnA LIKE 'aaa[_]bbb' --- .

2.用关键字ESCAPE 转义。

例子：WHERE ColumnA LIKE '%aaa/%bbb%' ESCAPE '/'.

3.(1)方式2不如1方便，适用面也窄小，清晰度也差。

  (2)方式0在使用动态SQL，尤其是“嵌套 + 代码生成”的高级应用中，很容易出错。

4.举例说明：

错误语句：select * from table_base where flag_topic  & #{topic_num} .

错误信息：Caused by: org.xml.sax.SAXParseException; lineNumber: 8; columnNumber: 54; The entity name must immediately follow the '&' in the entity reference.

正确语句： 　　select * from table_base where flag_topic   &amp; #{topic_num}.
```

### 常用函数

```sql
to_number(a,'b') --将a按格式b转换
to_char(a,'b') --将a按格式b转换
to_date(a,'b') --将a按格式b转换
months_between(a,b) --a,b为两个日期
NVL(a,b) --若a为空则输出b
coalesce(a,b,c...z) --若a为空则输出b，若b为空则输出c....都为空默认输出z
upper(a) --转为大写
lower(a) --转为小写
initcap(a) --首字母大写
instr(a,'b')=0 --a中不包含b
substr(a,b,c) --a中从b位置到c位置的数据,b>0时，从字符串的第b位开始截取长度为l 的子字符串；当b<0时，从字符串的倒数第b（绝对值）位开始截取长度为l 的子字符串；b=0时，系统强制将b转换成1；
replace(a,'b','c') --a中用c代替b
between a AND b --在a和b之间
TRIM(a from 'b') --从字符串b中剔除首尾的某字符（a），默认不指定字符时TRIM('b')剔除首尾的空格

```

### Oracle 换行符 空格符 回车符

```sql
① 换行符 chr(10)
② 回车符 chr(13)
③ 空格符 chr(9)

例1：效果对比。chr(10)在一个字段中换行显示一列数据，chr(13)同样是换行显示一行数据，chr(9)会显示一个空格。因此，需要在 oralce 的一个字段中同一列显示换行的两句话，在SQL语句中拼入 chr(10) 或者 chr(13) 都可以。

1 select '换行符1'||chr(10)||'换行符2'||chr(10)||'换行符3' from dual;
2 select '回车符1'||chr(13)||'回车符2'||chr(13)||'回车符3' from dual;
3 select '空格符1'||chr(9)||'空格符2'||chr(9)||'空格符3' from dual;
例2：当时字段中允许有特殊字符时，使用 update 替换掉语句中的特殊字符。

 update table set  col_name = replace(replace(replace(col_name, chr(10),''),chr(13), ''), chr(9), '');
 
```

### 语法

```sql
--1.truncate 和delete都是用来删除表中的数据，前者属于DDL，一次性删除整张表的数据,不可回滚；后者属于DML逐条删除数据，有记录，可回滚

--2.别名AS可不加 别名有空格时用"",没有空格时可以加"",也可以不加,但是不能加''.

--3.使用链接符要形如'K'||'K',而"K"||"K"非法.

--4.找相似 IS LIKE/IS NOT LIKE  找空 IS NULL/IS NOT NULL

--5.修改字段类型：alter table 表名 modify 字段名 数据类型(16),字段有数据只能修改长度，字段为空才能修改类型

--6.提取日期与输入日期对比
to_char(sale_date,'yyyy-mm-dd')=to_char(to_date('2021-5-2','yyyy-mm-dd'),'yyyy-mm-dd')

--7.prepareStatement执行sql以日期作为查询条件时占位符?存放String类型时间时不用加''否则报错
(完整) 年份值必须介于 -4713 和 +9999 之间, 且不为 0
--数据库中的''相当于java中的"",所以String类型不用再加''

--8.删除外键约束
oracle:
alter table 表名 drop constraint 约束名;
其他数据库:?
alter table 表名 drop foreign key 约束名;

```

### VARCHAR2和NUMBER转换关系

```sql
--插入：
VARCHAR2字段：插入NUMBER时可带可不带''
NUMBER字段：无法插入带非数字字符
--删除
VARCHAR2字段：当此字段全部为数字时，删除数据时该字段作为条件可不加'',若不纯为数字，则加''
NUMBER字段：该字段只能存入数字，删除数据时该字段作为条件可加可不加''
```

SQL语言

```sql
SQL语言共分为四大类：数据查询语言DQL，数据操纵语言DML，数据定义语言DDL，数据控制语言DCL。

1、数据查询语言DQL
数据查询语言DQL基本结构是由SELECT子句，FROM子句，WHERE
子句组成的查询块：
SELECT <字段名表>
FROM <表或视图名>
WHERE <查询条件>

2、数据操纵语言DML
数据操纵语言DML主要有三种形式：
1)插入：INSERT
2)更新：UPDATE
3)删除：DELETE

3、数据定义语言(DDL Data Definition)：create创建、alter更改、truncate截断、drop删除

4、DCL（Data Control Language，数据控制语言）：用来授予或回收访问数据库的某种特权，并控制数据库操纵事务发生的时间及效果。如：
grant：授权；
revoke：取消权限；

TCL（Transaction Control Language，事物控制语言）：
用来对事务进行管理。 如：
COMMIT : 保存已完成事务动作结果
SAVEPOINT : 保存事务相关数据和状态用以可能的回滚操作
ROLLBACK : 恢复事务相关数据至上一次COMMIT操作之后

```

### VARCHAR2和NUMBER的区别

```
--插入：
VARCHAR2字段：插入NUMBER时可带可不带''
NUMBER字段：无法插入带非数字字符
--删除
VARCHAR2字段：当此字段全部为数字时，删除数据时该字段作为条件可不加'',若不纯为数字，则加''
NUMBER字段：该字段只能存入数字，删除数据时该字段作为条件可加可不加''
```

