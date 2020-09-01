---
title: 阿里巴巴java开发手册-编程规约
date: 2020-08-14 09:15:55
categories: java开发手册
tags: 编程规约
---

### 编程规约

<!--more-->

#### 命名风格

##### 接口和实现类命名规则

1）【强制】对于 Service 和 DAO 类，基于 SOA 的理念，暴露出来的服务一定是接口，内部

的实现类用 Impl 的后缀与接口区别。

##### 三层架构各层命名规约：

A) Service/DAO 层方法命名规约

1） 获取单个对象的方法用 get 做前缀。

2） 获取多个对象的方法用 list 做前缀，复数形式结尾如：listObjects。 

3） 获取统计值的方法用 count 做前缀。 

4） 插入的方法用 save/insert 做前缀。

5） 删除的方法用 remove/delete 做前缀。

6） 修改的方法用 update 做前缀。

B) 领域模型命名规约

1） 数据对象：xxxDO，xxx 即为数据表名。

2） 数据传输对象：xxxDTO，xxx 为业务领域相关的名称。

3） 展示对象：xxxVO，xxx 一般为网页名称。

4） POJO 是 DO/DTO/BO/VO 的统称，禁止命名成 xxxPOJO。

####  常量定义

 

【强制】不允许任何魔法值（即未经预先定义的常量）直接出现在代码中。

反例：String key = "Id#taobao_" + tradeId;

 cache.put(key, value);

#### 代码格式

##### 换行

【强制】大括号的使用约定。如果是大括号内为空，则简洁地写成{}即可，不需要换行；如果

是非空代码块则：

1） 左大括号前不换行。

2） 左大括号后换行。

3） 右大括号前换行。

4） 右大括号后还有 else 等代码则不换行；表示终止的右大括号后必须换行。

##### 空格

1【强制】左小括号和字符之间不出现空格；同样，右小括号和字符之间也不出现空格；而左大

括号前需要空格。详见第 5 条下方正例提示。

反例：if (空格 a == b 空格)

2【强制】if/for/while/switch/do 等保留字与括号之间都必须加空格。

3【强制】任何二目、三目运算符的左右两边都需要加一个空格。

说明：运算符包括赋值运算符=、逻辑运算符&&、加减乘除符号等

4 

【强制】采用 4 个空格缩进，禁止使用 tab 字符。

说明：如果使用 tab 缩进，必须设置 1 个 tab 为 4 个空格。IDEA 设置 tab 为 4 个空格时，

请勿勾选 Use tab character；而在 eclipse 中，必须勾选 insert spaces for tabs。

```java
正例： 
public static void main(String[] args) { 
// 缩进 4 个空格 
String say = "hello"; 
// 运算符的左右必须有一个空格 
int flag = 0; 
// 关键词 if 与括号之间必须有一个空格，括号内的 f 与左括号，0 与右括号不需要空格 
if (flag == 0) { 
System.out.println(say); 
} 
// 左大括号前加空格且不换行；左大括号后换行 
if (flag == 1) { 
System.out.println("world"); 
// 右大括号前换行，右大括号后有 else，不用换行 
} else { 
System.out.println("ok"); 
// 在右大括号后直接结束，则必须换行 
} 
}
```

5【强制】注释的双斜线与注释内容之间有且仅有一个空格

```java
正例：
// 这是示例注释，请注意在双斜线之后有一个空格
String ygb = new String();
```

6【强制】单行字符数限制不超过 120 个，超出需要换行，换行时遵循如下原则：

1） 第二行相对第一行缩进 4 个空格，从第三行开始，不再继续缩进，参考示例。

2） 运算符与下文一起换行。

3） 方法调用的点符号与下文一起换行。

4） 方法调用中的多个参数需要换行时，在逗号后进行。 

5） 在括号前不要换行，见反例

