---
layout: post
title:  "Thrift Script v0.0.1 ——JAVA代码生成脚本"
date:   2014-12-13
desc: "Thrift Script v0.0.1 ——JAVA代码生成脚本"
keywords: "Java,Thrift,系统架构,木偶人,胡登军,Simon"
categories: [Java,Architecture]
tags: [Java,Thrift,系统架构]
icon: fa-java
---

Thrift 生成代码脚本已发布到github上了，有需要的可以clone下来：

https://github.com/simonhoo/thrift-script

![Thrift-Script]({{ site.img_path }}/thrift/thrift-script-release.png)

### 目录说明：
* gen-java: 生成的源代码，每次生成时，自动清空旧代码；
* idl: thrift 定义文件；
* libs: 生成Thrift代码所需要的JAR包；
* rcp: 所生成的代码编译打包之后的输出目录；

 

### 操作步骤：
* step 1. SET JAVA_HOME;
* step 2. SET ANT_HOME;
* step 3. 运行 gen-thrift.bat;
* step 4. 在gen-java目录可以看到最终生成的源代码；
* step 5. 在rpc目录是生成代码打包后的JAR；

