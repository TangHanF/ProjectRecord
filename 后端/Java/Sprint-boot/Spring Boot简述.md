# Spring Boot 概述

> Spring Boot是一个框架，主要理念就是消除项目中大量的配置文件，使项目更加短小精悍。我们知道 java 的开发显得很笨重：繁多的配置、开发效率低下、复杂的布署流程以及第三方技术集成难度大。所以说，spring boot就是在此环境下产生的。

# Spring Boot 的核心功能

1. **独立运行的Spring 项目**
   Spring Boot **可以以jar包的形式独立运行**，运行一个Spring Boot 项目只需要通过 java -jar xx.jar 来运行。
2. **内嵌Servlet 容器**
   Spring Boot 可以选择内嵌Tomcat、Jetty或Undertow，这样我们无须以war包形式部署项目。
3. **提供starter简化Maven 配置**
   Spring 提供了一系列的starter pom 来简化Maven 的依赖加载。
4. **自动配置Spring**
   Spring Boot 会根据在类路径中的jar包、类，为jar包里的类自动配置Bean，这样会极大地减少我们要使用的配置。Spring Boot只考虑了大多数的场景，并不是所有的场景。
5. **准生产的应用监控**
   Spring Boot 提供基于http、ssh、telnet对运行时的项目进行监控。
6. **无代码生成和xml配置**
   Spring Boot不是借助代码生成来实现的，而是通过条件注解来实现的，这是spring 4.x的新特性。Spring 4.x提倡使用Java配置和注解配置组合，而**Spring Boot不需要任何xml配置即可实现Spring 的所有配置**。

# Spring Boot 的优缺点

**优点：**

1. 快速构建项目；
2. 对主流开发框架的无配置集成；
3. 项目可以独立运行，无须外部依赖Servlet容器；
4. 提供运行时的应用监控；
5. 极大地提高了开发、部署效率；
6. 与云计算的天然集成。

**缺点：**

1. 书籍文档较少且不够深入；
2. 如果你不认同Spring 框架。