```java
//正例：
StringBuffer sb = new StringBuffer(); 
// 超过 120 个字符的情况下，换行缩进 4 个空格，点号和方法名称一起换行
sb.append("zi").append("xin")... 
.append("huang")... 
.append("huang")... 
.append("huang");
反例：
StringBuffer sb = new StringBuffer(); 
// 超过 120 个字符的情况下，不要在括号前换行
sb.append("zi").append("xin")...append 
("huang"); 
// 参数很多的方法调用可能超过 120 个字符，不要在逗号前换行
method(args1, args2, args3, ... 
, argsX);
```

7【强制】方法参数在定义和传入时，多个参数逗号后边必须加空格。

```java
//正例：下例中实参的 args1，后边必须要有一个空格。
method(args1, args2, args3);
```

8【强制】IDE 的 text file encoding 设置为 UTF-8; IDE 中文件的换行符使用 Unix 格式，

不要使用 Windows 格式。

#### OOP规约

1. 【强制】避免通过一个类的对象引用访问此类的静态变量或静态方法，无谓增加编译器解析成

本，直接用类名来访问即可。

2. 【强制】所有的覆写方法，必须加@Override 注解。

说明：getObject()与 get0bject()的问题。一个是字母的 O，一个是数字的 0，加@Override

可以准确判断是否覆盖成功。另外，如果在抽象类中对方法签名进行修改，其实现类会马上编

译报错。

3. 【强制】相同参数类型，相同业务含义，才可以使用 Java 的可变参数，避免使用 Object。

说明：可变参数必须放置在参数列表的最后。（提倡同学们尽量不用可变参数编程）

正例：public List<User> listUsers(String type, Long... ids) {...}

4. 【强制】外部正在调用或者二方库依赖的接口，不允许修改方法签名，避免对接口调用方产生

影响。接口过时必须加@Deprecated 注解，并清晰地说明采用的新接口或者新服务是什么。

5. 【强制】不能使用过时的类或方法。

说明：java.net.URLDecoder 中的方法 decode(String encodeStr) 这个方法已经过时，应

该使用双参数 decode(String source, String encode)。接口提供方既然明确是过时接口，

那么有义务同时提供新的接口；作为调用方来说，有义务去考证过时方法的新实现是什么。

6. 【强制】Object 的 equals 方法容易抛空指针异常，应使用常量或确定有值的对象来调用

equals。

正例："test".equals(object);

反例：object.equals("test");

说明：推荐使用 java.util.Objects#equals（JDK7 引入的工具类）

7. 【强制】所有的相同类型的包装类对象之间值的比较，全部使用 equals 方法比较。

说明：对于 Integer var = ? 在-128 至 127 范围内的赋值，Integer 对象是在

IntegerCache.cache 产生，会复用已有对象，这个区间内的 Integer 值可以直接使用==进行

判断，但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象，这是一个大坑，

推荐使用 equals 方法进行判断

8. 关于基本数据类型与包装数据类型的使用标准如下：

1） 【强制】所有的 POJO 类属性必须使用包装数据类型。

2） 【强制】RPC 方法的返回值和参数必须使用包装数据类型。

3） 【推荐】所有的局部变量使用基本数据类型。

说明：POJO 类属性没有初值是提醒使用者在需要使用时，必须自己显式地进行赋值，任何

NPE 问题，或者入库检查，都由使用者来保证。

正例：数据库的查询结果可能是 null，因为自动拆箱，用基本数据类型接收有 NPE 风险。

反例：比如显示成交总额涨跌情况，即正负 x%，x 为基本数据类型，调用的 RPC 服务，调用

不成功时，返回的是默认值，页面显示为 0%，这是不合理的，应该显示成中划线。所以包装

数据类型的 null 值，能够表示额外的信息，如：远程调用失败，异常退出

9. 【强制】定义 DO/DTO/VO 等 POJO 类时，不要设定任何属性默认值。

反例：POJO 类的 gmtCreate 默认值为 new Date()，但是这个属性在数据提取时并没有置入具

