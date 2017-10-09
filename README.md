# java基础

## java

### 引用传递和值传递

基本数据类型为值传递， 引用类型为引用传递String比较特殊，因为String是不可变的，所有会重新分配字符串常量空间

1 基本数据类型 输出结果为10

```
public class ValueTest {
    
    public static void main(String[] args) {
        int a = 10;
        changeVal(a);
        System.out.println(a);
    }
    
    public static void changeVal(int a){
        a += 10;
    }
    
}
```

2 特殊的String类型 输出为hello 

```
public class ValueTest {
    
    public static void main(String[] args) {
        String str = "hello";
        changeVal(str);
        System.out.println(str);
    }
    
    public static void changeVal(String str){
        str+=" world";
        System.out.println(str); // 此处输出为“hello world”
    }
    
}
```

3 引用类型 输出为hello world

```
public class ValueTest {
    
    public static void main(String[] args) {
        StringBuilder builder = new StringBuilder("hello");
        changeVal(builder);
        System.out.println(builder);
    }
    
    public static void changeVal(StringBuilder builder){
        builder.append(" world");
    }
    
}
```

### 抽象类和接口

1 抽象类反应的是一种继承关系，一个对象只能有一个父类，但是可以有多个接口

2 抽象类拥有自己的成员变量和非抽象方法，接口只能存在静态的不可变的成员数据（一般不在接口中定义成员数据），只能有抽象方法。

3 抽象类是对对象共性的抽象，接口是行为自上而下的抽象。

| 抽象类                              | 接口                                 |
| -------------------------------- | ---------------------------------- |
| 抽象类可以有抽象和非抽象方法。                  | 接口只能有抽象方法。 从Java 8开始，它也可以有默认和静态方法。 |
| 抽象类不支持多重继承。                      | 接口支持多继承。                           |
| 抽象类可以有`final`，`非final`，静态和非静态变量。 | 接口只有静态和`final`变量。                  |
| 抽象类可以提供接口的实现。                    | 接口不能提供抽象类的实现。                      |
| `abstract`关键字用来声明抽象类。            | `interface`关键字用于声明接口。              |

### java访问修饰符

| 访问修饰符     | 在类内  | 在包内  | 外部包只通过子类 | 外部包  |
| --------- | ---- | ---- | -------- | ---- |
| private   | Y    | N    | N        | N    |
| default   | Y    | Y    | N        | N    |
| protected | Y    | Y    | Y        | N    |
| public    | Y    | Y    | Y        | Y    |



### main函数中的args数组

创建类 命令行javac TestMain.java编译后，运行java TestMain aa bb cc dd  输出 hello aa   welcome bb

```
public class TestMain {    
    
    public static void main(String[] args) {    
        System.out.println("hello "+args[0]);    
        System.out.println("welcome "+args[1]);    
    }    
    
}
```

### 重载和重写

重载是同一类中，对某方法同名不同参数个数或者类型的拓展，调用方法时根据参数的类型和个数来决定使用哪一个方法，反应了静态多态性；返回值类型可以相同也可以不相同，不作为判断是否重载的标准

重写是对父类方法的重新实现，又成为覆盖，反映了动态多态性，重写的方法，返回值必须和父类相同

### 多态

父类引用指向子类对象

多态实现的三个必要条件：1继承， 2 重写， 3 向上转型

### synchronized关键字

通常用来对对象进行加锁，使对象的访问是排他的

### final关键字

修饰类，类不能被继承

修饰方法， 方法不能被重写

修饰变量，如果是基本数据类型，则值初始化后不能改变，如果是引用类型，则初始化后不能再指向其他对象。

### static关键字

修饰变量：无论实例化多少对象，静态变量只有一份拷贝，局部变量不能声明为static

修饰方法：声明独立于对象的静态方法，不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据

tips： 非static方法中可以有static字段和非static字段， static方法中只能有static字段

### char在java中为什么占两个字节

这是因为java使用`Unicode`系统而非`ASCII`码系统编码

### JDK JRE JVM之间的区别

jdk是java开发工具包 = jre + 开发工具

jre是java运行时环境，是jvm的实现

jvm是java虚拟机提供java字节码运行的环境主要用来加载代码， 验证代码， 执行代码， 提供运行时环境![110090359_45736](C:\Users\zsummer\Desktop\110090359_45736.png)

### java静态绑定和动态绑定

静态绑定：编译时确定对象的类型，如果在类中有任何private， static， final方法，则有静态绑定

```
class Dog {
    private void eat() {
        System.out.println("dog is eating...");
    }

    public static void main(String args[]) {
        Dog d1 = new Dog();
        d1.eat();
    }
}
```

动态绑定：在运行时确定对象的类型

```
class Animal {
    void eat() {
        System.out.println("animal is eating...");
    }
}

class Dog extends Animal {
    void eat() {
        System.out.println("dog is eating...");
    }

    public static void main(String args[]) {
        Animal a = new Dog();
        a.eat();
    }
}
```

### instanceof 运算符

对具有null值的变量使用instanceof运算符返回false

