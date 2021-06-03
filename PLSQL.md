#### PL/SQL概述

PL/SQL（Procedual Language extensions to SQL）是Oracle对标准SQL语言的过程化扩展，是Oracle数据库专用的一种高级程序设计语言

由于SQL语言将用户操作与实际的数据结构、算法等分离，无法对一些复杂的业务逻辑进行处理。因此Oracle数据库对标准的SQL语言进行了扩展，将SQL语言的非过程化与第三代开发语言的过程化结合，产生了PL/SQL语言。在PL/SQL语言中，既可以通过SQL语言实现对数据库的操作，也可以通过过程化语言中的复杂逻辑结构完成复杂的业务逻辑。

例如：

```plsql
DECLARE
  v_deptno emp.deptno%TYPE;
BEGIN
  SELECT deptno INTO v_deptno FROM emp WHERE empno=7844;
  IF v_deptno=10 THEN
    UPDATE emp SET sal=sal+100 WHERE empno=7844;
  ELSE
    UPDATE emp SET sal=sal+200 WHERE empno=7844;
  END IF;
END;
```

上述程序中，SELECT语句和2个UPDATE语句是非过程化的SQL语言，完成对数据库的操作；而变量的声明，IF语句的逻辑判断则是过程化语言的应用。


PL/SQL程序开发主要包括：存储过程、函数、包和触发器的应用开发。

#### PL/SQL的特点：

- 与SQL语言紧密集成，所有的SQL语句在PL/SQL中都可以得到支持

- 减少网络流量，提高应用程序的性能。

  ![减少网络流量](./PLSQL00.png)

- 模块化的程序设计功能，提高了系统可靠性。PL/SQL程序以块为单位，每个块就是一个完整的程序，实现特定的功能。块与块之间相互独立。应用程序可以通过接口从客户端调用数据库服务器端的程序块。例如：分页存储过程、订单存储过程、转账存储过程。

#### PL/SQL程序结构

```plsql
DECLARE
  声明部分，声明变量、常量、数据类型、游标、异常处理名称以及本地（局部）子程序定义等。
BEGIN
  执行部分，实现块的功能。该部分通过变量赋值、流程控制、数据查询、数据操纵、数据定义、事务控制、游标处理等实现块的功能
EXCEPTION
  异常处理部分，处理程序执行过程中产生的异常
END;
/
```

> 注意：
>
> 所有的PL/SQL块都是以"END;"结束

- 定义一个包含声明部分、执行部分和异常处理部分的PL/SQL块
  - 例如：找出工号为190的员工名字，并输出出来，如果没有这个员工则提示找不到这个员工
- SELECT ename INTO v_ename FROM emp WHERE empno=190;
  
- 定义一个只包含执行部分的PL/SQL块
  - 输出Hello,World!

#### PL/SQL块的分类

- 匿名块（无法重复调用）匿名内部类
- 命名块  存储过程、函数、触发器、包

#### 数据类型

- 数字类型：BINARY_INTEGER、PLS_INTEGER、NUMBER
  - NUMBER类型以十进制形式存储整数和浮点数，语法为NUMBER（p，s）。其中，p为精度，即所有有效数字位数；s为刻度范围，即小数位数。p的取值范围为1～38
  - BINARY_INTEGER类型用于表示从-2147483647～+2147483647之间的整数，以二进制形式存储。当发生溢出时，将自动转换成NUMBER类型。
  - PLS_INTEGER类型表示范围与BINARY_INTEGER相同，但发生溢出时会产生错误。

- 字符类型：CHAR、NCHAR、VARCHAR2、NVARCHAR2、VARCHAR、LONG
  
  - PL/SQL中的字符类型与Oracle数据库中的字符类型类似，但是允许字符串的长度有所不同。
- VARCHAR2，CHAR主要用于存储来自本地数据库字符集的字符，而NCHAR，NVARCHAR2 用于存储来自国家字符集的字符串。 
  
  | 类型      | PL/SQL中最大字节数 | Oracle中最大字节数 |
  | --------- | ------------------ | ------------------ |
  | VARCHAR2  | 32767              | 4000               |
  | NVARCHAR2 | 32767              | 4000               |
  | CHAR      | 32767              | 2000               |
  | NCHAR     | 32767              | 2000               |
| LONG      | 32760              | 2G                 |
  
- 日期类型：DATE、TIMESTAMP、INTERVAL

  - DATE：与数据库中的DATE类型相同，存储日期和时间信息，包括世纪、年、月、日、小时、分和秒，不包括秒的小数部分。
  - TIMESTAMP：与DATE类型相似，但包括秒的小数部分，有以下3种形式。
    - TIMESTAMP[(p)]：其中p为秒字段的小数部分精度。
    - TIMESTAMP[(p)]WITH TIME ZONE：返回当前时区的时间戳。
    - TIMESTAMP[(p)]WITH LOACL TIME ZONE：返回数据库时区的时间戳。

  - INTERVAL：用于存储两个时间戳之间的时间间隔，有下面两种形式。
    - INTERVAL YEAR [(p)]TO MONTH：两个时间戳相差的年数和月数。
    - INTERVAL DAY[(dp)] TO SECOND[(sp)]：两个时间戳相差的天数和秒数。

- 行标识类型：ROWID、UROWID
  - ROWID表示行的物理地址
  - UROWID既可以表示行的物理地址，也可以表示行的逻辑地址。

- 布尔类型：BOOLEAN（TRUE、FALSE、NULL）
  
  - 只能在PL/SQL中使用，其取值为逻辑值，包括TRUE、FALSE、NULL。
  
- 裸格式：RAW、LONG RAW

  | 类型     | PL/SQL中最大字节数 | Oracle中最大字节数 |
  | -------- | ------------------ | ------------------ |
  | RAW      | 32767              | 2000               |
  | LONG RAW | 32767              | 2G                 |

- LOB类型：CLOB、BLOB、NCLOB、BFILE
  - BLOB存放二进制数据，CLOB，NCLOB存放文本数据，而BFILE存放指向操作系统文件的指针。
  - LOB类型变量可以存储4 GB的数据量。

- 引用类型：REF CURSOR、REF object_type
  
  - 引用类型类似于其他高级语言中的指针类型。在PL/SQL中，引用类型包括游标的引用类型和对象的引用类型，即REF CURSOR和REF object_type
  
- 记录类型：RECORD
  - 记录类型是复合类型，类似于C语言中的结构体，是一个包含若干个成员分量的复合类型。
    在使用记录类型时，需要先在声明部分定义记录类型和记录类型的变量，然后在执行部分引用该记录类型变量或其成员分量。

- 集合类型：TABLE、VARRAY
  - 集合类型是复合类型，包括索引表类型、嵌套表类型和可变数组类型。
  - 集合类型与记录类型的区别在于，记录类型中的成员分量可以是不同类型的，类似于结构体，而集合类型中所有的成员分量必须具有相同的数据类型，类似于数组。 

