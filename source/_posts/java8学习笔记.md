---
title: java8学习笔记
date: 2020-08-02 13:54:40
categories: jak	
tags: java8
---



### Java 8新特性

java8的新特性主要有Stream流；Lambda表达式；通过行为参数化传递代码；函数式接口；接口的默认方法；全新的时间日期AP；Annotation 支持多重注解。等等

<!--more-->

#### 通过行为参数化传递代码

传递抽象化类，作为参数：

```java
//择标准建模
public interface ApplePredicate{ 
 boolean test (Apple apple); 
}
//多个实现
public class AppleHeavyWeightPredicate implements ApplePredicate{ 
 public boolean test(Apple apple){ 
 return apple.getWeight() > 150; 
 } 
} 
public class AppleGreenColorPredicate implements ApplePredicate{
 public boolean test(Apple apple){ 
 return "green".equals(apple.getColor()); 
 } 
}
//根据抽象条件筛选
public static List<Apple> filterApples(List<Apple> inventory, 
 ApplePredicate p){ 
 List<Apple> result = new ArrayList<>(); 
 for(Apple apple: inventory){ 
 if(p.test(apple)){ 
 result.add(apple); 
 } 
 } 
 return result; 
}
```

在Java 8中，List自带了一个sort方法（你也可以使用Collections.sort）。sort的行为

可以用java.util.Comparator对象来参数化，它的接口如下：

```java
// java.util.Comparator 
public interface Comparator<T> { 
 public int compare(T o1, T o2); 
}
//因此，你可以随时创建Comparator的实现，用sort方法表现出不同的行为。比如，你可以
//使用匿名类，按照重量升序对库存排序：
inventory.sort(new Comparator<Apple>() { 
 public int compare(Apple a1, Apple a2){ 
 return a1.getWeight().compareTo(a2.getWeight()); 
 } 
});
```

#### Lambda表达式

**Lambda 表达式** − Lambda 允许把函数作为一个方法的参数（函数作为参数传递到方法中）。

格式：

```java
(parameters) -> expression
或
(parameters) ->{ statements; }
```



##### 使用场景

在函数式接口上使用Lambda表达式。

将Lambda表达式作为参数传递给某个方法



##### 函数式接口

一言以蔽之，函数式接口就是只定义一个抽象方法的接口，但是可以有多个非抽象方法的接口。。



##### 函数描述符

函数式接口的抽象方法的签名基本上就是Lambda表达式的签名。我们将这种抽象方法叫作

函数描述符。



##### 使用函数式接口来传递行为

Java 8的库设计师帮你在java.util.function包中引入了几个新的函数式接口。如：Predicate、Consumer和Function



##### 变量作用域

lambda 表达式只能引用标记了 final 的外层局部变量，这就是说不能在 lambda 内部修改定义在域外的局部变量，否则会编译错误。



#### 方法引用

方法引用使用一对冒号 **::**

- **构造器引用：**它的语法是Class::new，或者更一般的Class< T >::new实例如下：

  ```java
  final Car car = Car.create( Car::new ); final List< Car > cars = Arrays.asList( car );
  ```

- **静态方法引用：**它的语法是Class::static_method，实例如下：

  ```java
  cars.forEach( Car::collide );
  ```

- **特定类的任意对象的方法引用：**它的语法是Class::method实例如下：

  ```java
  cars.forEach( Car::repair );
  ```

- **特定对象的方法引用：**它的语法是instance::method实例如下：

  ```java
  final Car police = Car.create( Car::new ); cars.forEach( police::follow );
  ```

  

#### 默认方法

Java 8 新增了接口的默认方法。

简单说，默认方法就是接口可以有实现方法，而且不需要实现类去实现其方法。

我们只需在方法名前面加个 default 关键字即可实现默认方法。



#### Stream 流

流是Java API的新成员，它允许你以声明性方式处理数据集合（通过查询语句来表达，而不

是临时编写一个实现）。就现在来说，你可以把它们看成遍历数据集的高级迭代器。

是一组便捷对集合处理的api。

- **stream()** − 为集合创建串行流。
- **parallelStream()** − 为集合创建并行流。



##### 只能遍历一次

请注意，和迭代器类似，流只能遍历一次。遍历完之后，我们就说这个流已经被消费掉了。

你可以从原始数据源那里再获得一个新的流来重新遍历一遍，就像迭代器一样。例如，以下代码会抛出一个异常，说流已被消

费掉了：

```java
List<String> title = Arrays.asList("Java8", "In", "Action"); 
Stream<String> s = title.stream(); 
s.forEach(System.out::println); 
s.forEach(System.out::println);//java.lang.IllegalStateException:流已被操作或关闭
```



总而言之，流的使用一般包括三件事：

 一个数据源（如集合）来执行一个查询；

 一个中间操作链，形成一条流的流水线；

 一个终端操作，执行流水线，并能生成结果。

![image-20200911102914791](D:\code\myBlog\source\_posts\java8学习笔记\image-20200911102914791.png)



##### forEach