```
class Dog2 {
    public static void main(String args[]) {
        Dog2 d = null;
        System.out.println(d instanceof Dog2);// false
    }
}
```

### java对象克隆

对象克隆是创建对象精确副本的方法， Object的clone（）方法用于克隆对象，被克隆的对象必须实现java.lang.Cloneable接口

```
class Student18 implements Cloneable {
    int rollno;
    String name;

    Student18(int rollno, String name) {
        this.rollno = rollno;
        this.name = name;
    }

    public Object clone() throws CloneNotSupportedException {
        return super.clone();
    }

    public static void main(String args[]) {
        try {
            Student18 s1 = new Student18(101, "amit");

            Student18 s2 = (Student18) s1.clone();

            System.out.println(s1.rollno + " " + s1.name);
            System.out.println(s2.rollno + " " + s2.name);

        } catch (CloneNotSupportedException c) {
        }

    }
}
```



### java设计模式

#### 单利模式

SingleObject.java

```
public class SingleObject {

	private static SingleObject singleObject = new SingleObject();
	
	public static SingleObject getInstance() {
		return singleObject;
	}
	
	public void say() {
		System.out.println("i am singleton!");
	}
}
```

Main.java

```
public class Main {
	public static void main(String[] args) {
		SingleObject object = SingleObject.getInstance();
		object.say();
	}
}
```



#### 工厂模式

Shape.java

```
public interface Shape {
	public void draw();
}
```

Triangle.java

```
public class Triangle implements Shape {
	@Override
	public void draw() {
		// TODO Auto-generated method stub
		System.out.println("draw triangle!");
	}
}
```

Circle.java

```
public class Circle implements Shape{
	@Override
	public void draw() {
		// TODO Auto-generated method stub
		System.out.println("draw circle!");
	}
}
```

ShapeFactory.java

```
public class ShapeFactory {

	public Shape getShape(String name) {
		if (name == null) {
			return null;
		} else if (name.equalsIgnoreCase("circle")) {
			return new Circle();
		} else if (name.equalsIgnoreCase("triangle")) {
			return new Triangle();
		}
		return null;
	}
}
```

使用工厂

```
	/**
	 * 测试工厂模式
	 * @param args
	 */
	public static void main(String[] args) {
		ShapeFactory factory = new ShapeFactory();
		Shape shape = factory.getShape("circle");
		shape.draw();
		
		Shape shape2 = factory.getShape("triangle");
		shape2.draw();
		
	}
		
}
```



# 数据库

## oracle

### 取消connect权限

revoke connect from user

## mysql

###授权，撤销权限

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



# 开发工具插件

## eclipse

## maven

### 改变maven jdk版本

在pom.xml中添加

```
<plugins> 
<plugin> 
<groupId>org.apache.maven.plugins</groupId> 
<artifactId>maven-compiler-plugin</artifactId> 
<version>2.3.2</version> 
<configuration> 
<source>1.7</source> 
<target>1.7</target> 
<encoding>UTF-8</encoding> 
</configuration> 
</plugin> 
</plugins>
```

### 阿里云镜像

```
<mirror>
    <!--This sends everything else to /public -->
    <id>nexus-aliyun</id>
    <mirrorOf>*</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

# 服务器

## apache

主配置文件 httpd.conf

## Tomcat

# 框架

## spring

### spring下载地址

http://maven.springframework.org/release/org/springframework/spring/

## mybatis

### mybatis教程

http://www.yiibai.com/mybatis/

### mybatis配置文件的environments标签的default属性

environments标签可以配置多个environment标签， 使用default属性告诉mybatis当前使用的environment 如果default属性根据environment的id属性找不到对应的id则可能会抱下面的错误

```
Exception in thread "main" org.apache.ibatis.exceptions.PersistenceException: 
### Error opening session.  Cause: java.lang.NullPointerException
### Cause: java.lang.NullPointerException
	at org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:26)
	at org.apache.ibatis.session.defaults.DefaultSqlSessionFactory.openSessionFromDataSource(DefaultSqlSessionFactory.java:91)
	at org.apache.ibatis.session.defaults.DefaultSqlSessionFactory.openSession(DefaultSqlSessionFactory.java:46)
	at com.yibai.mybatis.test.HelloMybatis.main(HelloMybatis.java:32)
Caused by: java.lang.NullPointerException
	at org.apache.ibatis.session.defaults.DefaultSqlSessionFactory.openSessionFromDataSource(DefaultSqlSessionFactory.java:86)
	... 2 more
```

### mybatis 使用utf8编码

配置文件中i添加？后边的内容

```
<property name="url" value="jdbc:mysql://127.0.0.1:3306/yibai?useUnicode=true&amp;characterEncoding=UTF-8&amp;zeroDateTimeBehavior=convertToNull"/>
```



## shiro

### shiro教程

http://www.yiibai.com/shiro/



![img](http://www.yiibai.com/uploads/images/201703/1403/660170344_46272.png)

# linux

## linux

### 26个linux常用指令

https://linux.cn/article-6160-1.html



## mac

### 虚拟机安装mac系统

http://blog.csdn.net/hamber_bao/article/details/51335834