- %TYPE、%ROWTYPE
  - 如果要定义一个类型与某个变量的数据类型或数据库表中某个列的数据类型一致（不知道该变量或列的数据类型）的变量，可以利用%TYPE来实现。
  - 如果要定义一个与数据库中某个表结构一致的记录类型的变量，可以使用%ROWTYPE来实现。 

#### 变量与常量的定义

variable_name [CONSTANT] datatype [NOT NULL] [DEFAULT|:=expression];

#### 记录类型（单行、多列）

定义记录类型的语法为：
TYPE record_type IS RECORD(
field1 datatype1 [NOT NULL][DEFAULT|:=expr1],
field2 datatype2 [NOT NULL][ DEFAULT|:=expr2],
……
fieldn datatypen [NOT NULL][ DEFAULT|:=exprn]
);

- 用户定义记录类型及变量

  ```plsql
  DECLARE
    TYPE t_emp IS RECORD(
       empno NUMBER(4), 
       ename CHAR(10),
       sal   NUMBER(6,2));
    v_emp t_emp;
  BEGIN
    SELECT empno,ename,sal INTO v_emp 
    FROM emp WHERE empno=7844;
    DBMS_OUTPUT.PUT_LINE(v_emp.ename||' '||v_emp.sal);
  END;
  ```

- 利用%ROWTYPE获取记录类型定义变量

  ```plsql
  DECLARE
    v_emp1 emp%ROWTYPE;
    v_emp2 emp%ROWTYPE;
    CURSOR c_emp IS SELECT empno,ename FROM emp WHERE deptno=10;
    v_emp10 c_emp%ROWTYPE; 
  BEGIN
    SELECT * INTO v_emp1 FROM emp WHERE empno=7844;
    OPEN c_emp;  
    LOOP
      FETCH c_emp INTO v_emp10;
      EXIT WHEN c_emp%NOTFOUND;
      DBMS_OUTPUT.PUT_LINE(v_emp10.empno||' '||v_emp10.ename); 
    END LOOP;  
    CLOSE c_emp;
  END; 
  ```

- 记录类型变量的应用

  - SELECT INTO 中使用

  ```plsql
  DECLARE
    v_emp emp%ROWTYPE; 
  BEGIN
    SELECT * INTO v_emp FROM emp
    WHERE empno=7844;
    DBMS_OUTPUT.PUT_LINE(v_emp.empno||' '||v_emp.ename||' '||v_emp.sal);  
  END;
  ```

  - INSERT语句中使用

  ```plsql
  DECLARE
   v_dept dept%ROWTYPE;
  BEGIN
   v_dept.deptno:=50;
   v_dept.loc:='BEIJING';
   v_dept.dname='DEV';
   INSERT INTO dept VALUES v_dept;
  ```

  - UPDATE中使用

  ```plsql
  DECLARE
   v_dept dept%ROWTYPE;
  BEGIN
   v_dept.deptno:=50;
   v_dept.loc:='TIANJIN';
   v_dept.dname='SALES';
   UPDATE dept SET ROW=v_dept WHERE deptno=50;
  END;
  ```

  - DELETE中使用

  ```plsql
  DECLARE
   v_emp emp%ROWTYPE;
  BEGIN
   SELECT * INTO v_emp FROM emp WHERE empno=7844;
   DELETE FROM emp WHERE deptno=v_emp.deptno;
  END;
  ```

#### 编译提示

编译指示是对编译程序发出的特殊指令，也称为伪指令，不会改变程序含义。它只是向编译程序传递信息，类似于嵌入在SQL中的注释。
在PL/SQL中使用PRAGMA关键字通知编译程序，PL/SQL语句的剩余部分是一个编译指示或命令。编译指示在编译时被处理，而不会在运行时被执行，类似于C语言中的#define。
PL/SQL提供以下4种编译指示：

- EXCEPTION_INIT：告诉编译程序将一个特定的错误号与程序中所声明的异常标识符关联起来。
- RESTRICT_REFERENCES：告诉编译程序打包程序的纯度，即对函数中可以使用的SQL语句和包变量进行限制。
- SERIALLY_REUSEABLE：告诉PL/SQL运行引擎时，在数据引用之间不要保持包级数据。
- AUTONOMOUS_TRANSACTION：告诉编译程序，该程序块为自治事务，即该事务的提交和回滚是独立进行的，该程序块的COMMIT或ROLLBACK不影响外层事务。

例如：

```plsql
DECLARE
	no_such_sequence EXCEPTION;
	PRAGMA EXCEPTION_INIT(no_such_sequence,-2289);
BEGIN
......
END;
```

```plsql
FUNCTION F_A_A_C_VALID_SUM(in_crm_dt CHARACTER) RETURN INTEGER as
	PRAGMA autonomous_transaction;
    --固化变量&类型&常量声明区
    v_etl_level     VARCHAR2(40) := UPPER('ADM');
    v_etl_task_name VARCHAR2(30) := UPPER('F_A_A_C_VALID_SUM');
    v_sys_no        VARCHAR2(20) := UPPER('CRM');
    v_flag          INTEGER := 0; --返回值为0程序正常，返回1则重跑
    v_return        INTEGER := 0;
BEGIN
......
END;
```

#### PL/SQL中的SQL语句

由于PL/SQL执行采用早期绑定，即在编译阶段对变量进行绑定，识别程序中标识符的位置，检查用户权限、数据库对象等信息，因此在PL/SQL中只允许出现: 

- SELECT 

  - 例如：根据员工名或员工号查询员工信息。
  - > 注意：
    >
    > SELECT…INTO语句只能查询一个记录的信息，如果没有查询到任何数据，会产生NO_DATA_FOUND异常；如果查询到多个记录，则会产生TOO_MANY_ROWS异常。
    > INTO句子后的变量用于接收查询的结果，变量的个数、顺序应该与查询的目标数据相匹配，也可以是记录类型的变量。

- DML(UPDATE、DELETE、INSERT)

- 事务控制语句（COMMIT、ROLLBACK、SAVEPOINT）

  > 注意：
  >
  > DDL语句不可以直接使用，除非使用动态SQL的方式执行

- 动态SQL（表的名字，变量的值都不固定）
  - EXECUTE IMMEDIATE DDL;
  - EXECUTE IMMEDIATE SQL INTO  变量名;

- RETURNING

  - 如果要查询当前DML语句操作的记录的信息，可以在DML语句末尾使用RETURNING语句返回该记录的信息。

  - RETURNING语句的基本语法：

    - RETURNING select_list_item INTO variable_list|record_variable; 
    - 例如：

    ```plsql
    DECLARE
       v_sal emp.sal%TYPE;
    BEGIN
       UPDATE emp SET sal=sal+100 WHERE empno=7844 
                                                RETURNING sal INTO v_sal;
       DBMS_OUTPUT.PUT_LINE(v_sal);
    END;
    ```