体值，在更新其它字段时又附带更新了此字段，导致创建时间被修改成当前时间。

10. 【强制】序列化类新增属性时，请不要修改 serialVersionUID 字段，避免反序列失败；如

果完全不兼容升级，避免反序列化混乱，那么请修改 serialVersionUID 值。

说明：注意 serialVersionUID 不一致会抛出序列化运行时异常。

11. 【强制】构造方法里面禁止加入任何业务逻辑，如果有初始化逻辑，请放在 init 方法中。
12. 【强制】POJO 类必须写 toString 方法。使用 IDE 中的工具：source> generate toString  时，如果继承了另一个 POJO 类，注意在前面加一下 super.toString。
13. 【强制】禁止在 POJO 类中，同时存在对应属性 xxx 的 isXxx()和 getXxx()方法。

说明：框架在调用属性 xxx 的提取方法时，并不能确定哪个方法一定是被优先调用到，神坑之一。

#### 日期时间

1.【强制】日期格式化时，传入 pattern 中表示年份统一使用小写的 y。

说明：日期格式化时，yyyy 表示当天所在的年，而大写的 YYYY 代表是 week in which year（JDK7 之后

引入的概念），意思是当天所在的周属于的年份，一周从周日开始，周六结束，只要本周跨年，返回的 YYYY

就是下一年。

```java
//正例：表示日期和时间的格式如下所示：
new SimpleDateFormat("yyyy-MM-dd HH:mm:ss")
```

2.【强制】在日期格式中分清楚大写的 M 和小写的 m，大写的 H 和小写的 h 分别指代的意义。

说明：日期格式中的这两对字母表意如下：

1） 表示月份是大写的 M； 

2） 表示分钟则是小写的 m； 

3） 24 小时制的是大写的 H； 

4） 12 小时制的则是小写的 h。

3.【强制】获取当前毫秒数：System.currentTimeMillis(); 而不是 new Date().getTime()。

说明：如果想获取更加精确的纳秒级时间值，使用 System.nanoTime 的方式。在 JDK8 中，针对统计时间

等场景，推荐使用 Instant 类。

4.【强制】不允许在程序任何地方中使用：1）java.sql.Date 2）java.sql.Time 3）

java.sql.Timestamp。

说明：第 1 个不记录时间，getHours()抛出异常；第 2 个不记录日期，getYear()抛出异常；第 3 个在构造

方法 super((time/1000)*1000)，fastTime 和 nanos 分开存储秒和纳秒信息。

反例： java.util.Date.after(Date)进行时间比较时，当入参是 java.sql.Timestamp 时，会触发 JDK 

BUG(JDK9 已修复)，可能导致比较时的意外结果

5.【强制】不要在程序中写死一年为 365 天，避免在公历闰年时出现日期转换错误或程序逻辑

错误。



#### 集合处理

1.【强制】关于 hashCode 和 equals 的处理，遵循如下规则：

1） 只要重写 equals，就必须重写 hashCode。 

2） 因为 Set 存储的是不重复的对象，依据 hashCode 和 equals 进行判断，所以 Set 存储的对象必须重写

这两个方法。

3） 如果自定义对象作为 Map 的键，那么必须覆写 hashCode 和 equals。

说明：String 因为重写了 hashCode 和 equals 方法，所以我们可以愉快地使用 String 对象作为 key 来使

用。

2.【强制】判断所有集合内部的元素是否为空，使用 isEmpty()方法，而不是 size()==0 的方式。

说明：前者的时间复杂度为 O(1)，而且可读性更好。

```java
//正例：
Map<String, Object> map = new HashMap<>();
if(map.isEmpty()) {
 System.out.println("no element in this map.");
}
```

3.【强制】在使用 java.util.stream.Collectors 类的 toMap()方法转为 Map 集合时，一定要使

用含有参数类型为 BinaryOperator，参数名为 mergeFunction 的方法，否则当出现相同 key

