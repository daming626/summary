#### PL/SQL����

PL/SQL��Procedual Language extensions to SQL����Oracle�Ա�׼SQL���ԵĹ��̻���չ����Oracle���ݿ�ר�õ�һ�ָ߼������������

����SQL���Խ��û�������ʵ�ʵ����ݽṹ���㷨�ȷ��룬�޷���һЩ���ӵ�ҵ���߼����д������Oracle���ݿ�Ա�׼��SQL���Խ�������չ����SQL���Եķǹ��̻���������������ԵĹ��̻���ϣ�������PL/SQL���ԡ���PL/SQL�����У��ȿ���ͨ��SQL����ʵ�ֶ����ݿ�Ĳ�����Ҳ����ͨ�����̻������еĸ����߼��ṹ��ɸ��ӵ�ҵ���߼���

���磺

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

���������У�SELECT����2��UPDATE����Ƿǹ��̻���SQL���ԣ���ɶ����ݿ�Ĳ�������������������IF�����߼��ж����ǹ��̻����Ե�Ӧ�á�


PL/SQL���򿪷���Ҫ�������洢���̡����������ʹ�������Ӧ�ÿ�����

#### PL/SQL���ص㣺

- ��SQL���Խ��ܼ��ɣ����е�SQL�����PL/SQL�ж����Եõ�֧��

- �����������������Ӧ�ó�������ܡ�

  ![������������](./PLSQL00.png)

- ģ�黯�ĳ�����ƹ��ܣ������ϵͳ�ɿ��ԡ�PL/SQL�����Կ�Ϊ��λ��ÿ�������һ�������ĳ���ʵ���ض��Ĺ��ܡ������֮���໥������Ӧ�ó������ͨ���ӿڴӿͻ��˵������ݿ�������˵ĳ���顣���磺��ҳ�洢���̡������洢���̡�ת�˴洢���̡�

#### PL/SQL����ṹ

```plsql
DECLARE
  �������֣������������������������͡��αꡢ�쳣���������Լ����أ��ֲ����ӳ�����ȡ�
BEGIN
  ִ�в��֣�ʵ�ֿ�Ĺ��ܡ��ò���ͨ��������ֵ�����̿��ơ����ݲ�ѯ�����ݲ��ݡ����ݶ��塢������ơ��α괦���ʵ�ֿ�Ĺ���
EXCEPTION
  �쳣�����֣��������ִ�й����в������쳣
END;
/
```

> ע�⣺
>
> ���е�PL/SQL�鶼����"END;"����

- ����һ�������������֡�ִ�в��ֺ��쳣�����ֵ�PL/SQL��
  - ���磺�ҳ�����Ϊ190��Ա�����֣���������������û�����Ա������ʾ�Ҳ������Ա��
- SELECT ename INTO v_ename FROM emp WHERE empno=190;
  
- ����һ��ֻ����ִ�в��ֵ�PL/SQL��
  - ���Hello,World!

#### PL/SQL��ķ���

- �����飨�޷��ظ����ã������ڲ���
- ������  �洢���̡�����������������

#### ��������

- �������ͣ�BINARY_INTEGER��PLS_INTEGER��NUMBER
  - NUMBER������ʮ������ʽ�洢�����͸��������﷨ΪNUMBER��p��s�������У�pΪ���ȣ���������Ч����λ����sΪ�̶ȷ�Χ����С��λ����p��ȡֵ��ΧΪ1��38
  - BINARY_INTEGER�������ڱ�ʾ��-2147483647��+2147483647֮����������Զ�������ʽ�洢�����������ʱ�����Զ�ת����NUMBER���͡�
  - PLS_INTEGER���ͱ�ʾ��Χ��BINARY_INTEGER��ͬ�����������ʱ���������

- �ַ����ͣ�CHAR��NCHAR��VARCHAR2��NVARCHAR2��VARCHAR��LONG
  
  - PL/SQL�е��ַ�������Oracle���ݿ��е��ַ��������ƣ����������ַ����ĳ���������ͬ��
- VARCHAR2��CHAR��Ҫ���ڴ洢���Ա������ݿ��ַ������ַ�����NCHAR��NVARCHAR2 ���ڴ洢���Թ����ַ������ַ����� 
  
  | ����      | PL/SQL������ֽ��� | Oracle������ֽ��� |
  | --------- | ------------------ | ------------------ |
  | VARCHAR2  | 32767              | 4000               |
  | NVARCHAR2 | 32767              | 4000               |
  | CHAR      | 32767              | 2000               |
  | NCHAR     | 32767              | 2000               |
| LONG      | 32760              | 2G                 |
  
- �������ͣ�DATE��TIMESTAMP��INTERVAL

  - DATE�������ݿ��е�DATE������ͬ���洢���ں�ʱ����Ϣ���������͡��ꡢ�¡��ա�Сʱ���ֺ��룬���������С�����֡�
  - TIMESTAMP����DATE�������ƣ����������С�����֣�������3����ʽ��
    - TIMESTAMP[(p)]������pΪ���ֶε�С�����־��ȡ�
    - TIMESTAMP[(p)]WITH TIME ZONE�����ص�ǰʱ����ʱ�����
    - TIMESTAMP[(p)]WITH LOACL TIME ZONE���������ݿ�ʱ����ʱ�����

  - INTERVAL�����ڴ洢����ʱ���֮���ʱ������������������ʽ��
    - INTERVAL YEAR [(p)]TO MONTH������ʱ�������������������
    - INTERVAL DAY[(dp)] TO SECOND[(sp)]������ʱ�������������������

- �б�ʶ���ͣ�ROWID��UROWID
  - ROWID��ʾ�е������ַ
  - UROWID�ȿ��Ա�ʾ�е������ַ��Ҳ���Ա�ʾ�е��߼���ַ��

- �������ͣ�BOOLEAN��TRUE��FALSE��NULL��
  
  - ֻ����PL/SQL��ʹ�ã���ȡֵΪ�߼�ֵ������TRUE��FALSE��NULL��
  
- ���ʽ��RAW��LONG RAW

  | ����     | PL/SQL������ֽ��� | Oracle������ֽ��� |
  | -------- | ------------------ | ------------------ |
  | RAW      | 32767              | 2000               |
  | LONG RAW | 32767              | 2G                 |

- LOB���ͣ�CLOB��BLOB��NCLOB��BFILE
  - BLOB��Ŷ��������ݣ�CLOB��NCLOB����ı����ݣ���BFILE���ָ�����ϵͳ�ļ���ָ�롣
  - LOB���ͱ������Դ洢4 GB����������

