> Created By:TangHanF
>
> Created Date:2018年4月18日

------------

# @RestController

> @RestController表示controller里面的方法都以json格式输出，不用再写什么jackjson配置的了！
>
> @RestController 注解告诉Spring以某种类型（例如：字符串）的形式渲染结果，并直接返回给调用者。
>
> 用于标注控制层组件(如 struts 中的 action)，包含 @Controller 和 @ResponseBody。

在以前的spring 开发的时候需要我们提供json接口的时候需要做那些配置呢

> 1. 添加 jackjson 等相关jar包
> 2. 配置spring controller扫描
> 3. 对接的方法添加@ResponseBody

就这样我们会经常由于配置错误，导致406错误等等，spring boot如何做呢，只需要类添加 `@RestController ` 即可，默认类中的方法都会以json的格式返回

```java
@RestController
public class HelloWorldController {
    @RequestMapping("/getUser")
    public User getUser() {
    	User user=new User();
    	user.setUserName("小明");
    	user.setPassWord("xxxx");
        return user;
    }
}
```

# @SpringBootApplication

> @SpringBootApplication是Spring Boot 项目的核心注解，主要目的是开启自动配置。main方法是一个标准的Java应用的main方法，主要作用是作为项目启动的入口。

> 包含 @Configuration、@EnableAutoConfiguration、@ComponentScan
> 通常用在主类上。

# @RequestMapping

> 提供路由信息。它告诉Spring任何来自"xxxxx"路径的HTTP请求都应该被映射到 xxxxx 方法。 

**注： @RestController 和 @RequestMapping 注解是Spring MVC注解（它们不是Spring Boot的特定部分）**



# @EnableAutoConfiguration

> 告诉Spring Boot根据添加的jar依赖猜测你想如何配置Spring。

由于 spring-boot-starter-web 添加了Tomcat和Spring MVC，所以auto-configuration将假定你正在开发一个web应用并相应地对Spring进行设置。Starter POMs和Auto-Configuration：设计auto-configuration的目的是更好的使用"Starter POMs"，但这两个概念没有直接的联系。你可以自由地挑选starter POMs以外的jar依赖，并且Spring Boot将仍旧尽最大努力去自动配置你的应用。

你可以通过将 @EnableAutoConfiguration 或 @SpringBootApplication 注解添加到一个 @Configuration 类上来选择自动配置。
注：你只需要添加一个 @EnableAutoConfiguration 注解。我们建议你将它添加到主 @Configuration 类上。

如果发现应用了你不想要的特定自动配置类，你可以使用 @EnableAutoConfiguration 注解的排除属性来禁用它们。

```java
1. import org.springframework.boot.autoconfigure.jdbc.*;  
2. import org.springframework.context.annotation.*;  

3. @Configuration  
4. @EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})  
5. public class MyConfiguration {  
6. }  

```



# @RequestBody

> 返回JSON格式数据。

# @ResponseBody

> 返回JSON格式数据。
>
> 方法、类注解。
>
> 表示该方法的返回结果直接写入 HTTP response body 中。一般在异步获取数据时使用，在使用`@RequestMapping` 后，返回值通常解析为跳转路径，加上 `@ResponseBody` 后返回结果不会被解析为跳转路径，而是直接写入 HTTP response body 中。比如异步获取 json 数据，**加上 `@ResponseBody` 后，会直接返回 json 数据**



# @Repository

> 用于标注数据访问组件，即 DAO 组件。

# @Service

> 用于标注业务层组件。



# @Configuration

