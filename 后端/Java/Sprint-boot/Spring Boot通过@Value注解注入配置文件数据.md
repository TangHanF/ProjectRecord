# 通过配置文件的注入属性的情况

通过`@Value`将外部配置文件的值动态注入到Bean中。配置文件主要有两类：

- **application.properties**

  `application.properties`在spring boot启动时默认加载此文件

- **自定义属性文件**

  - 自定义属性文件通过`@PropertySource`加载。
  - @PropertySource可以同时加载多个文件，也可以加载单个文件。
  - 如果相同第一个属性文件和第二属性文件存在相同key，则最后一个属性文件里的key启作用。
  - 加载文件的路径也可以配置变量，如下文的${anotherfile.configinject}，此值定义在第一个属性文件config.properties

## 配置文件内容

### application.properties

```
com.title=配置文件-标题
com.description=配置文件-描述
app.name=这是app.name
```

### config.properties

```
book.name=bookName
anotherfile.configinject=placeholder
deviceinfo.propertiesname=devices
```

### config_placeholder.properties

```
book.name.placeholder=bookNamePlaceholder
```

### devices.properties

```
MSR = COM1
IDCARD = COM2
```

## 类文件

###配置文件Bean：ConfigurationFileInject

```java
package com.springboot.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.PropertySource;
import org.springframework.core.env.Environment;
import org.springframework.stereotype.Component;

import java.util.HashMap;
import java.util.Map;

/**
 * Title: <br>
 * Packet:com.springboot.demo<br>
 * Description: <br>
 * Author:TangHanF<br>
 * Create Date: 2018-4-18.<br>
 * Modify User: <br>
 * Modify Date: <br>
 * Modify Description: <br>
 */
@Component
@PropertySource({"classpath:config.properties",
        "classpath:config_${anotherfile.configinject}.properties",
        "classpath:${deviceinfo.propertiesname}.properties"}
)
public class ConfigurationFileInject {
    @Value("${app.name}")
    private String appName; // 这里的值来自application.properties，spring boot启动时默认加载此文件

    @Value("${book.name}")
    private String bookName; // 注入第一个配置外部文件属性

    @Value("${book.name.placeholder}")
    private String bookNamePlaceholder; // 注入第二个配置外部文件属性

    @Autowired
    private Environment env;  // 注入环境变量对象，存储注入的属性值


    @Value("${MSR}")
    private String msrPort;

    @Value("${IDCARD}")
    private String idCard;


    public String getMsrPort() {
        return msrPort;
    }

    public void setMsrPort(String msrPort) {
        this.msrPort = msrPort;
    }

    public String getIdCard() {
        return idCard;
    }

    public void setIdCard(String idCard) {
        this.idCard = idCard;
    }

    public String getAppName() {
        return appName;
    }

    public void setAppName(String appName) {
        this.appName = appName;
    }

    public String getBookName() {
        return bookName;
    }

    public void setBookName(String bookName) {
        this.bookName = bookName;
    }

    public String getBookNamePlaceholder() {
        return bookNamePlaceholder;
    }

    public void setBookNamePlaceholder(String bookNamePlaceholder) {
        this.bookNamePlaceholder = bookNamePlaceholder;
    }

    public Environment getEnv() {
        return env;
    }

    public void setEnv(Environment env) {
        this.env = env;
    }

    @Override
    public String toString() {
        StringBuilder sb = new StringBuilder();
        sb.append("bookName=").append(bookName).append("\r\n")
                .append("bookNamePlaceholder=").append(bookNamePlaceholder).append("\r\n")
                .append("appName=").append(appName).append("\r\n")
                .append("env=").append(env).append("\r\n")
                // 从eniroment中获取属性值
                .append("env=").append(env.getProperty("book.name.placeholder")).append("\r\n");
        return sb.toString();
    }


    public Map<String, Object> getMap() {
        Map<String, Object> map = new HashMap<>();
        map.put("appName", getAppName());
        map.put("bookName", getBookName());
        map.put("bookNamePlaceholder", getBookNamePlaceholder());
        map.put("env", getEnv());
        map.put("msrPort", getMsrPort());
        map.put("IDCARD", getIdCard());

        return map;
    }
}

```



###启动类、调用：DemoApplication

```java 
package com.springboot.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;


@RestController
@SpringBootApplication
public class DemoApplication {

    // 通过 @Autowired 注解自动注入
    @Autowired
    ConfigurationFileInject configurationFileInject;

    @RequestMapping("/")
    public String index() {
        StringBuilder stringBuilder=new StringBuilder();

        String getAppName = configurationFileInject.getAppName();
        String getBookName = configurationFileInject.getBookName();
        String getBookNamePlaceholder = configurationFileInject.getBookNamePlaceholder();
        String getMsrPort = configurationFileInject.getMsrPort();
        String getIdCard = configurationFileInject.getIdCard();

        stringBuilder.append(String.format("%s>>>:%s<br/>","AppName",getAppName));
        stringBuilder.append(String.format("%s>>>:%s<br/>","BookName",getBookName));
        stringBuilder.append(String.format("%s>>>:%s<br/>","BookNamePlaceholder",getBookNamePlaceholder));
        stringBuilder.append(String.format("%s>>>:%s<br/>","MsrPort",getMsrPort));
        stringBuilder.append(String.format("%s>>>:%s<br/>","IdCard",getIdCard));
        return "<h1>Spring Boot运行成功！</h1><br/>" + stringBuilder.toString();
    }

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}

```



# 注意点

- `@PropertySource`注解指定资源文件路径
- 加载文件的路径也可以配置变量，如上面的`${anotherfile.configinject}`