- �������ͣ�REF CURSOR��REF object_type
  
  - �������������������߼������е�ָ�����͡���PL/SQL�У��������Ͱ����α���������ͺͶ�����������ͣ���REF CURSOR��REF object_type
  
- ��¼���ͣ�RECORD
  - ��¼�����Ǹ������ͣ�������C�����еĽṹ�壬��һ���������ɸ���Ա�����ĸ������͡�
    ��ʹ�ü�¼����ʱ����Ҫ�����������ֶ����¼���ͺͼ�¼���͵ı�����Ȼ����ִ�в������øü�¼���ͱ��������Ա������

- �������ͣ�TABLE��VARRAY
  - ���������Ǹ������ͣ��������������͡�Ƕ�ױ����ͺͿɱ��������͡�
  - �����������¼���͵��������ڣ���¼�����еĳ�Ա���������ǲ�ͬ���͵ģ������ڽṹ�壬���������������еĳ�Ա�������������ͬ���������ͣ����������顣 

- %TYPE��%ROWTYPE
  - ���Ҫ����һ��������ĳ���������������ͻ����ݿ����ĳ���е���������һ�£���֪���ñ������е��������ͣ��ı�������������%TYPE��ʵ�֡�
  - ���Ҫ����һ�������ݿ���ĳ����ṹһ�µļ�¼���͵ı���������ʹ��%ROWTYPE��ʵ�֡� 

#### �����볣���Ķ���

variable_name [CONSTANT] datatype [NOT NULL] [DEFAULT|:=expression];

#### ��¼���ͣ����С����У�

�����¼���͵��﷨Ϊ��
TYPE record_type IS RECORD(
field1 datatype1 [NOT NULL][DEFAULT|:=expr1],
field2 datatype2 [NOT NULL][ DEFAULT|:=expr2],
����
fieldn datatypen [NOT NULL][ DEFAULT|:=exprn]
);

- �û������¼���ͼ�����

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

- ����%ROWTYPE��ȡ��¼���Ͷ������

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

- ��¼���ͱ�����Ӧ��

  - SELECT INTO ��ʹ��

  ```plsql
  DECLARE
    v_emp emp%ROWTYPE; 
  BEGIN
    SELECT * INTO v_emp FROM emp
    WHERE empno=7844;
    DBMS_OUTPUT.PUT_LINE(v_emp.empno||' '||v_emp.ename||' '||v_emp.sal);  
  END;
  ```

  - INSERT�����ʹ��

  ```plsql
  DECLARE
   v_dept dept%ROWTYPE;
  BEGIN
   v_dept.deptno:=50;
   v_dept.loc:='BEIJING';
   v_dept.dname='DEV';
   INSERT INTO dept VALUES v_dept;
  ```

  - UPDATE��ʹ��

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

  - DELETE��ʹ��

  ```plsql
  DECLARE
   v_emp emp%ROWTYPE;
  BEGIN
   SELECT * INTO v_emp FROM emp WHERE empno=7844;
   DELETE FROM emp WHERE deptno=v_emp.deptno;
  END;
  ```

#### ������ʾ

����ָʾ�ǶԱ�����򷢳�������ָ�Ҳ��Ϊαָ�����ı�����塣��ֻ���������򴫵���Ϣ��������Ƕ����SQL�е�ע�͡�
��PL/SQL��ʹ��PRAGMA�ؼ���֪ͨ�������PL/SQL����ʣ�ಿ����һ������ָʾ���������ָʾ�ڱ���ʱ������������������ʱ��ִ�У�������C�����е�#define��
PL/SQL�ṩ����4�ֱ���ָʾ��

- EXCEPTION_INIT�����߱������һ���ض��Ĵ��������������������쳣��ʶ������������
- RESTRICT_REFERENCES�����߱������������Ĵ��ȣ����Ժ����п���ʹ�õ�SQL���Ͱ������������ơ�
- SERIALLY_REUSEABLE������PL/SQL��������ʱ������������֮�䲻Ҫ���ְ������ݡ�
- AUTONOMOUS_TRANSACTION�����߱�����򣬸ó����Ϊ�������񣬼���������ύ�ͻع��Ƕ������еģ��ó�����COMMIT��ROLLBACK��Ӱ���������

���磺

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
    --�̻�����&����&����������
    v_etl_level     VARCHAR2(40) := UPPER('ADM');
    v_etl_task_name VARCHAR2(30) := UPPER('F_A_A_C_VALID_SUM');
    v_sys_no        VARCHAR2(20) := UPPER('CRM');
    v_flag          INTEGER := 0; --����ֵΪ0��������������1������
    v_return        INTEGER := 0;