Stream 提供了新的方法 'forEach' 来迭代流中的每个数据。以下代码片段使用 forEach 输出了10个随机数

##### map（对每个元素的操作）

map 方法用于映射每个元素到对应的结果，以下代码片段使用 map 输出了元素对应的平方数：

##### filter

filter 方法用于通过设置的条件过滤出元素。以下代码片段使用 filter 方法过滤出空字符串：

##### limit

imit 方法用于获取指定数量的流。 以下代码片段使用 limit 方法打印出 10 条数据：

##### sorted

sorted 方法用于对流进行排序。

##### anyMatch

anyMatch方法可以回答“流中是否有一个元素能匹配给定的谓词”。比如，你可以用它来看

看菜单里面是否有素食可选择：

```java
if(menu.stream().anyMatch(Dish::isVegetarian)){ 

 System.out.println("The menu is (somewhat) vegetarian friendly!!"); 

} 
```

anyMatch方法返回一个boolean，因此是一个终端操作。

##### allMatch

allMatch方法的工作原理和anyMatch类似，但它会看看流中的元素是否都能匹配给定的谓词。比如，你可以用它来看看菜品是否有利健康（即所有菜的热量都低于1000卡路里）

```java
boolean isHealthy = menu.stream() 
 .allMatch(d -> d.getCalories() < 1000);
```

##### noneMatch

和allMatch相对的是noneMatch。它可以确保流中没有任何元素与给定的谓词匹配。比如，

你可以用noneMatch重写前面的例子：

```java
boolean isHealthy = menu.stream() 
 .noneMatch(d -> d.getCalories() >= 1000);
```



##### **findFirst**和indAny

findAny方法将返回当前流中的任意元素。

findFirst方法将返回当前流中的第一个元素。

你可能会想，为什么会同时有findFirst和findAny呢？答案是并行。找到第一个元素

在并行上限制更多。如果你不关心返回的元素是哪个，请使用findAny，因为它在使用并行流

时限制较少。

##### reduce归约

Lambda反复结合每个元素，直到流被归约成一个值。

```java
//求和
int sum = numbers.stream().reduce(0, (a, b) -> a + b);
```

##### 数值流

Java 8引入了三个原始类型特化流接口：IntStream、DoubleStream和LongStream

将流转换为特化版本的常用方法是mapToInt、mapToDouble和mapToLong。

```java
int calories = menu.stream() 
    //返回一个 IntStream
 .mapToInt(Dish::getCalories) 
 .sum();
```

##### 构建流

1由值创建流。使用静态方法Stream.of，通过显式值创建一个流。

2由数组创建流。使用静态方法Arrays.stream从数组创建一个流。

3由文件生成流。Java中用于处理文件等I/O操作的NIO API（非阻塞 I/O）已更新，以便利用Stream API。

java.nio.file.Files中的很多静态方法都会返回一个流。例如，一个很有用的方法是

Files.lines，它会返回一个由指定文件中的各行构成的字符串流

4由函数生成流。创建无限流。Stream API提供了两个静态方法来从函数生成流：Stream.iterate和Stream.generate。

这两个操作可以创建所谓的无限流：不像从固定集合创建的流那样有固定大小的流。由iterate

和generate产生的流会用给定的函数按需创建值，因此可以无穷无尽地计算下去！

```java
Stream.iterate(0, n -> n + 2) 
 .limit(10) 
 .forEach(System.out::println)
```



#### Java 8 日期时间 API

Java 8 在 **java.time** 包下提供了很多新的 API。以下为两个比较重要的 API：

- **Local(本地)** − 简化了日期时间的处理，没有时区的问题。
- **Zoned(时区)** − 通过制定的时区处理日期时间。

新的java.time包涵盖了所有处理日期，时间，日期/时间，时区，时刻（instants），过程（during）与时钟（clock）的操作。

##### 本地化时间API

LocalDate/LocalTime 和 LocalDateTime 类可以在处理时区不是必须的情况。

```java
      // 获取当前的日期时间
      LocalDateTime currentTime = LocalDateTime.now();
	  LocalDate date1 = currentTime.toLocalDate();
	     Month month = currentTime.getMonth();
      int day = currentTime.getDayOfMonth();
      int seconds = currentTime.getSecond();
        
      System.out.println("月: " + month +", 日: " + day +", 秒: " + seconds);
```

##### 使用时区的的日期时间API

```java
ZonedDateTime date1 = ZonedDateTime.parse("2015-12-03T10:15:30+05:30[Asia/Shanghai]");
```



#### java小知识

1 方法的签名:方法的名称和参数类型

2 匿名类:Java 中可以实现一个类中包含另外一个类，且不需要提供任何的类名直接实例化。

主要是用于在我们需要的时候创建一个对象来执行特定的任务，可以使代码更加简洁。

匿名类是不能有名字的类，它们不能被引用，只能在创建时用 **new** 语句来声明它们。

匿名类语法格式：

```java
class outerClass {

    // 定义一个匿名类
    object1 = new Type(parameterList) {
         // 匿名类代码
    };
}
```



