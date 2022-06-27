---
title: HIT-软件构造博客-具有可复用性、可维护性与健壮性的软件构造
date: 2022-06-08 20:34:23
description: 谈谈软件构造技术中应注意的几个必备良好性质
tags: HIT-SC
categories: HIT-SC
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206040831943.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}
# 1 可复用性的概念

> programming for reuse 面向复用编程：开发出可复用的软件
> 		programming with reuse 基于复用编程：利用已有的可复用软件搭建应用系统

优点：

+ 降低成本和开发时间
+ 经过充分的测试，可靠、稳定
+ 标准化，在不同应用中保持一致

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091832025.png" alt="image-20220609183209975" style="zoom:67%;" />

# 2 面向复用的软件构造技术

## 2.1 Liskov Substitution Principle 里氏替换原则（LSP）

> + 子类型多态：客户端可用统一的方式处理不同类型的对象
> + **在可以使用父类的场景，都可以用子类型代替而不会有任何问题**

+ 编译强制规则

  + 子类型可以增加方法，但**不可删除方法**

  + 子类型需要**实现**抽象类型中的**所有未实现方法**

  + **协变**：子类型中重写的方法必须有相同或子类型的返回值或者符合 co-variance 的参数

  + **逆变**：子类型中重写的方法必须使用同样类型的参数或者符合 contra-variance 的参数

  + 子类型中重写的方法**不能抛出额外的异常**

+ Also applies to specified behavior (methods):
  + Same or stronger invariants **更强的不变量**
  + Same or weaker preconditions **更弱的前置条件**
  + Same or stronger postconditions **更强的后置条件**

## 2.2 协变 & 反协变

父类型 → 子类型：

+ 协变：**返回值和异常**不变或越来越**具体**
+ 逆变（反协变）：**参数类型**要**相反地变化**，要不变或越来越**抽象**

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091834546.png" alt="image-20220609183406466" style="zoom:67%;" />

## 2.3 泛型

泛型类型是不支持协变的：如`ArrayList<String>`是`List<String>`的子类型，但`List<String>`不是`List<Object>`的子类型。这是因为发生了类型擦除，运行时就不存在泛型了，所有的泛型都被替换为具体的类型。但是在实际使用的过程中是存在能够处理不同的类型的泛型的需求的，如定义一个方法参数是`List<E>`类型的，但是要适应不同的类型的 E，于是可使用通配符`?`来解决这个需求：

+ 无类型条件限制：

  ```java
  public static void printList(List<?> list) {
  	for (Object elem: list)
  		System.out.print(elem + " ");
  }
  ```

+ 当为 A 类型的**父类型**

  ```java
  public static void printList(List<? super A> list){...}
  ```

+ 当为 A 类型的**子类型**

  ```java
  public static void printList(List<? extends A> list){...}
  ```

## 2.4 委派（Delegation）

+ 一个对象请求另一个对象的功能
+ 通过运行时动态绑定，实现对其他类中代码的动态复用
+ 委托发生在 object 层面；继承发生在 class 层面

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091836503.png" alt="image-20220609183648423" style="zoom:67%;" />

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091837799.png" alt="image-20220609183711733" style="zoom:67%;" />

以下列出一些 Types of Delegation：

### 2.4.1 依赖 Dependency

+ 临时性的 delegation
+ 把被 delegation 的对象**以参数方式传入**。只有在需要的时候才建立与被委派类的联系，而当方法结束的时候这种关系也就随之断开了。

```java
class Duck {
	//no field to keep Flyable object
	public void fly(Flyable f) { f.fly(); } //让这个鸭子以f的方式飞
    public void quack(Quackable q) { q.quack() }; //让鸭子以q的方式叫
}
```

### 2.4.2 关联 Association

+ 永久性的 delegation
+ 分为：组合（Composition）和聚合（Aggregation）
+ **被delegation的对象保存在rep中**，该对象的类型被永久的与此 ADT 绑定在了一起。

### 2.4.3 组合 Composition

+ 更强的 Association，但难以变化

+ 在**rep或构造方法中**设定

