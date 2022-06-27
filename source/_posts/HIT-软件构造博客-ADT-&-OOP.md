---
title: HIT-软件构造博客-ADT & OOP
date: 2022-05-27 14:23:45
description: 详解Java中的抽象数据类型与面向对象编程
tags: HIT-SC
categories: HIT-SC
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206040831945.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# 1 数据类型和类型检查

## 1.1 基本数据类型 & 对象数据类型

|                         基本数据类型                         |                       对象数据类型                        |
| :----------------------------------------------------------: | :-------------------------------------------------------: |
| `int`, `long`, `byte`, `short`, `char`, `float`, `double`, `boolean` | `Classes`, `interfaces`, `arrays`, `enums`, `annotations` |
|              只有值，没有ID (与其他值无法区分)               |                      既有ID，也有值                       |
|                            不可变                            |                        可变/不可变                        |
|                      在**栈**中分配内存                      |                    在**堆**中分配内存                     |
|              Can’t achieve unity of expression               |             Unity of expression with generics             |
|                            代价低                            |                         代价昂贵                          |

## 1.2 静态类型检查 & 动态类型检查

### 1.2.1 静态类型检查

+ 关于类型的检查，不考虑值。在编译阶段发现错误，避免将错误带入运行阶段，提高程序的正确性、健壮性。

+ 静态类型检查错误：语法错误、类名/函数名错误、参数数目错误、参数类型错误、返回值类型错误。

### 1.2.2 动态类型检查

+ 关于“值”的检查，在运行阶段发现错误。

+ 动态类型检查错误：非法的参数值、非法的返回值、越界、空指针。

## 1.3 Mutable可变 & Immutable不可变

+ 不变对象：一旦被创建，其值不能改变；如果是引用类型，也可以是不变的（一旦确定其指向的对象，不能再被改变指向其他对象）

  > 关于`final`：`final`类无法派生子类；`final`变量无法改变值/引用；`final`方法无法被子类重写

+ 可变对象：拥有方法可以修改自己的值/引用
+ `String`：immutable；`StringBuilder`：mutable
+ 我们关心 mutable 与 immutable 的区别，即使它们最终的值都是一样的。当只有一个引用指向该对象 ，二者没有区别；有多个引用的时候，差异就出现了，如下图所示：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091131494.png" alt="image-20220609113114452" style="zoom: 67%;" />

+ mutable 的优点：不可变类型频繁修改会产生大量的临时拷贝，需要垃圾回收；可变类型，最少化拷贝，以提高效率，获得更好的性能，适合在多个模块之间共享数据。
  UnmodifiableCollections：Java 设计有不可变的集合类提供使用
+ immutable 的优点：不可变类型更“安全”，在其他质量指标上表现更好；可变性使得难以理解程序正在做什么，更难满足方法的规约。

## 1.4 值的改变 & 引用的改变

+ 改变一个变量：将该变量指向另一个值的存储空间（引用）
+ 改变一个变量的值：将该变量当前指向的值的存储空间中写入一个新的值

## 1.5 表示泄露和防御式拷贝

+ 通过防御式拷贝，给客户端返回一个全新的对象（副本），客户端即使对数据做了更改，也不会影响到自己。例如：

  ```java
  return new Date(groundhogAnswer.getTime());
  ```

  但大部分时候该拷贝不会被客户端修改，可能造成大量的内存浪费。

+ 如果使用不可变类型，则节省了频繁复制的代价。不可变类型不需要防御式拷贝。

+ 安全地使用可变类型：不会涉及共享的局部变量；只有一个引用。但. 如果有多个引用（别名），使用可变类型就非常不安全。

## 1.6 Snapshot diagram（快照图）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091159453.png" alt="image-20220609115954386" style="zoom: 67%;" />

### 1.6.1 基本类型的值

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091205046.png" alt="image-20220609120524011" style="zoom: 80%;" />

### 1.6.2 对象类型的值

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091205944.png" alt="image-20220609120550900" style="zoom:67%;" />

#### 1.6.2.1 不可变对象（双线圈）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091207212.png" alt="image-20220609120753174" style="zoom:67%;" />