值时会抛出 IllegalStateException 异常。

说明：参数 mergeFunction 的作用是当出现 key 重复时，自定义对 value 的处理策略。

```java
//正例：
List<Pair<String, Double>> pairArrayList = new ArrayList<>(3);
pairArrayList.add(new Pair<>("version", 6.19));
pairArrayList.add(new Pair<>("version", 10.24));
pairArrayList.add(new Pair<>("version", 13.14));
Map<String, Double> map = pairArrayList.stream().collect(
// 生成的 map 集合中只有一个键值对：{version=13.14}
Collectors.toMap(Pair::getKey, Pair::getValue, (v1, v2) -> v2));
//反例：
String[] departments = new String[] {"iERP", "iERP", "EIBU"};
// 抛出 IllegalStateException 异常
Map<Integer, String> map = Arrays.stream(departments)
 .collect(Collectors.toMap(String::hashCode, str -> str))
```

4.【强制】在使用 java.util.stream.Collectors 类的 toMap()方法转为 Map 集合时，一定要注

意当 value 为 null 时会抛 NPE 异常。

```java
//说明：在 java.util.HashMap 的 merge 方法里会进行如下的判断：
if (value == null || remappingFunction == null)
throw new NullPointerException();
//反例：
List<Pair<String, Double>> pairArrayList = new ArrayList<>(2);
pairArrayList.add(new Pair<>("version1", 4.22));
pairArrayList.add(new Pair<>("version2", null));
Map<String, Double> map = pairArrayList.stream().collect(
// 抛出 NullPointerException 异常
Collectors.toMap(Pair::getKey, Pair::getValue, (v1, v2) -> v2));
```

5.【强制】ArrayList 的 subList 结果不可强转成 ArrayList，否则会抛出 ClassCastException 异 

常：java.util.RandomAccessSubList cannot be cast to java.util.ArrayList。

说明：subList 返回的是 ArrayList 的内部类 SubList，并不是 ArrayList 而是 ArrayList 的一个视图，对

于 SubList 子列表的所有操作最终会反映到原列表上。

6.【强制】使用 Map 的方法 keySet()/values()/entrySet()返回集合对象时，不可以对其进行添

加元素操作，否则会抛出 UnsupportedOperationException 异常。

7.【强制】Collections 类返回的对象，如：emptyList()/singletonList()等都是 immutable list，

不可对其进行添加或者删除元素的操作。

反例：如果查询无结果，返回 Collections.emptyList()空集合对象，调用方一旦进行了添加元素的操作，就

会触发 UnsupportedOperationException 异常。

8.【强制】在 subList 场景中，高度注意对父集合元素的增加或删除，均会导致子列表的遍历、

增加、删除产生 ConcurrentModificationException 异常。

9.【强制】使用集合转数组的方法，必须使用集合的 toArray(T[] array)，传入的是类型完全一

致、长度为 0 的空数组。

反例：直接使用 toArray 无参方法存在问题，此方法返回值只能是 Object[]类，若强转其它类型数组将出现

ClassCastException 错误。

```java
//正例：
List<String> list = new ArrayList<>(2);
list.add("guan");
list.add("bao");
String[] array = list.toArray(new String[0]);
```

 说明：使用 toArray 带参方法，数组空间大小的 length， 

1） 等于 0，动态创建与 size 相同的数组，性能最好。

2） 大于 0 但小于 size，重新创建大小等于 size 的数组，增加 GC 负担。

3） 等于 size，在高并发情况下，数组创建完成之后，size 正在变大的情况下，负面影响与 2 相同。

4） 大于 size，空间浪费，且在 size 处插入 null 值，存在 NPE 隐患。

10.【强制】在使用 Collection 接口任何实现类的 addAll()方法时，都要对输入的集合参数进行

NPE 判断。

说明：在 ArrayList#addAll 方法的第一行代码即 Object[] a = c.toArray(); 其中 c 为输入集合参数，如果

