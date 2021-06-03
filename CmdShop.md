
# 项目的目的

- 如何进行实体类的抽取
- 如何创建对象
- 如何给对象赋值
- 类之间的关系（终极目的）

## 一、登录实现

- cmd中运行程序，提示输入用户的id和密码
- 把输入的id和密码与customer.xls中的进行比对
- 如果正确，则提示登录成功，并显示当前有哪些商品可以购买

## 二、添加商品到购物车

- 根据商品ID，可以把商品加入购物车

## 三、下订单

- 查看购物车，可以下订单
- 下订单的时候需要生成一个新的excel（order.xlsx：里面存储了客户的id、客户的姓名、客户的电话、客户的地址、订单金额、商品名称）

## 四、要求

- 采用面向对象的思想去实现，根据需求，自己去设计相应的类


## 五、Idea创建项目并导入到github中

## 5.1 安装git

- 安装完git才能打开idea
- idea第一次打开后，不要做任何操作，马上打开任务管理器，找到idea64.exe进程，结束该进程，并重新打开idea

## 5.2 github中创建token

- token就是一个身份标识（github头像 - settings - Developer settings - Personal access takens - 创建一个新的tokens用于连接idea跟github）

## 5.3 idea中试用token登录到github

- 操作（idea - File - settings - Version Control - Github - 输入生成的tokens连接idea与github）

## 5.4 idea创建项目

## 5.5 idea中的项目导入到github

- 操作（idea - VCS - Import into Version Control - Share Project on Github）

## 六、创建程序

- 创建Test.java

- cmd中提示用户输入用户名和密码

## 七、读取excel

```java

	File file = new File("C:\\Users\\欧家明\\CmdShop\\src\\user.xlsx")
```

## 八、把读取到的excel的用户名和密码进行比对

```java

	username.equals(user.getUsername()) && password.equals(user.getPassword()
```


## 九、技术栈

- 类和对象
- 流程控制
- 数组
- 方法
- 接受键盘输入
- poi读取excel

## 十、github的开发模式

- master创建分支：每个项目组成员从master创建一个自己的分支，每天下班前，测试完毕没有问题的情况下再合并到master中

- 项目组的成员fork，每天下班前测试完毕没有问题的情况下，然后给创建仓库的人（项目经理或组长）提交PR（pull request）

## 十一、密码是纯数字的bug解决(防止读数带有小数点或成科学计数法)

### 11.1、解决方案

- String的方法
- 使用DecimalFormat类的format方法

修改前

```java

	value = cell.getNumericCellValue() + ""
```

修改后

```java

	DecimalFormat df = new DecimalFormat("#");
	value = df.format(cell.getNumericCellValue());
```


## 十二、改变读取users.xlsx的方式（getResourceAsStream的方式）

```java
InputStream in=Class.forName("Test").getResourceAsStream("/文件名.xlsx");
```


## 十三、解决用户名或密码错误，提示用户重新输入

### 13.1 解决方案：循环

- while
- for

```java

	boolean bo = true;
	while(bo) {
	    System.out.println("请输入用户名：");
	    Scanner scanner = new Scanner(System.in);
	    String username = scanner.next();
	
	    System.out.println("请输入密码：");
	    String password = scanner.next();
	
	    for (User user : users) {
	        if (username.equals(user.getUsername()) && password.equals(user.getPassword())) {
	            System.out.println("登陆成功");
	            bo = false;
				break;
			}
		}
		else {
			System.out.println("登陆失败!用户名或密码错误！");
		}

	}

```



## 十四、登录成功后，显示商品的信息

### 14.1 创建product.xlsx并添加商品的信息

### 14.2 创建ReadProductExcel.java

### 14.3 创建Product.java

- 实体类（Bean）

### 14.4 修改ReadProductExcel.java

加入如下方法

- getAllProduct（用于显示所有商品）
- getProductById（用于查找某个商品）
- getValue(获取excel中的值，由前两个方法调用)