BEGIN
......
END;
```

#### PL/SQL�е�SQL���

����PL/SQLִ�в������ڰ󶨣����ڱ���׶ζԱ������а󶨣�ʶ������б�ʶ����λ�ã�����û�Ȩ�ޡ����ݿ�������Ϣ�������PL/SQL��ֻ�������: 

- SELECT 

  - ���磺����Ա������Ա���Ų�ѯԱ����Ϣ��
  - > ע�⣺
    >
    > SELECT��INTO���ֻ�ܲ�ѯһ����¼����Ϣ�����û�в�ѯ���κ����ݣ������NO_DATA_FOUND�쳣�������ѯ�������¼��������TOO_MANY_ROWS�쳣��
    > INTO���Ӻ�ı������ڽ��ղ�ѯ�Ľ���������ĸ�����˳��Ӧ�����ѯ��Ŀ��������ƥ�䣬Ҳ�����Ǽ�¼���͵ı�����

- DML(UPDATE��DELETE��INSERT)

- ���������䣨COMMIT��ROLLBACK��SAVEPOINT��

  > ע�⣺
  >
  > DDL��䲻����ֱ��ʹ�ã�����ʹ�ö�̬SQL�ķ�ʽִ��

- ��̬SQL��������֣�������ֵ�����̶���
  - EXECUTE IMMEDIATE DDL;
  - EXECUTE IMMEDIATE SQL INTO  ������;

- RETURNING

  - ���Ҫ��ѯ��ǰDML�������ļ�¼����Ϣ��������DML���ĩβʹ��RETURNING��䷵�ظü�¼����Ϣ��

  - RETURNING���Ļ����﷨��

    - RETURNING select_list_item INTO variable_list|record_variable; 
    - ���磺

    ```plsql
    DECLARE
       v_sal emp.sal%TYPE;
    BEGIN
       UPDATE emp SET sal=sal+100 WHERE empno=7844 
                                                RETURNING sal INTO v_sal;
       DBMS_OUTPUT.PUT_LINE(v_sal);
    END;
    ```

#### ���̿���

- ѡ��ṹ

  - IF���

    - ```plsql
      IF ����1 THEN ���1
      	[ELSIF ����2 THEN ���2]
      	......
      	[ELSE ���]
    END IF;
      ```

  - CASE���

    - ��CASE

    - ```plsql
  CASE test_value
      	WHEN value1 THEN statement1;
  	WHEN value2 THEN statement2;
      	......
  	WHEN valuen THEN statementn;
      	[ELSE else_statement;]
      END CASE;
      ```
      
    - ����CASE
      
    - ```plsql
      CASE
      	WHEN condition1 THEN statement1;
        	WHEN condition2 THEN statement2;
      	......
        	WHEN conditionn THEN statementn;
      	[ELSE else_statement;]
      END CASE;
      ```
  
- IF���ͼ���CASE����������һ��Ա���ţ��޸ĸ�Ա���Ĺ��ʣ������Ա��Ϊ10�Ų��ţ���������100����Ϊ20�Ų��ţ���������150����Ϊ30�Ų��ţ���������200����������300�� 
  
- ������CASE���������������Ա���ţ��޸ĸ�Ա���Ĺ��ʣ�������ʵ���1000�����ʼ�200�����������1000~2000֮��������150�����������2000~3000֮�䣬������100����������50��
  
- ѭ���ṹ

  - ��ѭ��
    
  - ```plsql
    LOOP
      ���
      EXIT [WHEN ����];
    END LOOP;
    ```
    
  - ������ѭ���������50����¼

- WHILEѭ��

  - ```plsql
    WHILE ���� LOOP
        ���;
    END LOOP;
    ```

  - ����������WHILEѭ����������50����¼

- ����FORѭ��

  - ```plsql
    FOR loop_counter IN [REVERSE] low_bound..high_bound LOOP
      ���;
    END LOOP
    ```

#### �α�

�α꣨CURSOR����Oracleϵͳ���ڴ��п��ٵ�һ���������������д��SELECT��䷵�صĲ�ѯ�����ʹ���α�ʱ��SELECT����ѯ�Ľ�������ǵ�����¼��������¼��Ҳ������������¼���α깤�����У�������һ��ָ�루POINTER��,�ڳ�ʼ״̬��ָ���ѯ������׼�¼��

- �α����
  - ��ʽ�α꣺�û����塢���������ڷ��ض������ݵ�SELECT��ѯ
  - ��ʽ�α꣺ϵͳ�Զ����������ڴ���DML���ͷ��ص������ݵ�SELECT

- ��ʽ�α�
  - ��ʽ�α�Ĳ���
  - ��ʽ�α������
  - ��������ʽ�α�
  - ��ʽ�α�ļ���
  - �����α���»�ɾ������

- ��ʽ�α����

  - �����α�
    - �﷨
      
      ```plsql
      CURSOR cursor_name IS select_statement ;
      ```
      
    - ˵��
      �α������PL/SQL����������ֽ��ж��壻
      �α궨��ʱ��������PL/SQL�������������������α궨��֮ǰ���壻
      �����α�ʱ��û���������ݣ�ֻ�ǽ�������Ϣ���浽�����ֵ��У�
      �α궨��󣬿���ʹ��cursor_name%ROWTYPE�����α����ͱ�����
- ���α�
    - �﷨
      
      ```plsql
      OPEN cursor_name; 
      ```
      
  - ˵��
    ���仺����
    ִ���α궨��ʱ��Ӧ��SELECT��䣬����ѯ����������������С�
    һ���α�򿪣����޷��ٴδ򿪣������ȹرա�
    
  - �����α�
    - �﷨��ʽ
      
      ```plsql
      FETCH cursor_name INTO variable_list|record_variable; 
      ```
    
  - ˵��
      ��ʹ��FETCH���֮ǰ�����ȴ��α�
      ���α��һ��ʹ��FETCH���ʱ���α�ָ��ָ���һ����¼����˲����Ķ����ǵ�һ����¼��ʹ�ú��α�ָ��ָ����һ����¼��
      �α�ָ��ֻ�������ƶ������ܻ���
      INTO�Ӿ��еı���������˳���������ͱ����빤������ÿ�м�¼���ֶ�����˳���Լ���������һһ��Ӧ
      
  - �ر��α�
    - �﷨��ʽ
      
        ```plsql
        CLOSE cursor_name; 
        ```
        
    - ˵��
    �α�����Ӧ���ڴ湤������Ϊ��Ч���ͷ����α���ص�ϵͳ��Դ��
  
- �α갸������������Ĳ��źŲ�ѯĳ�����ŵ�Ա����Ϣ�����ź��ڳ�������ʱָ��������ĳ�����ŵ������ǲ�ȷ���ģ������ж���������Ҫ�����α�������

- ��ʽ�α������
  - %ISOPEN
    �����͡�����α��Ѿ��򿪣�����TRUE,����ΪFALSE��
  - %FOUND
    �����ͣ�������һ��ʹ��FETCH��䣬�з��ؽ����ΪTRUE,����ΪFALSE;
  - %NOTFOUND
    �����ͣ�������һ��ʹ��FETCH���,û�з��ؽ����ΪTRUE,����ΪFALSE;
  - %ROWCOUNT
    ��ֵ�ͣ����ص�ĿǰΪֹ���α껺����������Ԫ������
  - %BULK_ROWCOUNT��i��
    ��ֵ�ͣ�����ȡ��FORALL���ִ�����󶨲���ʱ��i��Ԫ����Ӱ���������

- ���������α�

  - �������α궨���﷨��ʽ
    
  - ```plsql
    CURSOR cursor_name(parameter1
    datatype[,parameter2 datatype��]) 
    IS select_statement 
    ```
    
  - �򿪲������α�ķ���
    
  - ```plsql
    OPEN cursor_name(parameter1
    [,parameter2��]) 
    ```
  ```
    
    > ע�⣺
    >
    > ����������α�ʱ��ֻ��ָ�����������ͣ�������ָ�������ĳ��ȡ����ȡ��̶ȣ�
    > �򿪴��������α�ʱ��ʵ�εĸ������������͵ȱ������α궨��ʱ�βθ������������͵���ƥ�䡣
  ```

- �������α갸��

  - ��ѯ�����ĳ�����ŵ�Ա����Ϣ

- ��ʽ�α�ļ���

  �����α��Ӧ�Ļ������п����ж��м�¼����PL/SQL��ÿ��ֻ�ܴ���һ�м�¼�����Ҫ����ѭ���ķ�ʽ�ӻ������м������ݽ��д�������ѭ�������Ĳ�ͬ�������α������ַ�����

  - ��ѭ�������α�
  - ���������ü�ѭ��ͳ�Ʋ�����������ŵ�ƽ������
  - WHILEѭ�������α�
  - ����������WHILEѭ��ͳ�Ʋ�����������ŵ�ƽ������
  - FORѭ�������α�
  - FOR loop_variable IN �α����ֻ���ʽSELECT���
    LOOP
        ִ�����;
      END LOOP;
    - ����FORѭ�������α�ʱ��ϵͳ���Զ��򿪡��������ر��αꡣϵͳ������������һ����������Ϊcursor_name%ROWTYPE��ѭ������loop_variable��Ȼ���Զ����α꣬���α껺��������ȡ���ݲ�����loop_variable�����У�ͬʱ����%FOUND���Լ����ȷ���Ƿ���������ݡ����α껺�����е����ݶ�������ϻ�ѭ���ж�ʱ��ϵͳ�Զ��ر��αꡣ
  - ����������FORѭ��ͳ�Ʋ�����������ŵ�ƽ������

- �����α���»�ɾ������

  - �α궨���﷨
    
  - ```plsql
    CURSOR cursor_name IS
    SELECT select_list_item FROM table  FOR UPDATE
    [OF column_reference] [NOWAIT]; 
    ```
    
  - > ע�⣺
    >
    > ���α�ʱ����Ӧ�ı������ͨ��SELECT�������������������κ������������û����ܶԸñ����DML������
  
  - �����ݶ����Ѿ��������Ự��������ǰ�Ự����ȴ���Ĭ��״̬������ָ����NOWAIT�Ӿ䣬�򲻵ȴ�������ORACLE����
  
  - ���ڶ���ѯʱ������ͨ��OF�Ӿ�ָ��ĳ��Ҫ�����ı���е���ʽ�����ض��ı���������������������������б������� 
    ���û�ִ��COMMIT��ROLLBACK����ʱ�������ϵ������Զ����ͷš� 
    
  - �޸Ļ�ɾ�����ݵ��﷨Ϊ
    UPDATE|DELETE��
    WHERE CURRENT OF cursor_name 
    
  - �������޸�Ա���Ĺ��ʣ����Ա���Ĳ��ź�Ϊ10���������100��������ź�Ϊ20���������150��������ź�Ϊ30���������200�����������250�� 
  
    > ע�⣺
    >
    > ����α궨��ʱû��ʹ��FOR UPDATE�Ӿ䣬�������ø��α��޸Ļ�ɾ�����ݿ��е����ݡ�

#### ��ʽ�α�

���е�SQL��䶼��һ��ִ�еĻ���������ʽ�α����ָ��û�������ָ�룬��ϵͳ�����ش򿪡�����͹رա���ʽ�α��ֳ�ΪSQL�αꡣ
��ʽ�α���Ҫ���ڴ���INSERT��UPDATE��DELETE�Լ����е�SELECT��INTO��䣬û��OPEN��FETCH��CLOSE�Ȳ������

- ��ʽ�α�����

  - SQL%ISOPEN��������ֵ���ж���ʽ�α��Ƿ��Ѿ��򿪡����û����ԣ�������ֵʼ��ΪFALSE����Ϊ����ʱϵͳ�Զ��򿪣�������������Զ��رա�
  
  - SQL%FOUND��������ֵ���жϵ�ǰ�Ĳ����Ƿ������ݿ����Ӱ�졣��������ݵĲ��롢ɾ�����޸Ļ��ѯ�����ݣ��򷵻�TRUE�����򷵻�FALSE��
  
  - SQL%NOTFOUND��������ֵ���жϵ�ǰ�Ĳ����Ƿ�����ݿ����Ӱ�졣���û�����ݵĲ��롢ɾ�����޸Ļ�û�в�ѯ�����ݣ��򷵻�TRUE�����򷵻�FALSE��

  - SQL%ROWCOUNT����ֵ�ͣ����ص�ǰ�������漰�����ݿ��е�������
  
  - �������޸�Ա����Ϊ1000��Ա�����ʣ����乤������100�������Ա�������ڣ�����emp���в���һ��Ա����Ϊ1000������Ϊ1500��Ա����
  
    > ע�⣺
    >
    > ��SELECT ....INTO���û�в�ѯ���κ�����ʱ���ἤ��NO_DATA_FOUND�쳣��

#### �α����

- ����
  - ��ʽ�α��ڶ���ʱ���ض��Ĳ�ѯ�󶨣���ṹ�ǲ���ģ�����ֳ�Ϊ��̬�αꡣ�α������һ��ָ����в�ѯ�������ָ�룬�����ض��Ĳ�ѯ�󶨣���˾��зǳ��������ԣ������ڴ��α����ʱ�����ѯ�����Է��ز�ͬ�ṹ�Ľ������
  - ʹ���α���������������α��������ͣ�REF CURSOR���������α���������α�����������α�������ر��α���� 

- �����α���������
  - �﷨
    - TYPE ref_cursor_type_name IS REF CURSOR [RETURN return_type]
      RETURN�Ӿ�����ָ��������α����ͷ��ؽ���������ͣ������ͱ����Ǽ�¼���͡���������α���������ʱ����RETURN�Ӿ䣬�����䶨��ı�����Ϊǿ�α�����������Ϊ���α������
    - ��Oracle 10g�У�ϵͳԤ������һ���α��������ͣ���ΪSYS_REFCURSOR������ֱ��ʹ���������α������ 

- �����α����
  - �﷨
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
      
    - SYS_REFCURSOR��Oracle10g��ʼ�ṩ���α�
  
- ���α����

  - �﷨

    - ```plsql
