### prepareStatement和Statement的区别

```java
SQL存在输入变量时
/*
简述：
perpareStatement：
	perpareStatement使用占位符?占位置,相当字符串类型，往占位符里放入数字类型或字符串类型,不需要'',相当于sql中的''等于java中的""，占位符不能单独处在'',""之间
缺点：占位符不能指代表名或字段名
select * from ? where ? = ?;  存入值后如下
select * from 'department' where 'Did' = '2';  错误提示找不到表

Statement使用拼sql，sql中varchar2（字符串）类型需要''包起来

两方法详解如下
*/
//prepareStatement:
    Connection conn=null;
    String url="jdbc:oracle:thin:@120.77.203.216:1521:orcl";
    PreparedStatement pstmt=null;
    String sql="SELECT * FROM emp where deptno=?";
    ResultSet rs=null;
    try {
        Class.forName("oracle.jdbc.driver.OracleDriver");
        conn=DriverManager.getConnection(url,"scott","tiger");
        System.out.println(conn);
        pstmt=conn.prepareStatement(sql);
        pstmt.setString(1,"ALLEN");
        rs=pstmt.executeQuery();
        while(rs.next()){
            String name=rs.getString("ename");
            float salay=rs.getFloat("sal");
            System.out.print("\t"+name);
            System.out.println("\t"+salay);
        }
    }
//Statenent
	Connection conn=null;
    String url="jdbc:oracle:thin:@120.77.203.216:1521:orcl";
    Statement stmt=null;
    String sql="SELECT * FROM emp where ename='"+"ALLEN"+"'";
    ResultSet rs=null;
    try {
        Class.forName("oracle.jdbc.driver.OracleDriver");
        conn=DriverManager.getConnection(url,"scott","tiger");
        System.out.println(conn);
        stmt=conn.createStatement();
        rs=stmt.executeQuery(sql);
        while(rs.next()){
            String name=rs.getString("ename");
            float salay=rs.getFloat("sal");
            System.out.print("\t"+name);
            System.out.println("\t"+salay);
        }
    }
```

### 往数据库插入时间

```java
Date date=new Date();
        System.out.println(new java.sql.Date(date.getTime()));
```

### 异常的使用

```
比如执行sql语句违反唯一性约束会出现异常，可以根据这个异常输出一个提示
```

### 结果集ResultSet

```
用JDBC从数据库中查询数据要用到结果集ResultSet，其中我们在获取结果的时候经常用到rs.next()方法来判断是否查询到了数据。

但是要特别注意，next()方法用一次，就往后移了一位，此时再使用next()来获取结果就是结果集中的第二个记录了。
```

