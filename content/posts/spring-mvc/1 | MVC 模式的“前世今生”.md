---
weight: 1
title: "Spring MVC 系列之 MVC 模式的“前世今生”"
date: 2020-03-05T16:30:05+08:00
lastmod: 2020-03-05T16:30:05+08:00
draft: false
author: "AlanYin"
resources:
- name: "tmp"
  src: "/tmp.jpg"

tags: ["content", "Markdown"]
categories: ["documentation"]

lightgallery: true

toc:
  auto: false
math:
enable: true
---

我们可能经常听到“**架构模式**”（architectural pattern）这个词，这到底是什么意思？其实所谓的架构模式，就是设计一个程序结构的学问，属于编程方法论的范畴。

这么说有些抽象，我们今天讨论的 MVC 就是一种架构模式，接下来，在正式介绍 Spring MVC 之前先有个直观的认识，我们一起来了解一下 MVC 模式和其发展历史，毕竟站在更高的角度可以帮助我们更好地了解它的整体设计的缘由。

## 什么是 MVC ?

MVC 是 Mode(模型)、View(视图)、Controller(控制) 三个单词的缩写，它们的作用大致如下：

|    组成    |                             作用                             |
| :--------: | :----------------------------------------------------------: |
|    View    | 最上层，即面向终端用户的视图层。用于给用户提供展示和操作的页面。 |
| Controller | 中间层，负责根据视图层的输入，选择对应的“数据层”数据，对其进行操作，产生最终数据。 |
|    Mode    |        最底层，即核心的“数据层”，程序需要操作的数据。        |

这三层相互独立又是紧密联系，每一层内部的变化不影响其他层，很好地体现了软件设计中“**解耦**”的思想。其中每一层都对外提供接口（Interface），供上面一层调用。通过这种优雅的设计，实现了模块化，修改视图展示或者变更数据都不用修改其他层，极大地方便了维护和升级。

> 为了方便理解，我们用一个简易计算器为例进行类比。在计算器中，外部的那些按钮和最上面的显示条，相当于"视图层"，那些需要运算的数字就是"数据层"，执行加减乘除的运算步骤相当于"控制层"。每一层执行不同的功能，整个结构清楚明了。

## MVC 波澜壮阔的“前世今生”

说到 MVC 模式，其实最早是由 Trygve Reenskaug 在1978年提出的一种软件架构，其目的是实现一种动态的程序设计，简化后续对程序的修改和扩展，使得程序实现部分复用成为可能，同时程序结构更加直观。

> [idea] 可见，程序的可复用性和可扩展性一直以来都是历代优秀程序员们对于代码的“追求”。

## 时代1：Model1 模式的出现，让“史前”的混沌世界出现黎明前的曙光

Model1 模式其实十分简单，它使用 JSP 页面和 JavaBean 相结合的方式。 JSP 页面负责接收客户端请求， JavaBean 负责业务逻辑处理、数据库操作和返回页面。

![Minion](/spring-mvc/images/86ecef19-4eac-46c6-bf57-fc185958bbb6.png)

<img src="/spring-mvc/images/86ecef19-4eac-46c6-bf57-fc185958bbb6.png" alt="86ecef19-4eac-46c6-bf57-fc185958bbb6" style="zoom:67%;" />

##### 那为什么 Model1 后来从江湖上“销声匿迹”了呢？

Model1 架构简单，适合小项目开发。然而，JSP 的职责不单一，职责过重，不方便维护，这也是为什么诞生后逐渐“退隐江湖”。

> [idea]这个架构设计违背了软件设计的**“职责单一”**原则。

## 时代2：Model2（MVC）模式出现，刀耕火种的原始时代迈入了石器时代

上面我们提到，Model1 虽然实现了一定程度的解耦，但 JSP 页面既要负责页面控制，又要负责逻辑处理，导致职责不单一。因此，Model2 应运而生，使得各部分各司其职，职责单一。

Model2 就是基于 MVC 模式架构，具体如下：

- Controller：负责用户交互（Servlet）
- Model：负责数据逻辑处理（JavaBeans）
- View：负责数据显示（JSP）

<img src="/spring-mvc/images/32f12903-1968-4a42-9cb2-cd1e9552c18f.png" alt="32f12903-1968-4a42-9cb2-cd1e9552c18f" style="zoom:67%;" />

#### Model2 模式有什么优缺点？

- 优点：职责清晰，较适合于大型项目
- 缺点：分层较多，不适合小型项目开发

#### 那 Model1 和 Model2 有什么区别？

Model2 在 Model1 的基础上分离了控制，将 JSP 中的逻辑操作部分分离出来（放在 controller 中），这样做既让 JSP 的职责变得单一，又更有利于分工开发，耦合度降低。因此，对于复杂的 Web 应用开发，更适合使用 Model2，而对于小型应用，使用 Model1 比较简单直接。

> [idea]可见，软件开发中一个重要的解耦的思想就是“**分层**，当已有的架构不满足“高内聚，低耦合”时，再抽象出新的分层就能极大的解决这类问题。像现代计算机体系也是在分层中逐渐迭代演进，逐步发展出今天庞大复杂的体系。