```java
Duck d = new Duck();
d.fly();
class Duck {
    //这两种实现方式的效果是相同的
	Flyable f = new FlyWithWings(); //写死在rep中
	public Duck() { f = new FlyWithWings(); } //写死在构造方法中
	public void fly(){ f.fly(); }
}
```

### 2.4.4 聚合 Aggregation

+ 更弱的 Association👆，可动态变化
+ 在**构造方法中传入参数**绑定

```java
Flyable f = new FlyWithWings();
Duck d = new Duck(f);
d.fly();
class Duck {
	Flyable f; // 这个必须由构造方法传入参数绑定
	public Duck(Flyable f) { this.f = f; } // 在此传入
    public void fly(){ f.fly(); }
}
```

## 2.5 组合（Composition）和CRP原则

1. 利用 delegation 的机制，将功能的具体实现与调用分离，在实现中又通过接口的继承树实现功能的不同实现方法，而在调用类中只需要创建具体的子类型然后调用即可。组合就是多个不同方面的 delegation 的结合。

   <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091847483.png" alt="image-20220609184701420" style="zoom: 60%;" />

2. 抽象层是不会轻易发生变化的，会发生变化的只有底层的具体的子类型，而具体功能的变化（实现不同的功能）也是在最底层，所以抽象层是稳定的。而在具体层，两个子类之间的委派关系就有可能是稳定的也有可能是动态的，这取决于需求和设计者的设计决策。

   <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091847511.png" alt="image-20220609184731435" style="zoom: 60%;" />

## 2.6 白盒框架 & 黑盒框架的原理与实现

### 2.6.1 黑盒框架

+ 通过实现特定接口进行框架扩展，采用的是**delegation机制**达到这种目的，通常采用的设计模式是策略模式(Strategy)和观察者模式(Observer)；
+ 黑盒所**预留**的是一个**接口**，在框架中只调用接口中的方法，而接口中方法的实现就依据派生出的子类型的不同而不同，它的客户端启动的就是框架本身。

### 2.6.2 白盒框架

+ 通过**继承和重写实现功能的扩展**，通常的设计模式是模板模式(Template Method)；
+ 白盒框架所执行的是**框架所写好的代码**，只有通过 override 其方法来实现新的功能，客户端启动的的是第三方开发者派生的子类型。

# 3 面向复用的设计模式

## 3.1 Adapter 适配器模式

+ 将某个类/接口转换为 client 期望的其他形式
+ 增加接口
  + 通过增加一个接口，将已存在的子类封装起来
  + client**面向接口编程**，从而隐藏了具体子类

> 适用场合：你已经有了一个类，但其方法与目前client的需求不一致。
> 		根据OCP原则，不能改这个类，所以扩展一个adaptor和一个统一接口。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091850809.png" alt="image-20220609185046743" style="zoom:50%;" />

## 3.2 Decorator 装饰者模式

继承组合会引起组合爆炸/代码重复。

+ 为对象增加不同侧面的特性
+ **对每一个特性构造子类，通过委派机制增加到对象上**
+ 客户端需要一个具有多种特性的 object，通过**逐层的装饰**来实现

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091904511.png" alt="image-20220609190400408" style="zoom:67%;" />

下面举一个例子：

+ `Stack`对应上图`Component`接口
+ `ArrayStack`对应`ConcreteComponent`，基础类
+ `StackDecorator`对应`Decorator`，装饰类（可以是抽象类）
+ `UndoStack`对应`ConcreteDecoratorA`，装饰类的具体类

```java
//Stack接口，定义了所有的Stack共性的基础的功能
interface Stack {
	void push(Item e);
	Item pop();
}
//最基础的类，啥个性也没有的Stack，只有共性的实现
public class ArrayStack implements Stack {
	... //rep
	public ArrayStack() {...}
	public void push(Item e) {...}
	public Item pop() { ... }
}
//装饰器类，可以是一个抽象类，用于扩展出有各个特性方面的各个子类
public abstract class StackDecorator implements Stack {
	protected final Stack stack; //用来保存delegation关系的rep
	public StackDecorator(Stack stack) {
		this.stack = stack; //建立稳定的delegation关系
	}
	public void push(Item e) {
		stack.push(e); //通过delegation完成任务
	}
	public Item pop() {
		return stack.pop(); //通过delegation完成任务
	}
}
//一个有撤销特性功能的子类
public class UndoStack extends StackDecorator implements Stack {
	private final UndoLog log = new UndoLog();
	public UndoStack(Stack stack) {
		super(stack); //调用父类的构造方法建立delegation关系
	}
	public void push(Item e) {
		log.append(UndoLog.PUSH, e); //实现个性化的功能
		super.push(e); //共性的功能通过调用父类的实现来完成
	}
	public void undo() {
		//implement decorator behaviors on stack
	}
	...
}
```