#### 流程控制

- 选择结构

  - IF语句

    - ```plsql
      IF 条件1 THEN 语句1
      	[ELSIF 条件2 THEN 语句2]
      	......
      	[ELSE 语句]
    END IF;
      ```

  - CASE语句

    - 简单CASE

    - ```plsql
  CASE test_value
      	WHEN value1 THEN statement1;
  	WHEN value2 THEN statement2;
      	......
  	WHEN valuen THEN statementn;
      	[ELSE else_statement;]
      END CASE;
      ```
      
    - 搜索CASE
      
    - ```plsql
      CASE
      	WHEN condition1 THEN statement1;
        	WHEN condition2 THEN statement2;
      	......
        	WHEN conditionn THEN statementn;
      	[ELSE else_statement;]
      END CASE;
      ```
  
- IF语句和简单型CASE案例：输入一个员工号，修改该员工的工资，如果该员工为10号部门，工资增加100；若为20号部门，工资增加150；若为30号部门，工资增加200；否则增加300。 
  
- 搜索型CASE案例：根据输入的员工号，修改该员工的工资，如果工资低于1000，则工资加200；如果工资在1000~2000之间则增加150；如果工资在2000~3000之间，则增加100；否则增加50；
  
- 循环结构

  - 简单循环
    
  - ```plsql
    LOOP
      语句
      EXIT [WHEN 条件];
    END LOOP;
    ```
    
  - 案例：循环给表添加50条记录

- WHILE循环

  - ```plsql
    WHILE 条件 LOOP
        语句;
    END LOOP;
    ```

  - 案例：利用WHILE循环向表中添加50条记录

- 数字FOR循环

  - ```plsql
    FOR loop_counter IN [REVERSE] low_bound..high_bound LOOP
      语句;
    END LOOP
    ```

#### 游标

游标（CURSOR）是Oracle系统在内存中开辟的一个工作区，在其中存放SELECT语句返回的查询结果。使用游标时，SELECT语句查询的结果可以是单条记录，多条记录，也可以是零条记录。游标工作区中，存在着一个指针（POINTER）,在初始状态它指向查询结果的首记录。

- 游标分类
  - 显式游标：用户定义、操作，用于返回多行数据的SELECT查询
  - 隐式游标：系统自动操作，用于处理DML语句和返回单行数据的SELECT

- 显式游标
  - 显式游标的操作
  - 显式游标的属性
  - 参数化显式游标
  - 显式游标的检索
  - 利用游标更新或删除数据

- 显式游标操作

  - 定义游标
    - 语法
      
      ```plsql
      CURSOR cursor_name IS select_statement ;
      ```
      
    - 说明
      游标必须在PL/SQL块的声明部分进行定义；
      游标定义时可以引用PL/SQL变量，但变量必须在游标定义之前定义；
      定义游标时并没有生成数据，只是将定义信息保存到数据字典中；
      游标定义后，可以使用cursor_name%ROWTYPE定义游标类型变量。
- 打开游标
    - 语法
      
      ```plsql
      OPEN cursor_name; 
      ```
      
  - 说明
    分配缓冲区
    执行游标定义时对应的SELECT语句，将查询结果检索到工作区中。
    一旦游标打开，就无法再次打开，除非先关闭。
    
  - 检索游标
    - 语法格式
      
      ```plsql
      FETCH cursor_name INTO variable_list|record_variable; 
      ```
    
  - 说明
      在使用FETCH语句之前必须先打开游标
      对游标第一次使用FETCH语句时，游标指针指向第一条记录，因此操作的对象是第一条记录，使用后，游标指针指向下一条记录。
      游标指针只能向下移动，不能回退
      INTO子句中的变量个数、顺序、数据类型必须与工作区中每行记录的字段数、顺序以及数据类型一一对应
      
  - 关闭游标
    - 语法格式
      
        ```plsql
        CLOSE cursor_name; 
        ```
        
    - 说明
    游标所对应的内存工作区变为无效，释放与游标相关的系统资源。
  
- 游标案例：根据输入的部门号查询某个部门的员工信息，部门号在程序运行时指定。由于某个部门的人数是不确定的，可能有多个，因此需要采用游标来处理。

- 显式游标的属性
  - %ISOPEN
    布尔型。如果游标已经打开，返回TRUE,否则为FALSE。
  - %FOUND
    布尔型，如果最近一次使用FETCH语句，有返回结果则为TRUE,否则为FALSE;
  - %NOTFOUND
    布尔型，如果最近一次使用FETCH语句,没有返回结果则为TRUE,否则为FALSE;
  - %ROWCOUNT
    数值型，返回到目前为止从游标缓冲区检索的元组数。
  - %BULK_ROWCOUNT（i）
    数值型，用于取得FORALL语句执行批绑定操作时第i个元素所影响的行数。

- 带参数的游标

  - 参数化游标定义语法格式
    
  - ```plsql
    CURSOR cursor_name(parameter1
    datatype[,parameter2 datatype…]) 
    IS select_statement 
    ```
    
  - 打开参数化游标的方法
    
  - ```plsql
    OPEN cursor_name(parameter1
    [,parameter2…]) 
    ```
  ```
    
    > 注意：
    >
    > 定义参数化游标时，只能指定参数的类型，而不能指定参数的长度、精度、刻度；
    > 打开带参数的游标时，实参的个数和数据类型等必须与游标定义时形参个数和数据类型等相匹配。
  ```

- 带参数游标案例

  - 查询并输出某个部门的员工信息

- 显式游标的检索

  由于游标对应的缓冲区中可能有多行记录，而PL/SQL中每次只能处理一行记录，因此要采用循环的方式从缓冲区中检索数据进行处理。根据循环方法的不同，检索游标有三种方法。

  - 简单循环检索游标
  - 案例：利用简单循环统计并输出各个部门的平均工资
  - WHILE循环检索游标
  - 案例：利用WHILE循环统计并输出各个部门的平均工资
  - FOR循环检索游标
  - FOR loop_variable IN 游标名字或显式SELECT语句
    LOOP
        执行语句;
      END LOOP;
    - 利用FOR循环检索游标时，系统会自动打开、检索、关闭游标。系统首先隐含定义一个数据类型为cursor_name%ROWTYPE的循环变量loop_variable，然后自动打开游标，从游标缓冲区中提取数据并放入loop_variable变量中，同时进行%FOUND属性检查以确定是否检索到数据。当游标缓冲区中的数据都检索完毕或循环中断时，系统自动关闭游标。
  - 案例：利用FOR循环统计并输出各个部门的平均工资

