---
title: Spring Boot那些事(0)-入门篇
date: 2017-07-21 16:21:53
categories: [Java]
tags: [Java,Spring Boot]
---

#### 什么是Spring Boot

读研期间主要写的是Java后端，工作之后开始更多地接触Node.js写后端程序，有对比才有伤害，让我深深的感受到了Java的重量级，开发的时候各种配置，部署的时候还有一堆要忙活，相对而言Node.js之类的新兴的后端语言显得格外的清新小巧。如果你觉得既然如此就可以就此放弃Java了，那就太草率了，毕竟Java作为后端主流语言不会就这么自甘堕落，Spring Boot应运而生，虽然很早之前就听过Spring Boot的大名，但是碍于当时论文的压力，一直没有深入地去了解，最近项目需要正好可以搞一搞熟悉一下。

Spring Boot推崇的是”习惯优于配置“，通俗的说可以这么理解，原来一个即使很简单的项目也需要有一大把的配置，但是后来发现很多时候大部分的配置都是一样的，你也会这么配，我也会这么配，但是如果你不知道你就不会配，你仍然需要去了解茫茫多的配置项才能运行一个其实非常简单的项目，当你陷入这种境地的时候，Spring Boot就给你带来了曙光，你可以摆脱大部分的通用配置，框架内置一套习惯的配置，你只需要对你需要的部分进行定制即可。

以前Java项目另外一个痛点就是部署，项目无论大小都需要配置一台服务器(Tomcat等)，然后把项目打包部署上去，所以你还要懂一套服务器部署的内容，可是明明有些项目就很简单啊，非要搞这么复杂，Spring Boot则告诉你，原来Java项目开发也可以很简单，框架内置了一个轻量级的Servlet容器(Tomcat或者Jetty等)，让你很容易地创建一个独立运行项目，只需一个命令，你就可以向运行普通Java程序一样运行一个Java后端程序，是不是很爽！

#### Spring Boot主要特点

1. 能够独立运行
Spring Boot创建的程序最终会打成一个jar包，因此，只需要`java -jar your-project-name.jar`一句命令就可以运行起来了。

2. 内置Servlet容器
Spring Boot项目会内置一个容器，如Tomcat、Jetty等，这样我们就不需要再额外配置服务器去部署了。

3. 自动装配
从spring最原始的xml配置bean一路走来，曾几何时觉得`@Autowired`自动装配已经非常好用了，而Spring Boot则可以根据类路径中的jar包、类，为jar包里的类自动装配bean，这样就更进一步地减少了配置的工作量。但是嘛，自动的总会出问题的，它并不能帮你解决任何问题，当你发现它做的不够的时候，还是需要手动地去配置一下，但是相比而言，它也能够应付一部分场景了。

4. 摆脱繁杂的XML和代码配置
Spring 4.x里已经可以通过注解来实现配置了，而Spring Boot则把这一特性发挥到了极致，一个项目里你甚至可以不写一行xml，不写一行配置代码，就可以完成。

5. 简化的Maven配置

Maven的出现已经可以帮我解决了很多依赖的问题，不用再一个一个jar包去下载导入，但是有没有这么一种感觉，我还是要在pom里面写很多，而且有时候我根本不知道要添加哪个jar包，这一点Spring Boot也想到了，它提供了一系列starter来简化Maven依赖，比如你只需要添加一个`spring-boot-starter-web`，如下，就可添加web开发中常用的依赖包。

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

#### 从哪里开始

1. https://start.spring.io/
说了那么多Spring Boot的好处，怎么开始呢？这一点也充分体现了其简单的特点，非常方便。

访问https://start.spring.io/ ，就可以看到Spring Boot官方的项目生成页面，你只需要填写项目的信息，选择一下依赖，然后点击`Generate Project`就可以生成项目文件并下载zip包。

在这里可以选择使用Maven管理还是Gradle管理项目依赖，使用Java、Kotlin还是Groovy，还有Spring Boot的版本，打包方式，Java版本，等等，其他的可以自行查看。当然即使生成项目的时候填错了也没关系，后面还可以改嘛。

2. 手动创建
求人不如求己，有时候你还是需要知道如何手动的去创建一个项目，说到底，所有的生成工具帮你生成还是一个Maven项目，或者Gradle项目，只不过是帮你填写好了一些信息而已，你完全可以自己手动填写。

这里以Maven项目为例：

1. 首先你需要新建一个空的Maven项目，这个就不说了，不会的去面壁；
2. 添加Spring Boot父依赖，提供相关的默认依赖，指定版本号，如下；

```xml
<parent>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-parent</artifactId>
  <version>1.5.4.RELEASE</version>
  <relativePath/> <!-- lookup parent from repository -->
</parent>
```

3. 添加相关starter

比如这里添加了web支持和security支持：

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

4. 添加编译插件

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-maven-plugin</artifactId>	
    </plugin>
  </plugins>	
</build>
```

5. 完成

2. 其他方式
除了这两种方式之外还有其他一些方式，比如Spring Boot CLI、Spring Tool Suite等等，这些就不做介绍了。

#### 如何开始

这里采用在`http://start.spring.io`上新建项目后下载，这是下载之后的文件目录：

```bash
.
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src
    ├── main
    │   ├── java
    │   │   └── site
    │   │       └── holten
    │   │           └── springboot0
    │   │               └── Springboot0Application.java
    │   └── resources
    │       └── application.properties
    └── test
        └── java
            └── site
                └── holten
                    └── springboot0
                        └── Springboot0ApplicationTests.java
12 directories, 6 files
```

我们首先看一下pom.xml，这里只添加了web starter：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>site.holten</groupId>
	<artifactId>springboot0</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>
	<name>springboot0</name>
	<description>Demo project for Spring Boot</description>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.4.RELEASE</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
		<project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
		<java.version>1.8</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>
	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
</project>
```

作为简单示例，我们直接在`Springboot0Application.java`中编写代码：

```java
package site.holten.springboot0;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
@RestController
@SpringBootApplication
public class Springboot0Application {
    public static void main(String[] args) {
        SpringApplication.run(Springboot0Application.class, args);
    }
    @RequestMapping("/")
    public String homepage() {
        return "this is home page!";
    }
    @RequestMapping("/hello/{name}")
    public String sayHello(@PathVariable String name) {
        return "hello " + name;
    }
}
```

这里了解这么几点就可以了：

- `SpringApplication.run(Springboot0Application.class, args)`：main方法中的这句话用来指定程序的入口；
- `@SpringBootApplication`：这个是最重要的，标识着这是一个Spring Boot项目，开启自动配置；
- `@RestController`：这个是Spring MVC里面的注解，组合了`@Controller`和`@ResponseBody`；
- `@RequestMapping`：用来映射请求路径/参数、处理类和方法；
- `@Controller`：表明这是一个Spring MVC的Controller，Dispatcher Servlet会自动扫描该类，发现其中的`@RequestMapping`注解并映射；
- `@ResponseBody`：用来支持把返回值放到response体内；

代码写完了，如何运行呢？

- 如果你是用的IDE，那么直接run或者debug就可以了；
- 如果没有，可以在命令行里运行`mvn spring-boot:run`，当然，前提是你要安装了maven，并且在项目根目录下；
- 然后在地址栏输入`http://localhost:8080/`或者`http://localhost:8080/hello/yourname`就可以看到结果了；

具体效果就不贴图了，自行体会～～～