+ 使用装饰对象：层层嵌套初始化`new Class1(new Class2(new Class3(...)))`

```java
// 先创建出一个基础类对象
Stack s = new ArrayStack();
// 利用UndoStack中继承到的自己到自己的委派建立起从UndoStack到ArrayStack的delegation关系
// 这样，UndoStack也就能够实现最基础的功能，并且自身也实现了个性化的功能
Stack us = new UndoStack(s);
// 通过一层层的装饰实现各个维度的不同功能
Stack ss = new SecureStack(new SynchronizedStack(us));
```

JDK 中装饰器模式的应用：

+ `static List<T> unmodifiableList(List<T> list)`
+ `static Set<T> synchronizedSet(Set<T> set)`

+ `static List<T> unmodifiableList(List<T> list)`
+ `static Set<T> synchronizedSet(Set<T> set)`

## 3.3 facade 外观模式（略）

## 3.4 Strategy 策略模式

+ 有多种不同的算法来实现同一个任务
+ 但需要 client 根据需要动态切换算法，而不是写死在代码里
+ **为不同的实现算法构造抽象接口，利用delegation，运行时动态传入client倾向的算法类实例**

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206092201732.png" alt="image-20220609220136644" style="zoom:50%;" />

## 3.5 Template Method 模板方法模式

+ 框架：白盒框架
+ 做事情的步骤一样，但具体方法不同
+ 共性的步骤在抽象类内公共实现，差异化的步骤在各个子类中实现
+ **使用继承和重写实现模板模式**

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206092202581.png" alt="image-20220609220200507" style="zoom:50%;" />

适用场合：有共性的算法流程，但算法各步骤有不同的实现典型的“将共性提升至超类型，将个性保留在子类型”

## 3.6 Iterator 迭代器模式

+ 客户端希望遍历被放入容器/集合类的一组 ADT 对象，无需关心容器的具体类型
+ 不管对象被放进哪里，都应该提供同样的遍历方式

实现方式是在 ADT 类中实现`Iterable`接口，该接口内部只有一个返回一个迭代器的方法，然后创建一个迭代器类实现 Iterator 接口，实现`hasnext()`、`next()`、`remove()`这三个方法。

# 4 可维护性的度量

## 4.1 可维护性的常见度量指标

指标：可维护性、可扩展性、灵活性、可适应性、可管理性、支持性

实际方法：

+ 继承的层次数
+ 类之间的耦合度
+ 单元测试的覆盖度

## 4.2 聚合度与耦合度

模块化编程：高内聚 & 低耦合

5 Rules of Modularity Design：

+ Direct Mapping **直接映射**
+ Few Interfaces **尽可能少的接口**
+ Small Interfaces **尽可能小的接口**
+ Explicit Interfaces **显式接口**
+ Information Hiding **信息隐藏**

# 5 可维护性的构造原则 SOLID

## 5.1 SRP: The Single Responsibility Principle **单一责任原则**

+ 责任：变化的原因
+ 不应该有多于 1 个原因让你的 ADT 发生变化，否则就**拆分**开

## 5.2 OCP: The Open-Closed Principle **开放-封闭原则**

+ **对扩展性的开放**
  + 模块的行为应是可扩展的
  + 从而该模块可表现出新的行为以满足需求的变化
+ **对修改的封闭**
  + 但模块自身的代码是不应被修改的
  + 扩展模块行为的一般途径是修改模块的内部实现
  + 如果一个模块不能被修改，那么它通常被认为是具有固定的行为
+ **关键的解决方案：抽象技术**

## 5.3 LSP: The Liskov Substitution Principle **里氏替换原则**

+ 子类型必须能够替换其基类型
+ 派生类必须能够通过其基类的接口使用，客户端无需了解二者之间的差异