- 利用游标更新或删除数据

  - 游标定义语法
    
  - ```plsql
    CURSOR cursor_name IS
    SELECT select_list_item FROM table  FOR UPDATE
    [OF column_reference] [NOWAIT]; 
    ```
    
  - > 注意：
    >
    > 打开游标时对相应的表加锁（通常SELECT操作不在数据上设置任何锁），其他用户不能对该表进行DML操作；
  
  - 若数据对象已经被其他会话加锁，则当前会话挂起等待（默认状态），若指定了NOWAIT子句，则不等待，返回ORACLE错误。
  
  - 对于多表查询时，可以通过OF子句指定某个要加锁的表的列的形式，对特定的表加锁，而其他表不加锁；否则所有表都加锁。 
    当用户执行COMMIT或ROLLBACK操作时，数据上的锁会自动被释放。 
    
  - 修改或删除数据的语法为
    UPDATE|DELETE…
    WHERE CURRENT OF cursor_name 
    
  - 案例：修改员工的工资，如果员工的部门号为10，则工资提高100；如果部门号为20，则工资提高150；如果部门号为30，则工资提高200；否则工资提高250。 
  
    > 注意：
    >
    > 如果游标定义时没有使用FOR UPDATE子句，则不能利用该游标修改或删除数据库中的数据。

#### 隐式游标

所有的SQL语句都有一个执行的缓冲区，隐式游标就是指向该缓冲区的指针，由系统隐含地打开、处理和关闭。隐式游标又称为SQL游标。
隐式游标主要用于处理INSERT、UPDATE，DELETE以及单行的SELECT…INTO语句，没有OPEN，FETCH，CLOSE等操作命令。

- 隐式游标属性

  - SQL%ISOPEN：布尔型值，判断隐式游标是否已经打开。对用户而言，该属性值始终为FALSE，因为操作时系统自动打开，操作完后立即自动关闭。
  
  - SQL%FOUND：布尔型值，判断当前的操作是否会对数据库产生影响。如果有数据的插入、删除、修改或查询到数据，则返回TRUE，否则返回FALSE。
  
  - SQL%NOTFOUND：布尔型值，判断当前的操作是否对数据库产生影响。如果没有数据的插入、删除、修改或没有查询到数据，则返回TRUE，否则返回FALSE。

  - SQL%ROWCOUNT：数值型，返回当前操作所涉及的数据库中的行数。
  
  - 案例：修改员工号为1000的员工工资，将其工资增加100。如果该员工不存在，则向emp表中插入一个员工号为1000，工资为1500的员工。
  
    > 注意：
    >
    > 当SELECT ....INTO语句没有查询到任何数据时，会激发NO_DATA_FOUND异常。

#### 游标变量

- 概念
  - 显式游标在定义时与特定的查询绑定，其结构是不变的，因此又称为静态游标。游标变量是一个指向多行查询结果集的指针，不与特定的查询绑定，因此具有非常大的灵活性，可以在打开游标变量时定义查询，可以返回不同结构的结果集。
  - 使用游标变量包括：定义游标引用类型（REF CURSOR）、声明游标变量、打开游标变量、检索游标变量、关闭游标变量 

- 定义游标引用类型
  - 语法
    - TYPE ref_cursor_type_name IS REF CURSOR [RETURN return_type]
      RETURN子句用于指定定义的游标类型返回结果集的类型，该类型必须是记录类型。如果定义游标引用类型时带有RETURN子句，则用其定义的变量称为强游标变量，否则称为弱游标变量。
    - 在Oracle 10g中，系统预定义了一个游标引用类型，称为SYS_REFCURSOR，可以直接使用它定义游标变量。 

- 声明游标变量
  - 语法
    - ```plsql
      ref_cursor_type_name variable_name;
      ```
    
    - ```plsql
      TYPE emp_cursor_type IS REF CURSOR 
                     RETURN emp%ROWTYPE;
      TYPE general_cursor_type IS REF CURSOR;
      v_emp emp_cursor_type;
    v_general general_cursor_type;
      my_cursor SYS_REFCURSOR;
      ```
      
    - SYS_REFCURSOR：Oracle10g开始提供该游标
  
- 打开游标变量

  - 语法

    - ```plsql
OPEN cursor_variable FOR select_statement;
      ```
      
      > 注意：
      >
      > 如果打开的游标变量是强游标变量，则查询语句的返回类型必须与游标引用类型定义中RETURN子句指定的返回类型相匹配。
      
    - ```plsql
      OPEN v_emp FOR SELECT * FROM emp;
      OPEN v_general FOR SELECT 
                           empno,ename,sal,deptno FROM emp;
      OPEN my_cursor FOR SELECT * FROM dept;
      ```
  
- 检索游标变量

  - 语法
    - ```plsql
      LOOP
      	FETCH cursor_variable INTO variable1, variable2, …;
      	EXIT WHEN cursor_variable%NOTFOUND;
      	……
    END LOOP; 
      ```
      
      > 注意：
      >
      > 检索游标变量时只能使用简单循环或WHILE循环，不能采用FOR循环。
    
  - 案例
  
    - 要求根据输入的不同表名进行不同处理，若表名为emp，则显示高于10号部门平均工资的员工信息；若表名为dept，则显示各个部门的人数。 

#### 异常处理

- PL/SQL程序的错误
  - 编译错误
  - 运行时错误

Oracle中对运行时错误的处理采用了异常处理机制。 一个错误对应一个异常，当错误产生时抛出相应的异常，并被异常处理器捕获，程序控制权传递给异常处理器，由异常处理器来处理运行时错误。 

- 运行时错误
  - Oracle错误（Oracle中任何一个错误都有一个唯一的错误编号）
  - 用户定义错误

- 异常类型

  - 预定义的Oracle异常（ Oracle错误）

  ```plsql
  DECLARE
    v_ename emp.ename%TYPE;
  BEGIN
    SELECT ename INTO v_ename FROM emp WHERE empno=7300;--SMITH
    dbms_output.put_line('名字；'||v_ename);
  EXCEPTION
    WHEN NO_DATA_FOUND THEN
      dbms_output.put_line('找不到这个员工');
  END;
  ```

  - 非预定义的Oracle异常（ Oracle错误没有和预定义异常与其关联）

  - 用户定义的异常（用户定义错误）

- 预定义的Oracle异常
  - 当Oracle错误产生时，与错误对应的预定义异常被自动抛出，通过捕获该异常可以对错误进行处理。
  - 常用预定义异常包括


| 异常名字            | 错误代码  | 描述                                       |
| ------------------- | --------- | ------------------------------------------ |
| CURSOR_ALREADY_OPEN | ORA-06511 | 尝试打开已经打开的游标                     |
| INVALID_CURSOR      | ORA-01001 | 不合法的游标操作（如要打开已经关闭的游标） |
| NO_DATA_FOUND       | ORA-01403 | 没有发现数据                               |
| INVALID_NUMBER      | ORA-01722 | 转换数字失败                               |
| TOO_MANY_ROWS       | ORA-01422 | 一个SELECT  INTO语句匹配多个数据行         |
| ZERO_DIVIDE         | ORA-01476 | 除数为0                                    |
| DUP_VAL_ON_INDEX    | ORA-00001 | 违反唯一性约束或主键约束                   |
| TIMEOUT_ON_RESOURCE | ORA-00051 | 在等待资源中出现超时                       |
| LOGIN_DENIED        | ORA-01017 | 无效用户名/密码                            |