```java

    public Product[] getAllProduct(InputStream in) {
        Product products[] = null;
        try {
            XSSFWorkbook xw = new XSSFWorkbook(in);
            XSSFSheet xs = xw.getSheetAt(0);
            products = new Product[xs.getLastRowNum()];
            for (int j = 1; j <= xs.getLastRowNum(); j++) {
                XSSFRow row = xs.getRow(j);
                Product product = new Product();
                for (int k = 0; k <= row.getLastCellNum(); k++) {
                    XSSFCell cell = row.getCell(k);
                    if (cell == null)
                        continue;
                    if (k == 0) {
                        product.setpId(this.getValue(cell));
                    } else if (k == 1) {
                        product.setpName(this.getValue(cell));
                    } else if (k == 2) {
                        product.setpDesc(this.getValue(cell));
                    } else if (k == 3) {
                        product.setpPrice(this.getValue(cell));
                    }
                    products[j-1]=product;
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
        return products;
    }

```
```java

    public Product getProductById(String id,InputStream in) {
       // Product products[] = null;
        try {
            XSSFWorkbook xw = new XSSFWorkbook(in);
            XSSFSheet xs = xw.getSheetAt(0);
            for (int j = 1; j <= xs.getLastRowNum(); j++) {
                XSSFRow row = xs.getRow(j);
                Product product = new Product();
                for (int k = 0; k <= row.getLastCellNum(); k++) {
                    XSSFCell cell = row.getCell(k);
                    if (cell == null)
                        continue;
                    if (k == 0) {
                        product.setpId(this.getValue(cell));
                    } else if (k == 1) {
                        product.setpName(this.getValue(cell));
                    } else if (k == 2) {
                        product.setpDesc(this.getValue(cell));//把字符串转Float
                    } else if (k == 3) {
                        product.setpPrice(this.getValue(cell));
                    }
                }
                if(id.equals(product.getpId())){
                    return product;
                }
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
        return null;
    }
```
```java

    private String getValue(XSSFCell cell) {
        String value;
        CellType type = cell.getCellTypeEnum();

        switch (type) {
            case STRING:
                value = cell.getStringCellValue();
                break;
            case BLANK:
                value = "";
                break;
            case BOOLEAN:
                value = cell.getBooleanCellValue() + "";
                break;
            case NUMERIC:
                DecimalFormat df = new DecimalFormat("#");
                value = df.format(cell.getNumericCellValue());
               /*System.out.println("处理后的：" + value);
                value = cell.getNumericCellValue() + "";*/
                break;
            case FORMULA:
                value = cell.getCellFormula();
                break;
            case ERROR:
                value = "非法字符";
                break;
            default:
                value = "";
                break;
        }
        return value;
    }
```

##  十五、登录成功显示商品信息

```java

	for (User user : users) {
        if (username.equals(user.getUsername()) && password.equals(user.getPassword())) {
            System.out.println("登陆成功");
            bo = false;
            for (Product product:products){
                System.out.print(product.getpId());
                System.out.print("\t"+product.getpName());
                System.out.print("\t"+product.getpDesc());
                System.out.println("\t"+product.getpPrice());
            }
		}
	}
```

## 十六、查找某个商品

使用方法getProductById（）查找商品信息，若有该商品信息则加入购物车

```java

    System.out.println("请输入商品ID");
    String pId=scanner.next();
    int count = 0;
    /*
    创建一个购物车的数组：存的是商品
     */
    Product carts[] = new Product[3];
    /*
    根据此ID去Excel中去查找是否有该ID的商品信息，如果有则返回该商品即可
     */
    ins = null;
    ins = Class.forName("Test").getResourceAsStream("/product.xlsx");
    Product product = readProductExcel.getProductById(pId, ins);
    System.out.println("要购买的商品价格：" + product.getpPrice());
    if(product!=null){
        carts[count++]=product;
    }
```

##十七、查看购物车

```java

	    /*
	    查看购物车
	     */
	    System.out.println("购物车商品信息如下：");
	    for (Product p:carts){
	        if (p!=null){
	            System.out.print(p.getpId());
	            System.out.print("\t" + p.getpName());
	            System.out.print("\t" + p.getpPrice());
	            System.out.println("\t" + p.getpDesc());
	        }
	    }
```
##十八、结账

```java

	Order order=new Order();
	order.setUser(user);
	order.setProducts(carts);
	int a=0;
	int b=0;
	float c=0;
	float d=0;
	for (Product o:carts){
	    if (o!=null) {
	        if (o.getpId().equals("111")) {
	            a += 1;
	            c += Float.parseFloat(o.getpPrice());
	            //c = Float.parseFloat(o.getpPrice()) * a;//覆盖前面的c值
	        } else if (o.getpId().equals("222")) {
	            b += 1;
	            d += Float.parseFloat(o.getpPrice());
	            //d = Float.parseFloat(o.getpPrice()) * b;//覆盖前面的d值
	        }
	    }
	}
	order.setTotalPrice(c+d);
	order.setFinalPay(c*1+d*1);//10折优惠
	System.out.println("购买商品111的数量为：" + a);
	System.out.println("购买商品222的数量为：" + b);
	System.out.println("购买商品111的价格为：" + c);
	System.out.println("购买商品222的价格为：" + d);
	System.out.println("总价= "+order.getFinalPay());
```