为 null，则直接抛出异常。

11.【强制】使用工具类 Arrays.asList()把数组转换成集合时，不能使用其修改集合相关的方法，

它的 add/remove/clear 方法会抛出 UnsupportedOperationException 异常。

说明：asList 的返回对象是一个 Arrays 内部类，并没有实现集合的修改方法。Arrays.asList 体现的是适配

器模式，只是转换接口，后台的数据仍是数组。

```java
 String[] str = new String[] { "yang", "hao" };
 List list = Arrays.asList(str);
//第一种情况：list.add("yangguanbao"); 运行时异常。
//第二种情况：str[0] = "changed"; 也会随之修改，反之亦然。
```

12 【强制】泛型通配符<? extends T>来接收返回的数据，此写法的泛型集合不能使用 add 方法， 

而<? super T>不能使用 get 方法，两者在接口调用赋值的场景中容易出错。

说明：扩展说一下 PECS(Producer Extends Consumer Super)原则：第一、频繁往外读取内容的，适合用

<? extends T>。第二、经常往里插入的，适合用<? super T>

13.【强制】在无泛型限制定义的集合赋值给泛型限制的集合时，在使用集合元素时，需要进行

instanceof 判断，避免抛出 ClassCastException 异常。

说明：毕竟泛型是在 JDK5 后才出现，考虑到向前兼容，编译器是允许非泛型集合与泛型集合互相赋值。

```java
//反例：
List<String> generics = null;
List notGenerics = new ArrayList(10);
notGenerics.add(new Object());
notGenerics.add(new Integer(1));
generics = notGenerics;
// 此处抛出 ClassCastException 异常
String string = generics.get(0);
```

14.【强制】不要在 foreach 循环里进行元素的 remove/add 操作。remove 元素请使用 Iterator

方式，如果并发操作，需要对 Iterator 对象加锁。



```java
/*说明：三个条件如下 
*1） x，y 的比较结果和 y，x 的比较结果相反。
*2） x>y，y>z，则 x>z。 
*3） x=y，则 x，z 比较结果和 y，z 比较结果相同。
**/
//反例：下例中没有处理相等的情况，交换两个对象判断结果并不互反，不符合第一个条件，在实际使用中可能会出现异常。
new Comparator<Student>() {
 @Override
 public int compare(Student o1, Student o2) {
 return o1.getId() > o2.getId() ? 1 : -1;
 }
};
```



#### 并发处理

1.【强制】获取单例对象需要保证线程安全，其中的方法也要保证线程安全。

说明：资源驱动类、工具类、单例工厂类都需要注意。

2.【强制】创建线程或线程池时请指定有意义的线程名称，方便出错时回溯。

正例：自定义线程工厂，并且根据外部特征进行分组，比如，来自同一机房的调用，把机房编号赋值给

whatFeaturOfGroup

```java
public class UserThreadFactory implements ThreadFactory {
 private final String namePrefix;
 private final AtomicInteger nextId = new AtomicInteger(1);
 // 定义线程组名称，在 jstack 问题排查时，非常有帮助
 UserThreadFactory(String whatFeaturOfGroup) {
 namePrefix = "From UserThreadFactory's " + whatFeaturOfGroup + "-Worker-";
 }
 @Override
 public Thread newThread(Runnable task) {
 String name = namePrefix + nextId.getAndIncrement();
 Thread thread = new Thread(null, task, name, 0, false);
 System.out.println(thread.getName());
 return thread;
 } }
```

3.【强制】线程资源必须通过线程池提供，不允许在应用中自行显式创建线程。

说明：线程池的好处是减少在创建和销毁线程上所消耗的时间以及系统资源的开销，解决资源不足的问题。

如果不使用线程池，有可能造成系统创建大量同类线程而导致消耗完内存或者“过度切换”的问题。

4.【强制】线程池不允许使用 Executors 去创建，而是通过 ThreadPoolExecutor 的方式，这