- 非预定义异常

  - 有一些Oracle错误没有预定义异常与其关联，需要在语句块的声明部分声明一个异常名称，然后通过编译指示PRAGMA EXCEPTION_INIT将该异常名称与一个Oracle错误相关联。此后，当执行过程出现该错误时将自动抛出该异常。

  - 例如，在执行下列操作时，产生ORA-02292的Oracle错误，由于没有与之对应的异常，因此该错误产生时没有异常抛出，从而无法捕获和处理。

  - SQL> DELETE FROM dept WHERE deptno=20;

    ORA-02292: 违反完整约束条件 (SCOTT.FK_DEPTNO) - 已找到子记录

  - 为了解决这样的问题，可以为该错误定义异常，然后通过异常来处理相应的错误。例如：

```plsql
DECLARE
  e_deptno_fk EXCEPTION;
  PRAGMA EXCEPTION_INIT(e_deptno_fk,-2292);
BEGIN
  ......
EXCEPTION
  ......
END;
```

- 用户自定义的异常
  - 用户定义错误是指，有些操作并不会产生Oracle错误，但是从业务规则角度考虑，认为是一种错误。例如，执行UPDATE操作没有更新任何行时，不会引发Oracle错误，也不会产生异常，但是，有时需要开发人员为此操作产生一个异常，以便进行处理，即用户定义异常。
  - 用户自定义异常必须在声明部分进行声明。当异常发生时，系统不能自动触发，需要用户使用RAISE语句。在异常处理部分捕捉并处理异常。

- 异常处理
  - 异常处理分3个步骤进行：
    - 在声明部分为错误定义异常，包括非预定义异常和用户定义异常。
    - 在执行过程中当错误产生时抛出与错误对应的异常。
    - 在异常处理部分通过异常处理器捕获异常，并进行异常处理。

