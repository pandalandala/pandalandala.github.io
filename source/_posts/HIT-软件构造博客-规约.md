---
title: HIT-软件构造博客-规约
date: 2022-05-08 09:45:32
description: HIT软件构造实验中对规约(spec)编写的引申
tags: HIT-SC
categories: HIT-SC
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206040831947.png
password: 
---

{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# 1 规约（specification）

规约是软件构造中常用的手段。程序员在编写代码设计 ADT 时应该对自己的方法进行某些约束，形成一种规范，明确指出方法应该与不应该进行的操作。在 ADT 设计完成之后编写测试的时候，也需要参照规约来设计测试，以对前面的代码进行完善的检查。在项目提交之后，用户在调用 API 等场景下也会参照写好的规约，从而大大节省时间并保证代码的正确性。规约好像一堵墙上的一排洞，程序员与用户站在墙的两侧，虽然无法看清对方所处场景的全貌，但却可以通过这一排洞进行必要的交流。这样的现象会导致**解耦（decoupling）**，即在规约之下，“各人自扫门前雪，休管他人瓦上霜”，双方都无须过多关注对方的代码，可以自行在规约之下改动自己的代码。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206071452428.png" alt="image-20220607145259328" style="zoom: 67%;" />

# 2 规约的作用

如 1.1 节中提到的，我们可以总结出：规约可以同时保证工程的效率和质量。除此之外，规约还有助于在工程中快速找到 bug 发生的源头，进而明确代码以及相应 bug 的责任方。除此之外，用户无需过多了解 API 另一端的代码，只需要阅读 spec 即可。

# 3 规约的结构：前置条件与后置条件

下面给出一个基本结构：

```Java
/**
     * TO-DO Some Explanations
     * @param
     * @param 
     * @param 
     * @param 
     * @return 
     * @throws 
     */
```

+ **前置条件**：对用户端的约束，使用方法时必须满足的条件。前置条件不仅限制参数，还限制了参数间的相互作用；在`param`处填写。
+ **后置条件**：对开发者的约束，方法结束时必须满足的条件。这一部分规定了可以静态检查的部分、异常检查在何时抛出、对象是否为`mutable`、返回值与输入的关系以及返回值类型等；在`param`处填写。
+ **契约**：前置条件如果满足，则后置条件也一定被满足；前置条件不满足，则后置条件也无须被满足，进而可能导致程序终止、返回不受控制的结果或抛出异常等。

下面是一个实际的例子，来源于[MIT 6.031: Software Construction Spring 2020 Problem Set 0: Turtle Graphics](http://web.mit.edu/6.031/www/sp20/psets/ps0/)：

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206071532186.png" alt="image-20220607153208092" style="zoom: 50%;" />

另外，非常显然地可以理解如下的这一点：规约中不应该约束代码实现细节、局部变量、方法类的私有域等。

本节最后我们回顾一下**行为等价性**。简单来说就是两个函数在具体的实现上也许不同，但都符合同一个规约，也就是说他们可以相互替换。这就是行为等价性。

# 4 规约的设计

## 4.1 调整规约强度

我们有时候希望调整规约的强度。现在假设我们已经有规约`Spec1`，并希望用更强的规约`Spec2`来替换`Spec1`。注意这样的替换是有条件的：

1. `Spec2`的前置条件不强于`Spec1`
2. 当满足`Spec1`前置条件时，`Spec2`的后置条件不能弱于`Spec1`

其中第一点似乎有些难以理解。事实上，`Spec2`的前置条件弱一些可以让用户有更少的限制，实质上是**对开发者提出了更多要求**；而`Spec1`的前置条件更强意味着开发者要满足更多的限制条件。

我们看一个 PPT 中的例子。

```Java
/** Original spec
     * static int findExactlyOne(int[] a, int val)
     * @param val occurs exactly once in a
     * @param returns index i such that a[i] = val
     */
```

```Java
/** A stronger spec 弱化前置条件
     * static int findOneOrMore,AnyIndex(int[] a, int val)
     * @param val occurs at least once in a
     * @param returns index i such that a[i] = val
     */
```

```Java
/** A much stronger spec 强化后置条件
     * static int findOneOrMore,FirstIndex(int[] a, int val)
     * @param val occurs at least once in a
     * @param returns lowest index i such that a[i] = val
     */
```

但注意下面的这个规约，我们无法比较它与`findOneOrMore`的强弱，因为它的前置条件与后置条件都较弱：

```Java
/**
     * static int findCanBeMissing(int[] a, int val)
     * @param nothing
     * @param returns index i such that a[i] = val, or -1 if no such i
     */
```

## 4.2 将规约图示化

我们来考虑将规约用图示的方式表示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206072102258.png" alt="image-20220607210246208" style="zoom:67%;" />

可以看到上图中`findFirst`和`findLast`都在圈中。一个规约会在一个集合中限定一定的范围，范围之内的方法都是满足规约的，范围之外的都或多或少地有不满足规约的地方。我们在 1.4.1 节中知道，为了加强一个规约，我们可以弱化前置条件或加强后置条件。加强后置条件意味着之前的一些方法可能并不在新的规约范围之内了；弱化前置条件也要满足更多的要求，之前在规约之内的方法可能会被排除在外。这样的现象都对应着**规约集合范围的缩小**，如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206072108481.png" alt="image-20220607210854438" style="zoom: 60%;" />

对于 1.4.1 节中无法比较强弱的两个规约，我们在这里依然有相同的结论，如下图所示。

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206072109361.png" alt="image-20220607210955319" style="zoom:80%;" />

## 4.3 设计规约的基本原则

1. 规约应具有**内聚性（coherent）**。我们看一个例子：

   ```java
   /**
        * static int sumFind(int[] a, int[] b, int val)
        * @param returns index i such that a[i] = val, or -1 if no such i
        * @returns the sum of all indices in arrays a and b at which val appears
        */
   ```

   这并不是一个好的规约设计的例子，因为它在两个数组里面查找并相加下标，显得这个过程过于复杂和奇怪。如果我们分成两个方法来写各自的规约，分别完成查找操作和运算操作，不仅会提高代码的可复用性，而且也会让人更便于理解我们正在做的事。

2. 规约应是**信息丰富的（informative）**。

   ```java
   /**
        * static V put(Map<K,V> map, K key, V val)
        * @param val may be null, and map may contain null values
        * @param inserts (key, val) into the mapping, overriding any existing mapping for key, and returns old value for key, unless none, in which case it returns null
        */
   ```

   可以看到在前置条件中并没有规定`key`的对应值不能是`null`，但后置条件中`null`被用作一个返回的条件，这让用户无法判断`key`究竟是不存在还是对应值是`null`。这样的情况我们就说它并不是信息丰富的。

3. 规约（的后置条件）应**足够强**。对于错误的输入直接抛出异常，甚至允许用户任意改变是不良好的。我们直接看下面的例子，如果抛出了异常`NullPointerException`，开发者就不容易知道`list2`中导致异常的源头，并且对于用户可能对`list1`进行的更改无从得知：

   ```java
   /**
        * static void addAll(List<T> list1, List<T> list2)
        * @param adds the elements of list2 to list1, unless it encounters a null element, at which point it throws a NullPointerException
        */
   ```

4. 规约（的前置条件）应**足够弱**。

   ```java
   /**
        * static File open(String filename)
        * @param opens a file named filename
        */
   ```

   这一规约希望打开一个文件，但我们对于此还有很多细节不够清楚，我们说它前置条件过强，增加了开发者实现的难度。

5. 使用**抽象数据类型**。

   ```java
   /**
        * static ArrayList<T> reverse(ArrayList<T> list)
        * @param returns a new list which is the reversal of list, i.e. newList[i] = list[n-i-1] for all 0 ≤ i < n, where n = list.size()
        */
   ```

   抽象数据类型会让大家都更自如地进行开发或实用，例如我们这时更希望看到`List`而不是`ArrayList`，以及`HashSet`而不是`Set`。我们看到上述代码传入传出的都必须是`ArrayList`，但我们看条件中并没有用到某些`ArrayList`特有的特性。那么为什么不写成更抽象的数据类型`List`呢？

6. 权衡**是否使用前置条件**。

   用户不会喜欢太强的前置条件，因此我们需要考虑检查参数的代价。另外我们需要考虑方法是否是私有方法，如果答案是肯定的话我们当然可以进行检查；若不然，是可能被其他开发者使用的公有方法，则规约不宜有太多前置条件。

# 5 测试

我们简单回顾一下**黑盒测试**。黑盒测试顾名思义，是指仅以规约为依赖项的测试。我们还是看一个 PPT 中的例子：

```java
/**
     * static int find(int[] arr, int val)
     * @param val occurs in arr
     * @param returns index i such that arr[i] = val
     */
```

这一规约给出了前置条件：`val`必须在`arr`中；但后置条件却很弱：当`arr`中有多个`val`，我们不知道会返回哪一个。我们看下面的代码便可以知道不好的测试是怎样的，好的测试是怎样的：

```java
int[] array = new int[] { 7, 7, 7 };
assertEquals(0, find(array, 7));  // bad test case: violates the spec
assertEquals(7, array[find(array, 7)]);  // correct
```

# 6 Alibaba的Java开发手册

仅作阅读材料，可以给我们日常的代码编写以灵感，值得一看。

> 1. 【强制】存储方案和底层数据结构的设计获得评审一致通过，并沉淀成为文档。
>
>    说明：有缺陷的底层数据结构容易导致系统风险上升，可扩展性下降，重构成本也会因历史数据迁移和系统平滑过渡而陡然增加，所以，存储方案和数据结构需要认真地进行设计和评审，生产环境提交执行后，需要进行 double check。
>
>    正例：评审内容包括存储介质选型、表结构设计能否满足技术方案、存取性能和存储空间能否满足业务发展、表或字段之间的辩证关系、字段名称、字段类型、索引等；数据结构变更（如在原有表中新增字段）也需要进行评审通过后上线。
>
> 2. 【强制】在需求分析阶段，如果与系统交互的 User 超过一类并且相关的 User Case 超过 5 个，
>    使用用例图来表达更加清晰的结构化需求。
>
> 3. 【强制】如果某个业务对象的状态超过 3 个，使用状态图来表达并且明确状态变化的各个触发条件。
>
>    说明：状态图的核心是对象状态，首先明确对象有多少种状态，然后明确两两状态之间是否存
>    在直接转换关系，再明确触发状态转换的条件是什么。
>
>    正例：淘宝订单状态有已下单、待付款、已付款、待发货、已发货、已收货等。比如已下单与已收货这两种状态之间是不可能有直接转换关系的。
>
> 4. 【强制】如果系统中某个功能的调用链路上的涉及对象超过 3 个，使用时序图来表达并且明确各调用环节的输入与输出。
>
>    说明：时序图反映了一系列对象间的交互与协作关系，清晰立体地反映系统的调用纵深链路。
>
> 5. 【强制】如果系统中模型类超过 5 个，并且存在复杂的依赖关系，使用类图来表达并且明确类之间的关系。
>
>    说明：类图像建筑领域的施工图，如果搭平房，可能不需要，但如果建造蚂蚁 Z 空间大楼，肯定需要详细的施工图。
>
> 6. 【强制】如果系统中超过 2 个对象之间存在协作关系，并且需要表示复杂的处理流程，使用活动图来表示。
>
>    说明：活动图是流程图的扩展，增加了能够体现协作关系的对象泳道，支持表示并发等。
>
> 7. 【推荐】需求分析与系统设计在考虑主干功能的同时，需要充分评估异常流程与业务边界。
>
>    反例：用户在淘宝付款过程中，银行扣款成功，发送给用户扣款成功短信，但是支付宝入款时由于断网演练产生异常，淘宝订单页面依然显示未付款，导致用户投诉。
>
> 8. 【推荐】类在设计与实现时要符合单一原则。
>    说明：单一原则最易理解却是最难实现的一条规则，随着系统演进，很多时候，忘记了类设计的初衷。
>
> 9. 【推荐】谨慎使用继承的方式来进行扩展，优先使用聚合/组合的方式来实现。
>
>    说明：不得已使用继承的话，必须符合里氏代换原则，此原则说父类能够出现的地方子类一定能够出现，比如，“把钱交出来”，钱的子类美元、欧元、人民币等都可以出现。
>
> 10. 【推荐】系统设计时，根据依赖倒置原则，尽量依赖抽象类与接口，有利于扩展与维护。
>
>     说明：低层次模块依赖于高层次模块的抽象，方便系统间的解耦。
>
> 11. 【推荐】系统设计时，注意对扩展开放，对修改闭合。
>
>     说明：极端情况下，交付的代码都是不可修改的，同一业务域内的需求变化，通过模块或类的扩展来实现。
>
> 12. 【推荐】系统设计阶段，共性业务或公共行为抽取出来公共模块、公共配置、公共类、公共方法等，避免出现重复代码或重复配置的情况。
>
>     说明：随着代码的重复次数不断增加，维护成本指数级上升。
>
> 13. 【推荐】避免如下误解：敏捷开发 = 讲故事 + 编码 + 发布。
>
>     说明：敏捷开发是快速交付迭代可用的系统，省略多余的设计方案，摒弃传统的审批流程，但核心关键点上的必要设计和文档沉淀是需要的。
>
>     反例：某团队为了业务快速发展，敏捷成了产品经理催进度的借口，系统中均是勉强能运行但像面条一样的代码，可维护性和可扩展性极差，一年之后，不得不进行大规模重构，得不偿失。
>
> 14. 【参考】系统设计主要目的是明确需求、理顺逻辑、后期维护，次要目的用于指导编码。
>
>     说明：避免为了设计而设计，系统设计文档有助于后期的系统维护，所以设计结果需要进行分类归档保存。
>
> 15. 【参考】设计的本质就是识别和表达系统难点，找到系统的变化点，并隔离变化点。
>
>     说明：世间众多设计模式目的是相同的，即隔离系统变化点。
>
> 16. 【参考】系统架构设计的目的：
>
>     + 确定系统边界。确定系统在技术层面上的做与不做。
>     +  确定系统内模块之间的关系。确定模块之间的依赖关系及模块的宏观输入与输出。
>     + 确定指导后续设计与演化的原则。使后续的子系统或模块设计在规定的框架内继续演化。
>     + 确定非功能性需求。非功能性需求是指安全性、可用性、可扩展性等。