## 5.4 ISP: The Interface Segregation Principle **接口隔离原则**

+ 不能强迫客户端依赖于它们不需要的接口：只提供必需的接口（聚合接口）
+ 客户端不应依赖于它们不需要的方法

## 5.5 DIP: The Dependency Inversion Principle **依赖转置原则**

+ 抽象的模块不应依赖于具体的模块
+ 具体应依赖于抽象

# 6 面向可维护性的设计模式和构造技术

## 6.1 Factory Method 工厂方法模式

一种虚拟构造器。

+ 当 client 不知道要创建哪个具体类的实例，或者不想在 client 代码中指明要具体创建的实例时，用工厂方法。
+ 定义一个用于创建对象的接口，让其子类来决定实例化哪一个类，从而使一个类的实例化延迟到其子类。

## 6.2 Abstract Factory 抽象工厂模式（略）

## 6.3 Proxy 代理模式（略）

## 6.4 Observer 观察者模式（略）

## 6.5 Visitor 访问者模式

### 6.5.1 访问者模式

+ 对特定类型的 object 的特定操作(visit)，在运行时将二者动态绑定到一起，该操作可以灵活更改，无需更改被 visit 的类
+ 本质上：**将数据和作用于数据上的某种/些特定操作分离开来**
+ 为 ADT 预留一个将来可扩展功能的“接入点”，外部实现的功能代码可以在不改变 ADT 本身的情况下通过 delegation 接入 ADT

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206092207694.png" alt="image-20220609220736610" style="zoom: 67%;" />

+ 即：“我”（源 ADT）允许（调用`this.accept()`）“你”（`visitor`）来访问我的数据（在`accept()`方法内委派`visitor.visit()`）——数据源主动允许访问
+ 使得访问方法可以变化
+ **可以为源ADT预留功能**

```java
/* Abstract element interface (visitable) */
public interface ItemElement {
	public int accept(ShoppingCartVisitor visitor); //埋下一个槽
}
/* Concrete element */
public class Book implements ItemElement{
	private double price;
	...
	int accept(ShoppingCartVisitor visitor) {
		visitor.visit(this); //把自己通过这个槽传过去
	}
}
public class Fruit implements ItemElement{
	private double weight;
	...
	int accept(ShoppingCartVisitor visitor) {
		visitor.visit(this); //所有的子类都会实现这个槽
	}
}
/* Abstract visitor interface */
public interface ShoppingCartVisitor {
	int visit(Book book);
	int visit(Fruit fruit);
}
public class ShoppingCartVisitorImpl implements ShoppingCartVisitor { //一种实现
	public int visit(Book book) {
		int cost=0;
		if(book.getPrice() > 50) cost = book.getPrice()-5;
		else cost = book.getPrice();
		System.out.println("Book ISBN::"+book.getIsbnNumber() + " cost ="+cost);
		return cost;
	}
	public int visit(Fruit fruit) {
		int cost = fruit.getPricePerKg()*fruit.getWeight();
		System.out.println(fruit.getName() + " cost = "+cost);
		return cost;
	}
}
/* Client */
public class ShoppingCartClient {
	public static void main(String[] args) {
		ItemElement[] items = new ItemElement[]{new Book(20, "1234"),
            new Book(100, "5678"), new Fruit(10, 2, "Banana"), new Fruit(5, 5, "Apple")};
		int total = calculatePrice(items);
		System.out.println("Total Cost = " + total);
	}
	private static int calculatePrice(ItemElement[] items) {
		ShoppingCartVisitor visitor = new ShoppingCartVisitorImpl();
		int sum=0;
		for(ItemElement item : items)
			sum = sum + item.accept(visitor);
		return sum;
	}
}
```

### 6.5.2 Visitor 与 Iterator

+ Iterator：以遍历的方式访问集合数据而无需暴露其内部表示，**将“遍历”这项功能delegate到外部的iterator对象**。
+ Visitor：**在特定ADT上执行某种特定操作，但该操作不在ADT内部实现，而是delegate到独立的visitor对象**，客户端可**灵活扩展/改变visitor的操作算法**，而不影响 ADT。

### 6.5.3 Strategy 与 Visitor

