# java基础

## java

### java常用5大类包

1 **java.lang.***  变成语言基础类包，最重要的类是Object和Class

2 **java.util.*** 各种工具类包，比如集合，日期等

3 **java.io.*** 提供了全面的io接口，包括文件读写等

4 **java.net.*** 提供了网络相关的接口

5 **java.sql.*** 提供了数据库相关的接口

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

### ^运算符

```
计算6^3 结果为5，^表示异或 即相异为1
6=110
3=011
6^3 = 110^011 = 101 = 5
```

### 移位运算符“>>” "<<" ">>>>"

```
10>>3 相当于吧10的二进制数左移3位， 结果转换成十进制数就是10乘以2的3次方
```

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

### 输出字符的assic码值

A---Z ---a---z assic由大到小 Z与a之间还有一些特殊符号 比如‘[’

```
System.out.println(Integer.valueOf('a'));
System.out.println(Integer.valueOf('z'));
System.out.println(Integer.valueOf('A'));
System.out.println(Integer.valueOf('Z'));

char c = 92;
System.out.println(c);

/*** 控制台输出结果为 ***/
97
122
65
90
\
```

### String的equals方法的实现

```
public boolean equals(Object anObject) {
        if (this == anObject) {
            return true;
        }
        if (anObject instanceof String) {
            String anotherString = (String)anObject;
            int n = value.length;
            if (n == anotherString.value.length) {
                char v1[] = value;
                char v2[] = anotherString.value;
                int i = 0;
                while (n-- != 0) {
                    if (v1[i] != v2[i])
                        return false;
                    i++;
                }
                return true;
            }
        }
        return false;
    }
```

### String的 == 比较

```
/**
	 * == 比较的是栈中的内容是否相同， 基本数据类型存储在栈中，引用类型的地址存储在栈中，内容存储在堆中。
	 * String重写了hashCode方法 所以这里返回的hashCode值相同 但是实际上地址是不同的 ，所以使用==时返回false 但是hashCode 却相等
	 * 使用字面量创建字符串的时候，会先到字符串缓冲池中寻找是否有相同的字符串，如果有则直接指向该字符串，如果没有则重新创建。而使用new关键字 则会直接重新创建。
	 */
	public static void run4() {
		String str1 = "ab";
		String str2 = "ab";
		String str3 = new String(str1);
		
		System.out.println(str1 == str2); // true
		System.out.println(str1 == str3); // false
		
		System.out.println(str1.hashCode()); // 3105
		System.out.println(str2.hashCode()); // 3105
		System.out.println(str3.hashCode()); // 3105
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

### 线程的生命周期

![img](http://www.yiibai.com/uploads/images/201704/1304/832110400_15852.jpg)

### 线程优先级

java线程优先级在1-10（MIN_PRIORITY-MAXPRIORITY）默认优先级为5（NORM_PRIORITY）,线程优先级并不能保证线程的执行顺序。

# 开发工具插件

## eclipse

### 快捷键

```
ctrl + shift + p      跳转到对应的括号

ctrl + alt + H 找到选中方法被调用的位置，并生成调用树
ctrl + shift + G 找到该方法被调用的位置。
F4  查看typeHierachy继承树 
```

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

### tomcat的多种部署方式

​	热加载和热部署可以提高开发阶段的效率，配置的属性为：

​	热加载：reloadabel = "true"  (不清空session，不释放内存)

​	热部署：autoDeploy = "true" （清空session，释放内存）

* 直接将web项目拷贝到webapps目录下

* 修改server.xml：在conf文夹下下找到server.xml文件，打开找到Host标签，在里边添加如下代码

  ```
  <!-- 
  	path:app访问路径
  	docBase:app路径
  	reloadabel：开发阶段一般设置为true，方便开发，发布阶段一般设置为false，提高程序访问速度
  -->
  <Context path="/appPath" docBase="F:\work\appPath\WebRoot"  reloadable ="true"debug="0" 		privileged="true">
  </Context> 
  ```

* 在conf/catalina/localhost 目录下添加配置文件 xxx.xml

  ```
  <!-- 
  	app访问路径为xxx（配置文件名字）
  	docBase:app路径
  	reloadabel：开发阶段一般设置为true，方便开发，发布阶段一般设置为false，提高程序访问速度
  -->
  <Context docBase="F:\work\appPath\WebRoot"  reloadable ="true"debug="0" 			privileged="true">
  </Context> 
  ```

  ​

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

### dbcp和c3p0

dbcp 需要的jar包为：commons-dbcp.jar、commons-pool.jar

c3p0需要的jar包为：c3p0-0.9.2.1.jar mchange-commons-java-0.2.3.4.jar

## shiro

### shiro教程

http://www.yiibai.com/shiro/



![img](http://www.yiibai.com/uploads/images/201703/1403/660170344_46272.png)



## mac

### 虚拟机安装mac系统

http://blog.csdn.net/hamber_bao/article/details/51335834