OPEN cursor_variable FOR select_statement;
      ```
      
      > ע�⣺
      >
      > ����򿪵��α������ǿ�α���������ѯ���ķ������ͱ������α��������Ͷ�����RETURN�Ӿ�ָ���ķ���������ƥ�䡣
      
    - ```plsql
      OPEN v_emp FOR SELECT * FROM emp;
      OPEN v_general FOR SELECT 
                           empno,ename,sal,deptno FROM emp;
      OPEN my_cursor FOR SELECT * FROM dept;
      ```
  
- �����α����

  - �﷨
    - ```plsql
      LOOP
      	FETCH cursor_variable INTO variable1, variable2, ��;
      	EXIT WHEN cursor_variable%NOTFOUND;
      	����
    END LOOP; 
      ```
      
      > ע�⣺
      >
      > �����α����ʱֻ��ʹ�ü�ѭ����WHILEѭ�������ܲ���FORѭ����
    
  - ����
  
    - Ҫ���������Ĳ�ͬ�������в�ͬ����������Ϊemp������ʾ����10�Ų���ƽ�����ʵ�Ա����Ϣ��������Ϊdept������ʾ�������ŵ������� 

#### �쳣����

- PL/SQL����Ĵ���
  - �������
  - ����ʱ����

Oracle�ж�����ʱ����Ĵ���������쳣������ơ� һ�������Ӧһ���쳣�����������ʱ�׳���Ӧ���쳣�������쳣���������񣬳������Ȩ���ݸ��쳣�����������쳣����������������ʱ���� 

- ����ʱ����
  - Oracle����Oracle���κ�һ��������һ��Ψһ�Ĵ����ţ�
  - �û��������

- �쳣����

  - Ԥ�����Oracle�쳣�� Oracle����

  ```plsql
  DECLARE
    v_ename emp.ename%TYPE;
  BEGIN
    SELECT ename INTO v_ename FROM emp WHERE empno=7300;--SMITH
    dbms_output.put_line('���֣�'||v_ename);
  EXCEPTION
    WHEN NO_DATA_FOUND THEN
      dbms_output.put_line('�Ҳ������Ա��');
  END;
  ```

  - ��Ԥ�����Oracle�쳣�� Oracle����û�к�Ԥ�����쳣���������

  - �û�������쳣���û��������

- Ԥ�����Oracle�쳣
  - ��Oracle�������ʱ��������Ӧ��Ԥ�����쳣���Զ��׳���ͨ��������쳣���ԶԴ�����д���
  - ����Ԥ�����쳣����


| �쳣����            | �������  | ����                                       |
| ------------------- | --------- | ------------------------------------------ |
| CURSOR_ALREADY_OPEN | ORA-06511 | ���Դ��Ѿ��򿪵��α�                     |
| INVALID_CURSOR      | ORA-01001 | ���Ϸ����α��������Ҫ���Ѿ��رյ��α꣩ |
| NO_DATA_FOUND       | ORA-01403 | û�з�������                               |
| INVALID_NUMBER      | ORA-01722 | ת������ʧ��                               |
| TOO_MANY_ROWS       | ORA-01422 | һ��SELECT  INTO���ƥ����������         |
| ZERO_DIVIDE         | ORA-01476 | ����Ϊ0                                    |
| DUP_VAL_ON_INDEX    | ORA-00001 | Υ��Ψһ��Լ��������Լ��                   |
| TIMEOUT_ON_RESOURCE | ORA-00051 | �ڵȴ���Դ�г��ֳ�ʱ                       |
| LOGIN_DENIED        | ORA-01017 | ��Ч�û���/����                            |

- ��Ԥ�����쳣

  - ��һЩOracle����û��Ԥ�����쳣�����������Ҫ�������������������һ���쳣���ƣ�Ȼ��ͨ������ָʾPRAGMA EXCEPTION_INIT�����쳣������һ��Oracle������������˺󣬵�ִ�й��̳��ָô���ʱ���Զ��׳����쳣��

  - ���磬��ִ�����в���ʱ������ORA-02292��Oracle��������û����֮��Ӧ���쳣����˸ô������ʱû���쳣�׳����Ӷ��޷�����ʹ���

  - SQL> DELETE FROM dept WHERE deptno=20;

    ORA-02292: Υ������Լ������ (SCOTT.FK_DEPTNO) - ���ҵ��Ӽ�¼

  - Ϊ�˽�����������⣬����Ϊ�ô������쳣��Ȼ��ͨ���쳣��������Ӧ�Ĵ������磺

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

- �û��Զ�����쳣
  - �û����������ָ����Щ�������������Oracle���󣬵��Ǵ�ҵ�����Ƕȿ��ǣ���Ϊ��һ�ִ������磬ִ��UPDATE����û�и����κ���ʱ����������Oracle����Ҳ��������쳣�����ǣ���ʱ��Ҫ������ԱΪ�˲�������һ���쳣���Ա���д������û������쳣��
  - �û��Զ����쳣�������������ֽ������������쳣����ʱ��ϵͳ�����Զ���������Ҫ�û�ʹ��RAISE��䡣���쳣�����ֲ�׽�������쳣��

- �쳣����
  - �쳣�����3��������У�
    - ����������Ϊ�������쳣��������Ԥ�����쳣���û������쳣��
    - ��ִ�й����е��������ʱ�׳�������Ӧ���쳣��
    - ���쳣������ͨ���쳣�����������쳣���������쳣����

- �쳣����

  - Oracle�е�3���쳣������Ԥ�����쳣��ϵͳ���壬�����������쳣����Ҫ�û����塣

  - �����쳣����

    - e_exception EXCEPTION;

  - ����Ƿ�Ԥ������쳣����Ҫ���쳣��һ��Oracle��������������﷨Ϊ��
    PRAGMA EXCEPTION_INIT(e_exception, -#####);

    > ע�⣺
    >
    > Oracle�ڲ��������һ������5λ����ʾ����-02292������-20999��-20000Ϊ�û��������ı����š�

- �쳣�׳�
  - ����ϵͳ�����Զ�ʶ��Oracle�ڲ�������˵��������ʱϵͳ���Զ��׳���֮��Ӧ��Ԥ�����쳣���Ԥ�����쳣�����ǣ�ϵͳ�޷�ʶ���û����������˵��û�����������ʱ����Ҫ�û��ֶ��׳���֮��Ӧ���쳣��
  - �û������쳣���׳��﷨Ϊ
    RAISE user_define_exception�� 

- �쳣�����봦��

  - �쳣�������Ļ�����ʽΪ

  - ```plsql
    EXCEPTION
    WHEN exception1[OR excetpion2��]THEN 
       sequence_of_statements1;
    WHEN exception3[OR exception4��]THEN 
       sequence_of_statements2;
    ����
    WHEN OTHERS THEN 
       sequence_of_statementsn;
    END;
    ```

  - > ע�⣺
    >
    > һ���쳣���������Բ������쳣��ֻ����WHEN�Ӿ�����OR���Ӽ��ɣ�
    >
    > һ���쳣ֻ�ܱ�һ���쳣���������񣬲����д��� 

- Ԥ�����쳣���䴦��
  
  - ��ѯ��ΪSMITH��Ա�����ʣ������Ա�������ڣ��������There is not such an employee!����������ڶ��ͬ����Ա�����������Ա���ź͹��ʡ�
  
- ��Ԥ�����쳣����
  
  - ɾ��dept���в��ź�Ϊ10�Ĳ�����Ϣ���������ɾ���������There are subrecords in emp table!����
  
- �Զ����쳣����
  
  - �޸�7844Ա���Ĺ��ʣ���֤�޸ĺ��ʲ�����6000��(RETURNING sal INTO v_sal)
  
- OTHERS�쳣����

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

��ȻOTHERS���Բ�������쳣��������������ش�����Ϣ���޷��жϵ������ĸ�����������쳣����˿���ͨ��������������ȡ���������Ϣ��

SQLCODE�����ص�ǰ������롣
������û�������󷵻�ֵΪ1��
�����ORA-1403��NO DATA FOUND���󣬷���ֵΪ100
����Oracle�ڲ����󷵻���Ӧ�Ĵ���š� 
SQLERRM�����ص�ǰ�������Ϣ�ı���
�����Oracle�ڲ����󣬷���ϵͳ�ڲ��Ĵ���������
������û���������򷵻���Ϣ�ı�Ϊ��User-defined Exception���� 

���磺

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

- �쳣�Ĵ���

  - ��PL/SQL���ִ�в��ֲ����쳣�󣬸��ݵ�ǰ���Ƿ��и��쳣�������������д������ɹ���ɸ����顣Ȼ�󣬳���Ŀ������̴��ݵ�������飬����ִ�С�
    - ���磺��ѯԱ������ΪJOAN��Ա����нˮ
    - NO_DATA_FOUND
  - �����ǰ����û�и��쳣����������ͨ������������ִ�в��ֲ������쳣���������쳣��
    - ���磺��ѯ10�Ų��ŵĹ���
    - NO_DATA_FOUND
    - TOO_MANY_ROWS

  - ������ִ�в��ֵ��쳣�������������ֻ��쳣�����ֵ��쳣������ڱ�����û�д������ն����������д�������ˣ�ͨ���ڳ����������쳣�����ַ���OTHERS�쳣���������Ա�֤û�д���©����⣬������󽫴��ݵ����û�����

- ʵѵ��

  ![ʵѵ��](./PLSQL01.png)

#### �洢����

- �洢���̴���

  - �����﷨

  - ```plsql
    CREATE [OR REPLACE] PROCEDURE procedure_name
    (parameter1_name [mode] datatype 
        [DEFAULT|:=value]
    [, parameter2_name [mode] datatype 
        [DEFAULT|:=value],��])
    AS|IS
       /*Declarative section is here */
    BEGIN
       /*Executable section is here*/ 
    EXCEPTION
       /*Exception section is here*/ 
    END[procedure_name]; 
    ```

  - ������ģʽ 

    - IN��Ĭ�ϲ���ģʽ����ʾ�����̱�����ʱ��ʵ��ֵ�����ݸ��βΣ��ڹ����ڣ��β��������ã�ֻ�ܶ��ò������������޸ĸò��������ӳ�����ý������ص��û���ʱ��ʵ��û�б��ı䡣INģʽ���������ǳ�������ʽ��
    - OUT��ʾ�����̱�����ʱ��ʵ��ֵ�����ԣ��ڹ����ڣ��β���δ��ʼ����PL/SQL���������ã���ʼֵΪNULL�����Խ��ж�/д���������ӳ�����ý����󷵻ص��û���ʱ���β�ֵ������ʵ�Ρ�OUTģʽ����ֻ���Ǳ����������ǳ�������ʽ��
    - IN OUT��ʾ�����̱�����ʱ��ʵ��ֵ�����ݸ��βΣ��ڹ����ڣ��β����ѳ�ʼ����PL/SQL���������ã��ɶ���д�����ӳ�����ý������ص��û���ʱ���β�ֵ������ʵ�Ρ�IN OUTģʽ����ֻ���Ǳ����������ǳ�������ʽ�� 

- ����������
  - �������β�ʱ�����ܶ����βεĳ��Ȼ򾫶ȡ��̶ȣ���������Ϊ�������ݻ��Ƶ�һ���ֱ����ݵģ�����ʵ�ξ����ġ�
  - �������ݷ�ʽ
    - ���ӳ��򱻵���ʱ��ʵ�����β�֮��ֵ�Ĵ��ݷ�ʽȡ���ڲ�����ģʽ��IN����Ϊ���ô��ݣ���ʵ�ε�ָ�뱻���ݸ��βΣ�OUT��IN OUT����Ϊֵ���ݣ���ʵ�ε�ֵ�����Ƹ��βΡ�
    - ����Ĭ��ֵ
      ����Ϊ��������Ĭ��ֵ�������洢���̱�����ʱ���û�и��ò�������ֵ�������Ĭ��ֵ����Ҫע�⣬��Ĭ��ֵ�Ĳ���Ӧ�÷��ڲ����б����� 

- ����������һ���洢���̣��Բ��ź�Ϊ��������ѯ�ò��ŵ�ƽ�����ʣ�������ò����б�ƽ�����ʸߵ�Ա���š�Ա������

ͨ�����洢���̲���Ҫ����ֵ�������Ҫ����һ��ֵ����ͨ����������ʵ�֡����ǣ����ϣ�����ض��ֵ������ʹ��OUT��IN OUTģʽ������ʵ�֡�

- ����������һ���洢���̣��Բ��ź�Ϊ���������ظò��ŵ���������߹��ʡ�

- �洢���̵���

  - ��SQL*PLUS�е���

    ```plsql
    EXEC  procedure_name(parameter_list)��CALL procedure_name(parameter_list)
    EXECUTE show_emp(10)
    ```

  - ��PL/SQL���е���

    ```plsql
    BEGIN
          procedure_name(parameter_list);
    END��
    ```

    ��PL/SQL�����У��洢���̿�����Ϊһ�������ı��ʽ�����á� 

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

- ����

  - ��������

    - �����﷨Ϊ 

    - ```plsql
      CREATE [OR REPLACE] FUNCTION function_name 
      (parameter1_name [mode] datatype 
          [DEFAULT|:=value]
      [, parameter2_name [mode] datatype 
          [DEFAULT|:=value],��])
      RETURN return_datatype 
      AS|IS
           /*Declarative section is here */
      BEGIN
          /*Executable section is here*/ 
      EXCEPTION
          /*Exception section is here*/ 
      END [function_name]; 
      ```

    - > ע�⣺
      > �ں��������ͷ���������б�֮�󣬱������һ��RETURN�����ָ����������ֵ�����ͣ�������Լ������ֵ�ĳ��ȡ����ȡ��̶ȵȡ����ʹ��%TYPE������������ذ������ȡ����ȡ��̶ȵ�Լ����Ϣ��
      > �ں�����Ķ����У��������ٰ���һ��RETURN ��䣬��ָ����������ֵ��Ҳ�����ж��RETURN��䣬������ֻ��һ��RETURN��䱻ִ�С�

- ����������һ���Բ��ź�Ϊ���������ظò�����߹��ʵĺ�����

�����Ҫ�������ض��ֵ������ʹ��OUT��IN OUTģʽ������

- ����������һ���������Բ��ź�Ϊ���������ز���������������������ƽ�����ʡ�

- ��������

  - ��SQL����е��ú���

  - ��PL/SQL�е��ú���

  - > ע�⣺
    > ����ֻ����Ϊ���ʽ��һ���ֱ����á�

  - ������ͨ����return_maxsal�����ĵ��ã�����������ŵ���߹��ʣ�ͨ����ret_deptinfo�������ã��������������������������ƽ�����ʡ�

  - ����������SQL�������²��ֵ���

    - SELECT����Ŀ����
    - WHERE��HAVING�Ӿ�
    - CONNECT BY��START WITH��ORDER BY��GROUP BY�Ӿ�
    - INSERT����VALUES�Ӿ���
    - UPDATE����SET�Ӿ���

  - ���Ҫ��SQL�е��ú�������ô������������������ƺ�Ҫ��

    - ��SELECT����еĺ��������޸ģ�INSERT��UPDATE��DELETE�����ú�����SQL�����ʹ�õı�
    - ������һ��Զ�̻��в�����ʹ��ʱ�����ܶ�/д��װ����
    - ����������һ���洢���ݿ���󣨻�洢�ڰ��У�
    - �����Ĳ���ֻ��ʹ��INģʽ
    - ��ʽ�������ͱ���ʹ�����ݿ���������
    - ���ص��������ͱ��������ݿ���������

#### ��

- ������ǰ���һ�������ӳ���Ԫ�����̡������ȣ�������������һ��ȫ�ֽṹ ��

- ������
  - ���ݿ����ð�
  - �û������İ�

- ������
  - ��ͷ
    - ��ͷ�����˰����������ݣ�����̡��������αꡢ���͡��쳣�ͱ����ȣ����й��̺ͺ���ֻ����ԭ����Ϣ���������κ��ӳ�����롣  
  - ����
    - �����а������ڰ�ͷ�еĹ��̺ͺ�����ʵ�ִ��롣�����л����԰����ڰ�ͷ��û�������ı������αꡢ���͡��쳣�����̺ͺ���������������˽��Ԫ�أ�ֻ����ͬһ�������������̺ͺ���ʹ�á�

- ������ͷ

```plsql
CREATE OR REPLACE PACKAGE package_name 
IS|AS
[PRAGMA SERIALLY_RESUABLE]
  type_definition|variable_declaration|
  exception_declaration|cursor_declaration| 
  procedure_ declaration|function_ declaration