+ visitor 是**站在外部client的角度**，灵活增加对 ADT 的各种不同操作（哪怕 ADT 没实现该操作）
+ strategy 则是**站在内部ADT的角度**，灵活变化对其内部功能的不同配置。

## 6.6 State 状态模式（略）

## 6.7 Memento 备忘录模式（略）

# 7 语法驱动的构造

以下给出三种最重要的操作：

+ Concatenation 连接：`x ::= y z` $x$ matches $y$ followed by $z$
+ Repetition 重复：`x ::= y*` $x$ matches zero or more $y$
+ Union 选择：`x ::= y | z` $x$ matches either $y$ or $z$

给出以下的代码，写出`URL：http://didit.csail.mit.edu:4949/`的语法解析树：

```java
url ::= 'http://' hostname (':' port)? '/'
hostname ::= word '.' hostname | word '.' word
port ::= [0-9]+
word ::= [a-z]+
```

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091933371.png" alt="image-20220609193325292" style="zoom: 50%;" />

# 8 健壮性和正确性的含义和区别

## 8.1 健壮性

**健壮性**：系统在不正常输入或不正常外部环境下仍能够表现正常的程度

+ 面向健壮性的编程
  + 处理未期望的行为和错误终止
  + 即使终止执行，也要准确/无歧义的向用户展示全面的错误信息
  + 错误信息有助于进行 debug
+ Robustness principle (Postel’s Law)：对自己的代码要保守，对用户的行为要开放

## 8.2 正确性

**正确性**：程序按照 spec 加以执行的能力，是最重要的质量指标

---

健壮性与正确性的区别：

+ 正确性：永不给用户错误的结果
+ 健壮性：尽可能保持软件运行而不是总是退出
+ 正确性倾向于直接报错(error)，健壮性则倾向于容错(fault-tolerance)

# 9 错误与异常处理

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091941162.png" alt="image-20220609194102051" style="zoom:50%;" />

## 9.1 Throwable

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091944180.png" alt="image-20220609194414094" style="zoom:67%;" />

## 9.2 Java中的内部错误（Error） & 异常（Exception）

+ 内部错误：程序员通常无能为力，一旦发生，想办法让程序优雅的结束
  + 用户输入错误
  + 设备错误
  + 物理限制
+ 异常：你自己程序导致的问题，可以捕获、可以处理

> 由于程序员对Error通常无法预料无法解决，因此重点关注可被解决的Exception

## 9.3 异常处理

Java 中 Exception 可以被分为两个部分，蓝色的运行时异常和绿色的其他异常。

### 9.3.1 运行时异常

由程序员在代码里处理不当造成，在源代码中引入了故障，而如果在代码中提前进行验证，这些故障就可以避免。动态类型检查的时候会发现这种异常，而一旦出现，代码就必然有错误，可以通过调试解决。

### 9.3.2 其他异常

由外部原因造成，程序员无法完全控制的外在问题所导致的，即使在代码中提前加以验证，也无法完全避免失效发生。

---

> Java’s exception handling consists of three operations:
> + Declaring exceptions (throws)声明“本方法可能会发生XX异常”
> + Throwing an exception (throw)抛出XX异常
> + Catching an exception (try, catch, finally) 捕获并处理XX异常

## 9.4 Checked & Unchecked Exceptions区别

|                    | Checked exception                                            | Unchecked exception                                         |
| :-: | :-: | :-: |
| Basic              | 必须被**显式地捕获或者传递** (`try-catch-finally-throw`)，否则编译器无法通过,在静态类型检查时就会报错 | 异常可以不必捕获或抛出，编译器不去检查,不会给出任何错误提示 |
| Class of Exception | **继承自`Exception`类**(上图中的绿色部分)                    | 继承自`RuntimeException`类(上图中的蓝色部分)                |
| Handling           | 从异常发生的现场**获取详细的信息**，利用异常返回的信息来明确操作失败的原因，并加以合理的**恢复处理** | **简单打印异常信息，无法再继续处理**                        |
| Appearance         | 代码看起来复杂，**正常逻辑代码和异常处理代码混在一起**       | 清晰，简单                                                  |

选取 checked exception 还是 unchecked exception 可遵循下面的原则：