#### 1.6.2.2 可变对象（单线圈）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091208807.png" alt="image-20220609120854768" style="zoom:67%;" />

#### 1.6.2.3 不可变的引用：双线箭头

引用是不可变的，但指向的值却可以是可变的。

#### 1.6.2.4 可变的引用：单线箭头

可变的引用，也可指向不可变的值。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091244292.png" alt="image-20220609124408253" style="zoom:80%;" />

### 1.6.3 复杂数据类型：集合类Snapshot

+ `List`

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091300467.png" alt="image-20220609130004416" style="zoom: 60%;" />

+ `Set`

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091300980.png" alt="image-20220609130030941" style="zoom:80%;" />

+ `Map`

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091300415.png" alt="image-20220609130041342" style="zoom: 50%;" />

+ `MyIterator`

  <img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091258562.png" alt="image-20220609125845504" style="zoom:80%;" />

## 1.7 有用的immutable类型

+ 基本类型及其封装对象类型都是不可变的
+ 包装器得到的结果是不可变的，只能看

# 2 设计规约（Specification）

本部分内容见博客：[HIT - 软件构造博客 - 规约](https://pandalandala.github.io/2022/05/08/HIT-%E8%BD%AF%E4%BB%B6%E6%9E%84%E9%80%A0%E5%8D%9A%E5%AE%A2-%E8%A7%84%E7%BA%A6/)。不再赘述。

内容：Spec 概念、前置条件 & 后置条件、行为等价性、Spec 的写法、Spec 的强度。

# 3 抽象数据类型（ADT）

设计 ADT：规格 Spec–>表示 Rep–>实现 Impl

## 3.1 四类ADT操作

+ Creators
  + 实现：构造函数 constructor 或静态方法（也称 factory method）
+ Producers
  + 需要有“旧对象”
  + `return`新对象
  + eg. `String.concat()`
+ Observers
  + eg. `List`的`.size()`
+ Mutators
  + 改变对象属性
  + 若返回值为`void`，则必然改变了对象内部状态（必然是 mutator）

## 3.2 表示独立性

+ client 使用 ADT 时无需考虑其内部如何实现，ADT**内部**表示的变化**不应影响外部**spec 和客户端。

## 3.3 抽象函数AF & 表示不变量RI

+ 抽象值构成的空间（抽象空间）：客户端看到和使用的值
+ 程序内部用来表示抽象值的空间（表示空间）：程序内部的值

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206091740607.png" alt="image-20220609174050490" style="zoom: 80%;" />

+ Mapping：满射、未必单射（未必双射）

  > ADT开发者关注表示空间R，client关注抽象空间A

+ **抽象函数（AF）**：

  + **R和A之间映射关系的函数**
  + 即如何去解释 R 中的每一个值为 A 中的每一个值。
  + AF : R → A
  + R 中的部分值并非合法的，在 A 中无映射值

+ **表示不变性（RI）**：

  + **某个具体的“表示”是否是“合法的”**
  + 所有表示值的一个子集，包含了所有合法的表示值
  + 一个条件，描述了什么是“合法”的表示值

  > 检查RI：
  > 随时检查RI是否满足
  > **在所有可能改变rep的方法内都要检查**
  > Observer方法可以不用，但建议也要检查，以防止你的“万一”

## 3.4 测试ADT

因为测试相当于 client 使用 ADT，所以它也不能直接访问 ADT 内部的数据域，所以只能调用其他方法去测试被测试的方法。

+ 针对 creator：构造对象之后，用 observer 去观察是否正确
+ 针对 observer：用其他三类方法构造对象，然后调用被测 observer，判断观察结果是否正确
+ 针对 producer：produce 新对象之后，用 observer 判断结果是否正确

## 3.5 以注释的形式撰写AF、RI、 Safety from Rep Exposure

+ 在代码中用注释形式记录 AF 和 RI
  + 精确的记录 RI：rep 中的所有 fields 何为有效
  + 精确记录 AF：如何解释每一个 R 值
+ 表示泄漏的安全声明
+ 给出理由，证明代码并未对外泄露其内部表示——自证清白

# 4 面向对象编程（OOP）

## 4.1 接口（Interface）& 抽象类（Abstract Class）& 具体类（Concrete Class）

+ 接口：定义 ADT

+ 类：实现 ADT

> Concrete class --> Abstract Class --> Interface

### 4.1.1 接口

+ 接口之间可以继承与扩展
+ 一个类可以实现多个接口（从而具备了多个接口中的方法）
+ 一个接口可以有多种实现类

### 4.1.2 抽象类

+ 至少有一个抽象方法
+ 抽象方法 Abstract Method
  + 未被实现
  + 如果某些操作是所有子类型都共有，但彼此有差别，可以在父类型中设计抽象方法，在各子类型中重写

### 4.1.3 具体类

+ 实现所有父类未实现的方法

## 4.2 继承（Inheritance） & 重写（Override）

+ 类 & 类：继承
+ 类 & 接口：实现、扩展

### 4.2.1 Override

重写的函数：完全同样的 signature

+ 实际执行时调用哪个方法，运行时决定
+ 重写的时候，不要改变原方法的本意
+ 运行阶段进行动态检查
+ 父类型中的被重写函数体
  + 不为空：该方法是可以被直接复用的；对某些子类型来说，有特殊性，可重写父类型中的函数，实现自己的特殊要求
  + 为空：其所有子类型都需要这个功能；但各有差异，没有共性，在每个子类中均需要重写

### 4.2.2 Super

+ 重写之后，利用`super()`复用了父类型中函数的功能，还可以对其进行扩展
+ 如果是在构造方法中调用父类的构造方法，则必须在构造方法的第一行调用`super()`

> 严格继承：子类只能添加新方法，无法重写超类中的方法（方法带`final`关键字）

## 4.3 多态（Polymorphism） & 重载（Overload）

### 4.3.1 重载

### 4.3.2 特殊多态：功能重载

+ 方便 client 调用：**client可用不同的参数列表，调用同样的函数**
+ 根据参数列表进行最佳匹配
  + `public void changeSize(int size, String name, float pattern) {}`
  + **重载函数错误情况**
    + `public void changeSize(int length, String pattern, float size) {}`：虽然参数名不同，但类型相同
    + `public boolean changeSize(int size, String name, float pattern) {}`：参数列表必须不同
  + 在**编译阶段**时决定要具体执行哪个方法（与之相反，overridden methods 则是在 run-time 进行 dynamic checking）
  + 可以在同一个类内重载，也可在子类中重载
+ 参数化多态：使用泛型`?`编程
+ 子类型多态：期望不同类型的对象可以统一处理而无需区分，遵循 LSP 原则

# 5 ADT和OOP中的等价性

## 5.1 不可变对象的引用等价性 & 对象等价性

+ `==`：引用等价性；相同内存地址；对于基本数据类型
+ `equals()`：对象等价性；对于对象类型
+ 在自定义 ADT 时，需要用`@Override`重写`Object.equals()`（在 Object 中实现的**缺省equals()是在判断引用等价性**）
+ 如果用`==`，是在判断两个对象身份标识 ID 是否相等（指向内存里的同一段空间）

## 5.2 `equals()` & `hashCode()`

### 5.2.1 `equals()`

`equals()`的性质：自反、传递、对称、一致性

+ `equals()`重写范例
  1. 判断引用等价性
  2. 判断类的一致性
  3. 判断具体值是否满足等价条件（自定义）
+ `instanceof`：
  + 判断类
  + 仅在 equals 里使用

### 5.2.2 `hashCode()`

+ **等价的对象必须有相同的`hashCode`**
+ 不相等的对象，也可以映射为同样的`hashCode`，**但性能会变差**
+ 自定义 ADT 要重写 hashcode
+ 返回值是内存地址

## 5.3 可变对象的观察等价性 & 行为等价性

+ 观察等价性： 在不改变状态的情况下，两个 mutable 对象是否看起来一致
+ 行为等价性：调用对象的任何方法都展示出一致的结果

> 对可变类型来说，往往倾向于实现严格的观察等价性， 但在有些时候，观察等价性可能导致bug，甚至可能破坏RI。