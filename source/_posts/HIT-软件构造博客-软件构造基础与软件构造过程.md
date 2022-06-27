---

title: HIT-软件构造博客-软件构造基础与软件构造过程
date: 2022-05-18 12:34:42
description: 从软件构造的多维视图、各阶段划分、内外部质量指标谈起
tags: HIT-SC
categories: HIT-SC
cover: https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/img/202206040831946.png
password: 
---
{% note info flat %}
文章可能有不完善之处，详见[这里](https://pandalandala.github.io/2022/06/06/TO-DO-LIST/)；如在阅读过程中遇到其他问题或 bug，或对 blog 有更多的意见或建议，欢迎[在这里提issue](https://github.com/pandalandala/pandalandala.github.io/issues)或点击下方链接发送邮件！[![Mail](https://img.shields.io/badge/Email-zxrshawn@icloud.com-blue?style=flat&logo=mail.ru)](mailto:zxrshawn@icloud.com)
{% endnote %}

{% note warning flat %}文章图片设置为 lazyload（延迟加载）；如遇图片加载失败请尝试刷新当前网页或科学上网。
{% endnote %}

# 1 软件构造的多维度视图

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206081921951.png" alt="image-20220608192158862" style="zoom: 67%;" />

我们在第 2 节中将对此图进行详细介绍。

# 2 软件构造的阶段划分、各阶段的构造活动

## 2.1 构造阶段：Build-Time Views

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206081923473.png" alt="image-20220608192351405" style="zoom:67%;" />

+ Code-level view: 代码的逻辑组织：functions, classes, methods, interfaces
+ Component-level view: 代码的物理组织：files, directories, packages, libraries
+ Moment view: 特定时刻的软件形态
+ Period view: 软件形态随时间变化

以下是我们课程中需要关注的地方：

![image-20220608202603138](https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082026209.png)

### 2.1.1 Build-time, moment, and code-level view

+ 源代码
+ 函数、类、方法、接口
+ 三个相关层面
  + **词汇**：使用的语句、字符串、变量、注释（半结构化）
  + **语法**：语法树、流程图（彻底结构化）
  + **语义**：源代码实现的目标 & 组成部分联系情况

### 2.1.2 Build-time, period, and code-level view

+ 记录 Code Churn
+ 学会使用版本控制工具

### 2.1.3 Build-time, moment, and component-level view

+ 模块化组织为文件、目录
+ 文件被压缩为`package`和`library`
+ 与库文件链接。开发者像使用编程语言指令一样使用库中的功能。编程时和 build 时，需告诉`IDE`和`JVM`在哪里寻找某些库。
  + 静态链接：发生在构造阶段；复制；不依赖；缺点：难以升级
  + 动态链接：不会加入可执行文件；做标记；运行时根据标记装载库至内存；发布软件时，记得将程序所有依赖的动态库都复制给用户；优点：易于升级

### 2.1.4 Build-time, period, and component-level view

+ 如何在不同版本间变化
+ Software Configuration Item (SCI) ：配置项

## 2.2 运行阶段：Run-Time View

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082018752.png" alt="image-20220608201846678" style="zoom:67%;" />

+ Code-level view:  代码层面：逻辑实体在内存中的呈现
+ Component-level view: 构件层面：物理实体在物理硬件环境中的呈现
+ Moment view: 逻辑/物理实体在内存/硬件环境中特定时刻的形态
+ Period view: 逻辑/物理实体在内存/ 硬件环境中的形态随时间变化

还要注意此视图下的可执行程序、原生机器码、程序完全解释执行、库文件、分布式程序等。

### 2.2.1  Run-time, moment, and code-level view

+ Code snapshot：代码快照图
+ 运行时程序变量层面状态
+ Memory dump 内存信息转储
+ 查看内存使用情况
+ 宏观：任务管理器

### 2.2.2 Run-time, period and code-level view

+ UML 类图
+ **Execution tracing 执行跟踪**
+ 用日志方式记录程序执行的调用次序

### 2.2.3 Run-time, moment, and component-level view

+ UML 中的部署图

### 2.2.4 Run-time, period, and component-level view

+ 事件日志：系统层面

# 3 内部/外部的质量指标

这一节我们介绍内部与外部的质量指标。内部质量因素影响软件本身和它的开发者；外部质量因素影响用户；外部质量取决于内部质量

## 3.1 外部质量因素

### 3.1.1 正确性（Correctness）

**正确性是最重要的质量指标**。我们有以下几种手段保证正确性：

+ 测试和调试：发现不正确、消除不正确
+ 防御式编程：在写程序的时候就确保正确性
+ 形式化方法：通过形式化验证发现问题

### 3.1.2 鲁棒性（Robustness）

+ 健壮性是针对异常情况的处理， 是对正确性的补充
+ 出现异常时程序不能崩溃
+ 异常取决于 spec 的范畴

### 3.1.3 易扩展性（Extendibility）

+ 易于调整且适应变化，且软件是易变的
+  scale 规模越大，扩展 spec 越不容易

### 3.1.4 复用性（Reusability）

+ 利用已有的复用性好的程序，开发成本少；一次开发，多 次使用
+ 利用代码间的共性与相似的模式

### 3.1.5 兼容性（Compatibility）

+ 不同的软件系统之间可以容易地集成和融合
+ 难点：不同软件有不同的设定/规定，是集成的难点
+ 保持设计的同构性

### 3.1.6 效率（Efficiency）

+ 要先保证正确性，再保证性能
+ 对性能的关注要与其他质量属性进行折中
+ 过度的优化将导致软件不再适应变化和复用
+ **过早优化是万恶之源**

### 3.1.7 可移植性（Portability）

+ 软件可方便的在不同的技术环境之间移植
+ 对不同的硬件操作系统也能应对自如

### 3.1.8 易用性（Ease of use）

+ 要让用户容易学习、安装、操作、监控
+ 给用户提供详细的指南

### 3.1.9 功能性（Functionality）

+ 要注意不能过度追求太多功能：程序设计中一种不适宜的趋 势，即软件开发者增加越来越多的功能，企图跟上竞争，其结果是程 序极为复杂、不灵活、占用过多的磁盘空间

### 3.1.10 时效性（Timeliness）（略）

## 3.2 内部质量因素

可读性、易理解性、清晰、复杂度、大小……

## 3.3 权衡各质量因素

正确的软件开发过程中，开发者应该将不同质量因素之间如何做出折中的设 计决策和标准明确的写下来。虽然需要折中，但正确性绝不能与其他质量因素折中。

# 4 软件配置管理SCM与版本控制系统VCS

## 4.1 软件配置管理：SCM

+ 追踪和控制软件的变化
+ 核心：版本控制和基线的确立
+ 软件配置项 SCI：软件中发生变化的基本单元（例如文件）

## 4.2 版本控制系统：VCS

+  版本：为软件的任一特定时刻的形态指 派一个唯一的编号，作为“身份标识”

+ 为什么需要 VCS： 回滚到上一个版本；比较两个版本的差异；备份软件版本历史；获取备份；合并

+ 本地版本控制系统：仓库存储于开发者本地机器，无法共享和合作
+ 集中式版本控制系统：仓库存储于独立的服务器，支持多开发者之间的协作
+ 分布式版本控制系统：仓库存储于：独立的服务器 + 每个开发者的本地机器

# 5 Git

## 5.1 基本指令

+ 取得项目的 Git 仓库：
  + 在工作目录中初始化新仓库：`git init`后`git add`
  + 从现有仓库克隆： `git clone [url]` 

+ 添加文件：`git add .`
+ 检查当前文件状态：`git status`
+ 查看已暂存的更新：`git diff --cached`；未暂存的更新：`git diff`
+ 提交文件：`git commit -m "..."`
+ 跳过使用暂存区域：`git commit -a -m "..."`
+ 移除文件：`git rm`
+ 对远程仓库的操作：
  + `git remote`：获取当前配置的所有远程仓库
  + `git remote add [shortname] [url]`：添加一个远程仓库
  + `git fetch`：从远程仓库抓取数据到本地
  + `git pull`： 从一个仓库或者本地的分支拉取并且整合代码
  + `git push [remote-name] [branch-name]`：将本地仓库中的数据推送到远程仓库
  + `git remote show [remote-name]`：查看某个远程仓库的详细信息
  + `git remote rm`：从本地移除远程仓库

+ push 到远程仓库：`git push origin master`
+ 从远程仓库 pull：`git pull origin master`

### 5.1.1 管理变化

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082203477.png" alt="image-20220608220349396" style="zoom:67%;" />

### 5.1.2 分支Branch和合并Merge

+ 新建分支：`git checkout -b branch_name`
+ 切换分支：`git checkout branch_name or git checkout master`
+ 选择一个分支与当前分支合并：`git merge branch_name2`（之前已有指令`git checkout branch_name1`）

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082207241.png" alt="image-20220608220740154" style="zoom: 50%;" />

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082208878.png" alt="img" style="zoom: 57%;" />

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082208103.png" alt="image-20220608220840027" style="zoom: 50%;" />

## 5.2 工作原理和结构

### 5.2.1 Object Graph

+ 版本之间的演化关系图
+ A->B：在版本 B 的基础上作出变化，形成了版本 A

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082211593.png" alt="image-20220608221104533" style="zoom: 50%;" />

### 5.2.2 Commit

+ 每个 commit 指向一个父亲
+ 分支：多个 commit 指向一个父亲
+ 合并：一个 commit 指向两个父亲

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082212018.png" alt="image-20220608221222943" style="zoom: 67%;" />

+ 管理变化：Git 存储发生变化的文件（而非代码行），不变化的文件不重复存储

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082212747.png" alt="image-20220608221248704" style="zoom: 80%;" />

+ Commits: nodes in Object Graph

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082214251.png" alt="image-20220608221449124" style="zoom: 50%;" />

# 6 GitHub

<img src="https://cdn.jsdelivr.net/gh/pandalandala/imgbed@main/202206/202206082216017.png" alt="image-20220608221612913" style="zoom: 67%;" />

# 7 软件构造的一般过程

## 7.1 编程

+  从用途上划分：编程语言、建模语言、配置语言、构建语言
+ 从形态上划分：基于语言学的构造语言、基于数学的形式化构造语言、基于图形的可视化构造语言

## 7.2 审查/静态代码分析（略）

## 7.3 动态代码分析

+ 动态分析：要执行程序并观察现 象、收集数据、分析不足
+ 利用测试度量技术（如覆盖率）确保 代码的可能功能均被充分测试到
+ 用来测量程序的时空复杂度

## 7.4 Debug与测试

+ 调试是识别错误的根本原因并对其进行纠正的过程
+ 测试和调试不会提升软 件质量，而是发现和解决缺陷的主要手段

## 7.5 重构

+ 重构：在不改变功能的前提下优化代码