- 异常定义

  - Oracle中的3种异常，其中预定义异常由系统定义，而其他两种异常则需要用户定义。

  - 定义异常方法

    - e_exception EXCEPTION;

  - 如果是非预定义的异常，需要将异常与一个Oracle错误相关联，其语法为：
    PRAGMA EXCEPTION_INIT(e_exception, -#####);

    > 注意：
    >
    > Oracle内部错误号用一个负的5位数表示，如-02292。其中-20999～-20000为用户定义错误的保留号。

- 异常抛出
  - 由于系统可以自动识别Oracle内部错误，因此当错误产生时系统会自动抛出与之对应的预定义异常或非预定义异常。但是，系统无法识别用户定义错误，因此当用户定义错误产生时，需要用户手动抛出与之对应的异常。
  - 用户定义异常的抛出语法为
    RAISE user_define_exception； 

- 异常捕获与处理

  - 异常处理器的基本形式为

  - ```plsql
    EXCEPTION
    WHEN exception1[OR excetpion2…]THEN 
       sequence_of_statements1;
    WHEN exception3[OR exception4…]THEN 
       sequence_of_statements2;
    ……
    WHEN OTHERS THEN 
       sequence_of_statementsn;
    END;
    ```

  - > 注意：
    >
    > 一个异常处理器可以捕获多个异常，只需在WHEN子句中用OR连接即可；
    >
    > 一个异常只能被一个异常处理器捕获，并进行处理。 

- 预定义异常及其处理
  
  - 查询名为SMITH的员工工资，如果该员工不存在，则输出“There is not such an employee!”；如果存在多个同名的员工，则输出其员工号和工资。
  
- 非预定义异常案例
  
  - 删除dept表中部门号为10的部门信息，如果不能删除则输出“There are subrecords in emp table!”。
  
- 自定义异常案例
  
  - 修改7844员工的工资，保证修改后工资不超过6000。(RETURNING sal INTO v_sal)
  
- OTHERS异常处理

```plsql
DECLARE
  v_sal emp.sal%TYPE;
  e_highlimit EXCEPTION;
BEGIN
  SELECT sal INTO v_sal FROM emp WHERE ename='JOAN';
  UPDATE emp SET sal=sal+100 WHERE empno=7900;
  IF v_sal>6000 THEN 
    RAISE e_highlimit;
  END IF;
EXCEPTION
  WHEN e_highlimit THEN
    DBMS_OUTPUT.PUT_LINE('The salary is too large!');
    ROLLBACK;
  WHEN OTHERS THEN
    DBMS_OUTPUT.PUT_LINE('There is some wrong in selecting!');
END;
/
```

虽然OTHERS可以捕获各种异常，但并不返回相关错误信息，无法判断到底是哪个错误产生了异常，因此可以通过两个函数来获取错误相关信息。

SQLCODE：返回当前错误代码。
如果是用户定义错误返回值为1；
如果是ORA-1403：NO DATA FOUND错误，返回值为100
其他Oracle内部错误返回相应的错误号。 
SQLERRM：返回当前错误的消息文本。
如果是Oracle内部错误，返回系统内部的错误描述；
如果是用户定义错误，则返回信息文本为“User-defined Exception”。 

例如：

```plsql
DECLARE
  v_sal emp.sal%TYPE;
  e_highlimit EXCEPTION;
  v_code NUMBER(6);
  v_text VARCHAR2(200);
BEGIN
  SELECT sal INTO v_sal FROM emp WHERE ename='JOAN';
  UPDATE emp SET sal=sal+100 WHERE empno=7900;
  IF v_sal>6000 THEN 
    RAISE e_highlimit;
  END IF;
EXCEPTION
  WHEN e_highlimit THEN
    DBMS_OUTPUT.PUT_LINE('The salary is too large!');
    ROLLBACK;
  WHEN OTHERS THEN
    v_code:=SQLCODE;
    v_text:=SQLERRM;   
    DBMS_OUTPUT.PUT_LINE(v_code||' '||v_text);
END;
/
```

- 异常的传播

  - 当PL/SQL块的执行部分产生异常后，根据当前块是否有该异常处理器，并进行错误处理，成功完成该语句块。然后，程序的控制流程传递到外层语句块，继续执行。
    - 例如：查询员工名字为JOAN的员工的薪水
    - NO_DATA_FOUND
  - 如果当前语句块没有该异常处理器，则通过在外层语句块的执行部分产生该异常来传播该异常。
    - 例如：查询10号部门的工资
    - NO_DATA_FOUND
    - TOO_MANY_ROWS

  - 无论是执行部分的异常，还是声明部分或异常处理部分的异常，如果在本块中没有处理，最终都将向外层块中传播。因此，通常在程序最外层的异常处理部分放置OTHERS异常处理器，以保证没有错误被漏掉检测，否则错误将传递到调用环境。

- 实训题

  ![实训题](./PLSQL01.png)

#### 存储过程

- 存储过程创建

  - 基本语法

  - ```plsql
    CREATE [OR REPLACE] PROCEDURE procedure_name
    (parameter1_name [mode] datatype 
        [DEFAULT|:=value]
    [, parameter2_name [mode] datatype 
        [DEFAULT|:=value],…])
    AS|IS
       /*Declarative section is here */
    BEGIN
       /*Executable section is here*/ 
    EXCEPTION
       /*Exception section is here*/ 
    END[procedure_name]; 
    ```

  - 参数的模式 

    - IN（默认参数模式）表示当过程被调用时，实参值被传递给形参；在过程内，形参起常量作用，只能读该参数，而不能修改该参数；当子程序调用结束返回调用环境时，实参没有被改变。IN模式参数可以是常量或表达式。
    - OUT表示当过程被调用时，实参值被忽略；在过程内，形参起未初始化的PL/SQL变量的作用，初始值为NULL，可以进行读/写操作；当子程序调用结束后返回调用环境时，形参值被赋给实参。OUT模式参数只能是变量，不能是常量或表达式。
    - IN OUT表示当过程被调用时，实参值被传递给形参；在过程内，形参起已初始化的PL/SQL变量的作用，可读可写；当子程序调用结束返回调用环境时，形参值被赋给实参。IN OUT模式参数只能是变量，不能是常量或表达式。 

- 参数的限制
  - 在声明形参时，不能定义形参的长度或精度、刻度，它们是作为参数传递机制的一部分被传递的，是由实参决定的。
  - 参数传递方式
    - 当子程序被调用时，实参与形参之间值的传递方式取决于参数的模式。IN参数为引用传递，即实参的指针被传递给形参；OUT，IN OUT参数为值传递，即实参的值被复制给形参。
    - 参数默认值
      可以为参数设置默认值，这样存储过程被调用时如果没有给该参数传递值，则采用默认值。需要注意，有默认值的参数应该放在参数列表的最后。 

- 案例：创建一个存储过程，以部门号为参数，查询该部门的平均工资，并输出该部门中比平均工资高的员工号、员工名。

通常，存储过程不需要返回值，如果需要返回一个值可以通过函数调用实现。但是，如果希望返回多个值，可以使用OUT或IN OUT模式参数来实现。

- 案例：创建一个存储过程，以部门号为参数，返回该部门的人数和最高工资。

- 存储过程调用

  - 在SQL*PLUS中调用

    ```plsql
    EXEC  procedure_name(parameter_list)或CALL procedure_name(parameter_list)
    EXECUTE show_emp(10)
    ```

  - 在PL/SQL块中调用

    ```plsql
    BEGIN
          procedure_name(parameter_list);
    END；
    ```

    在PL/SQL程序中，存储过程可以作为一个独立的表达式被调用。 

  - ```plsql
    DECLARE
      v_avgsal emp.sal%TYPE;
      v_count  NUMBER;
    BEGIN
       show_emp(20);
       return_deptinfo(10,v_avgsal,v_count);
       DBMS_OUTPUT.PUT_LINE(v_avgsal||' '||v_count);
    END;
    ```

- 函数

  - 函数创建

    - 基本语法为 

    - ```plsql
      CREATE [OR REPLACE] FUNCTION function_name 
      (parameter1_name [mode] datatype 
          [DEFAULT|:=value]
      [, parameter2_name [mode] datatype 
          [DEFAULT|:=value],…])
      RETURN return_datatype 
      AS|IS
           /*Declarative section is here */
      BEGIN
          /*Executable section is here*/ 
      EXCEPTION
          /*Exception section is here*/ 
      END [function_name]; 
      ```

    - > 注意：
      > 在函数定义的头部，参数列表之后，必须包含一个RETURN语句来指明函数返回值的类型，但不能约束返回值的长度、精度、刻度等。如果使用%TYPE，则可以隐含地包括长度、精度、刻度等约束信息；
      > 在函数体的定义中，必须至少包含一个RETURN 语句，来指明函数返回值。也可以有多个RETURN语句，但最终只有一个RETURN语句被执行。

- 案例：创建一个以部门号为参数，返回该部门最高工资的函数。

如果需要函数返回多个值，可以使用OUT或IN OUT模式参数。

- 案例：创建一个函数，以部门号为参数，返回部门名、部门人数及部门平均工资。

- 函数调用

  - 在SQL语句中调用函数

  - 在PL/SQL中调用函数

  - > 注意：
    > 函数只能作为表达式的一部分被调用。

  - 案例：通过对return_maxsal函数的调用，输出各个部门的最高工资；通过对ret_deptinfo函数调用，输出各个部门名、部门人数及平均工资。

  - 函数可以在SQL语句的以下部分调用

    - SELECT语句的目标列
    - WHERE和HAVING子句
    - CONNECT BY，START WITH，ORDER BY，GROUP BY子句
    - INSERT语句的VALUES子句中
    - UPDATE语句的SET子句中

  - 如果要在SQL中调用函数，那么函数必须符合下列限制和要求：

    - 在SELECT语句中的函数不能修改（INSERT，UPDATE，DELETE）调用函数的SQL语句中使用的表
    - 函数在一个远程或并行操作中使用时，不能读/写封装变量
    - 函数必须是一个存储数据库对象（或存储在包中）
    - 函数的参数只能使用IN模式
    - 形式参数类型必须使用数据库数据类型
    - 返回的数据类型必须是数据库数据类型

#### 包

- 概念包是包含一个或多个子程序单元（过程、函数等）的容器。包是一种全局结构 。

- 包类型
  - 数据库内置包
  - 用户创建的包

- 包构成
  - 包头
    - 包头声明了包中所有内容，如过程、函数、游标、类型、异常和变量等，其中过程和函数只包括原型信息，不包含任何子程序代码。  
  - 包体
    - 包体中包含了在包头中的过程和函数的实现代码。包体中还可以包括在包头中没有声明的变量、游标、类型、异常、过程和函数，但是它们是私有元素，只能由同一包体中其他过程和函数使用。

- 创建包头

```plsql
CREATE OR REPLACE PACKAGE package_name 
IS|AS
[PRAGMA SERIALLY_RESUABLE]
  type_definition|variable_declaration|
  exception_declaration|cursor_declaration| 
  procedure_ declaration|function_ declaration
END [package_name];
```

> 注意：
> 元素声明的顺序可以是任意的，但必须先声明后使用；
> 所有元素是可选的；
> 过程和函数的声明只包括原型，不包括具体实现。

- 包头示例：创建一个包头，包括2个变量、2个过程和1个异常。

  ```plsql
  CREATE OR REPLACE PACKAGE pkg_emp
  AS
    minsal   NUMBER;
    maxsal   NUMBER;
    e_beyondbound  EXCEPTION;
    PROCEDURE update_sal(
             p_empno NUMBER, p_sal NUMBER);
    PROCEDURE add_employee(
             p_empno NUMBER,p_sal NUMBER);
  END pkg_emp;
  ```

- 创建包体

```plsql
CREATE OR REPLACE PACKAGE BODY package_name 
IS|AS
[PRAGMA SERIALLY_RESUABLE]
  type_definition|variable_declaration|
  exception_declaration|
  cursor_declaration| 
  procedure_definition |
  function_definition
END [package_name]; 
```

```plsql
CREATE OR REPLACE PACKAGE BODY pkg_emp
AS
    PROCEDURE update_sal(p_empno NUMBER, p_sal NUMBER)
    AS
    BEGIN
      SELECT min(sal), max(sal) INTO minsal,maxsal FROM emp;
      IF p_sal BETWEEN minsal AND maxsal THEN
        UPDATE emp SET sal=p_sal WHERE empno=p_empno;
        IF SQL%NOTFOUND THEN
          RAISE_APPLICATION_ERROR(-20000,'The employee doesn''t exist');
        END IF;
      ELSE
        RAISE e_beyondbound;
      END IF;
   EXCEPTION
      WHEN e_beyondbound THEN
         DBMS_OUTPUT.PUT_LINE('The salary is beyond bound! ');
    END update_sal; 
    PROCEDURE add_employee(p_empno NUMBER,p_sal NUMBER)
    AS
    BEGIN
      SELECT min(sal), max(sal) INTO minsal,maxsal FROM emp;
      IF p_sal BETWEEN minsal AND maxsal THEN
         INSERT INTO emp(empno,sal) VALUES(p_empno,p_sal);
      ELSE
         RAISE e_beyondbound;
      END IF;
  EXCEPTION
    WHEN e_beyondbound THEN
      DBMS_OUTPUT.PUT_LINE('The salary is beyond bound! ');
  END add_employee;
END pkg_emp;
```

- 包的调用：在包头内声明的任何元素是公有的，在包外都是可见的

  - 包外：通过package.element形式调用；

  - 包内：直接通过元素名进行调用。 

  - 在包体中定义而没有在包头中声明的元素是私有的，只能在包体中引用 

  - 调用包pkg_emp中的过程update_sal，修改7844员工工资为3000。调用add_employee添加一个员工号为1357，工资为4000的员工。

    ```plsql
    BEGIN
      pkg_emp.update_sal(7844,3000);
      pkg_emp.add_employee(1357,4000);
    END;
    ```

#### 触发器

- 概念
  - 触发器是一种特殊类型的存储过程，编译后存储在数据库服务器中。
  - 当特定事件发生时，由系统自动调用执行，而不能由应用程序显式地调用执行。
  - 触发器不接受任何参数。
  - 触发器主要用于维护那些通过创建表时的声明约束不可能实现的复杂的完整性约束，并对数据库中特定事件进行监控和响应。

- 触发器类型
  - DML触发器
    - 建立在基本表上的触发器，响应基本表的INSERT，UPDATE，DELETE操作。
  - INSTEAD OF触发器
    - 建立在视图上的触发器，响应视图上的INSERT，UPDATE，DELETE操作。
  - 系统触发器
    - 建立在系统或模式上的触发器，响应系统事件和DDL（CREATE，ALTER，DROP）操作。 

- 触发器组成
  - 触发器由触发器头部和触发器体两个部分组成
  - 主要包括：
    - 作用对象：触发器作用的对象包括表、视图、数据库和模式。
    - 触发事件：激发触发器执行的事件。如DML、DDL、数据库系统事件等。
    - 触发时间：用于指定触发器在触发事件完成之前还是之后执行。如果指定为AFTER，则表示先执行触发事件，然后再执行触发器；如果指定为BEFORE，则表示先执行触发器，然后再执行触发事件。
    - 触发级别：触发级别用于指定触发器响应触发事件的方式。默认为语句级触发器，即触发事件发生后，触发器只执行一次。如果指定为FOR EACH ROW，即为行级触发器，则触发事件每作用于一个记录，触发器就会执行一次。
    - 触发条件：由WHEN子句指定一个逻辑表达式，当触发事件发生，而且WHEN条件为TRUE时，触发器才会执行。
    - 触发操作：触发器执行时所进行的操作。

- DML触发器的种类
  - 语句级前触发器
  - 语句级后触发器
  - 行级前触发器
  - 行级后触发器

- DML触发器的执行顺序
  - 如果存在，则执行语句级前触发器
  - 对于受触发事件影响的每一个记录
    - 如果存在，则执行行级前触发器
    - 执行当前记录的DML操作（触发事件）
    - 如果存在，则执行行级后触发器
  - 如果存在，则执行语句级后触发器

- 创建DML触发器

  ```plsql
  CREATE [OR REPLACE] TRIGGER trigger_name
  BEFORE|AFTER triggering_event [OF column_name]
  ON table_name]
  [FOR EACH ROW]
  [WHEN trigger_condition]
  DECLARE
       /*Declarative section is here */
  BEGIN
       /*Exccutable section si here*/ 
  EXCEPTION
       /*Exception section is here*/ 
  END [trigger_name];
  ```

- 语句级触发器

  - 在默认情况下创建的DML触发器为语句级触发器，即触发事件发生后，触发器只执行一次。 

  - 创建一个触发器，禁止在休息日改变雇员信息

  - ```plsql
    CREATE OR REPLACE TRIGGER trg_emp_weekend
    BEFORE INSERT OR UPDATE OR DELETE ON emp
    BEGIN
       IF TO_CHAR(SYSDATE, 'DY', 'nls_date_language=american') IN('SAT', 'SUN')
      THEN
          RAISE_APPLICATION_ERROR(-20000, 'Can''t operate in weekend.');
      END IF;
    END trg_emp_weekend;
    ```

- 触发器响应多个DML事件

| 谓词      | 行为                                        |
| --------- | ------------------------------------------- |
| INSERTING | 如果触发语句是INSERT，则为TRUE；否则为FALSE |
| UPDATING  | 如果触发语句是UPDATE，则为TRUE；否则为FALSE |
| DELETING  | 如果触发语句是DELETE，则为TRUE；否则为FALSE |

- 响应多个DML事件案例：为emp表创建一个日志触发器，当执行插入操作时，统计操作后员工人数；当执行更新操作时，统计更新后员工平均工资；当执行删除操作时，统计删除后各部门的人数。

- 行级触发器
  - 行级触发器是指执行DML操作时，每操作一个记录，触发器就执行一次，一个DML操作涉及多少个记录，触发器就执行多少次。
  - 在行级触发器中可以使用WHEN条件，进一步控制触发器的执行。
  - 在行级触发器中引入了:old和:new 两个标识符，来访问和操作当前被处理记录中的数据。 

- 标识符

  - :old和:new作为triggering_table%ROWTYPE类型的两个变量

  - 引用方式

    - :old.field和:new.field （执行部分）
    - old.field 和new.field   (WHEN条件中)

  - 在不同触发事件中，:old和:new的意义不同

    | 触发事件 | :old                     | :new                       |
    | -------- | ------------------------ | -------------------------- |
    | INSERT   | 未定义，所有字段都为NULL | 当语句完成时，被插入的记录 |
    | UPDATE   | 更新前原始记录           | 当语句完成时，更新后的记录 |
    | DELETE   | 记录被删除前的原始值     | 未定义，所有字段都为NULL   |

  - 案例：为emp表创建一个触发器，当插入新员工时显示新员工的员工号、员工名；当更新员工工资时，显示修改后的员工工资；当删除员工时，显示被删除的员工的员工号、员工名。

  - 在行级触发器中，可以使用WHEN子句进一步控制触发器的执行。例如：修改员工工资时，保证修改后的工资高于修改前的工资。

  - ```plsql
    CREATE OR REPLACE TRIGGER trg_emp_update_row
    BEFORE UPDATE OF sal ON emp
    FOR EACH ROW
    WHEN(new.sal<old.sal)
    BEGIN
    	RAISE_APPLICATION_ERROR(-20002,'The salary is lower!');
    END;
    ```

- INSTEAD OF触发器
  - 特点
    - 只能定义在视图上
    - Instead-of触发器是行级触发器
    - Instead-of触发器由DML操作激发，而DML操作本身并不执行
  - 作用
    - 修改一个本来不可以修改的视图

- 如果视图中包含下列任何一项，则该视图不可修改
  - 集合操作符（UNION，UNION ALL，MINUS，INTERSECT）；
  - 聚集函数（SUM，AVG等）；
  - GROUP BY，CONNECT BY或START WITH子句；
  - DISTINCT操作符；
  - 涉及多个表的连接操作。

- 创建INSTEAD OF触发器的基本语法

```plsql
CREATE [OR REPLACE] TRIGGER trigger_name
INSTEAD OF triggering_event [OF column_name]
ON view_name 
FOR EACH ROW
[WHEN trigger_condition]
DECLARE
      /*Declarative section is here */
BEGIN
      /*Exccutable section si here*/ 
EXCEPTION
      /*Exception section is here*/ 
END [trigger_name];
```

案例：创建一个包括员工及其所在部门信息的视图empdept，然后向视图中插入一条记录(2345,’TOM’,3000,90,’SALES’)

```plsql
CREATE OR REPLACE VIEW empdept 
AS
SELECT empno,ename,sal,dname 
FROM emp,dept WHERE emp.deptno=dept.deptno  
WITH CHECK OPTION;

SQL> INSERT INTO empdept VALUES(2345, 'TOM',3000,'SALES');
INSERT INTO empdept
*
第 1 行出现错误:
ORA-01733: 此处不允许虚拟列
```

在empdept视图上创建一个INSTEAD OF触发器

```plsql
CREATE OR REPLACE TRIGGER trig_view
INSTEAD OF INSERT ON empdept
FOR EACH ROW
DECLARE
	v_deptno dept.deptno%TYPE;
BEGIN
	SELECT deptno INTO v_deptno FROM dept WHERE dname=:new.dname;
	INSERT INTO emp(empno,ename,deptno,sal) VALUES (:new.empno,:new.ename,v_deptno,:new.sal);
END;
/
```

```sql
CREATE OR REPLACE VIEW test AS SELECT p.*,c.*,o.amount
FROM product p,customer c,orders o
WHERE p.id=o.id
AND c.acid=o.acid;
/
INSERT INTO test VALUES(6,'内存',230.0,'数码',4,'贾柳','桂林',3);
CREATE OR REPLACE TRIGGER trigger3
INSTEAD OF INSERT ON test
BEGIN
  INSERT INTO product VALUES(:NEW.id,:NEW.name,:NEW.price,:NEW.type);
  INSERT INTO customer VALUES(:NEW.acid,:NEW.acname,:NEW.acaddress);
  INSERT INTO orders VALUES(:NEW.acid,:NEW.id,:NEW.amount);
END;
/
```

- 系统触发器
  - 触发事件
    - DDL事件（CREATE、ALTER、DROP、RENAME、GRANT、REVOKE、AUDIT、NOAUDIT、COMMENT、TRUNCATE、ANALYZE、ASSOCIATE STATISTICS、DISASSOCIATE STATISTICS等）
    - 数据库事件（STARTUP、SHUTDOWN，LOGON、LOGOFF、SERVERERROR等），触发时间由具体事件决定

| 事件        | 允许计时 | 描述                   |
| ----------- | -------- | ---------------------- |
| STARTUP     | AFTER    | 实例启动时触发         |
| SHUTDOWN    | BEFORE   | 实例关闭时触发         |
| SERVERERROR | AFTER    | 服务器发生错误触发     |
| LOGON       | AFTER    | 用户和实例建立会话触发 |
| LOGOFF      | BEFORE   | 用户注销时触发         |

- 创建系统触发器

```plsql
CREATE [OR REPLACE] TRIGGER trigger_name
BEDORE|AFTER ddl_event_list|database_event_list
ON DATABASE|SCHEMA
[WHEN trigger_condition]
DECLARE
	/* Declarative section is here */
BEGIN
	/* Executable section is here */
EXCEPTION
	/* Exception section is here */
END [trigger_name];
```

- 案例：将每个用户的登录信息写入temp_table表中

- ```plsql
  CREATE OR REPLACE TRIGGER log_user_connection
  AFTER LOGON ON DATABASE
  BEGIN
  	INSERT INTO temp_table VALUES(user,sysdate);
  END log_user_connection;
  /
  ```

- 当数据库执行CREATE操作时，将创建对象的信息记录到ddl_creations表中

- ```plsql
  CREATE TABLE ddl_creations(
  	user_id			VARCHAR2(30),
      object_type		VARCHAR2(20),
      object_name		VARCHAR2(30),
      object_owner	VARCHAR2(30),
      creation_date	DATE
  );
  CREATE OR REPLACE TRIGGER log_creations
  AFTER CREATE ON DATABASE
  BEGIN
  	INSERT INTO ddl_creations VALUES(ora_login_user,ora_dict_obj_type,ora_dict_obj_name,ora_dict_obj_owner,sysdate);
  END;
  /
  ```

  - 事件属性函数
  
  <img src = "./PLSQL03.png" align="center">

  <img src = "./PLSQL04.png" align="center">
  
- 实训题

  ![实训题](./PLSQL02.png)