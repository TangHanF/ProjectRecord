# @RestController

> @RestController表示controller里面的方法都以json格式输出，不用再写什么jackjson配置的了！
>
> @RestController 注解告诉Spring以某种类型（例如：字符串）的形式渲染结果，并直接返回给调用者。

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







# @Configuration

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



# @Component



# @PersistenceContext

