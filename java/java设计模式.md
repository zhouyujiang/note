# 单例

## 单例的7中写法

单例需要考虑的地方：1 静态 唯一性，即只被new一次，2线程安全，保证在多线程的情况下只被new一次

最好使用前三种：饿汉模式和静态内部类的方式

### 饿汉模式

```
public class Singleton{
	private static Singleton singleton = new Singleton();
	private Singleton() {};
	public static Singleton getInstance() {
     	return singleton; 
	}
}
```

### 饿汉模式（变种,和上变的差别不大）

```
public class Singleton{
	private static Singleton singleton;
	static{
      	singleton = new Singleton();
	}
	private Singleton() {};
	public static Singleton getInstance() {
     	return singleton; 
	}
}
```

### 静态内部内

```
public class Singleton{
  	private static class SingletonHolder{
      	private static final Singleton singleton = new Singleton();
  	}
  	private Singleton(){};
  	public static final Singleton getInstance() {
      	return SingletonHolder.singleton;
  	}
}
```

### 懒汉模式（线程不安全）

```
public class Singleton {
	private static Singleton singleton;
	private Singleton(){};
	public static Sinigle getInstance{
     	if(null == singleton){
         	singleton = new Singleton();
     	}
     	return singleton;
	}  
}
```

### 懒汉模式（线程安全）

```
public class Singleton {
	private static Singleton singleton;
	private Singleton(){};
	public static syncronized Sinigle getInstance{
     	if(null == singleton){
         	singleton = new Singleton();
     	}
     	return singleton;
	}  
}
```

### 枚举

```
public enum Songleton {
  	INSTANCE;
  	public void whateverMethod() {
  	}
}
```

### 双重校验锁

```
public class Singleton {  
    private volatile static Singleton singleton;  
    private Singleton (){}  
    public static Singleton getInstance() {  
    if (singleton == null) {  
        synchronized (Singleton.class) {  
        	if (singleton == null) {  
              singleton = new Singleton();  
        	}  
        }  
    }  
    return singleton;  
    }  
}  
```