+ checked exception：如果客户端可以通过其他的方法恢复异常，而对开发者来说错误可预料但不可预防，它的出现已经脱离了程序能够掌控的范围。
+ unchecked exception：如果客户端对出现的这种异常无能为力，而对开发者来说错误可预料可预防，它可以通过调整程序来避免出现。

## 9.5 Checked异常的处理机制

### 9.5.1 自定义异常类

可以选择创建自定义异常类型：

```java
public class FooException extends Exception {
	public FooException() { super(); }
	public FooException(String message) { super(message); }
	public FooException(String message, Throwable cause) { super(message, cause);	}
	public FooException(Throwable cause) { super(cause); }
}
```

### 9.5.2 声明异常 & 抛出异常

使用`throw`关键字抛出异常，如：`throw new EOFException()`；

```java
String readData(Scanner in) throws EOFException // 声明：本函数可能发生该异常
{
	// TO-DO
	while (// TO-DO)
	{
		if (!in.hasNext()) // EOF encountered
		{
			if (n < len)
				throw new EOFException(); // Exception
		}
		// TO-DO
	}
	return s;
}
```

### 9.5.3 捕获异常 & 处理异常

可以使用`try-catch`语法对抛出的异常进行处理，也可以用`throws`语法将异常抛给上一级调用，然后在上一级中使用`try-catch`处理。

```java
public static void fun() throws IOException { // 已声明可能抛出的Exception
    // TO-DO
}
public static void main(String args[]) {
	try{
        fun();
    } catch (IOExeption e) { // 延迟到此处catch
        e.printStackTrace();
    }
}
```

我们可以看到`try-catch`捕获到的异常可能有两个来源：一是自己内部的代码产生的，二是调用了其他的方法，并且该方法未处理抛给了本方法。本来`catch`语句是用于`exception handling`的，但也可以在`catch`里抛出异常，目的是更改`exception`的类型，更方便客户端获取错误信息并处理，如下所示：

```java
try {
	// TO-DO
}
catch (AException e) { // 捕获到A异常
	// 抛出B异常+异常消息
	throw new BException( "error:" + e. getMessage());
}
```

## 9.6 Finally

处理异常时释放资源：当异常抛出时，方法中正常执行的代码被终止，如果异常发生前曾申请过某些资源，那么异常发生后这些资源要被恰当的清理，所以形成了`try-catch-finally`结构。不管程序是否碰到异常，`finally`都会被执行。

## 9.7 LSP & 异常

+ 如果子类型中 override 了父类型中的方法，那么子类型中方法抛出的异常不能比父类型抛出的异常类型更宽泛，**异常不能逆变**
+ 子类型方法可以抛出更具体的异常，也可以不抛出任何异常，**异常可以协变**
+ **如果父类型的方法未抛出异常，那么子类型的方法也不能抛出异常**

目的：让客户端能够用统一的方式处理不同类型的对象。

# 10 断言与防御式编程

## 10.1 防御式编程的基本思想

+ 最好的防御就是不要引入 bug
+ 如果无法避免
  + 尝试着将 bug 限制在最小的范围内
  + 限定在一个方法内部，不扩散
+ Fail fast：尽快失败，就容易发现、越早修复

## 10.2 断言Assertion

### 10.2.1 断言

+ 在**开发阶段**的代码中嵌入，**检验某些“假设”是否成立**。若成立，表明程序运行正常，否则表明存在错误。

+ 断言即是对代码中程序员所做假设的文档化，也不会影响运行时性能(在实际使用时，`assertion`都会被 disabled)

+ 语法：`assert condition : message;`

  所构造`message`在发生错误时显示给用户，便于快速发现错误所在

+ 作用：最高效、快速地找出/改正 bug；提高可维护性

| Assertion        | Exception        |
| :-: | :-: |
| 提高“**正确性**” | 提高“**健壮性**” |
| 错误/异常处理是提高健壮性，处理外部行为；断言是提高正确性，处理内部行为 | 使用异常来处理你“预料到可以发生”的不正常情况；使用断言处理“绝不应该发生”的情况 |
| 内部行为 | 外部行为 |
| 处理“绝不应该发生”的情况 | 处理“可以预料到会发生”的情况 |

