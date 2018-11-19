> 作者：TangHanF（GuoFu）
>
> 日期：2018年6月12日
>
> 说明：转载请注明出处，谢谢！🤝
>
> 联系方式：guofu_gh@163.com

# 基础点

- Spring框架：轻量级的企业级开发的一站式解决方案[^1]
- 每一个被Spring管理的Java对象都称之为`Bean`
- Spring提供了一个IoC容器用来初始化对象，解决对象间的依赖和对象的使用
- Spring是模块化的，因此可以按需使用相应的模块

**Spring框架四大原则：**

> 1）使用POJO[^2]进行轻量级和最小侵入式开发
>
> 2）通过依赖注入和基于接口编程实现松耦合
>
> 3）通过AOP和默认习惯进行声明式编程
>
> 4）使用AOP和模板减少模式化代码

- 控制反转（IoC）是通过依赖注入[^3]实现的

## 常用注解总结

### 声明Bean的注解：

> - @Component：没用明确角色
> - @Service：在业务逻辑层（Service）使用
> - @Repository：在数据访问层（Dao）使用
> - @Controller：在展现层（MVC--->Spring MVC）使用
>
> 以上注解作用都是等效，都是告诉Spring容器这是需要进行管理的Bean。通过不同的注解在不同逻辑层进行注解，更加清晰。
>
> @ComponentScan注解会扫描包名下，加入以上注解的类并注册为Bean。

### 注入Bean的注解，一般情况下通用，都是等效的：

> - @Autowired：Spring提供的注解
> - @Inject：JSR-330提供的注解
> - @Resource：JSR-250提供的注解
>
> 以上注解都可以注解到set方法或者属性上，建议注解在属性上，代码少、结构层次清晰

---------

### @Configuration

> 声明注解类是一个配置类

### @ComponentScan

> 自动扫面包下面的使用@Service、@Component、@Repository、@Controller注解的类并注册为Bean。（通常和@Configuration一起使用）

---------

- `Java配置`是Spring4.x推荐的配置方式，完全可以代替xml配置，同时也是Spring Boot推荐的配置
  - Java配置通过`@Configuration`[^4]和`@Bean`[^5]实现的
  - Java配置与`注解配置`的使用原则：`全局配置使用Java配置（如数据库、MVC相关配置），业务Bean的配置使用注解配置（@Component、@Service、@Repository、@Controller）`

### @ConfigurationProperties

将properties属性和一个Bean以及其属性关联（基于类型安全的配置方式）。即配置与类关联

### @EnableConfigurationProperties

开启对`@ConfigurationProperties`注解配置Bean的支持，格式：

> @EnableConfigurationProperties(配置类.class)

从而明确指定使用哪个类装载配置信息



# 脚注区

--------

[^1]: 解决方案就是可以基于Spring解决Java EE开发的所有问题
[^2]: POJO（Plain Old Java Object），无任何限制的普通Java对象
[^3]: 依赖注入：容器负责创建对象和维护对象间的依赖关系，而不是通过对象本身负责自己的创建和解决自己的依赖。主要目的是为了解耦，体现了“组合”概念
[^4]: @Configuration：声明当前类是一个配置类，相当于一个Spring哦·配置的xml文件
[^5]: @Bean：注解在方法上，声明当前方法的返回值是一个Bean

