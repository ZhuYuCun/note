# 前言
> 博文目的：从零开始搭建一个SpringBoot项目、熟悉
> 开发工具：`Idea`， `java8`
> 工作环境：`windows 10`

如果没有，首先移步：
[Idea使用](链接地址)
[Java安装（8）](链接地址)
[Windows10安装](链接地址)

# 一、项目搭建  
1、使用Idea开发工具，选择`file>New>Project`
2、选择`Spring Initializr`  
右边Project SDK即使用的sdk版本（需要先安装java）。
选择开始服务Url，这个url地址可生成项目初始化的工程文件（选择Default即可）。
点击下一步

* 这一步其实就是选择了一个SDK后选择代码模板，spring是一个框架，而springBoot只是一个整合了spring的各个框架的工具，你可以选择使用自己需要的来搭建自己的项目。
  
3、这一页的说明是项目的结构配置：
Group： 一般以项目地址（域名）倒置命名，如：`com.baidu`, `net.alibaba`之类的，会生成相应的项目结构
Artifact：指项目名 如 `blog`   
Java Version: 与之前选择的jdk要一致

4、完成

# 二、项目结构说明
`.idea`:  
`.mvn`:  
`src`: 项目文件，这个就是整个项目写源代码的地方  
`.ignore`:  
`pom.xml`:  项目配置文件，里面会声明项目的基本信息、项目公共依赖的库及版本等  

其他的暂时不管
  

# src目录  
## main
 `java` 文件是写业务代码的文件，下面已生成多级目录，以上提到的项目名称即是当前项目的业务代码文件夹。  

 `resources`是放置项目内部配置、如数据库连接，全局变量设置  
## test
单元测试代码写在这  

# 源代码  
以下是 net.zyc的Group，以blog的Artifact生成的，

```java
// BlogApplication 项目入口文件
package net.zyc.blog; // 文件属于某个包 我们构建的blog这个
import org.springframework.boot.SpringApplication;  // spring自带的 一个class
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // 注解 
public class BlogApplication {
    public static void main(String[] args) {
        SpringApplication.run(BlogApplication.class, args);  // 入口方法 使用框架启动项目
    }
}
```  

- 这是pom.xml文件，记录了想项目的依赖项
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.1</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>net.zyc</groupId>
    <artifactId>blog</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>blog</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
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

# 结尾  
到此为止我们就搭建了一个简单的Spring Boot项目，当然这只是万里长征第一步，项目既无法运行、也看不到任何可视化，他提供的是一个可供开发使用的壳子，这个壳子里面我们会一步步加入内容，加入依赖、来实现我们的业务。