样的处理方式让写的同学更加明确线程池的运行规则，规避资源耗尽的风险。

说明：Executors 返回的线程池对象的弊端如下： 

1） FixedThreadPool 和 SingleThreadPool：

允许的请求队列长度为 Integer.MAX_VALUE，可能会堆积大量的请求，从而导致 OOM。 

2） CachedThreadPool：

允许的创建线程数量为 Integer.MAX_VALUE，可能会创建大量的线程，从而导致 OOM。

5.【强制】SimpleDateFormat 是线程不安全的类，一般不要定义为 static 变量，如果定义为 static，

必须加锁，或者使用 DateUtils 工具类。

```java
//正例：注意线程安全，使用 DateUtils。亦推荐如下处理：
private static final ThreadLocal<DateFormat> df = new ThreadLocal<DateFormat>() {
 @Override
 protected DateFormat initialValue() {
 return new SimpleDateFormat("yyyy-MM-dd");
 }
};

```

6.【强制】必须回收自定义的 ThreadLocal 变量，尤其在线程池场景下，线程经常会被复用，

如果不清理自定义的 ThreadLocal 变量，可能会影响后续业务逻辑和造成内存泄露等问题。

尽量在代理中使用 try-finally 块进行回收。

```java
//正例：
objectThreadLocal.set(userInfo);
try {
 // ...
} finally {
 objectThreadLocal.remove();
}
```

7.【强制】高并发时，同步调用应该去考量锁的性能损耗。能用无锁数据结构，就不要用锁；能

锁区块，就不要锁整个方法体；能用对象锁，就不要用类锁。

说明：尽可能使加锁的代码块工作量尽可能的小，避免在锁代码块中调用 RPC 方法。

8.【强制】对多个资源、数据库表、对象同时加锁时，需要保持一致的加锁顺序，否则可能会造

成死锁。

说明：线程一需要对表 A、B、C 依次全部加锁后才可以进行更新操作，那么线程二的加锁顺序也必须是 A、 

B、C，否则可能出现死锁。

9.【强制】在使用阻塞等待获取锁的方式中，必须在 try 代码块之外，并且在加锁方法与 try 代

码块之间没有任何可能抛出异常的方法调用，避免加锁成功后，在 finally 中无法解锁。

说明一：如果在 lock 方法与 try 代码块之间的方法调用抛出异常，那么无法解锁，造成其它线程无法成功

获取锁。

说明二：如果 lock 方法在 try 代码块之内，可能由于其它方法抛出异常，导致在 finally 代码块中，unlock

对未加锁的对象解锁，它会调用 AQS 的 tryRelease 方法（取决于具体实现类），抛出

IllegalMonitorStateException 异常。

说明三：在 Lock 对象的 lock 方法实现中可能抛出 unchecked 异常，产生的后果与说明二相同。

```java
//正例：
Lock lock = new XxxLock();
// ...
lock.lock();
try {
 doSomething();
 doOthers();
} finally {
 lock.unlock();
}
//反例：
Lock lock = new XxxLock();
// ...
try {
 // 如果此处抛出异常，则直接执行 finally 代码块
 doSomething();
 // 无论加锁是否成功，finally 代码块都会执行
 lock.lock();
 doOthers();
} finally {
 lock.unlock();
}
```

10.【强制】在使用尝试机制来获取锁的方式中，进入业务代码块之前，必须先判断当前线程是否

持有锁。锁的释放规则与锁的阻塞等待方式相同。

说明：Lock 对象的 unlock 方法在执行时，它会调用 AQS 的 tryRelease 方法（取决于具体实现类），如果

当前线程不持有锁，则抛出 IllegalMonitorStateException 异常。

```java
//正例：
Lock lock = new XxxLock();
// ...
boolean isLocked = lock.tryLock();
if (isLocked) {
 try {
 doSomething();
 doOthers();
 } finally {
 lock.unlock();
 } }
```