### 10.2.2 `assert`使用场景

+ 内部不变量：判断某个局部变量应该满足的条件，`assert x > 0`
+ 表示不变量：`checkRep()`
+ 控制流不变量：例如，若不想让程序走向`switch-case`的某个分支，则可以用断言直接在分支上`assert false;`
+ 方法的前置条件：判断传入参数是否满足前置条件
+ 方法的后置条件：判断结果时候满足后置条件

# 11 代码调试（略）

## 11.1 调试的基本过程和方法

## 11.2 使用日志开展调试

# 12 软件测试与测试优先的编程

+ Unit 单元测试：function、class
+ Integration 集成测试：classes、packages、components、subsystems
+ System 系统测试：system
+ Regression 回归测试：修改后再测试
+ Acceptance 验收测试
+ 静态测试：
  + 不执行程序
  + Reviews
  + walkthroughs 预排/演练/走查
  + inspections 视察
+ 动态测试：
  + 执行程序，有测试用例
  + Debugger

## 12.1 使用 JUnit 进行单元测试（Unit Test）

+ 针对软件最小单元
+ 隔离模块
+ 容易定位错误，容易调试

JUnit 在测试方法前使用`@Test`annotation 来表明这是一个 JUnit 测试方法。如果要在测试开始之前做一些准备则在准备方法前添加`@Before`annotation，如果要在测试结束后做一些收尾工作则在收尾方法前添加`@After`annotation。JUnit 使用的是断言机制来完成测试，常用的有三种测试方法：`assertEquals()`、`assertTrue()`、`assertFalse()`。

## 12.2 黑盒测试

白盒测试是对程序内部代码结构的测试；黑盒测试是对程序外部表现出来的行为的测试：

+ 检查代码功能
+ 不关心内部细节
+ 检查程序是否符合规约
+ 用尽可能少的测试用例尽快运行、尽可能大发现程序错误

## 12.3 等价类划分和边界值分析

### 12.3.1 Equivalence Partitioning 等价类划分

+ **针对每个输入数据需要满足的约束条件，划分等价类**，导出测试用例
+ 每个等价类代表着对输入约束加以“满足/违反”的“有效/无效”数据集合
+ 基于假设：相似的输入会展示相似的行为
  + 因此，每个等价类选一个做代表即可，可以降低测试用例数量

### 12.3.2 Boundary Value Analysis 边界值分析

+ **大量错误出现在输入域的边界而不是中央**
+ 对等价类划分的补充

### 12.3.3 覆盖划分的方法

+ Full Cartesian product：笛卡尔积、全覆盖
  + 测试完备、用例数量多、测试代价高
+ Cover each Part：覆盖每个取值，最少 1 次即可
  + 测试用例少、代价低、测试覆盖度不够高（例子：大整数乘法）
+ 二维输入空间
+ 两个数的正负性：++，±，-+，–
+ 特殊值：0，1，-1
+ 很大的数

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206092109730.png" alt="image-20220609210949603" style="zoom:45%;" />

+ 大于、等于、小于

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206092110639.png" alt="image-20220609211024589" style="zoom:67%;" />

## 12.4 测试覆盖度

Code Coverage 代码覆盖度：已有的测试用例有多大程度覆盖了被测程序 。

+ 代码覆盖度越低，测试越不充分；
+ 代码覆盖度越高，测试代价越高。

测试覆盖种类：

+ Function 函数覆盖
+ Statement 语句覆盖
+ Branch 分支覆盖
  + if、while、switch-case、for
+ Condition 条件覆盖 ≈ 分支覆盖
+ Path 路径覆盖
  + 分支的组合 = 路径

测试效果：路径覆盖 > 分支覆盖 > 语句覆盖
		测试难度：路径覆盖 > 分支覆盖 > 语句覆盖

> 100%语句覆盖是common（正常）目标
> 		100%分支覆盖是desirable（令人满意的），arduous（很难实现），有些行业有更高标准
> 		100%路径覆盖是infeasible（不可实行的）

## 12.5 以注释的形式撰写测试策略

+ 在程序中显式记录测试策略（根据什么来选择测试用例）
+ 在代码评审的过程中，其他人可以理解你的测试，并评判测试是否足够充分