> @Configuration可理解为用spring的时候xml里面的<beans>标签
>
> 参考：[@Configuration和@Bean的用法和理解](https://blog.csdn.net/u012260707/article/details/52021265)

### 自定义Filter

我们常常在项目中会使用filters用于录调用日志、排除有XSS威胁的字符、执行权限验证等等。Spring Boot自动添加了OrderedCharacterEncodingFilter和HiddenHttpMethodFilter，并且我们可以自定义Filter。

两个步骤：

> 1. 实现Filter接口，实现Filter方法
> 2. 添加`@Configuration` 注解，将自定义Filter加入过滤链

好吧，直接上代码

```java
@Configuration
public class WebConfiguration {
    @Bean
    public RemoteIpFilter remoteIpFilter() {
        return new RemoteIpFilter();
    }
    
    @Bean
    public FilterRegistrationBean testFilterRegistration() {

        FilterRegistrationBean registration = new FilterRegistrationBean();
        registration.setFilter(new MyFilter());
        registration.addUrlPatterns("/*");
        registration.addInitParameter("paramName", "paramValue");
        registration.setName("MyFilter");
        registration.setOrder(1);
        return registration;
    }
    
    public class MyFilter implements Filter {
		@Override
		public void destroy() {
			// TODO Auto-generated method stub
		}

		@Override
		public void doFilter(ServletRequest srequest, ServletResponse sresponse, FilterChain filterChain)
				throws IOException, ServletException {
			// TODO Auto-generated method stub
			HttpServletRequest request = (HttpServletRequest) srequest;
			System.out.println("this is MyFilter,url :"+request.getRequestURI());
			filterChain.doFilter(srequest, sresponse);
		}

		@Override
		public void init(FilterConfig arg0) throws ServletException {
			// TODO Auto-generated method stub
		}
    }
}
```

# @Bean

> 相当于 XML 中的,**放在方法的上面，而不是类**，意思是产生一个 bean, 并交给 spring 管理。

# @Component

> 泛指组件，当组件不好归类的时候，我们可以使用这个注解进行标注。

# @ComponentScan

> 组件扫描。相当于如果扫描到有 `@Component` `@Controller` `@Service` 等这些注解的类，则把这些类注册为 bean。

# @PersistenceContext





# @Configuration

> 指出该类是 Bean 配置的信息源，相当于 XML 中的，一般加在主类上。

# @Bean

> 相当于 XML 中的,**放在方法的上面，而不是类**，意思是产生一个 bean, 并交给 spring 管理。

# @EnableAutoConfiguration

> 让 Spring Boot 根据应用所声明的依赖来对 Spring 框架进行自动配置，一般加在主类上。

# @AutoWired

> byType 方式。把配置好的 Bean 拿来用，完成属性、方法的组装，它可以对类成员变量、方法及构造函数进行标注，完成自动装配的工作。
> 当加上（required=false）时，就算找不到 bean 也不报错。

# @Qualifier

> 当有多个同一类型的 Bean 时，可以用 @Qualifier(“name”)来指定。与 @Autowired 配合使用

# @Resource

> `@Resource(name="name",type="type")`没有括号内内容的话，默认 byName。与 @Autowired 干类似的事。

# @RequestMapping

> RequestMapping 是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。
> 该注解有六个属性：
>
> - params:指定 request 中必须包含某些参数值是，才让该方法处理。
> - headers:指定 request 中必须包含某些指定的 header 值，才能让该方法处理请求。
> - value:指定请求的实际地址，指定的地址可以是 URI Template 模式
> - method:指定请求的 method 类型， GET、POST、PUT、DELETE 等
> - consumes:指定处理请求的提交内容类型（Content-Type），如 application/json,text/html;
> - produces:指定返回的内容类型，仅当 request 请求头中的(Accept)类型中包含该指定类型才返回

# @RequestParam

> 用在方法的参数前面。
> @RequestParam String a =request.getParameter(“a”)。

# @PathVariable

> 路径变量。参数与大括号里的名字一样要相同。

```
RequestMapping("user/get/mac/{macAddress}") public String getByMacAddress(@PathVariable String macAddress){//do something;
}
```

# @Profiles

> Spring Profiles 提供了一种隔离应用程序配置的方式，并让这些配置只能在特定的环境下生效。
> 任何 @Component 或 @Configuration 都能被 @Profile 标记，从而限制加载它的时机。

```java
@Configuration
@Profile("prod) 
public class ProductionConfiguration { 

	// …

}
```

# @ConfigurationProperties

> - Spring Boot 将尝试校验外部的配置，默认使用 JSR-303（如果在 classpath 路径中）。
> - @ConfigurationProperties 根据类型校验和管理 application 中的 bean。
> - 你可以轻松的为你的 @ConfigurationProperties 类添加 JSR-303 javax.validation 约束注解：

```java
@Component
@ConfigurationProperties(prefix="connection") 
public class ConnectionSettings {
	@NotNull 
	private InetAddress remoteAddress; 
	
	// ... getters and setters
}
```

# 全局异常处理

## @ControllerAdvice

> 包含 @Component。可以被扫描到。
> 统一处理异常。

## @ExceptionHandler

> `@ExceptionHandler(Exception.class)`用在方法上面表示遇到这个异常就执行以下方法。