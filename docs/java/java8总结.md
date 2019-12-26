# Java8 总结

## 接口的默认方法 defualt

Java 8允许通过使用 `default` 关键字向接口添加非抽象方法实现。 此功能也称为[虚拟扩展方法](http://stackoverflow.com/a/24102730)。

例子
```java
public interface  Formula {
    double calculate(int a);

    default double sqrt(int a) {
        return Math.sqrt(a);
    }
}
```
Formula接口在拥有calculate方法之外同时还定义了sqrt方法，实现了Formula接口的子类只需要实现一个calculate方法，默认方法sqrt将在子类上可以直接使用。
```java
public class DemoApp implements Formula{
    public double calculate(int a) {
        return sqrt(a * 100);
    }

    public static  void  main(String[] args){
        DemoApp app = new DemoApp();
        double a = app.calculate(100);     // 100.0
        double b =  app.sqrt(16);           // 4.0
        System.out.println(a);
        System.out.println(b);
    }

}
```

## Lambda表达式
  Lambda 的基本结构为 (arguments) -> body，有如下几种情况：

 - 参数类型可推导时，不需要指定类型，如 (a) -> System.out.println(a)
 - 当只有一个参数且类型可推导时，不强制写 (), 如 a -> System.out.println(a)
 - 参数指定类型时，必须有括号，如 (int a) -> System.out.println(a)
 - 参数可以为空，如 () -> System.out.println(“hello”)
 - body 需要用 {} 包含语句，当只有一条语句时 {} 可省略

对上面的例子进行改写
   ```java
  public class LambdaDemo {
    public static void main(String[] args){
        Formula formula = a-> a*100;
        System.out.println(formula.calculate(10));
        System.out.println(formula.sqrt(16));
    }
  }
   ```
### 函数式接口
##### 概念  
Java Lambda 表达式以函数式接口为基础。什么是函数式接口（FunctionalInterface）？ 简单说来就是只有一个方法（函数）的接口，这类接口的目的是为了一个单一的操作，也就相当于一个单一的函数了。常见的接口如：Runnable, Comparator 都是函数式接口，并且都标注了注解 @FunctionalInterface 。
