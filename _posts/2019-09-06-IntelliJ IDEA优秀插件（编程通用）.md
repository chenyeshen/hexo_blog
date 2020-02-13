---
layout:     post
title:      IntelliJ IDEA优秀插件（编程通用）
subtitle:   学习笔记
date:       2019-09-06
author:     chenyeshen
header-img: img/img29.jpg
catalog: true
tags:
    - idea插件
    
---



#### **Mybatis Log Plugin**

#### **RestfulToolkit**

#### Gsonformat

#### codehelper.generator

#### GenerateAllSetter

#### **Grep Console**

#### **CodeGlance **

#### **IDEA Restart**

#### **Maven Helper**

#### **JRebel**

#### **SonarLint**

SonarLint是一款强大快速的能帮助开发者发现代码里的bug或是代码质量优化点的扩展工具。支持很多主流的语言：JAVA、js、PHP、Python。也支持主流的IDE们，idea、Eclipse、vs等。在idea里更是以插件的形式让人无缝接入 

可在线安装，也可离线安装，插件下载地址：https://www.sonarlint.org/

#### Lombok

#### Alibaba Java Coding Guidelines

#### CodeMaker   

开发过程中，经常手工编写重复代码。现在，可以通过 CodeMaker 来定义 Velocity 模版来支持自定义代码模板来生成代码。目前，CodeMaker 自带两个模板。Model：根据当前类生成一个与其拥有类似属性的类，用于自动生成持久类对应的领域类。Converter：该模板需要两个类作为输入的上下文，用于自动生成领域类与持久类的转化类。详细使用文档，参考：https://github.com/x-hansong/CodeMaker

#### REST client

在日常开发过程中，我们或多或少都涉及到 API 接口的测试。例如，有的小伙伴使用 Chrome 的 Postman 插件，或者使用火狐的 restclient 等工具。事实上，这些工具是测试 API 接口非常有效的方式之一，笔者之前也一直使用 Postman 完成 API 接口的测试工作。今天，笔者推荐另外一个非常好用的小工具，能够帮助读者快速测试 API 接口。这个工具就是 IDEA 的 Editor REST Client。IDEA 的 Editor REST Client 在 IntelliJ IDEA 2017.3 版本就开始支持，在 2018.1 版本添加了很多的特性。事实上，它是 IntelliJ IDEA 的 HTTP Client 插件。详细使用文档，参考：http://blog.720ui.com/2018/restclient_use/



#### Kubernetes   K8s工具

参考 https://plugins.jetbrains.com/plugin/10485-kubernetes 支持编辑 Kubernetes 资源文件，如下： 可以比较方便的查看yaml中的各项 placeholder 的默认值，且可以方便的链接到value位置。



#### Free Mybatis plugin

#### UnitGenerator   单元测试测试生成工具

单元测试是必不可少的！我们可以使用 JUnitGenerator 插件来自动创建了单元测试。我们可以使用提供的 velocity 模板定制单元测试输出代码。如果在已经存在单元测试的地方创建了单元测试，则会提示用户进行覆盖或合并操作。合并操作允许用户有选择地创建目标文件内容。详细使用文档，参考：https://plugins.jetbrains.com/plugin/3064-junitgenerator-v2-0



#### 字符串工具：String Manipulation



#### POJO to JSON     领域对象转JSON工具

为了测试需要，我们需要将简单 Java 领域对象转成 JSON 字符串方便用 postman 或者 curl 模拟数据。详细使用文档，参考：https://plugins.jetbrains.com/plugin/9686-pojo-to-json



#### Redis可视化：Iedis

参考：https://plugins.jetbrains.com/plugin/9228-iedis 使用参考：https://codesmagic.com/iedis/userguide/getting-started 可方便的执行增删查改及使用命令行进行操作。



**Stackoverflow **

这个插件其实是最实用的插件，程序猿遇到的问题，基本都能找到回答，但是它使用的是google搜索引擎，对于，不购买vpn的同学来说，感觉好鸡肋呀~

选中需要搜索的问题，然后，右键点击



#### **FindBugs**

Idea自带的检查工具已经很强大，如有需要也可以加上Alibaba Java Coding Guidelines的代码检查工具，但是，说白这些工具其实更多的是规范性检查，如果需要更深入的去检查异常，可以使用此插件~

右键点击文件，包或者工程

**IdeaJad**

以前查看class文件形式的时候或者jar，都会使用一个外部反编译工具，这样操作明显不方便，使用此插件可以一直在idea中查看文件~  ps：其实Inteli Idea这个编译器已经自带了反编译功能，老夫~~~~~~

选择class文件，右键 Decompile,完成反编译



**Free-idea-mybatis**

mybatis xml和对应的mapper之间来回切换的时候，有时候不同人开发，放置的位置又不同，使用此插件后，来回切换的时候异常方便，和所放置的位置无关~



**MyBatisCodeHelperPro**

这个是一款比较实用的插件。但是，现在需要收费啦，貌似是需要花费29块钱，送两个激活码。不过，也可以申请7天的免费测试码，体验一下在购买也可以的。收费掩盖不了她的魅力所在，这也是行业发展的趋势。具体功能如下（总有一款适合你~）：

- 提供Mapper接口与配置文件中对应SQL的导航.
- 编辑XML文件时自动补全.
- 根据Mapper接口, 使用快捷键生成xml文件及SQL标签.
- ResultMap中的property支持自动补全，支持级联(属性A.属性B.属性C).
- 快捷键生成@Param注解.
- XML中编辑SQL时, 括号自动补全.
- XML中编辑SQL时, 支持参数自动补全(基于@Param注解识别参数).
- 自动检查Mapper XML文件中ID冲突.
- 自动检查Mapper XML文件中错误的属性值.
- 支持Find Usage.
- 支持重构从命名.
- 支持别名.
- 自动生成ResultMap属性.
- 快捷键: Option + Enter(Mac) | Alt + Enter(Windows).



**VisualVM Launcher**

一般可用于在本地开发进行压力测试，性能测试之类的监控器，其他场景一般不推荐使用此模式启动，还会启动另外一个Visual vm窗口，这个窗口是JDK bin目录下的JvisualVM 