END [package_name];
```

> ע�⣺
> Ԫ��������˳�����������ģ���������������ʹ�ã�
> ����Ԫ���ǿ�ѡ�ģ�
> ���̺ͺ���������ֻ����ԭ�ͣ�����������ʵ�֡�

- ��ͷʾ��������һ����ͷ������2��������2�����̺�1���쳣��

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

- ��������

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

- ���ĵ��ã��ڰ�ͷ���������κ�Ԫ���ǹ��еģ��ڰ��ⶼ�ǿɼ���

  - ���⣺ͨ��package.element��ʽ���ã�

  - ���ڣ�ֱ��ͨ��Ԫ�������е��á� 

  - �ڰ����ж����û���ڰ�ͷ��������Ԫ����˽�еģ�ֻ���ڰ��������� 

  - ���ð�pkg_emp�еĹ���update_sal���޸�7844Ա������Ϊ3000������add_employee���һ��Ա����Ϊ1357������Ϊ4000��Ա����

    ```plsql
    BEGIN
      pkg_emp.update_sal(7844,3000);
      pkg_emp.add_employee(1357,4000);
    END;
    ```

#### ������

- ����
  - ��������һ���������͵Ĵ洢���̣������洢�����ݿ�������С�
  - ���ض��¼�����ʱ����ϵͳ�Զ�����ִ�У���������Ӧ�ó�����ʽ�ص���ִ�С�
  - �������������κβ�����
  - ��������Ҫ����ά����Щͨ��������ʱ������Լ��������ʵ�ֵĸ��ӵ�������Լ�����������ݿ����ض��¼����м�غ���Ӧ��

- ����������
  - DML������
    - �����ڻ������ϵĴ���������Ӧ�������INSERT��UPDATE��DELETE������
  - INSTEAD OF������
    - ��������ͼ�ϵĴ���������Ӧ��ͼ�ϵ�INSERT��UPDATE��DELETE������
  - ϵͳ������
    - ������ϵͳ��ģʽ�ϵĴ���������Ӧϵͳ�¼���DDL��CREATE��ALTER��DROP�������� 

- ���������
  - �������ɴ�����ͷ���ʹ������������������
  - ��Ҫ������
    - ���ö��󣺴��������õĶ����������ͼ�����ݿ��ģʽ��
    - �����¼�������������ִ�е��¼�����DML��DDL�����ݿ�ϵͳ�¼��ȡ�
    - ����ʱ�䣺����ָ���������ڴ����¼����֮ǰ����֮��ִ�С����ָ��ΪAFTER�����ʾ��ִ�д����¼���Ȼ����ִ�д����������ָ��ΪBEFORE�����ʾ��ִ�д�������Ȼ����ִ�д����¼���
    - �������𣺴�����������ָ����������Ӧ�����¼��ķ�ʽ��Ĭ��Ϊ��伶���������������¼������󣬴�����ִֻ��һ�Ρ����ָ��ΪFOR EACH ROW����Ϊ�м����������򴥷��¼�ÿ������һ����¼���������ͻ�ִ��һ�Ρ�
    - ������������WHEN�Ӿ�ָ��һ���߼����ʽ���������¼�����������WHEN����ΪTRUEʱ���������Ż�ִ�С�
    - ����������������ִ��ʱ�����еĲ�����

- DML������������
  - ��伶ǰ������
  - ��伶�󴥷���
  - �м�ǰ������
  - �м��󴥷���

- DML��������ִ��˳��
  - ������ڣ���ִ����伶ǰ������
  - �����ܴ����¼�Ӱ���ÿһ����¼
    - ������ڣ���ִ���м�ǰ������
    - ִ�е�ǰ��¼��DML�����������¼���
    - ������ڣ���ִ���м��󴥷���
  - ������ڣ���ִ����伶�󴥷���

- ����DML������

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

- ��伶������

  - ��Ĭ������´�����DML������Ϊ��伶���������������¼������󣬴�����ִֻ��һ�Ρ� 

  - ����һ������������ֹ����Ϣ�ոı��Ա��Ϣ

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

- ��������Ӧ���DML�¼�

| ν��      | ��Ϊ                                        |
| --------- | ------------------------------------------- |
| INSERTING | ������������INSERT����ΪTRUE������ΪFALSE |
| UPDATING  | ������������UPDATE����ΪTRUE������ΪFALSE |
| DELETING  | ������������DELETE����ΪTRUE������ΪFALSE |

- ��Ӧ���DML�¼�������Ϊemp����һ����־����������ִ�в������ʱ��ͳ�Ʋ�����Ա����������ִ�и��²���ʱ��ͳ�Ƹ��º�Ա��ƽ�����ʣ���ִ��ɾ������ʱ��ͳ��ɾ��������ŵ�������

- �м�������
  - �м���������ִָ��DML����ʱ��ÿ����һ����¼����������ִ��һ�Σ�һ��DML�����漰���ٸ���¼����������ִ�ж��ٴΡ�
  - ���м��������п���ʹ��WHEN��������һ�����ƴ�������ִ�С�
  - ���м���������������:old��:new ������ʶ���������ʺͲ�����ǰ�������¼�е����ݡ� 

- ��ʶ��

  - :old��:new��Ϊtriggering_table%ROWTYPE���͵���������

  - ���÷�ʽ

    - :old.field��:new.field ��ִ�в��֣�
    - old.field ��new.field   (WHEN������)

  - �ڲ�ͬ�����¼��У�:old��:new�����岻ͬ

    | �����¼� | :old                     | :new                       |
    | -------- | ------------------------ | -------------------------- |
    | INSERT   | δ���壬�����ֶζ�ΪNULL | ��������ʱ��������ļ�¼ |
    | UPDATE   | ����ǰԭʼ��¼           | ��������ʱ�����º�ļ�¼ |
    | DELETE   | ��¼��ɾ��ǰ��ԭʼֵ     | δ���壬�����ֶζ�ΪNULL   |

  - ������Ϊemp����һ������������������Ա��ʱ��ʾ��Ա����Ա���š�Ա������������Ա������ʱ����ʾ�޸ĺ��Ա�����ʣ���ɾ��Ա��ʱ����ʾ��ɾ����Ա����Ա���š�Ա������

  - ���м��������У�����ʹ��WHEN�Ӿ��һ�����ƴ�������ִ�С����磺�޸�Ա������ʱ����֤�޸ĺ�Ĺ��ʸ����޸�ǰ�Ĺ��ʡ�

  - ```plsql
    CREATE OR REPLACE TRIGGER trg_emp_update_row
    BEFORE UPDATE OF sal ON emp
    FOR EACH ROW
    WHEN(new.sal<old.sal)
    BEGIN
    	RAISE_APPLICATION_ERROR(-20002,'The salary is lower!');
    END;
    ```

- INSTEAD OF������
  - �ص�
    - ֻ�ܶ�������ͼ��
    - Instead-of���������м�������
    - Instead-of��������DML������������DML����������ִ��
  - ����
    - �޸�һ�������������޸ĵ���ͼ

- �����ͼ�а��������κ�һ������ͼ�����޸�
  - ���ϲ�������UNION��UNION ALL��MINUS��INTERSECT����
  - �ۼ�������SUM��AVG�ȣ���
  - GROUP BY��CONNECT BY��START WITH�Ӿ䣻
  - DISTINCT��������
  - �漰���������Ӳ�����

- ����INSTEAD OF�������Ļ����﷨

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

����������һ������Ա���������ڲ�����Ϣ����ͼempdept��Ȼ������ͼ�в���һ����¼(2345,��TOM��,3000,90,��SALES��)

```plsql
CREATE OR REPLACE VIEW empdept 
AS
SELECT empno,ename,sal,dname 
FROM emp,dept WHERE emp.deptno=dept.deptno  
WITH CHECK OPTION;

