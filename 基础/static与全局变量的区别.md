```java
public class Test8 {
    private static int i=1;
    public void f1(){
        i=2;
        System.out.println(i);
    }
    public void f2(){
        i=3;
        System.out.println(i);
    }
    public static void main(String[] args) {
        Test8 t=new Test8();
        System.out.println(new Test8().i);
        new Test8().f1();
        System.out.println(new Test8().i);
        new Test8().f2();
        System.out.println(new Test8().i);
    }
}
结果：
    1
    2
    2
    3
    3
```

```java
public class Test8 {
    private int i=1;
    public void f1(){
        i=2;
        System.out.println(i);
    }
    public void f2(){
        i=3;
        System.out.println(i);
    }
    public static void main(String[] args) {
        Test8 t=new Test8();
        System.out.println(new Test8().i);
        new Test8().f1();
        System.out.println(new Test8().i);
        new Test8().f2();
        System.out.println(new Test8().i);
    }
}
结果：
    1
    2
    1
    3
    1
```

