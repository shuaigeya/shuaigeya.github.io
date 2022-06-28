---
title: Spring基础概念篇
date: 2022-06-28 15:40:21
tags:
- spring
categories:
- 框架篇
---
## 1.什么是Spring
容器框架：可以管理所有的组件（类）
## 2.IOC 和 AOP

**IOC**：也叫控制反转，是一种设计思想，将原本程序中手动创建对象的控制权交给Sping框架来管理。IOC容器是Sping用来实现IOC的载体，IOC容器实际上就是个MAP，MAP中存放各种对象。IOC容器就像是一个工厂，当我们需要创建一个对象时，只需要配置好配置文件、注解即可，完全不用考虑对象是如何被创建出来的。

**AOP**:面向切面编程，将那些与业务无关，却为业务模块所共同调用的逻辑或泽恩封装起来，便于减少系统重复代码，降低耦合性，有利于未来的扩展和可维护性。



## 3.springMVC执行流程。
1.用户发送请求，这个请求会先到dispatcherServlet(中央控制器)。

2.中央控制器接受请求调用handlerMappers（处理器映射器），并由此知道该请求由哪个controller处理 。

3.中央控制器调用 HandlerAdapter （处理器适配器），告诉中央控制器应该要去执行哪个controller。

4.前端控制器调用HandlerAdapter,HandlerAdapter经过适配器调用具体的controller。

5.controller执行完返回modelAndView（视图和数据），并层层返回给中央控制器。

6.中央适配器把modelAadView交给viewReslover(视图解析器)，然后返回真正的视图。

7.前端控制器将数据模型填充到视图中。

8.前端控制器将响应结果返回给用户。