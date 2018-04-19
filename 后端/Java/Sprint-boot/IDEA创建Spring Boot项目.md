# 1. 新建Spring Initializr 项目

![img](assets/1240732-20171210185304130-1613507897.png)

# 2. 填写项目信息

![img](assets/1240732-20171210185455021-2123052165.png)

# 3. 选择项目使用的技术

![img](assets/1240732-20171210185604036-1671118057.png)

# 4. 填写项目名称

![img](assets/1240732-20171210185652505-1527919520.png)

# 5. 项目架构及依赖

![img](assets/1240732-20171210190507802-1074917446.png)

# 6. 添加测试控制器

直接在入口类中编写。

```java
package com.springboot.first;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@SpringBootApplication
public class FirstApplication {

    @RequestMapping("/")
    String index() {
        return "Hello Spring Boot";
    }
    public static void main(String[] args) {
        SpringApplication.run(FirstApplication.class, args);
    }
}
```

@SpringBootApplication是Spring Boot 项目的核心注解，主要目的是开启自动配置。main方法是一个标准的Java应用的main方法，主要作用是作为项目启动的入口。

# 7. 运行项目

把它当成一个java类运行就可以了，右键菜单中选择，如图：

![img](assets/1240732-20171210190955396-606058819.png)

运行信息：
![img](assets/1240732-20171210191115740-1641227994.png)

8. 运行结果，如图：

![img](assets/1240732-20171210191207115-1995148064.png)