SQL> INSERT INTO empdept VALUES(2345, 'TOM',3000,'SALES');
INSERT INTO empdept
*
�� 1 �г��ִ���:
ORA-01733: �˴�������������
```

��empdept��ͼ�ϴ���һ��INSTEAD OF������

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
INSERT INTO test VALUES(6,'�ڴ�',230.0,'����',4,'����','����',3);
CREATE OR REPLACE TRIGGER trigger3
INSTEAD OF INSERT ON test
BEGIN
  INSERT INTO product VALUES(:NEW.id,:NEW.name,:NEW.price,:NEW.type);
  INSERT INTO customer VALUES(:NEW.acid,:NEW.acname,:NEW.acaddress);
  INSERT INTO orders VALUES(:NEW.acid,:NEW.id,:NEW.amount);
END;
/
```

- ϵͳ������
  - �����¼�
    - DDL�¼���CREATE��ALTER��DROP��RENAME��GRANT��REVOKE��AUDIT��NOAUDIT��COMMENT��TRUNCATE��ANALYZE��ASSOCIATE STATISTICS��DISASSOCIATE STATISTICS�ȣ�
    - ���ݿ��¼���STARTUP��SHUTDOWN��LOGON��LOGOFF��SERVERERROR�ȣ�������ʱ���ɾ����¼�����

| �¼�        | �����ʱ | ����                   |
| ----------- | -------- | ---------------------- |
| STARTUP     | AFTER    | ʵ������ʱ����         |
| SHUTDOWN    | BEFORE   | ʵ���ر�ʱ����         |
| SERVERERROR | AFTER    | �������������󴥷�     |
| LOGON       | AFTER    | �û���ʵ�������Ự���� |
| LOGOFF      | BEFORE   | �û�ע��ʱ����         |

- ����ϵͳ������

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

- ��������ÿ���û��ĵ�¼��Ϣд��temp_table����

- ```plsql
  CREATE OR REPLACE TRIGGER log_user_connection
  AFTER LOGON ON DATABASE
  BEGIN
  	INSERT INTO temp_table VALUES(user,sysdate);
  END log_user_connection;
  /
  ```

- �����ݿ�ִ��CREATE����ʱ���������������Ϣ��¼��ddl_creations����

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

  - �¼����Ժ���
  
  <img src = "./PLSQL03.png" align="center">

  <img src = "./PLSQL04.png" align="center">
  
- ʵѵ��

  ![ʵѵ��](./PLSQL02.png)