11.【强制】并发修改同一记录时，避免更新丢失，需要加锁。要么在应用层加锁，要么在缓存加

锁，要么在数据库层使用乐观锁，使用 version 作为更新依据。

说明：如果每次访问冲突概率小于 20%，推荐使用乐观锁，否则使用悲观锁。乐观锁的重试次数不得小于

3 次。

12.【强制】多线程并行处理定时任务时，Timer 运行多个 TimeTask 时，只要其中之一没有捕获抛

出的异常，其它任务便会自动终止运行，使用 ScheduledExecutorService 则没有这个问题。

#### 控制语句

1.【强制】在一个 switch 块内，每个 case 要么通过 continue/break/return 等来终止，要么

注释说明程序将继续执行到哪一个 case 为止；在一个 switch 块内，都必须包含一个 default

2.【强制】当 switch 括号内的变量类型为 String 并且此变量为外部参数时，必须先进行 null

判断。

```java
//反例：如下的代码输出是什么？
public class SwitchString {
 public static void main(String[] args) {
 method(null);
 }
 public static void method(String param) {
 switch (param) {
 // 肯定不是进入这里
 case "sth":
 System.out.println("it's sth");
 break;
 // 也不是进入这里
 case "null":
 System.out.println("it's null");
 break;
 // 也不是进入这里
 default:
 System.out.println("default");
 }
 } }
```

3.【强制】在 if/else/for/while/do 语句中必须使用大括号。

说明：即使只有一行代码，禁止不采用大括号的编码方式：if (condition) statements; 

4.【强制】三目运算符 condition? 表达式 1 : 表达式 2 中，高度注意表达式 1 和 2 在类型对齐

时，可能抛出因自动拆箱导致的 NPE 异常。

说明：以下两种场景会触发类型对齐的拆箱操作：

1） 表达式 1 或表达式 2 的值只要有一个是原始类型。

2） 表达式 1 或表达式 2 的值的类型不一致，会强制拆箱升级成表示范围更大的那个类型。

```java
//反例：
Integer a = 1;
Integer b = 2;
Integer c = null;
Boolean flag = false;
// a*b 的结果是 int 类型，那么 c 会强制拆箱成 int 类型，抛出 NPE 异常
Integer result=(flag? a*b : c)
```

5.【强制】在高并发场景中，避免使用”等于”判断作为中断或退出的条件。

说明：如果并发控制没有处理好，容易产生等值判断被“击穿”的情况，使用大于或小于的区间判断条件

来代替。

反例：判断剩余奖品数量等于 0 时，终止发放奖品，但因为并发处理错误导致奖品数量瞬间变成了负数，

这样的话，活动无法终止。



#### 注释规约

1.【强制】类、类属性、类方法的注释必须使用 Javadoc 规范，使用/**内容*/格式，不得使用

// xxx 方式。

说明：在 IDE 编辑窗口中，Javadoc 方式会提示相关注释，生成 Javadoc 可以正确输出相应注释；在 IDE

中，工程调用方法时，不进入方法即可悬浮提示方法、参数、返回值的意义，提高阅读效率。

2.【强制】所有的抽象方法（包括接口中的方法）必须要用 Javadoc 注释、除了返回值、参数、

异常说明外，还必须指出该方法做什么事情，实现什么功能。

说明：对子类的实现要求，或者调用注意事项，请一并说明。

3【强制】所有的类都必须添加创建者和创建日期。

说明：在设置模板时，注意 IDEA 的@author 为`${USER}`，而 eclipse 的@author 为`${user}`，大小写有

区别，而日期的设置统一为 yyyy/MM/dd 的格式。

```java
正例：
 /**
* @author yangguanbao
* @date 2016/10/31
*/
```

4 【强制】方法内部单行注释，在被注释语句上方另起一行，使用//注释。方法内部多行注释使

用/* */注释，注意与代码对齐。

5【强制】所有的枚举类型字段必须要有注释，说明每个数据项的用途。