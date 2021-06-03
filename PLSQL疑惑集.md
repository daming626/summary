```sql
SQL> DECLARE
  2  CURSOR cur_emp IS SELECT a.ename,a.empno,a.deptno,b.ename,b.empno,b.deptno FROM emp a,emp b WHERE a.empno=b.mgr;
  3  v_emp emp%ROWTYPE;
  4  BEGIN
  5    For v_emp IN cur_emp
  6    LOOP
  7      dbms_output.put_line('员工姓名：'||v_emp.ename||chr(9)||'员工号：'||v_emp.empno||chr(9)||'部门号：'||v_emp.deptno);
  8    END LOOP;
  9  END;
 10  /

--错误提示
ORA-06550: 第 5 行, 第 3 列: 
PLS-00402: alias required in SELECT list of cursor to avoid duplicate column names
ORA-06550: 第 5 行, 第 3 列: 
PL/SQL: Statement ignored

--纠正 SELECT b表的字段加别名
SQL> DECLARE
  2  CURSOR cur_emp IS SELECT a.ename,a.empno,a.deptno,b.ename bname,b.empno bempno,b.deptno bdeptno FROM emp a,emp b WHERE a.empno=b.mgr;
  3  v_emp emp%ROWTYPE;
  4  BEGIN
  5    For v_emp IN cur_emp
  6    LOOP
  7      dbms_output.put_line('员工姓名：'||v_emp.ename||chr(9)||'员工号：'||v_emp.empno||chr(9)||'部门号：'||v_emp.deptno);
  8    END LOOP;
  9  END;
 10  /
员工姓名：JONES	员工号：7566	部门号：20
员工姓名：JONES	员工号：7566	部门号：20
员工姓名：BLAKE	员工号：7698	部门号：30
员工姓名：BLAKE	员工号：7698	部门号：30
员工姓名：BLAKE	员工号：7698	部门号：30
员工姓名：BLAKE	员工号：7698	部门号：30
员工姓名：BLAKE	员工号：7698	部门号：30
员工姓名：CLARK	员工号：7782	部门号：10
员工姓名：SCOTT	员工号：7788	部门号：20
员工姓名：KING	员工号：7839	部门号：10
员工姓名：KING	员工号：7839	部门号：10
员工姓名：KING	员工号：7839	部门号：10
员工姓名：FORD	员工号：7902	部门号：20
PL/SQL procedure successfully completed
```

```sql
SQL> DECLARE
  2  CURSOR cur_emp IS SELECT a.ename,a.empno,a.deptno FROM emp a,emp b WHERE a.empno=b.mgr;
  3  v_emp emp%ROWTYPE;
  4  BEGIN
  5    OPEN cur_emp;
  6    For v_emp IN cur_emp
  7    LOOP
  8      dbms_output.put_line('员工姓名：'||v_emp.ename||chr(9)||'员工号：'||v_emp.empno||chr(9)||'部门号：'||v_emp.deptno);
  9    END LOOP;
 10    CLOSE cur_emp;
 11  END;
 12  /

--错误提示
ORA-06511: PL/SQL: 游标已经打开
ORA-06512: 在 line 2
ORA-06512: 在 line 6

--纠正 去掉open close游标(目前常见SELECT * 要加)
```

```sql

```

