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



## tomcat

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

## apache

主配置文件 httpd.conf

## spring

### spring下载地址

http://maven.springframework.org/release/org/springframework/spring/

## linux

### 26个linux常用指令

https://linux.cn/article-6160-1.html



