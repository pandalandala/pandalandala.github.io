---
title: HIT-软件构造博客-Java中的functional programming
date: 2022-04-29 11:20:42
description: 由Java中的functional programming谈起
tags: HIT-SC
categories: HIT-SC
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202205311419170.png
password: 
---
{% note info flat %}文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com){% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# 1 函数式编程

尽可能多地了解 Java 中的函数式编程特性有助于我们更好地完成一个软件、体系或项目的开发。

从 Java 8 开始，Java 在原有的面向对象编程、命令式编程（C、C++、Javascript…）、声明式编程（SQL、html、css…）等编程范式上新增了函数式编程的支持，将行为参数化并理解为一个具体的函数或方法，将函数也作为一个可以向其他参数传递的函数。函数式编程的语言还有早期的 Scala、python、C#、js(ES6)等，当然也少不了 Haskell——Haskell 会逼迫我们只能用纯函数式特性来解决问题。函数式编程更关心**数据的映射**，命令式编程更关心**解决问题的步骤**。

函数式编程的优点：

+ 代码简洁，逻辑清晰
+ 保证线程安全，内部的 API 屏蔽了对多线程的关注（这里要多解释一句，由于多个线程之间状态不共享，不会造成资源冲突，更不会有死锁等问题，因而从根源上便于并发）
+ 复用性高

函数式编程的缺点：

+ 和汉语和英语语法的理解方式差异较大，并且不便于调试
+ 函数内数据 immutable 可能占用资源

下面先看一个函数式编程的例子，例如创建一个 Runnable 的匿名类：

```Java
Runnable runnable = new Runnable() {
    @Override
    public void run() {
        System.out.println("Welcome to my blog!");
    }
};
```

事实上我们一直在重复一些东西，但又说不上来具体是什么。我们再来看另一个写法：

```Java
Runnable runnable = () -> System.out.println("Welcome to my blog!");
```

这样是不是感觉更简洁了？

Java 8 为函数式编程的引入做了许多准备工作，例如函数式接口、静态方法、默认实现（被`default`修饰的方法）等。Java 中的函数式编程可以被概括为：**$\lambda$ 表达式 + 方法引用 + stream API = Java 函数式编程**。

# 2 函数式接口

函数式接口中的抽象方法最多只能有一个，通常标注为`@FunctionInterface`；但可以有多个非抽象方法。常用的函数式接口存放在`java.util.function`中，包括`Function`、`Supplier`、`Consumer`等。

# 3  $\lambda$ 表达式

$\lambda$表达式是一种匿名函数，其实质还是函数式接口的匿名实现类；没有名称，只有参数列表、函数主体、返回类型等。我们在写一些匿名的内部类时编译器会提示某处可转换为 $\lambda$ 表达式。

```java
//无参无返回值
Runnable noArgsNoRet = () -> System.out.println("Hello Lambda");

//有参无返回值
Consumer<String> oneArgsNoRet = str -> System.out.println(str);

//无参有方法体
Supplier<String> noArgsHasRet = () -> {
    String str = "a" + "b";
    return str;
};

//有两个参数有返回值
BinaryOperator<Integer> add = (x, y) -> x + y;

//注明类型的参数
Consumer<String> oneArgs = (String str) -> System.out.println(str);
```

 $\lambda$ 表达式主要的作用是实例化某些函数式接口、替换匿名类等，并且不需要声明参数和返回类型。如 1.1 中所说，仅当接口中只有一个抽象方法时，才可以使用$\lambda$表达式。我们接着看上面的代码，似乎是右边的函数给左边的变量赋值。但 Java 是 OOP 的，变量只会被赋值为基本类型或对象，因此函数不可能被赋值为变量。因此 Java 只是将函数传递给了抽象接口的方法，让抽象接口的方法以该函数来实现。这就是**对行为抽象**。

进一步地，纯函数式编程中的变量并不像命令式编程中的变量一样，前者的值是不可变（immutable）的；真正的纯函数式编程不该使用可变变量以及其他命令式的控制结构等。从理论上来讲函数式编程语言是通过具有**图灵完全**性质的**$\lambda$ 演算**完成的，不过大多数情况下还是被编译成冯·诺依曼机的机器语言指令来执行。

# 4 静态方法

1.2 节中我们提到了<u>对行为抽象</u>这一概念。事实上，静态方法这一概念诞生的目的便是出于编写类库的需要，对行为进行抽象，但接口内的静态方法却不能被继承。Btw，方法引用可以使用两个冒号来实现，例如`System.out::println`、`Cat::meowmeow`。

# 5 Stream API

**Stream API** 是 Java 8 中新加入的 API，可用于处理集合操作等，也是函数式编程的精髓。我们可以将其理解为生产产品的流水线，Stream API 正是那样地有条理。Stream 一般由三部分构成：

1. 数据源：获取 Stream，如`list.stream()`。集合中可以使用`Collection.stream`、`parallelStream`等；数组的话没有自身的 API，一般借助`Arrays.stream`；此外还有数字 Stream 和自行创建。
2. 中间处理：分为有状态操作和无状态操作；对 Stream 元素进行处理，如`filter`、`sorted`、`map`等。
3. 终端处理：分为短路操作和非短路操作；生成结果。短路操作顾名思义了，有点像我们熟知的短路运算。