## 时代3：Struts1 匆匆登上历史舞台，又快速落幕

**为什么会诞生 Struts1？**

[Struts1](https://siteson.github.io/post/history-of-mvc-mode/#fn:3) 出现的目的是为了帮助开发者减少运用 MVC 模型开发 Web 应用的时间。因为使用 Struts1可以提高系统的维护和开发效率，我们只需要配置和编码实现Action 和 ActionForm 就可以了。

#### Struts1 组成部分

<img src="/spring-mvc/images/3caecd79-99cd-4fc7-8cb7-ed5478858427.jpg" alt="3caecd79-99cd-4fc7-8cb7-ed5478858427" style="zoom:80%;" />

为了让你更清楚地看到 Servlet 和 Struts1的区别，接下来我们一起来看下它们的执行过程。

#### Servlet 的执行过程

使用Servlet， 需要每个页面都设置一个 Servlet 类来处理请求和响应，然后再获取用户提交的数据并把数据与持久化类对应起来。再做判断，决定跳转，再让JSP显示。

<img src="/spring-mvc/images/d5ff3203-b93e-4f4f-ada3-dba81bc86f70.png" alt="d5ff3203-b93e-4f4f-ada3-dba81bc86f70" style="zoom:80%;" />

#### Struts1 的执行过程

使用 Struts1时，通过运行时（runtime）初始化ActionServlet，再把所有持久化类的各个属性设为null。当有请求来时，通过name属性找到form-beans中form-bean的name属性，得到ActionForm的包名类名。然后实例化form，把用户数据提交给它，调用form的validate 方法验证。ActionErrors返回null表示验证通过，否则失败返回。验证通过会根据请求的Action类型实例化Action，执行Action的execute方法。根据传进来的ActionForm持久化对象可以取到传进来的数据，这个数据可以先和数据库中的数据交互，再决定跳转。

换句话说，也就是 Struts1封装了request.getParameter()，再把数据传给JavaBean持久化类。另外，Struts1弥补了JPS标签的不足，为开发提供了便利。

<img src="/spring-mvc/images/12f67b3d-87ab-4e09-8da7-925d93956dc8.png" alt="12f67b3d-87ab-4e09-8da7-925d93956dc8" style="zoom:80%;" />

## 时代4：Struts2 野心勃勃却“创业未半而中道崩殂”

### Struts2 诞生背景

Struts2 和 Struts1的差别巨大，**Struts2以 WebWork 为核心，采用拦截器的机制来处理用户的请求**，这样的设计使得控制器的业务逻辑与Servlet API完全脱离。

### Struts1 与Struts2 有什么区别？

我们主要从Action类、线程模式、Servlet依赖、捕获输入、表达式语言等五个方面来进行比较。

|   比较项    |                           Struts1                            |                      Struts2                       |
| :---------: | :----------------------------------------------------------: | :------------------------------------------------: |
|  Action类   |                   Action类继承一个抽象基类                   | Action类可以实现一个Action接口，也可以实现其他接口 |
|  线程模式   | 单例设计模式且是必须是线程安全，因为仅有一个Action的实例处理所有请求 |    每一个请求产生一个实例，因此没有线程安全问题    |
| Servlet依赖 | 依赖于Servlet API，因为当一个Action被调用时<br/>HttpservletRequest和HttpServletResponse被传递给execute方法 |     不依赖于容器，允许Action脱离容器单独被测试     |
|  捕获输入   | 使用ActionForm对象捕获输入，所有的ActionForm必须继承一个基类 |           直接使用Action属性作为输入属性           |
| 表达式语言  |                     整合了JSTL El表达式                      |       不仅可以使用JSTL，也支持ognl表达式语言       |

### 为什么 Struts2“中道崩殂”？

随着历史的车轮滚滚向前，曾经风靡一时的 Struts2 最终被 Spring MVC所取代，最主要是因为 Struts2 的安全问题异常严峻，Struts2 的安全漏洞，让不少公司吃尽了苦头，慢慢磨掉了用户的信心。

> [idea]做产品一定要为用户考虑，有用户意识，否则，曾经哪怕光芒万丈，也只是过往云烟。

## 时代5：迈入 Spring MVC 如日中天的时代

#### SpringMVC 原理图

![8e93b907-8cf4-44cd-b9c7-e3a06b668eec](spring-mvc/images/8e93b907-8cf4-44cd-b9c7-e3a06b668eec.jpg)

### Spring MVC和 Struts2 有什么区别？

|    区别点    |                          Spring MVC                          |                           Struts2                            |
| :----------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|   入口不同   |                           servlet                            |                            filter                            |
| 生命周期不同 | MVC Controller是单例，所以效率更高，但不能用成员变量获取参数 | Struts2 Action 是多例，所以效率比较低，可以用成员变量获取参数 |



#### 参考链接：

[1]https://siteson.github.io/post/history-of-mvc-mode/

[2]http://www.ruanyifeng.com/blog/2007/11/mvc.html