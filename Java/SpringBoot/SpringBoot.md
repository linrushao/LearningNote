javase：oop

mysql：持久化

html+css+jquery+框架：视图，框架不熟练

javaweb：独立开发MVC三层架构的网站：原始

ssm：框架：简化了我们的开发流程，配置也开始较为复杂；

 war：tomcat运行

spring再简化：SpringBoot-jar：内嵌tomcat；微服务架构！

服务越来越多：splringcloud；

![image-20201217212326581](SpringBoot.assets/image-20201217212326581.png)

新服务架构：服务网格

# 1.SpringBoot入门

## 0 什么是SpringBoot

学过javaweb的同学就知道，开发一个web应用，从最初开始接触Servlet结合Tomcat, 跑出一个Hello Wolrld程序，是要经历特别多的步骤；后来就用了框架Struts，再后来是SpringMVC，到了现在的SpringBoot，过一两年又会有其他web框架出现

言归正传，什么是SpringBoot呢，就是一个javaweb的开发框架，和SpringMVC类似，对比其他javaweb框架的好处，官方说是简化开发，约定大于配置， you can “just run”，能迅速的开发web应用，几行代码开发一个http接口。

所有的技术框架的发展似乎都遵循了一条主线规律：从一个复杂应用场景 衍生 一种规范框架，人们只需要进行各种配置而不需要自己去实现它，这时候强大的配置功能成了优点；发展到一定程度之后，人们根据实际生产应用情况，选取其中实用功能和设计精华，重构出一些轻量级的框架；之后为了提高开发效率，嫌弃原先的各类配置过于麻烦，于是开始提倡“约定大于配置”，进而衍生出一些一站式的解决方案。

是的这就是Java企业级应用->J2EE->spring->springboot的过程。

随着 Spring 不断的发展，涉及的领域越来越多，项目整合开发需要配合各种各样的文件，慢慢变得不那么易用简单，违背了最初的理念，甚至人称配置地狱。Spring Boot 正是在这样的一个背景下被抽象出来的开发框架，目的为了让大家更容易的使用 Spring 、更容易的集成各种常用的中间件、开源软件；

Spring Boot 基于 Spring 开发，Spirng Boot 本身并不提供 Spring 框架的核心特性以及扩展功能，只是用于快速、敏捷地开发新一代基于 Spring 框架的应用程序。也就是说，它并不是用来替代 Spring 的解决方案，而是和 Spring 框架紧密结合用于提升 Spring 开发者体验的工具。Spring Boot 以**约定大于配置的核心思想**，默认帮我们进行了很多设置，多数 Spring Boot 应用只需要很少的 Spring 配置。同时它集成了大量常用的第三方库配置（例如 Redis、MongoDB、Jpa、RabbitMQ、Quartz 等等），Spring Boot 应用中这些第三方库几乎可以零配置的开箱即用。

简单来说就是SpringBoot其实不是什么新的框架，它默认配置了很多框架的使用方式，就像maven整合了所有的jar包，spring boot整合了所有的框架 。

Spring Boot 出生名门，从一开始就站在一个比较高的起点，又经过这几年的发展，生态足够完善，Spring Boot 已经当之无愧成为 Java 领域最热门的技术。

**Spring Boot的主要优点：**

- 为所有Spring开发者更快的入门
- **开箱即用**，提供各种默认配置来简化项目配置
- 内嵌式容器简化Web项目
- 没有冗余代码生成和XML配置的要求

## 1.1.POM文件

### 1.1.1.父项目

```xml
<!-- 
导入父项目：
1.The spring-boot-starter-parent is a special starter that provides useful Maven defaults. It also provides a dependency-management section so that you can omit(省略) version tags for “blessed” dependencies.

2.You can see that spring-boot-starter-parent provides no dependencies by itself.
parent这个启动器本身不会提供任何依赖，它做的是资源(依赖、版本version)的管理者(management)，添加具体的stater就会下载相应的依赖。比如，做web应用的开发，就添加 spring-boot-starter-web 就会下载web相关的模块！

3、虽然 parent 对依赖的版本有管理的作用，但是我们可以重写依赖的版本来替换 spring boot 推荐的版本
-->
<!--1、SpringBoot的pom文件中导入父项目-->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.4.RELEASE</version>
</parent>

<!--2、spring-boot-starter-parent的父项目是spring-boot-dependencies
spring-boot-dependencies 定义很多jar的版本，它是真正来管理SpringBoot应用里所有依赖的版本！
-->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.2.4.RELEASE</version>
    <relativePath>../../spring-boot-dependencies</relativePath>
</parent>
```

- `spring-boot-dependencies`是SpringBoot应用版本仲裁中心！以后我们导入依赖默认是不需要写版本的！
- 没有在`spring-boot-dependencies`管理的依赖我们自然需要声明版本号。

### 1.1.1.启动器(starter)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

- **spring-boot-starter**-==web==：spring-boot-starter是SpringBoot场景启动器。`spring-boot-starter-web`帮我导入了Web模块需要正常运行的组件。

- **一句话：SpringBoot将所有的功能场景都抽取出来，做成一个个的starter(启动器)，只需要在项目中引入这些starter相关场景的所有依赖都会导入进来！要用什么功能就导入什么starter(启动器)即可。**

## 1.2.自动配置

### 1.2.1.@SpringBootApplication

> 主配置类

```java
/**
 * @SpringBootApplication 来标注一个主程序类，说明这是一个SpringBoot应用
 */
@SpringBootApplication
public class ApplicationJD {
    public static void main(String[] args) {
        SpringApplication.run(ApplicationJD.class, args);
    }
}
```

**@SpringBootApplication**：该注解标注在某个类上说明，这个类是SpringBoot应用的主配置类，就可以运行主配置类的main()方法来启动SpringBoot应用！

**@SpringBootApplication 是一个组合注解,主要由@SpringBootConfiguration和@EnableAutoConfiguration组成。**



### 1.2.2.@SpringBootConfiguration

```java
/**
 * @SpringBootApplication 是一个组合注解，该注解表示SpringBoot的配置类。
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
		@Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
public @interface SpringBootApplication {
    

/**
 * @SpringBootConfiguration 是由@Configuration组成的
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {
```

- **@SpringBootConfiguration：**该注解表示SpringBoot的配置类。
  - @SpringBootConfiguration标注在某个类上，表示这是一个SpringBoot配置类。
  - @SpringBootConfiguration由@Configuration注解组成的，@Configuration也是代表配置类。
  - 只不过@SpringBootConfiguration是SpringBoot定义的注解，@Configuration是Spring定义的注解。
  - **注意：@Configuration是由@Component组成的，标注@Configuration的类也是Spring容器的一个组件。**

### 1.2.3.@EnableAutoConfiguration

```java
/**
 * @EnableAutoConfiguration：开启自动配置功能
 * 以前我们需要配置的东西,SpringBoot帮我们配置,@EnableAutoConfiguration告诉SpringBoot开启自动配置功能,这样自动置才能生效。
 * @EnableAutoConfiguration 由 @AutoConfigurationPackage 和 @Import(AutoConfigurationImportSelector.class)组成。
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {

/**
* @AutoConfigurationPackage
*/ 
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@Import(AutoConfigurationPackages.Registrar.class)
public @interface AutoConfigurationPackage {
```

- @AutoConfigurationPackage：自动配置包。
  - @Import(AutoConfigurationPackages.Registrar.class)：@import是Spring的底层注解，给容器导入组件。
  - **一句话：@AutoConfigurationPackage就是将主配置类(@SpringBootApplication标注的这个类)的所在包及下面所有子包和所有组件扫描到SpringBoot容器中。**
- @Import(AutoConfigurationImportSelector.class)：给容器导入组件。
  - AutoConfigurationImportSelector：这个类是给容器导入组件的选择器。将需要导入的组件以全类名的方式返回，这些组件就会被添加到容器中。
  - **一句话：(AutoConfigurationImportSelector.class会给SpringBoot导入非常多的配置类(xxxAutoConfiguration)，这些自动配置类会给容器中导入这个场景需要的所有组件，并配置好这些组件。**



### 1.2.4.总结

- `@SpringBootApplication`：主配置类 + 包扫描 +  导入xxxAutoConfiguration配置类。
  - `@SpringBootConfiguration`：SpringBoot声明的配置类。
    - `@Configuration`：Spring声明的配置类，也是一个组件@Component。
  - `@EnableAutoConfiguration`：包扫描 +  导入xxxAutoConfiguration配置类。
    - `@AutoConfigurationPackage`：包扫描。
    - `@Import(AutoConfigurationImportSelector.class)`：**SpringBoot在启动时从类路径下的`META-INF/spring.factories`中获取EnableAutoConfiguration指定的值，再将这些值作为自动配置类导入到容器中，自动配置类就生效了。**

### 1.3 原理初探

**自动配置：**

**pom.xml**

- Spring-boot-dependencies:核心依赖在父工程中
- 我们在写或者引入springboot依赖的时候，不需要指定版本，因为有这些版本仓库

**启动器**

- ```xml
  <!--启动器-->
  <dependency>   
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter</artifactId>
  </dependency>
  ```

- 启动器：说白了就是Springboot的启动场景

- 比如spring-boot-starter-web，他就会帮我们自动导入web环境所有的依赖

- springboot会将所有的功能场景，都变成一个个的启动器

- 我们要使用什么功能，就值需要找到对应的启动器`starter`

**主程序**

```java
//标注这个类是一个springboot的应用
@SpringBootApplication
public class SpringbootStudyApplication {

    public static void main(String[] args) {
        SpringApplication.run(SpringbootStudyApplication.class, args);
    }
}
```

**注解**

- ```java
  //springboot的配置
  @SpringBootConfiguration
  
  	//spring配置类
    @Configuration 
  
  	//说明这也是一个spring的组件
    @Component	
  
  //自动配置
  @EnableAutoConfiguration
  
  	//自动配置包
  	@AutoConfigurationPackage 
  
  	//自动配置	
  		@Import(AutoConfigurationPackages.Registrar.class)
  
  	//自动配置导入选择
  	@Import(AutoConfigurationImportSelector.class)
  
  //获取所有的配置
  List<String> configurations = getCandidateConfigurations(annotationMetadata, attributes);
  ```

获取候选的配置

```java
  protected List<String> getCandidateConfigurations(AnnotationMetadata metadata, AnnotationAttributes attributes) {
    List<String> configurations = SpringFactoriesLoader.loadFactoryNames(getSpringFactoriesLoaderFactoryClass(),
                                                                         getBeanClassLoader());
    Assert.notEmpty(configurations, "No auto configuration classes found in META-INF/spring.factories. If you "
                    + "are using a custom packaging, make sure that file is correct.");
    return configurations;
  }
  1234567
```

META-INF/spring.factories.

**结论：**

Springboot所有自动配置都是在启动的时候扫描并加载 ：`spring.factories`所有的自动配置类都在这里面，但是不一定生效，要判断条件是否成立，只要导入了对应的strater，就有了对应的启动器，有了启动器，我们自动装配就会生效，然后配置成功

1. springboot在启动的时候，从类路径下 /META-INF/spring.factories.获取指定的值；

![在这里插入图片描述](SpringBoot.assets/202010130811539.png)

1. 将这些自动配置的类导入容器，自动配置就会生效，帮我们进行自动配置
2. 以前我们需要手动配置的东西，现在Springboot帮我们做了
3. 整合javaEE，解决方案和自动配置的东西都在spring-boot-autoconfigure包下
4. 它会把所有需要导入的组件，以类名的方式返回，这些组件就会添加到容器
5. 容器中也会存在XXXXautoConfiguration的文件(@Bean)，就是这些类给容器中导入了这个场景所需要的所有组件,并自动配置，@Configuration,JavaConfig
6. 有了自动配置类，免去了我们自己编写配置文件的步骤

**启动原理：**

 最初以为就是运行了一个main方法，没想到却开启了一个服务；

```java
@SpringBootApplication
public class SpringbootApplication {
    public static void main(String[] args) {
        //该方法返回一个ConfigurableApplicationContext对象
        //参数一：应用入口的类，    参数二：命令行参数
        SpringApplication.run(SpringbootApplication.class, args);
    }
} 
123456
```

**这个类主要做了以下四件事情：**

1、推断应用的类型是普通的项目还是Web项目

2、查找并加载所有可用初始化器 ， 设置到initializers属性中

3、找出所有的应用程序监听器，设置到listeners属性中

4、推断并设置main方法的定义类，找到运行的主类

**run方法流程分析**

![image-20201220215844818](SpringBoot.assets/image-20201220215844818.png)

# 

# 2.配置文件

## 2.1.配置文件介绍 

- SpringBoot使用一个全局的配置文件，配置文件的名字是固定的：`application.properties`和`application.yml`。
- 配置文件的作用：修改SpringBoot自动配置的默认值。
- `application.properties`和`application.yml`一般都放在src/main/resources目录下。

## 2.2.YAML语法

> 基本语法

```yaml
# 1、key: value表示一对键值对(中间的空格必须有！)

# 2、以空格的缩进来控制层级关系，只要是左对齐的一列数据，都是同一个层级的。
# 属性和值也是大小写敏感的！
server:
  port: 1997
```

> 值的写法

```yaml
# 1、普通的值(数字、字符串、布尔)
# key: value 直接写就可以
# 字符串默认不用加单引号/双引号。

# 双引号：会转义字符串里面的特殊字符。
name: "zhangsan \n lisi"   # zhangsan 换行 lisi

# 单引号：不会转义字符串里面的特殊字符。单引号就是原样输出！
name: 'zhangsan \n lisi'   # zhangsan \n lisi

# 2、对象和Map(属性和值/键值对)

# 对象就是k: v Map和对象的写法相似
# 只是注意空格和缩进就可以了！
friends:
	name: zhangsan
	age: 18
	addr: beijing

# 3、数组(List、Set)

# 数组用"- "来表示数组中的一个元素
pets: 
	- cat:
		name: tom
	- dog
		name: ErHa
```

## 2.3.配置文件值的注入

### 2.3.1.@ConfigurationProperties

> Person类

```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;
import java.util.Date;
import java.util.List;
import java.util.Map;

/**
 * @ConfigurationProperties默认从全局配置文件中获取值。
 * @ConfigurationProperties 将配置文件中每一个属性的值,映射到这个组件中。
 * @ConfigurationProperties 告诉SpringBoot将实体类中的所有属性和配置文件中相关的配置进行绑定
 * prefix = "person"：配置文件中哪个下面的所有属性进行映射
 *
 * @Component: 需要把entity加入到容器中才能把yml的值映射到实体类中
 */
@Component
@ConfigurationProperties(prefix = "person")
public class Person {

    private String name;

    private Integer age;

    private boolean sex;

    private Date birth;

    private Map<String, Object> map;

    private List<Object> list;

    private Dog dog;

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", sex=" + sex +
                ", birth=" + birth +
                ", map=" + map +
                ", list=" + list +
                ", dog=" + dog +
                '}';
    }
}
```

> Dog类

```java
public class Dog {

    private String name;

    private Integer age;

    @Override
    public String toString() {
        return "Dog{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

> 依赖

```xml
 <!--导入配置文件处理器-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-configuration-processor</artifactId>
    <optional>true</optional>
</dependency>
```

> application.yaml

```yaml
person:
# 普通的key-value
  name: zhangsan
  age: 18
  sex: true
  birth: 2020/7/7
# Map
  map:
    k1: v1
    k2: v2
    k3: v3
# List
  list:
    - list01
    - list02
    - list03
# 对象
  dog:
    name: tom
    age: 3
```

> 测试

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class ConfigurationMappingTest {

    @Autowired
    private Person person;

    /**
     * 测试application.yaml配置文件值映射到整个实体类中的字段
     */
    @Test
    public void yamlToEntityAll() {
        System.out.println(person);
    }
}
```

### 2.3.2@Value

> @Value的使用

```java
public class Person {

    /**
     * 从配置文件中获取值
     */
    @Value("${person.name}")
    private String name;

    /**
     * Spring计算表达式
     */
    @Value("#{11 * 2}")
    private Integer age;

    /**
     * 直接赋值
     */
    @Value("true")
    private boolean sex;
   
}
```

### 2.3.3.@ConfigurationProperties和@Value的区别

|                     | @ConfigurationProperties | @Value     |
| ------------------- | ------------------------ | ---------- |
| 功能                | 批量注入配置文件中的属性 | 一个个指定 |
| 松散绑定            | 支持                     | 不支持     |
| SpEL                | 不支持                   | 支持       |
| JSR303数据校验      | 支持                     | 不支持     |
| 复杂数据类型(Map等) | 支持                     | 不支持     |

松散绑定：firstName可以在配置文件中使用first-name。

**一句话：如果我们只是在某个业务逻辑中需要获取配置文件中的某项值，就使用@Value。如果我们专门编写了一个JavaBean来和配置文件进行映射，那么就直接使用@ConfigurationProperties。**

### 2.3.4.JSR303数据校验

```java
@Component
@ConfigurationProperties(prefix = "person")
@Validated // 开始JSR303数据校验
public class Person {

    /**
     * @Email 表示name字段必须填写成邮箱格式
     */
    @Email
    private String name;
```

### 2.3.5.@PropertySource

**@PropertySource：用于加载指定的配置文件。**

**@ConfigurationProperties默认从全局配置文件(application.yml)中获取值。**

> 写person.properties配置文件

```properties
person.name=zhangsan
person.age=18
person.sex=false
```

> 使用@PropertySource注解

```java
/**
 * @PropertySource 只能读取到properties文件中的配置,不能读取到yaml文件的配置
 * @PropertySource 的value是一个数组,可以读取多个指定的配置文件
 */
@Component
@PropertySource(value = {"classpath:person.properties"})
@ConfigurationProperties(prefix = "person")
public class Person {

    private String name;

    private Integer age;

    private boolean sex;
}
```

### 2.3.6.@ImportResource

**@ImportResource：导入Spring的配置文件，让配置文件里面的内容生效。**

SpringBoot中没有Spring的配置文件，我们自己编写的配置文件，SpringBoot也不能自动识别。想让Spring的配置文件加载进SpringBoot中，使用@ImportResource标注在配置上即可。

==这种为SpringBoot添加组件的方式SpringBoot并不推荐。==

```java
// 导入Spring的配置文件使其生效
@ImportResource(locations = {"classpath:beans.xml"})
```

### 2.3.7.@Bean

SpringBoot推荐使用全注解的方式来给Spring容器添加组件！

```java
/**
 * @Configuration： 该注解指明当前类是一个配置类，替代Spring的xml配置文件！
 * 在Spring的xml配置文件中使用<bean><bean/>标签来添加组件。
 * 在@Configuration配置类中使用@Bean注解就可以添加组件。
 */
@Configuration
public class AppMainConf {
    /**
     * @Bean： 将方法的返回值添加到Spring容器中。这个组件默认的id就是方法名！
     */
    @Bean
    public HelloService helloService() {
        System.out.println("*********配置类给容器中添加helloService组件了*********");
        return new HelloService();
    }
}
```

## 2.4.配置文件占位符

```yaml
# 1、占位符可以使用随机数
# 2、占位符也可以引用之前的值
person:
  name: zhangsan${random.uuid} # 随机字符串
  age: ${random.int} # 随机的整数
  dog:
    name: ${person.name} # 引用上面的值
```

## 2.5.profile多环境支持

profile是Spring対不同环境提供不同配置功能的支持，可以通过激活、指定参数等方式快速切换环境。

> 多Profile文件

```yaml
# 我们在主配置文件编写的时候，文件名可以是 application-{profile}.properties/yml
# 在默认情况下使用的application.yml的配置

# application-dev.yml开发环境配置
server:
  port: 8081
  
# application-prod.yml生产环境配置
server:
  port: 8082

# application.yml主配置文件中激活指定配置文件，这样SpringBoot项目就会使用dev环境的配置文件了
spring:
  profiles:
    active: dev 
```

> yaml文件支持多文档块方式

```yaml
server:
  port: 8080
# 激活dev开发环境
spring:
  profiles:
    active: dev
---
# 开发环境
server:
  port: 8081
spring:
  profiles: dev
---
# 生产环境
server:
  port: 8082
spring:
  profiles: prod
```

> 命令行方式指定配置文件

```java
java -jar [jar的名字] --spring.profiles.active=dev
```

## 2.6.配置文件的加载顺序

```shell
# 1、配置文件的优先级从高到低
# 所有位置的配置文件SpringBoot都会被加载，高优先级配置内容会覆盖低优先级配置的内容(覆盖的相同的配置)
# 这四个配置文件都会被SpringBoot加载，不同的配置会形成互补配置！
file:/config/application.yml       # 当前项目下的config文件夹下的配置文件
file:/application.yml              # 当前项目下的配置文件
classpath:/config/application.yml  # resources目录下的config文件夹下的配置文件
classpath:/application.yml         # resources目录下的配置文件

# 2、项目打包之后可以通过spring.config.location命令行来改变默认的配置文件位置
# 所有的配置文件都会被加载并且都会起作用，形成互补配置
java -jar [jar的名字] --spring.config.location=C:\Users\14666\Desktop
```

# 3.自动配置

## 3.1.自动配置原理

```java
//以HttpEncodingAutoConfiguration为例来学习SpringBoot的自动配置

@Configuration(proxyBeanMethods = false) // 表示这是一个配置类
@EnableConfigurationProperties(HttpProperties.class)  // 启用ConfigurationProperties功能，将配置文件中对应的值和HttpProperties绑定起来。

@ConditionalOnWebApplication(type = ConditionalOnWebApplication.Type.SERVLET) // Spring底层注解@Conditional，如果满足指定的条件，整个配置类才会生效。判断当前应用是否是Web应用！如果是web应用，当前配置类生效。

@ConditionalOnClass(CharacterEncodingFilter.class) // 判断当前项目是否有CharacterEncodingFilter这个类
@ConditionalOnProperty(prefix = "spring.http.encoding", value = "enabled", matchIfMissing = true) //判断配置文件中是否存在"spring.http.encoding"这个个配置，matchIfMissing = true如果不存在也是默认存在的。如果配置文件中不配置spring.http.encoding，这个配置类也是生效的！
public class HttpEncodingAutoConfiguration {
```

- 所有在配置文件中能配置的属性都是在【xxxProperties】类中封装，配置文件能配置什么就可以参照某个功能对应的这个属性类。
- **XXXAutoConfiguration是自动配置类，它会给容器中添加组件，然后也会对应的XXXProperties，封装配置文件的相关属性。**

## 3.2.@Conditional

**@Conditional是Spring中的注解，作用是@Conditional指定的条件成立，才给容器中添加组件，配置类里面的所有内容才会生效。**

| @Conditional扩展注解            | 作用（判断是否满足当前指定条件）                 |
| ------------------------------- | ------------------------------------------------ |
| @ConditionalOnJava              | 系统的Java版本是否符合要求                       |
| @ConditionalOnBean              | 容器中存在指定的Bean                             |
| @ConditionalOnMissingBean       | 容器中不存在指定的Bean                           |
| @ConditionalOnExpression        | 满足SpEL表达式                                   |
| @ConditionalOnClass             | 系统中有指定的类                                 |
| @ConditionalOnMissingClass      | 系统中没有指定的类                               |
| @ConditionalOnSingleCondidate   | 容器中只有一个指定的Bean，或者这个Bean是首选Bean |
| @ConditionalOnProperty          | 系统中指定的属性是否有指定的值                   |
| @ConditionalOnResource          | 类路径下是否存在指定资源文件                     |
| @ConditionalOnWebApplication    | 当前是Web环境                                    |
| @ConditionalOnNotWebApplication | 当前不是Web环境                                  |

**一句话：自动配置类必须在一定条件下才能生效。**

> 我们怎么知道哪些自动配置类生效？？

```yaml
# 1、在SpringBoot的配置文件中加入如下配置就可以打印出自动配置报告
debug: true

# 2、在应用启动的时候就会出现"项目评估报告"，就可以查看启用了哪些AutoConfiguration
============================
CONDITIONS EVALUATION REPORT
============================


Positive matches:
-----------------

   AopAutoConfiguration matched:
      - @ConditionalOnProperty (spring.aop.auto=true) matched (OnPropertyCondition)

   AopAutoConfiguration.ClassProxyingConfiguration matched:
      - @ConditionalOnMissingClass did not find unwanted class 'org.aspectj.weaver.Advice' (OnClassCondition)
      - @ConditionalOnProperty (spring.aop.proxy-target-class=true) matched (OnPropertyCondition)

   DispatcherServletAutoConfiguration matched:
      - @ConditionalOnClass found required class 'org.springframework.web.servlet.DispatcherServlet' (OnClassCondition)
      - found 'session' scope (OnWebApplicationCondition)

   DispatcherServletAutoConfiguration.DispatcherServletConfiguration matched:
      - @ConditionalOnClass found required class 'javax.servlet.ServletRegistration' (OnClassCondition)
      - Default DispatcherServlet did not find dispatcher servlet beans (DispatcherServletAutoConfiguration.DefaultDispatcherServletCondition)

```

# 4.日志

## 4.1.日志框架

左边选一个日志门面（抽象层），右边选一个来实现！

| 日志门面(日志的抽象层)                                       | 日志的实现                  |
| ------------------------------------------------------------ | --------------------------- |
| ~~**JCL(Jakarta Commons Logging)**~~、SLF4j(Simple Logging  Facade For Java)、~~**jboss-logging**~~ | Log4j、JUL、Log4j2、Logback |

- 日志框架的选择：
  - 日志门面：SLF4j。
  - 日志实现：Logback。

- SpringBoot底层是Spring框架，Spring框架默认使用`JCL`；SpringBoot选用的日志框架是`SLF4j`和`Logback`。

## 4.2.SLF4j的使用

> 基本使用

以后开发的时候，日志记录方法的调用，不应该直接调用日志的实现类，而是调用日志抽象层的方法。

给系统中导入SLF4j的jar和Logback的jar。

```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorld {
  public static void main(String[] args) {
    Logger logger = LoggerFactory.getLogger(HelloWorld.class);
    logger.info("Hello World");
  }
}
```

## 4.3.SLF4j的使用原理

> SLF4j适配其他日志框架

每一个日志的实现框架都有自己的配置文件。使用SLF4j以后，**配置文件还是做成日志实现框架的配置文件。**

![SLF4j使用原理](SpringBoot.assets/concrete-bindings.png)

## 4.4.统一日志框架

问题：开发A系统使用SLF4j + Logback，但是使用了Spring（Commons-logging）、Hibernate（jBoss-logging）、MyBatis。。。。所以，要统一日志框架！即使是别的日志框架，和A系统一起使用SLF4j和Logback一起输出。

![统一日志框架](SpringBoot.assets/legacy.png)

**如何让系统所有的日志框架都统一到SLF4j？**

1、将系统中其他日志框架先排除。

2、用中间的jar来替换原有的日志框架。

3、我们再来导入SLF4j其他的日志实现。

## 4.4.SpringBoot日志关系

> SpringBoot日志依赖

![SpringBoot日志依赖](SpringBoot.assets/20200708152815377.png)

- `log4j-to-slf4j`、`logback-classic`、`jul-to-slf4j`把其他的日志框架转成`slf4j`。
- `slf4j-api`是SpringBoot导入了日志抽象层SLF4J。

**如果我们要引入其他框架？一个要把这个框架默认的日志依赖移除掉？**

**SpringBoot能自动适配所有的日志，而且底层使用slf4j + logback的方式记录日志，引入其他框架的时候，只需要把这个框架依赖的日志框架排除掉即可。**

## 4.5.SpringBoot日志使用

> 日志级别

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class LogTest {

    private Logger logger = LoggerFactory.getLogger(getClass());

    /**
     * 日志的级别由低到高：trace < debug < info < warn < error
     * 可以调整项目日志级别,日志就只会在这个级别以后的级别生效。
     * SpringBoot默认的日志级别是Info
     */
    @Test
    public void testLogLevel() {
        logger.trace("*****trance日志*****");
        logger.debug("*****debug日志*****");
        logger.info("*****info日志*****");
        logger.warn("*****warn日志*****");
        logger.error("*****error日志*****");
    }
}
```

> 日志级别的调整和日志输出的位置

```yaml
# 1、com.ymy.spring.boot.log 这个包下的日志都会输入出trace和trace以上的日志了！！
logging:
  level:
    com.ymy.spring.boot.log: trace

# 2、默认情况下日志只会打印到控制台上,配置logging.file.name会在当前项目下输出日志
# 不指定路径会在当前项目下生产日志文件,指定路径会在指定路径下生成日志
  file:
    name: C:/Users/14666/Desktop/springboot.log
# 3、logging.file.path 生成的日志文件默认为spring.log，只需要写日志文件路径
  file:
    path: C:/Users/14666/Desktop/log/
```

# 5.Web开发

## 5.1.静态资源映射规则

### 5.1.1.webjars静态资源的映射

关于SpringBoot静态资源的映射规则在`WebMvcAutoConfiguration`中。

```java
@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    if (!this.resourceProperties.isAddMappings()) {
        logger.debug("Default resource handling disabled");
        return;
    }
    Duration cachePeriod = this.resourceProperties.getCache().getPeriod();
    CacheControl cacheControl = this.resourceProperties.getCache().getCachecontrol().toHttpCacheControl();
    if (!registry.hasMappingForPattern("/webjars/**")) {
        customizeResourceHandlerRegistration(registry.addResourceHandler("/webjars/**")
                                             .addResourceLocations("classpath:/META-INF/resources/webjars/")
                                             .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
    }
    String staticPathPattern = this.mvcProperties.getStaticPathPattern();
    if (!registry.hasMappingForPattern(staticPathPattern)) {
        customizeResourceHandlerRegistration(registry.addResourceHandler(staticPathPattern)
                                             .addResourceLocations(getResourceLocations(this.resourceProperties.getStaticLocations()))
                                             .setCachePeriod(getSeconds(cachePeriod)).setCacheControl(cacheControl));
    }
}
```

**静态资源映射规则：**

- 所有`/webjars/**`的请求都去`classpath:/META-INF/resources/webjars/`这个目录下找资源。webjars就是以jar的方式引入静态资源。可以百度搜索webjars，在pom中添加相应的依赖就可以了。

### 5.1.2.ResourceProperties静态资源映射

> ResourceProperties

```java
@ConfigurationProperties(prefix = "spring.resources", ignoreUnknownFields = false)
public class ResourceProperties {

	private static final String[] CLASSPATH_RESOURCE_LOCATIONS = { "classpath:/META-INF/resources/",
			"classpath:/resources/", "classpath:/static/", "classpath:/public/" };
```

**静态资源映射规则：**

- 所有访问`/**`的请求都会去`classpath:/META-INF/resources/`、`classpath:/resources/`、`classpath:/static/`、`classpath:/public/`这些路径下找资源。

> 测试访问静态资源



![image-20230310195958800](SpringBoot.assets/image-20230310195958800.png)

**浏览器输入http://localhost:8080/asserts/css/bootstrap.min.css就可以访问静态资源。**

### 5.1.3.欢迎页映射规则

静态资源文件夹下的所有`index.html`页面，被`/**`映射。

静态资源文件夹：`classpath:/META-INF/resources/`、`classpath:/resources/`、`classpath:/static/`、`classpath:/public/`。

浏览器访问`localhost:8080/index.html`会去静态资源文件夹将下找这个html页面。

### 5.1.4.图标映射规则

所有的`**/favicon.ico`都是在静态资源文件夹下找。

## 5.2.thymeleaf

### 5.2.1.引入thymeleaf

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

### 5.2.2.thymeleaf的使用

**ThymeleafProperties可以修改thymeleaf的配置。**

```java
@ConfigurationProperties(prefix = "spring.thymeleaf")
public class ThymeleafProperties {

	private static final Charset DEFAULT_ENCODING = StandardCharsets.UTF_8;

    // 只要我们把HTML页面放到"classpath:/templates/"下，thymeleaf就能找到
	public static final String DEFAULT_PREFIX = "classpath:/templates/";

    // 并且配置了默认的后缀是.html
	public static final String DEFAULT_SUFFIX = ".html";
```

> thymeleaf语法

```html
<!--1、导入thymeleaf名称空间-->
<html lang="en" xmlns:th="http://www.thymeleaf.org"></html>

<!--2、thymeleaf语法-->

<!--
th:text 将div里面的文本内容设置为我们指定的值;
可以使用[th:任意属性]来替换原生HTML属性的值.
-->
<div th:text="${hello}"></div>

<!--片段包含-->
th:insert   
th:replcae

<!--遍历-->
th:each

<!--判断-->
th:if
th:unless
th:switch
th:case

<!--声明变量-->
th:object
th:with

<!--属性修改-->
th:attr
th:attrprepend
th:attrappend

<!--修改指定属性默认值-->
th:value
th:href
th:src
...

<!--修改标签体内容-->
th:text
th:utext   不转义特殊字符

<!--声明片段-->
th:fragment

<!--移除片段-->
th:remove
```

> thymeleaf表达式语法

```properties
1.Simple expressions(表达式语法):
	1.1.Variable Expressions: ${...}              # 获取变量表达式
		(1)获取对象的属性、调用方法；
		(2)使用内置的基本对象(${#locale.country})
			#ctx : the context object. 
			#vars: the context variables. 
			#locale : the context locale. 
			#request : (only in Web Contexts) the HttpServletRequest object. 
			#response : (only in Web Contexts) the HttpServletResponse object. 
			#session : (only in Web Contexts) the HttpSession object. 
			#servletContext : (only in Web Contexts) the ServletContext object.
		(3)使用内置的工具对象
			#execInfo : information about the template being processed. 
			#messages : methods for obtaining externalized messages inside variables expressions, in the same way as they would be obtained using #{…} syntax. 
			#uris : methods for escaping parts of URLs/URIs #conversions : methods for executing the configured conversion service (if any). 
			#dates : methods for java.util.Date objects: formatting, component extraction, etc. 
			#calendars : analogous to #dates , but for java.util.Calendar objects. 
			#numbers : methods for formatting numeric objects. 
			#strings : methods for String objects: contains, startsWith, prepending/appending, etc. 
			#objects : methods for objects in general. 
			#bools : methods for boolean evaluation. #arrays : methods for arrays. 
			#lists : methods for lists. 
			#sets : methods for sets. 
			#maps : methods for maps. 
			#aggregates : methods for creating aggregates on arrays or collections. 
			#ids : methods for dealing with id attributes that might be repeated (for example, as a result of an iteration).
	
	1.2.Selection Variable Expressions: *{...}    # 变量的选择表达式,和${}在功能上是一样的，只不过有补充
		(1)补充：配合 th:object="${session.user}" 使用
	
	1.3.Message Expressions: #{...}    # 获取国际化内容的        
	1.4.Link URL Expressions: @{...}   # 定义URL链接 
	1.5.Fragment Expressions: ~{...}       # 片段引用表达式 

2.Literals(字面量)：
    2.1.Text literals: 'one text' , 'Another one!' ,… 
    2.2.Number literals: 0 , 34 , 3.0 , 12.3 ,… 
    2.3.Boolean literals: true , false 
    2.4.Null literal: null 
    2.5.Literal tokens: one , sometext , main ,…

3.Text operations(文本操作):
    3.1.String concatenation: + 
    3.2.Literal substitutions: |The name is ${name}|

4.Arithmetic operations(数学运算):
    4.1.Binary operators: + , - , * , / , % 
    4.2.Minus sign (unary operator): -

5.Boolean operations(布尔操作):
    5.1.Binary operators: and , or 
    5.2.Boolean negation (unary operator): ! , not

6.Comparisons and equality(比较运算):
	6.1.Comparators: > , < , >= , <= ( gt , lt , ge , le ) 
	6.2.Equality operators: == , != ( eq , ne )

7.Conditional operators(条件运算):
	7.1.If-then: (if) ? (then) 
	7.2.If-then-else: (if) ? (then) : (else) 
	7.3.Default: (value) ?: (defaultvalue)

8.Special tokens(特殊操作):
	8.1No-Operation: _
```

## 5.3.SpringMVC自动配置原理

**官网链接：https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-auto-configuration**

Spring Boot provides auto-configuration for Spring MVC that works well with most applications.

The auto-configuration adds the following features on top of Spring’s defaults:

- Inclusion of `ContentNegotiatingViewResolver` and `BeanNameViewResolver` beans.

  - SpringBoot自动配置了ViewResolver，视图解析器，根据方法的返回值得到视图对象，决定如何渲染(转发、重定向)。
  - `ContentNegotiatingViewResolver`：作用就是组合所有的视图解析器。
  - 如何定制视图解析器：我们可以在容器中添加一个`ViewResolver`视图解析器，`ContentNegotiatingViewResolver` 就会自动的将我们的视图解析器组合进来

- Support for serving static resources, including support for WebJars (covered [later in this document](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-static-content))).

- Automatic registration of `Converter`, `GenericConverter`, and `Formatter` beans.

  - `Converter`：转换器，对象类型转换使用`Converter`组件。
  - `Formatter` ：格式化器，2020-12-17需要转化成日期类型，就需要使用格式化器。
  - 自己添加的`Converter`和`Formatter` 只需要放在容器中即可。

- Support for `HttpMessageConverters` (covered [later in this document](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-message-converters)).

  - `HttpMessageConverters`：SpringMVC用来转换Http请求和响应的`HttpMessageConverter集合，可以获取容器中所有的`HttpMessageConverter`。
  - 添加自己的`HttpMessageConverter`，只需要将组件加入到容器即可。																		

- Automatic registration of `MessageCodesResolver` (covered [later in this document](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-message-codes)).

  - `MessageCodesResolver` ：用来定义错误代码的生成规则。

- Static `index.html` support.

- Custom `Favicon` support (covered [later in this document](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-favicon)).

- Automatic use of a `ConfigurableWebBindingInitializer` bean (covered [later in this document](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/spring-boot-features.html#boot-features-spring-mvc-web-binding-initializer)).

  - 我们可以配置一个`ConfigurableWebBindingInitializer` 添加到容器来替换默认的。

    ```java
    @Override
    protected ConfigurableWebBindingInitializer getConfigurableWebBindingInitializer(
        FormattingConversionService mvcConversionService, Validator mvcValidator) {
        try {
            // 从容器中拿ConfigurableWebBindingInitializer
            return this.beanFactory.getBean(ConfigurableWebBindingInitializer.class);
        }
        catch (NoSuchBeanDefinitionException ex) {
            // 从容器中拿不到就调用父类的方法
            return super.getConfigurableWebBindingInitializer(mvcConversionService, mvcValidator);
        }
    }
    ```

  - `ConfigurableWebBindingInitializer` ：数据绑定器的作用是**将请求数据绑定到JavaBean中**。

**扩展SpringMVC：**If you want to keep those Spring Boot MVC customizations and make more [MVC customizations](https://docs.spring.io/spring/docs/5.2.3.RELEASE/spring-framework-reference/web.html#mvc) (interceptors, formatters, view controllers, and other features), you can add your own `@Configuration` class of type `WebMvcConfigurer` but **without** `@EnableWebMvc`.

**完全接管SpringMVC：**If you want to take complete control(完全控制) of Spring MVC, you can add your own `@Configuration` annotated with `@EnableWebMvc`, or alternatively(或者)add your own `@Configuration`-annotated `DelegatingWebMvcConfiguration` as described in the Javadoc of `@EnableWebMvc`.

If you want to provide custom instances of `RequestMappingHandlerMapping`, `RequestMappingHandlerAdapter`, or `ExceptionHandlerExceptionResolver`, and still keep the Spring Boot MVC customizations, you can declare a bean of type `WebMvcRegistrations` and use it to provide custom instances of those components.

## 5.4.国际化

### 5.4.1.编写国际化配置文件

![国际化配置文件](SpringBoot.assets/20200709124522243.png)



### 5.4.2.国际化相关的组件

> SpringBoot自动配置好了国际化相关的组件

```java
@Configuration(proxyBeanMethods = false)
@ConditionalOnMissingBean(name = AbstractApplicationContext.MESSAGE_SOURCE_BEAN_NAME, search = SearchStrategy.CURRENT)
@AutoConfigureOrder(Ordered.HIGHEST_PRECEDENCE)
@Conditional(ResourceBundleCondition.class)
@EnableConfigurationProperties
public class MessageSourceAutoConfiguration {

	private static final Resource[] NO_RESOURCES = {};

	@Bean
	@ConfigurationProperties(prefix = "spring.messages")
	public MessageSourceProperties messageSourceProperties() {
        /* MessageSourceProperties中的basename默认是"message"
        * 我们项目中的basename就是login，去掉后面的"语言名"和"国家名"
        */
		return new MessageSourceProperties();
	}

	@Bean
	public MessageSource messageSource(MessageSourceProperties properties) {
		ResourceBundleMessageSource messageSource = new ResourceBundleMessageSource();
		if (StringUtils.hasText(properties.getBasename())) {
            // 设置国际化文件的basename
			messageSource.setBasenames(StringUtils
					.commaDelimitedListToStringArray(StringUtils.trimAllWhitespace(properties.getBasename())));
		}
		if (properties.getEncoding() != null) {
			messageSource.setDefaultEncoding(properties.getEncoding().name());
		}
		messageSource.setFallbackToSystemLocale(properties.isFallbackToSystemLocale());
		Duration cacheDuration = properties.getCacheDuration();
		if (cacheDuration != null) {
			messageSource.setCacheMillis(cacheDuration.toMillis());
		}
		messageSource.setAlwaysUseMessageFormat(properties.isAlwaysUseMessageFormat());
		messageSource.setUseCodeAsDefaultMessage(properties.isUseCodeAsDefaultMessage());
		return messageSource;
	}
```

> 在application.yml中修改SpringBoot国际化相关的basename

```yaml
spring:
  messages:
# 修改basename
    basename: i18n.login 
```

> 去HTML页面获取国际化的值

```html
<h1 class="h3 mb-3 font-weight-normal" th:text="#{login.tip}">Please sign in</h1>

<label class="sr-only" th:text="#{login.username}">Username</label>
<input type="text" class="form-control" th:placeholder="#{login.username}" required="" autofocus="">
<label class="sr-only" th:text="#{login.password}">Password</label>
<input type="password" class="form-control" th:placeholder="#{login.password}" required="">

<label>
    <input type="checkbox" value="remember-me"> [[#{login.remember}]]
</label>

<button class="btn btn-lg btn-primary btn-block" type="submit" th:text="#{login.button}">Sign in</button>
```

### 5.4.3.区域信息解析器

> 默认LocaleResolver

```java
// WebMvcAutoConfiguration中配置的区域信息解析器
// 默认的区域信息解析器是根据Http请求的请求头来获取Locale进行国际化
@Bean
@ConditionalOnMissingBean
@ConditionalOnProperty(prefix = "spring.mvc", name = "locale")
public LocaleResolver localeResolver() {
    if (this.mvcProperties.getLocaleResolver() == WebMvcProperties.LocaleResolver.FIXED) {
        return new FixedLocaleResolver(this.mvcProperties.getLocale());
    }
    AcceptHeaderLocaleResolver localeResolver = new AcceptHeaderLocaleResolver();
    localeResolver.setDefaultLocale(this.mvcProperties.getLocale());
    return localeResolver;
}
```

> 自定义LocaleResolver

```java
/**
 * 自定义的login.html的区域信息解析器
 * 根据请求来解析地区，可以实现点击切换语言的功能
 */
public class LoginLocaleResolver implements LocaleResolver {
    @Override
    public Locale resolveLocale(HttpServletRequest request) {
        Locale locale = Locale.getDefault();
        // LoginConstant.PARAM_KEY 是 language
        String language = request.getParameter(LoginConstant.PARAM_KEY);
        if (!StringUtils.isEmpty(language)) {
            String[] split = language.split("_");
            locale = new Locale(split[0], split[1]);
        }
        return locale;
    }
}
```

login.html页面中发送的请求

```html
<a class="btn btn-sm" th:href="@{/index.html(language=zh_CN)}">中文</a>
<a class="btn btn-sm" th:href="@{/index.html(language=en_US)}">English</a>
```

在配置类中添加自定义的区域信息解析器

```java
/**
     * 自定义区域信息解析器
     * @return
     */
@Bean
public LocaleResolver localeResolver() {
    return new LoginLocaleResolver();
}
```

## 5.5.登录拦截器

> 拦截器

```java
/**
 * 登录拦截器
 */
public class LoginHandlerInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        Object key = request.getSession().getAttribute(LoginConstant.LOGIN_SESSION_KEY);
        if (key == null) {
            // 未登录返回到登录页面
            request.setAttribute("message", "没有权限,请先登录");
            request.getRequestDispatcher("/index.html").forward(request, response);
            return false;
        }else {
            // 已经登录,方向请求
            return true;
        }
    }
}
```

> 将拦截器加入容器

```java
/**
 * SpringMVC的扩展配置
 */
@Configuration
public class WebMvcConf implements WebMvcConfigurer {

    /**
     * 配置拦截器
     */
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginHandlerInterceptor())
                .addPathPatterns("/**")
                // 排除登录、首页、静态资源路径
                .excludePathPatterns("/","/index","/index.html", LoginConstant.LOGIN_PATH, "/asserts/**" );
    }
}
```

## 5.6.RESTfulAPI

> 基本请求模板

| 行为 | 请求方式 | URL       |
| ---- | -------- | --------- |
| 查询 | GET      | /emp      |
| 添加 | POST     | /emp      |
| 修改 | PUT      | /emp/{id} |
| 删除 | DELETE   | /emp/{id} |

> 实验请求架构

| 行为         | 请求方式 | URL       |
| ------------ | -------- | --------- |
| 查询所有员工 | GET      | /emps     |
| 查询某个员工 | GET      | /emp/{id} |
| 来到添加页面 | GET      | /emp      |
| 添加员工     | POST     | /emp/{id} |
| 来到修改页面 | GET      | /emp/{id} |
| 修改某个员工 | PUT      | /emp/{id} |
| 删除员工     | DELETE   | /emp/{id} |

## 5.7.数据列表展示

### 5.7.1.thymeleaf公共元素抽取

```html
<!--1、抽取公共片段-->
<div th:fragment="copy">      
    &copy; 2011 The Good Thymes Virtual Grocery    
</div> 

<!--1、插入公共片段-->
~{templatename::fragmentname} ：模板名，片段名

<div th:insert="~{footer :: copy}"></div>
```

**三种引入公共片段的th属性：**

- `th:insert` is the simplest: it will simply insert the specified fragment as the body of its host tag.
  - 将公共片段整个插入到声明的元素中。
- `th:replace` actually replaces its host tag with the specified fragment.
  - 将声明的元素替换为公共片段。
- `th:include` is similar to th:insert , but instead of inserting the fragment it only inserts the contents of this fragment.
  - 将公共片段的内容包含到声明的元素中

```html
<!--抽取的公共片段-->
<footer th:fragment="copy">  
    &copy; 2011 The Good Thymes Virtual Grocery 
</footer>

<!--三种引入公共片段的方式-->
<body>
  ...
  <div th:insert="footer :: copy"></div>
  <div th:replace="footer :: copy"></div>
  <div th:include="footer :: copy"></div> 
</body>


<!--三种方式的效果-->
<body>
  ...
  <div>    
      <footer>      
          &copy; 2011 The Good Thymes Virtual Grocery    
      </footer>  
  </div>
  <footer>    
      &copy; 2011 The Good Thymes Virtual Grocery  
  </footer>
  <div>    
      &copy; 2011 The Good Thymes Virtual Grocery  
   </div>  
</body
```

### 5.8.2.SideBar链接高亮

```html
<!--1、sidebar片段加入判断！-->
<li class="nav-item">
    <a th:href="@{/main.html}"
       th:class="${activeUri=='main.html' ? 'nav-link active' : 'nav-link'}">
       Dashboard
    </a>
</li>

<li class="nav-item">
    <a th:href="@{/emps}"
       th:class="${activeUri=='emps' ? 'nav-link active' : 'nav-link'}">
       员工管理
    </a>
</li>

<!--2、DashBoard引入sidebar添加activeUri='main.html'-->
<div th:replace="fragments/SideBar :: sidebar(activeUri='main.html')"></div>

<!--3、list引入sidebar添加activeUri='emps'-->
<div th:replace="fragments/SideBar :: sidebar(activeUri='emps')"></div>
```

## 5.8.日期格式

日期格式有2020-7-10，2020/7/10，2020.7.10；SpringMVC将页面提交的值需要转换为指定的类型；

**SpringMVC默认是使用2020/7/10的格式**。

```yaml
# 修改SpringMVC默认的日期格式 yaml修改即可
spring:
  mvc:
    date-format: yyyy-MM-dd
```

# 6.错误处理机制

## 6.1.SpringBoot默认错误处理机制

- 浏览器访问，默认返回一个错误页面。

- 如果是APP访问，默认响应一个json数据

- 原理：参照`ErrorMvcAutoConfiguration`。给容器添加了以下组件

  ```java
  // DefaultErrorAttributes 帮我们在页面共享信息
  @Bean
  @ConditionalOnMissingBean(value = ErrorAttributes.class, search = SearchStrategy.CURRENT)
  public DefaultErrorAttributes errorAttributes() {
      return new DefaultErrorAttributes(this.serverProperties.getError().isIncludeException());
  }
  
  @Bean
  @ConditionalOnMissingBean(value = ErrorController.class, search = SearchStrategy.CURRENT)
  public BasicErrorController basicErrorController(ErrorAttributes errorAttributes,
                                                   ObjectProvider<ErrorViewResolver> errorViewResolvers) {
      return new BasicErrorController(errorAttributes, this.serverProperties.getError(),
                                      errorViewResolvers.orderedStream().collect(Collectors.toList()));
  }
  
  @Bean
  public ErrorPageCustomizer errorPageCustomizer(DispatcherServletPath dispatcherServletPath) {
      return new ErrorPageCustomizer(this.serverProperties, dispatcherServletPath);
  }
  
  @Bean
  @ConditionalOnBean(DispatcherServlet.class)
  @ConditionalOnMissingBean(ErrorViewResolver.class)
  DefaultErrorViewResolver conventionErrorViewResolver() {
      return new DefaultErrorViewResolver(this.applicationContext, this.resourceProperties);
  }
  ```

- 执行步骤

  ```java
  // 1、一旦出现4xx或者5xx的错误ErrorPageCustomizer(定制错误的响应规则)就会生效。
  // ErrorPageCustomizer会拿到path。
  @Value("${error.path:/error}")
  private String path = "/error";   // 系统出现错误后会来到/error请求进行处理
  
  // 2、BasicErrorController处理默认/error请求
  @Controller
  @RequestMapping("${server.error.path:${error.path:/error}}")
  public class BasicErrorController extends AbstractErrorController {
      // MediaType.TEXT_HTML_VALUE = "text/html"
      // 该方法就是产生HTML的数据
      // 浏览器发送的请求来到这个方法处理
      @RequestMapping(produces = MediaType.TEXT_HTML_VALUE)
      public ModelAndView errorHtml(HttpServletRequest request, HttpServletResponse response) {
          HttpStatus status = getStatus(request);
          Map<String, Object> model = Collections
              .unmodifiableMap(getErrorAttributes(request, isIncludeStackTrace(request, MediaType.TEXT_HTML)));
          response.setStatus(status.value());
  
          // 去哪个页面作为错误页面，包含页面地址和页面内容
          ModelAndView modelAndView = resolveErrorView(request, response, status, model);
          return (modelAndView != null) ? modelAndView : new ModelAndView("error", model);
      }
  
      protected ModelAndView resolveErrorView(HttpServletRequest request, HttpServletResponse response,   HttpStatus status,Map<String, Object> model) {
          // 所有的ErrorViewResolver得到ModelAndView
          for (ErrorViewResolver resolver : this.errorViewResolvers) {
              ModelAndView modelAndView = resolver.resolveErrorView(request, status, model);
              if (modelAndView != null) {
                  return modelAndView;
              }
          }
          return null;
      }
  
      // 产生json数据
      // 其他客户端发送的请求来到这个方法处理
      @RequestMapping
      public ResponseEntity<Map<String, Object>> error(HttpServletRequest request) {
          HttpStatus status = getStatus(request);
          if (status == HttpStatus.NO_CONTENT) {
              return new ResponseEntity<>(status);
          }
          Map<String, Object> body = getErrorAttributes(request, isIncludeStackTrace(request, MediaType.ALL));
          return new ResponseEntity<>(body, status);
      }
  }
  
  // 3、DefaultErrorViewResolver来得到ModelAndview
  public class DefaultErrorViewResolver implements ErrorViewResolver, Ordered {
  
      private static final Map<Series, String> SERIES_VIEWS;
  
      static {
          Map<Series, String> views = new EnumMap<>(Series.class);
          views.put(Series.CLIENT_ERROR, "4xx");
          views.put(Series.SERVER_ERROR, "5xx");
          SERIES_VIEWS = Collections.unmodifiableMap(views);
      }
  
      @Override
      public ModelAndView resolveErrorView(HttpServletRequest request, HttpStatus status, Map<String, Object> model) {
          ModelAndView modelAndView = resolve(String.valueOf(status.value()), model);
          if (modelAndView == null && SERIES_VIEWS.containsKey(status.series())) {
              modelAndView = resolve(SERIES_VIEWS.get(status.series()), model);
          }
          return modelAndView;
      }
  
      private ModelAndView resolve(String viewName, Map<String, Object> model) {
          // SpringBoot可以在error目录下找到页面
          String errorViewName = "error/" + viewName;
  
          // 如果模板引擎能解析这个地址，就用模板引擎解析
          TemplateAvailabilityProvider provider = this.templateAvailabilityProviders.getProvider(errorViewName,
                                                                                                 this.applicationContext);
          if (provider != null) {
              // 模板引擎可用的情况下返回到指定view视图地址
              return new ModelAndView(errorViewName, model);
          }
          // 模板引擎不可用调用resolveResource()，在静态资源文件夹下找errorViewName对应的页面 error/404.html
          return resolveResource(errorViewName, model);
      }
  
      private ModelAndView resolveResource(String viewName, Map<String, Object> model) {
          for (String location : this.resourceProperties.getStaticLocations()) {
              try {
                  Resource resource = this.applicationContext.getResource(location);
                  resource = resource.createRelative(viewName + ".html");
                  if (resource.exists()) {
                      return new ModelAndView(new HtmlResourceView(resource), model);
                  }
              }
              catch (Exception ex) {
              }
          }
          return null;
      }
  }
  ```




## 6.2.如何定制错误的响应？

### 6.2.1定制错误页面

- 有模板引擎的情况下，直接在`templates`下创建`error`文件夹。`error`文件夹下面的`HttpStatus.html`(需要用状态码给错误页面命名)就可以被解析返回给浏览器。

  - 错误页面可以获取到的信息？`DefaultErrorAttributes`可以帮我们在页面获取信息！

    ```java
    @Override
    public Map<String, Object> getErrorAttributes(WebRequest webRequest, boolean includeStackTrace) {
     Map<String, Object> errorAttributes = new LinkedHashMap<>();
     // 1、可以在错误页面获取到时间戳
     errorAttributes.put("timestamp", new Date());
     // 2、可以在错误页面获取到状态码
     addStatus(errorAttributes, webRequest);
     // 1、可以在错误页面获取到错误信息 Exception对象 Exception的Message Errors(JSR303数据校验的信息)
     addErrorDetails(errorAttributes, webRequest, includeStackTrace);
     addPath(errorAttributes, webRequest);
     return errorAttributes;
        
    }
    ```

- 没有模板引擎，就会在静态资源文件夹下找error/404.html。

- 模板引擎和静态资源文件夹下都没有自己写的错误页面，就会来到SpringBoot默认的错误页面。

### 6.2.2.定制错误数据

> @ControllerAdvice

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotExistException.class)
    public String handelException(HttpServletRequest request, Exception ex) {
        // 传入我们自己的状态码，这个一定要写
        request.setAttribute("javax.servlet.error.status_code", 400);
        Map<String, Object> map = new HashMap<>();
        map.put("tip", "自定义的全局异常处理器");
        // 将Map放在请求域中
        request.setAttribute("ext", map);
        return "forward:/error";
    }
}
```

> 将我们定制的错误信息携带出去

```java
package com.ymy.spring.boot.web.component;

import org.springframework.boot.web.servlet.error.DefaultErrorAttributes;
import org.springframework.stereotype.Component;
import org.springframework.web.context.request.RequestAttributes;
import org.springframework.web.context.request.WebRequest;

import java.util.Map;
// 自己写的ErrorAttributes
@Component
public class MyErrorAttribute extends DefaultErrorAttributes {
    @Override
    public Map<String, Object> getErrorAttributes(WebRequest webRequest, boolean includeStackTrace) {
        Map<String, Object> map = super.getErrorAttributes(webRequest, includeStackTrace);
        // 可以从请求域中获取map
        Map ext = (Map)webRequest.getAttribute("ext", RequestAttributes.SCOPE_REQUEST);
        map.put("ext", ext);
        return map;
    }
}
```

# 7.数据访问(框架整合)

## 7.1.Spring Data简介

对于数据访问层，无论是`SQL`还是`NoSQL` ，`Spring Boot`默认采用整合`Spring Data`的方式进行统一管理，添加大量自动配置，屏蔽了很多设置。引入各种`Template`，`Repository`来简化我们対数据访问层的操作。对我们来说只需要进行简单的设置即可。

## 7.2.JDBC

> 依赖

```xml
<!--jdbc-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<!--mysql驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```

> application.yml配置

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: 333
    url:  jdbc:mysql://39.97.3.60:3306/jdbc?characterEncoding=utf8&useSSL=false&serverTimezone=UTC
    type: com.mysql.cj.jdbc.MysqlConnectionPoolDataSource
```

## 7.3.Druid

### Druid简介

Java程序很大一部分要操作数据库，为了提高性能操作数据库的时候，又不得不使用数据库连接池。

Druid 是阿里巴巴开源平台上一个数据库连接池实现，结合了 C3P0、DBCP 等 DB 池的优点，同时加入了日志监控。

Druid 可以很好的监控 DB 池连接和 SQL 的执行情况，天生就是针对监控而生的 DB 连接池。

Druid已经在阿里巴巴部署了超过600个应用，经过一年多生产环境大规模部署的严苛考验。

Spring Boot 2.0 以上默认使用 Hikari 数据源，可以说 Hikari 与 Driud 都是当前 Java Web 上最优秀的数据源，我们来重点介绍 Spring Boot 如何集成 Druid 数据源，如何实现数据库监控。

Github地址：https://github.com/alibaba/druid/

> 依赖

```xml
<!--druid-->
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>druid</artifactId>
    <version>${druid.version}</version>
</dependency>

<!--jdbc-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>

<!--mysql驱动-->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
</dependency>
```

> 配置Druid

```yaml
# application.yml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    username: root
    password: 333
    url:  jdbc:mysql://39.97.3.60:3306/jdbc?characterEncoding=utf8&useSSL=false&serverTimezone=UTC
    type: com.alibaba.druid.pool.DruidDataSource
    
    #最大连接池数量
    max-active: 20
    #初始化时建立物理连接的个数。初始化发生在显示调用init方法，或者第一次getConnection时
    initial-size: 10
    # 获取连接时最大等待时间，单位毫秒。配置了maxWait之后，缺省启用公平锁，
    # 并发效率会有所下降，如果需要可以通过配置useUnfairLock属性为true使用非公平锁。
    max-wait: 60000
    #最小连接池数量
    min-idle: 5
    #有两个含义：
    #1: Destroy线程会检测连接的间隔时间
    #2: testWhileIdle的判断依据，详细看testWhileIdle属性的说明
    time-between-eviction-runs-millis: 60000
    #配置一个连接在池中最小生存的时间，单位是毫秒
    min-evictable-idle-time-millis: 180000
    #用来检测连接是否有效的sql，要求是一个查询语句。如果validationQuery为null，testOnBorrow、testOnReturn、testWhileIdle都不会其作用。
    validation-query: select 'x'
    #连接有效性检查的超时时间 1 秒
    validation-query-timeout: 1
    #申请连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能。
    test-on-borrow: false
    #设置从连接池获取连接时是否检查连接有效性，true时，如果连接空闲时间超过minEvictableIdleTimeMillis进行检查，否则不检查;false时，不检查
    test-while-idle: true
    #归还连接时执行validationQuery检测连接是否有效，做了这个配置会降低性能
    test-on-return: false
    #是否缓存preparedStatement，也就是PSCache。PSCache对支持游标的数据库性能提升巨大，比如说oracle。在mysql下建议关闭。
    pool-prepared-statements: true
    #要启用PSCache，必须配置大于0，当大于0时，poolPreparedStatements自动触发修改为true。在Druid中，
    # 不会存在Oracle下PSCache占用内存过多的问题，可以把这个数值配置大一些，比如说100
    max-open-prepared-statements: 20
    #数据库链接超过3分钟开始关闭空闲连接 秒为单位
    remove-abandoned-timeout: 1800
    #对于长时间不使用的连接强制关闭
    remove-abandoned: true
    #打开后，增强timeBetweenEvictionRunsMillis的周期性连接检查，minIdle内的空闲连接，
    keep-alive: true
    # 通过connectProperties属性来打开mergeSql功能；慢SQL记录
    connect-properties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=5000
    #是否超时关闭连接 默认为false ,若为true 就算数据库恢复连接，也无法连接上
    break-after-acquire-failure: false
    #设置获取连接出错时的自动重连次数
    connection-error-retry-attempts: 1
    #设置获取连接时的重试次数，-1为不重试
    not-full-fimeout-retry-count: 2
    #重连间隔时间 单位毫秒
    acquire-retry-delay: 10000
    # 设置获取连接出错时是否马上返回错误，true为马上返回
    fail-fast: true
    #属性类型是字符串，通过别名的方式配置扩展插件，常用的插件有：
    #监控统计用的filter:stat日志用的filter:log4j防御sql注入的filter:wall
    filters: stat,wall
```

> Druid的配置

```java
@Configuration
public class DruidConf {

    /**
     * 配置Druid的监控Servlet
     */
    @Bean
    public ServletRegistrationBean statViewServlet() {
        ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
        Map<String, String> initParams = new HashMap<>();
        initParams.put("loginUsername", "admin");
        initParams.put("loginPassword", "admin");
        initParams.put("allow", ""); // 默认就是允许所有
        bean.setInitParameters(initParams);
        return bean;
    }

    /**
     * 配置一个Web监控的Filter
     */
    @Bean
    public FilterRegistrationBean webStatFilter() {
        FilterRegistrationBean bean = new FilterRegistrationBean();
        bean.setFilter(new WebStatFilter());
        Map<String, String> initParams = new HashMap<>();
        initParams.put("exclusions","*.js,*.css,/druid/*");
        bean.setInitParameters(initParams);
        bean.setUrlPatterns(Arrays.asList("/*"));
        return bean;
    }

    @Bean
    @ConfigurationProperties(prefix = "spring.datasource")
    public DataSource druidDataSource() {
        return new DruidDataSource();
    }
}
```

## 7.4.MyBatis

> 依赖

```xml
<properties>
    <mybatis.spring.boot.starter.version>2.1.1</mybatis.spring.boot.starter.version>
</properties>
<!--mybatis-->
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
    <version>${mybatis.spring.boot.starter.version}</version>
</dependency>
```

> application.yml

```yaml
mybatis:
  config-location: classpath:mybatis/mybatis-conf.xml
  mapper-locations: classpath:mybatis/mapper/*.xml
```

> myBatis全局配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
</configuration>
```

> mapper映射文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.ymy.spring.boot.mapper.DepartmentMapper">
</mapper>
```



## 7.5 MyBatis Plus

**(1) 依赖**

```xml
<!-- 依赖 -->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-boot-starter</artifactId>
    <version>3.4.1</version>
</dependency>
```



**(2) 分析自动配置**

```shell
1、MybatisPlusAutoConfiguration：配置类; MybatisPlusProperties：配置项的绑定。
prefix = mybatis-plus

2、SqlSessionFactory：myBatisPlus 已经在容器中注册好了，该组件是myBatis的核心组件。使用的是SpringBoot中配置的数据源

3、mapperLocations：自动配置好的。Locations of MyBatis mapper files.
默认是：classpath*:/mapper/**/*.xml

4、SqlSessionTemplate：容器中自动配置好。

5、AutoConfiguredMapperScannerRegistrar：@Mapper标注的接口也会被自动扫描
```



**(3) 使用myBatis Plus**

在 Spring Boot 启动类中添加 `@MapperScan` 注解，扫描 Mapper 文件夹：

```java
/**
 * @MapperScan： 全局扫描,有这个就不用在接口上写 @Mapper 了
 */
@MapperScan("com.ymy.boot.mapper")
@SpringBootApplication
public class MainApplication {
    public static void main(String[] args) {
        SpringApplication.run(MainApplication.class, args);
    }
}
```



创建用户类

```java
@Data
@AllArgsConstructor
@NoArgsConstructor
public class User {
    private Integer id;
    private String name;
    private Integer age;
    private String email;
}
```



创建 mapper

```java
/**
 * 只需要我们的 Mapper 继承BaseMapper 就可以拥有CRUD能力
 */
public interface UserMapper extends BaseMapper<User> {
}
```



测试

```java
@Slf4j
@SpringBootTest
public class TestMyBatisPlusMapper {

    @Resource
    private UserMapper userMapper;

    // 测试查询
    @Test
    void testQuery() {
        User user = userMapper.selectById(1);
        log.info("用户信息：" + user);
    }
}
```

## 7.6 SpringBoot整合Redis

**目标**：在Spring Boot项目中使用Junit测试RedisTemplate的使用

**分析**：

1. 添加启动器依赖；spring-boot-starter-data-redis
2. 配置application.yml中修改redis的连接参数；（redis需要启动）
3. 编写测试类应用RedisTemplate操作redis中的5种数据类型（string/hash/list/set/sorted set）

**小结**：

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class RedisTest {

    @Autowired
    private RedisTemplate redisTemplate;

    @Test
    public void test(){
        //string 字符串
        //redisTemplate.opsForValue().set("str", "heima");
        redisTemplate.boundValueOps("str").set("heima");
        System.out.println("str = " + redisTemplate.opsForValue().get("str"));

        //hash 散列
        redisTemplate.boundHashOps("h_key").put("name", "heima");
        redisTemplate.boundHashOps("h_key").put("age", 13);
        //获取所有域
        Set set = redisTemplate.boundHashOps("h_key").keys();
        System.out.println(" hash散列的所有域：" + set);
        //获取所有值
        List list = redisTemplate.boundHashOps("h_key").values();
        System.out.println(" hash散列的所有域的值：" + list);

        //list 列表
        redisTemplate.boundListOps("l_key").leftPush("c");
        redisTemplate.boundListOps("l_key").leftPush("b");
        redisTemplate.boundListOps("l_key").leftPush("a");
        //获取全部元素
        list = redisTemplate.boundListOps("l_key").range(0, -1);
        System.out.println(" list列表中的所有元素：" + list);

        // set 集合
        redisTemplate.boundSetOps("s_key").add("a", "b", "c");
        set = redisTemplate.boundSetOps("s_key").members();
        System.out.println(" set集合中的所有元素：" + set);

        // sorted set 有序集合
        redisTemplate.boundZSetOps("z_key").add("a", 30);
        redisTemplate.boundZSetOps("z_key").add("b", 20);
        redisTemplate.boundZSetOps("z_key").add("c", 10);
        set = redisTemplate.boundZSetOps("z_key").range(0, -1);
        System.out.println(" zset有序集合中的所有元素：" + set);
    }
}

```



# 8.SpringBoot事件监听

配置四个监听器：

- **ApplicationContextInitializer(要写在META-INF/spring.factories中)**
- **ApplicationRunner(直接加入到容器中)**
- **CommandLineRunner(直接加入到容器中)**
- **SpringApplicationRunListener(要写在META-INF/spring.factories中)**

```java
// 1.ApplicationContextInitializer
public class HelloApplicationContextInitializer implements ApplicationContextInitializer<ConfigurableApplicationContext> {
    @Override
    public void initialize(ConfigurableApplicationContext applicationContext) {
        System.out.println("*****ApplicationContextInitializer*****" + applicationContext);
    }
}

// 2.ApplicationRunner
@Component
public class HelloApplicationRunner implements ApplicationRunner {
    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println("****ApplicationRunner***run");
    }
}

// 3.CommandLineRunner
@Component
public class HelloCommandLineRunner implements CommandLineRunner {
    @Override
    public void run(String... args) throws Exception {
        System.out.println("****HelloCommandLineRunner****");
    }
}

// 4.SpringApplicationRunListener
public class HelloSpringApplicationRunListener implements SpringApplicationRunListener {

    public HelloSpringApplicationRunListener(SpringApplication application, String[] args) {

    }

    @Override
    public void starting() {
        System.out.println("*****SpringApplicationRunListener*****starting");
    }

    @Override
    public void environmentPrepared(ConfigurableEnvironment environment) {
        Object osName = environment.getSystemProperties().get("os.name");
        System.out.println("*****SpringApplicationRunListener*****environmentPrepared " + osName);
    }

    @Override
    public void contextPrepared(ConfigurableApplicationContext context) {
        System.out.println("*****SpringApplicationRunListener*****contextPrepared");
    }

    @Override
    public void contextLoaded(ConfigurableApplicationContext context) {
        System.out.println("*****SpringApplicationRunListener*****contextLoaded");
    }

    @Override
    public void started(ConfigurableApplicationContext context) {
        System.out.println("*****SpringApplicationRunListener*****started");
    }

    @Override
    public void running(ConfigurableApplicationContext context) {
        System.out.println("*****SpringApplicationRunListener*****running");
    }

    @Override
    public void failed(ConfigurableApplicationContext context, Throwable exception) {
        System.out.println("*****SpringApplicationRunListener*****failed");
    }
}
```



控制台输出顺序

```shell
*****SpringApplicationRunListener*****starting
*****SpringApplicationRunListener*****environmentPrepared Windows 10
*****ApplicationContextInitializer*****
*****SpringApplicationRunListener*****contextPrepared
*****SpringApplicationRunListener*****contextLoaded
*****SpringApplicationRunListener*****started
****ApplicationRunner***run
****CommandLineRunner****
*****SpringApplicationRunListener*****running
```

# 9.自定义Starter

## 9.1.基本介绍

**starter：**

- 这个场景需要使用到的依赖是什么？
- 如果编写自动配置？

```java
@Configuration             // 指定这个类是个配置类
@ConditionalOnXXX          // 在指定条件成立的情况下自动配置类生效
@AutoConfigureAfter        // 指定自动配置类的顺序
@Bean                      // 给容器中添加组件
@ConfigurationPropertis    // 结合Properties类来绑定相关的配置
@EnableConfigurationProperties  // 让xxxProperties生效并加入到容器中

自动配置类要能加载
将需要启动就加载的自动配置类，配置在META-INF/spring.factories
```

## 9.2.模式介绍

-  启动器只用来做依赖导入。
-  专门来写一个自动配置模块。
-  启动器依赖自动配置，别人只需要引入启动器(starter)，自动配置就配置好了
-  starter的命名：`mybatis-spring-boot-starter`，自定义启动器名-spring-boot-starter。

## 9.3.自动配置模块

> pom

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.ymy</groupId>
    <artifactId>spring-boot-08-autoconfiguration</artifactId>
    <version>1.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.4.RELEASE</version>
    </parent>

    <properties>
        <java.version>1.8</java.version>
        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <dependencies>
        <!--引入spring-boot-starter 所有starter的基本配置-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter</artifactId>
        </dependency>

        <!--导入配置文件处理器-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
    </dependencies>
</project>
```

> HelloProperties

```java
@ConfigurationProperties(prefix = "ymy.hello")
public class HelloProperties {

    private String prefix;

    private String suffix;

    public String getPrefix() {
        return prefix;
    }

    public void setPrefix(String prefix) {
        this.prefix = prefix;
    }

    public String getSuffix() {
        return suffix;
    }

    public void setSuffix(String suffix) {
        this.suffix = suffix;
    }
}
```

> HelloService

```java
public class HelloService {

    private HelloProperties helloProperties;

    public HelloProperties getHelloProperties() {
        return helloProperties;
    }

    public void setHelloProperties(HelloProperties helloProperties) {
        this.helloProperties = helloProperties;
    }

    public String sayHello(String name) {
        return helloProperties.getPrefix() + name + helloProperties.getSuffix();
    }
}
```

> 自动配置

```java
package com.ymy.spring.boot.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.autoconfigure.condition.ConditionalOnWebApplication;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
@ConditionalOnWebApplication // web应用才生效
@EnableConfigurationProperties(value = HelloProperties.class)
public class HelloServiceAutoConfiguration {

    @Autowired
    private HelloProperties helloProperties;
	
    // 这样就把HelloService组件加入了容器,并且可以在yml中配置
    @Bean
    public HelloService helloService() {
        HelloService helloService = new HelloService();
        helloService.setHelloProperties(helloProperties);
        return helloService;
    }
}
```

> spring.factories

```properties
# 在resources目录下创建spring.factories文件
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.ymy.spring.boot.service.HelloServiceAutoConfiguration
```

## 9.4.自定义starter

自定义starter需要把我们写的自动配置模块导入进来并且安装到本地仓库，就可以让其他项目来使用了！

# 10.SpringBoot与缓存

![缓存](SpringBoot.assets/20200712201214264.png)

## 10.1.核心概念

| 概念           | 描述                                                         |
| -------------- | ------------------------------------------------------------ |
| Cache          | 缓存接口，定义缓存操作。实现有：RedisCache、EHCache、ConcurrentHashMap等 |
| CacheManager   | 缓存管理器，管理各种缓存（Cache）插件                        |
| @Cacheable     | 主要针对方法配置，能够根据方法的请求参数対其结果进行缓存     |
| @CacheEvict    | 清空缓存                                                     |
| @CachePut      | 保证方法被调用，又希望结果被缓存                             |
| @EnableCaching | 开启基于注解的缓存                                           |
| KeyGenerator   | 缓存数据时key的生成策略                                      |
| serialize      | 缓存时value的序列化策略                                      |

## 10.2.缓存的使用

> 步骤

- 开启注解的缓存`@EnableCaching`。
- 在方法上标注缓存注解`@Cacheable`、`@CacheEvict`、`@CachePut`。

> 缓存的SpEL表达式

| 名字          | 位置                    | 描述                                                         | 示例                 |
| ------------- | ----------------------- | ------------------------------------------------------------ | -------------------- |
| methodName    | root object             | 当前被调用的方法名                                           | #root.methodName     |
| method        | root object             | 当前被调用的方法                                             | #root.method.name    |
| target        | root object             | 当前被调用的目标对象                                         | #root.target         |
| targetClass   | root object             | 当前被调用的目标对象类                                       | #root.targetClass    |
| args          | root object             | 当前被调用的方法的参数列表                                   | #root.args[0]        |
| caches        | root object             | 当前被调用方法使用的缓存列表，如(@Cacheable(value={"cache1","cache2"}))，则有两个Cache | #root.caches[0].name |
| argument name | evaluation      context | 方法参数的名字，可以直接#参数名，也可以使用#p0#a0的形式，0代表参数的索引 | #iban、#a0、#p0      |
| result        | evaluation      context | 方法执行后的返回值（仅当方法执行之后的判断有效，如'unless'，'cache put'的表达式 'cache evict'的表达式beforeInvocation=false） | #result              |

> @cacheable

```java
import com.ymy.spring.boot.cache.entity.Employee;
import com.ymy.spring.boot.cache.mapper.EmployeeMapper;
import com.ymy.spring.boot.cache.support.SimpleResponse;
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Service;
import org.springframework.web.bind.annotation.PathVariable;

import javax.annotation.Resource;

@Service
public class EmployeeService {

    @Resource
    private EmployeeMapper employeeMapper;

    /**
     * @Cacheable 将方法的运行结果进行缓存，以后再要相同的数据，直接从缓存中获取，不用调用方法。
     * CacheManager管理多个Cache组件，每个缓存组件有自己唯一的名字。
     *
     * 运行时机：先查缓存，再运行目标方法。
     *
     * @Cacheable 的属性：
     *      value/cacheNames：指定缓存的名字。
     *      key：缓存数据时使用的key。默认是使用方法参数的值！ key = "#id" 可以使用SpEL表达式。
     *      keyGenerator：可以自己指定key的生成器。(key和keyGenerator二选一使用)。
     *      cacheManager：指定缓存管理器。
     *      cacheResolver：指定缓存解析器。（cacheManager和cacheResolver二选一）。
     *      condition：指定符合条件的情况下，才进行缓存。
     *      unless：否定缓存。当unless的条件为true，就不会缓存。（unless和condition用法相反）。
     *      sync：是否使用同步模式。
     *
     */
    @Cacheable(cacheNames = {"employee"}, key = "#root.args[0]")
    public SimpleResponse getEmployeeById(Integer id) {
        Employee employee = employeeMapper.getEmployeeById(id);
        if (employee == null) {
            return new SimpleResponse(404, "数据库没有该员工！", null);
        }
        return new SimpleResponse(200, "查询成功", employee);
    }
}
```

> @CachePut

```java
	/**
     * @CachePut 既调用方法又更新缓存数据。
     * 修改了数据库的某个数据，同时更新缓存
     * 运行时机：
     *     1.先调用目标方法
     *     2.将目标方法的结果缓存起来
     */
    @CachePut(cacheNames = {"employee"}, key = "#employee.id")
    public SimpleResponse updateEmployee(Employee employee) {
        Integer ret = employeeMapper.updateEmployee(employee);
        if (ret > 0) {
            return new SimpleResponse(200, "修改成功", 
                                      employeeMapper.getEmployeeById(employee.getId()));
        }
        return new SimpleResponse(500, "修改失败", null);
    }
```

> @CacheEvict

```java
    /**
     * @CacheEvict 缓存清除
     *
     *  key：指定要清除的缓存的key。
     *  allEntries：是否清除所有缓存。默认是false。
     *  beforeInvocation：缓存的清除是否在方法执行之前清除。默认是false，代表在方法执行之后才清除缓存。
     *      beforeInvocation=true：无论目标方法是否异常。缓存都会被清除！
     */
    @CacheEvict(cacheNames = {"employee"}, key = "#id", beforeInvocation = true)
    public SimpleResponse deleteEmployee(Integer id) {
        Integer ret = employeeMapper.deleteEmployee(id);
        if (ret > 0) {
            return new SimpleResponse(200, "删除成功", ret);
        }
        return new SimpleResponse(500, "删除失败", ret);
    }
```





## 10.3.缓存工作原理

```java
// 1、缓存的配置类
0 = "org.springframework.boot.autoconfigure.cache.GenericCacheConfiguration"
1 = "org.springframework.boot.autoconfigure.cache.JCacheCacheConfiguration"
2 = "org.springframework.boot.autoconfigure.cache.EhCacheCacheConfiguration"
3 = "org.springframework.boot.autoconfigure.cache.HazelcastCacheConfiguration"
4 = "org.springframework.boot.autoconfigure.cache.InfinispanCacheConfiguration"
5 = "org.springframework.boot.autoconfigure.cache.CouchbaseCacheConfiguration"
6 = "org.springframework.boot.autoconfigure.cache.RedisCacheConfiguration"
7 = "org.springframework.boot.autoconfigure.cache.CaffeineCacheConfiguration"
8 = "org.springframework.boot.autoconfigure.cache.SimpleCacheConfiguration"
9 = "org.springframework.boot.autoconfigure.cache.NoOpCacheConfiguration"

// 2、SpringBoot默认使用的是SimpleCacheConfiguration
SimpleCacheConfiguration matched:
- Cache org.springframework.boot.autoconfigure.cache.SimpleCacheConfiguration automatic cache type (CacheCondition)
- @ConditionalOnBean (types: org.springframework.cache.CacheManager; SearchStrategy: all) did not find any beans (OnBeanCondition)

// 3、SimpleCacheConfiguration给容器中加入了ConcurrentMapCacheManager
ConcurrentMapCacheManager可以获取和创建ConcurrentMapCache类型的组件

// 4、缓存的运行流程
    public Cache getCache(String name) {
    Cache cache = this.cacheMap.get(name);
    if (cache == null && this.dynamic) {
        synchronized (this.cacheMap) {
            cache = this.cacheMap.get(name);
            if (cache == null) {
                cache = createConcurrentMapCache(name);
                this.cacheMap.put(name, cache);
            }
        }
    }
    return cache;
    }
(1)目标方法在发送SQL之前，先去查询Cache(缓存组件)，按照CacheNames指定的名字获取。CacheManager先获取相应的缓存，第一次获取如果没有Cache组件会自动创建。
(2)去Cache中查找缓存的内容，使用一个key，默认就是方法的参数名。key是按照某种策略生成的。
(3)没有查到缓存就调用目标方法。
(4)将目标方法返回的结果放到缓存中。
```

## 10.4.自定义KeyGenerator

> 定义KeyGenerator

```java
@Configuration
public class CacheConf {
    @Bean(name = "myKeyGenerator")
    public KeyGenerator keyGenerator() {
        return new KeyGenerator() {
            @Override
            public Object generate(Object target, Method method, Object... params) {
                return method.getName() + "[" + Arrays.asList(params).toString() + "]";
            }
        };
    }
}
```

> 使用KeyGenerator

```java
@Cacheable(cacheNames = {"employee"}, keyGenerator = "myKeyGenerator")
public SimpleResponse getEmployeeById(Integer id) {
    Employee employee = employeeMapper.getEmployeeById(id);
    if (employee == null) {
        return new SimpleResponse(404, "数据库没有该员工！", null);
    }
    return new SimpleResponse(200, "查询成功", employee);
}
```

## 10.5.Redis缓存

> 依赖

```xml
<!--redis-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```

导入Redis依赖，SpringBoot缓存就使用了Redis。



> 配置RedisCacheManager

```java
package com.ymy.spring.boot.cache.conf;

import com.fasterxml.jackson.annotation.JsonAutoDetect;
import com.fasterxml.jackson.annotation.PropertyAccessor;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.jsontype.impl.LaissezFaireSubTypeValidator;
import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.cache.CacheManager;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.redis.cache.RedisCacheConfiguration;
import org.springframework.data.redis.cache.RedisCacheManager;
import org.springframework.data.redis.connection.RedisConnectionFactory;
import org.springframework.data.redis.core.RedisTemplate;
import org.springframework.data.redis.serializer.Jackson2JsonRedisSerializer;
import org.springframework.data.redis.serializer.RedisSerializationContext;
import org.springframework.data.redis.serializer.RedisSerializer;
import org.springframework.data.redis.serializer.StringRedisSerializer;

import java.net.UnknownHostException;
import java.time.Duration;

@Configuration
public class RedisConf {
    @Bean
    public CacheManager cacheManager(RedisConnectionFactory factory) {
        RedisSerializer<String> redisSerializer = new StringRedisSerializer();
        Jackson2JsonRedisSerializer jackson2JsonRedisSerializer = new Jackson2JsonRedisSerializer(Object.class);

        //解决查询缓存转换异常的问题
        ObjectMapper objectMapper = new ObjectMapper();
        objectMapper.setVisibility(PropertyAccessor.ALL, JsonAutoDetect.Visibility.ANY);
        objectMapper.activateDefaultTyping(LaissezFaireSubTypeValidator.instance, ObjectMapper.DefaultTyping.NON_FINAL);
        jackson2JsonRedisSerializer.setObjectMapper(objectMapper);

        // 配置序列化（解决乱码的问题）
        RedisCacheConfiguration config = RedisCacheConfiguration.defaultCacheConfig()
                .serializeKeysWith(RedisSerializationContext.SerializationPair.fromSerializer(redisSerializer))
                .serializeValuesWith(RedisSerializationContext.SerializationPair.fromSerializer(jackson2JsonRedisSerializer))
                .disableCachingNullValues();

        RedisCacheManager cacheManager = RedisCacheManager.builder(factory)
                .cacheDefaults(config)
                .build();
        return cacheManager;
    }
}
```

# 11.定时任务

```java
@Service
public class ScheduledService {
    /**
     * @Scheduled 定时任务
     * second, minute, hour, day of month, month, and day of week
     * 0 * * * * MON-TUE：任意月的星期二的每个整分钟都会调用一次该方法
     */
    @Scheduled(cron = "0 * * * * MON-TUE")
    public void hello() {
        System.out.println("hello");
    }
}

@EnableScheduling // @EnableScheduling需要开启定时任务功能！
@SpringBootApplication
public class SpringBoot10TaskApplication {
    public static void main(String[] args) {
        SpringApplication.run(SpringBoot10TaskApplication.class, args);
    }
}
```

**cron表达式**

| 字段 | 允许值         | 允许的特殊字符                   |
| ---- | -------------- | -------------------------------- |
| 秒   | 0-59           | `,` `-` `*` `/`                  |
| 分   | 0-59           | `,` `-` `*` `/`                  |
| 小时 | 0-23           | `,` `-` `*` `/`                  |
| 日期 | 1-31           | `,` `-` `*` `/` `?` `L` `W` `C`  |
| 月份 | 1-12           | `,` `-` `*` `/`                  |
| 星期 | 0-7或者SUN—SAT | `,` `-` `*` `/` `?` `L`  `C` `#` |



**特殊字符的含义**

| 特殊字符 | 含义                       |
| -------- | -------------------------- |
| `,`      | 枚举                       |
| `_`      | 区间                       |
| `*`      | 任意                       |
| `/`      | 步长                       |
| `?`      | 日/星期冲突匹配            |
| `L`      | 最后                       |
| `W`      | 工作日                     |
| `C`      | 和calendar联系后计算过的值 |
| `#`      | 星期，4#2，第二个星期四    |



`@Scheduled`属性：

- `fixedDelay`：上一个任务结束和下一个任务开始的间隔时间（单位毫秒）。
- `fixedRate`：两次定时任务开始的时间间隔。
- `initialDelay`：在第一个定时任务执行之前，需要延迟的时间。



# 12.邮件任务

## 12.1. 依赖和配置

```xml
<!--mail-->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
</dependency>
```

> 配置

```yaml
spring:
  mail:
    username: 1466637477@qq.com # 配置发送的邮箱
    password: oexnnqprsuqngcbj # 配置邮箱的授权码
    host: smtp.qq.com  # 邮箱服务器地址
    default-encoding: UTF-8
    port: 587
```

```properties
spring.mail.properties.mail.stmp.socketFactory.class=javax.net.ssl.SSLSocketFactory
spring.mail.properties.mail.debug=true
```



## 12.2. 简单邮件

```java
@Resource
private JavaMailSenderImpl mailSender;

@Test
public void senderSimpleEmail() {
    SimpleMailMessage mail = new SimpleMailMessage();
    // 邮件的标题
    mail.setSubject("测试发送邮件");
    // 邮件的内容
    mail.setText("********测试********");
    // 邮件发送给谁
    mail.setTo("YmyLearning@163.com");
    // 谁发送的！
    mail.setFrom("1466637477@qq.com");
    mailSender.send(mail);
}
```



## 12.3. 复杂邮件

```java
@Resource
private JavaMailSenderImpl mailSender;

@Test
public void senderEmail() throws Exception{
    // 1、创建一个复杂的消息邮件
    MimeMessage mimeMessage = mailSender.createMimeMessage();
    // multipart为true 表示要上传文件
    MimeMessageHelper mimeMessageHelper = new MimeMessageHelper(mimeMessage, true);

    // 2、设计邮件内容
    mimeMessageHelper.setSubject("测试发送复杂邮件");
    mimeMessageHelper.setText("<b>今天7点30开会</b>", true);
    mimeMessageHelper.addAttachment("毕业声登记表.pdf", new File("C:\\Users\\14666\\Desktop\\毕业声登记表.pdf"));
    mimeMessageHelper.setTo("YmyLearning@163.com");
    mimeMessageHelper.setFrom("1466637477@qq.com");

    // 3、发送邮件
    mailSender.send(mimeMessage);
}
```



## 12.4. Thymeleaf邮件模板

**（1）依赖**

```xml
<!-- thymeleaf -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```



**（2）HTML模板**

```html
<!DOCTYPE html>
<html lang="en" xmlns:th="http://www.thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>邮件模板</title>
    <style type="text/css">
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        .w {
            width: 800px;
            margin: 20px auto;
        }

        .tab,
        .tab td,
        .tab th {
            border: 1px solid pink;
            text-align: center;
            border-collapse: collapse;
        }
    </style>
</head>

<body>
<div class="w">
    <!--  注意：引用一定要写 ${xxx}  -->
    <h4>
        Hello <span th:text="${username}"></span>, 欢迎来到xxx大家庭！
    </h4>
    <div>
        <h5>您的入职信息如下！</h5>
        <table class="tab">
            <tr>
                <td>职位：</td>
                <td th:text="${position}"></td>
            </tr>
            <tr>
                <td>薪水：</td>
                <td th:text="${salary}"></td>
            </tr>
            <tr>
                <td>部门：</td>
                <td th:text="${department}"></td>
            </tr>
        </table>
    </div>
</div>
</body>
</html>
```



**（3）发送邮件**

```java
/**
 * @author Ringo
 * @since 2021/4/13 11:45
 */
@SpringBootTest
public class MainTest {

    // 发送邮件
    @Resource
    private JavaMailSender mailSender;

    // Thymeleaf 模板引擎
    @Resource
    private SpringTemplateEngine templateEngine;

    @Autowired
    private MailProperties mailProperties;

    @Test
    void sendMail() throws Exception {
        MimeMessage message = mailSender.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(message, true);

        // 1: 解析 Thymeleaf 模板
        Context context = new Context();
        context.setVariable("username", "Ringo");
        context.setVariable("position", "Java工程师");
        context.setVariable("department", "技术部");
        context.setVariable("salary", "8000");
        String process = templateEngine.process("Mail.html", context);

        // 2: 设置邮件内容
        helper.setSubject("测试邮件主题");
        helper.setText(process, true);
        helper.setSentDate(new Date());
        helper.setTo("594707128@qq.com");
        helper.setFrom(mailProperties.getUsername());

        // 3: 发送邮件
        mailSender.send(message);
    }
}
```

# 15、SpringSecurity（安全）

## 安全简介

在 Web 开发中，安全一直是非常重要的一个方面。安全虽然属于应用的非功能性需求，但是应该在应用开发的初期就考虑进来。如果在应用开发的后期才考虑安全的问题，就可能陷入一个两难的境地：一方面，应用存在严重的安全漏洞，无法满足用户的要求，并可能造成用户的隐私数据被攻击者窃取；另一方面，应用的基本架构已经确定，要修复安全漏洞，可能需要对系统的架构做出比较重大的调整，因而需要更多的开发时间，影响应用的发布进程。因此，从应用开发的第一天就应该把安全相关的因素考虑进来，并在整个应用的开发过程中。

市面上存在比较有名的：Shiro，Spring Security ！

认证，授权

## 认识SpringSecurity

Spring Security 是针对Spring项目的安全框架，也是Spring Boot底层安全模块默认的技术选型，他可以实现强大的Web安全控制，对于安全控制，我们仅需要引入 spring-boot-starter-security 模块，进行少量的配置，即可实现强大的安全管理！

记住几个类：

- WebSecurityConfigurerAdapter：自定义Security策略
- AuthenticationManagerBuilder：自定义认证策略
- @EnableWebSecurity：开启WebSecurity模式

1. 引入 Spring Security 模块

```xml
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-security</artifactId>
</dependency>
1234
```

1. 编写基础配置类

```java
package com.kuang.config;

@EnableWebSecurity // 开启WebSecurity模式
public class SecurityConfig extends WebSecurityConfigurerAdapter {
  @Override
  protected void configure(HttpSecurity http) throws Exception {

  }
}
123456789
```

1. 定制请求的授权规则

```java
@Override
protected void configure(HttpSecurity http) throws Exception {
   // 定制请求的授权规则
   // 首页所有人可以访问
   http.authorizeRequests().antMatchers("/").permitAll()
  .antMatchers("/level1/**").hasRole("vip1")
  .antMatchers("/level2/**").hasRole("vip2")
  .antMatchers("/level3/**").hasRole("vip3");
}
123456789
```

1. 测试一下：发现除了首页都进不去了！因为我们目前没有登录的角色，因为请求需要登录的角色拥有对应的权限才可以！
2. 在configure()方法中加入以下配置，开启自动配置的登录功能！

```java
// 开启自动配置的登录功能
// "/login" 请求来到登录页
// /login?error 重定向到这里表示登录失败
http.formLogin();
1234
```

 此时如果没有权限就会跳转至登陆页

1. 定义认定规则，重写configure(AuthenticationManagerBuilder auth)方法

```java
//认证
@Override
protected void configure(AuthenticationManagerBuilder auth) throws Exception {
  //数据正常应该从数据库中取，现在从内存中取
  auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())
    .withUser("admin").password(new BCryptPasswordEncoder().encode("123")).roles("vip1","vip2")
    .and()
    .withUser("root").password(new BCryptPasswordEncoder().encode("123")).roles("vip1","vip2","vip3")
    .and()
    .withUser("guest").password(new BCryptPasswordEncoder().encode("123")).roles("vip1");
12345678910
```

 这里设置密码加密`auth.inMemoryAuthentication().passwordEncoder(new BCryptPasswordEncoder())`否则会报`There is no PasswordEncoder mapped for the id "null"`错误,创建的每个用户也必须添加密码加密**`.password(new BCryptPasswordEncoder().encode("123"))`**

1. 测试,发现，登录成功，并且每个角色只能访问自己认证下的规则！搞定

## 权限控制和注销

### 注销

1. 开启自动配置的注销的功能

   ```html
   //定制请求的授权规则
   @Override
   protected void configure(HttpSecurity http) throws Exception {
      //....
      //开启自动配置的注销的功能
         // /logout 注销请求
      http.logout();
   }
   12345678
   ```

2. 我们在前端，增加一个注销的按钮，index.html 导航栏中

   ```html
   <a class="btn btn-primary" th:href="@{/logout}">注销</a>
   1
   ```

3. 测试发现，点击注销按钮后会跳转到登陆页面，此时想要在注销成功后跳转到指定页面需要在请求后添加`.logoutSuccessUrl("/");`

   ```java
   // .logoutSuccessUrl("/"); 注销成功来到首页
   http.logout().logoutSuccessUrl("/");
   12
   ```

### 权限控制

**需求：**用户没有登录的时候，导航栏上只显示登录按钮，用户登录之后，导航栏可以显示登录的用户信息及注销按钮！还有就是，比如admin这个用户，它只有 vip2，vip3功能，那么登录则只显示这两个功能，而vip1的功能菜单不显示！

1. 导入maven依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/org.thymeleaf.extras/thymeleaf-extras-springsecurity4 -->
   <dependency>
      <groupId>org.thymeleaf.extras</groupId>
      <artifactId>thymeleaf-extras-springsecurity5</artifactId>
      <version>3.0.4.RELEASE</version>
   </dependency>
   123456
   ```

2. 导入命名空间

   ```html
   xmlns:sec="http://www.thymeleaf.org/extras/spring-security"
   1
   ```

3. 修改index页面,增加判断

   ```html
   <div>
     <!--如果未登录则显示以下内容-->
     <div sec:authorize="!isAuthenticated()">
       <a class="btn btn-primary" th:href="@{/toLogin}">登陆</a>
     </div>
     <!--如果已登录则显示以下内容-->
     <div sec:authorize="isAuthenticated()">
       用户名<p sec:authentication="name"></p>
       角色<p sec:authentication="principal.authorities"></p>
       <a class="btn btn-primary" th:href="@{/logout}">注销</a>
     </div>
   </div>
   <!--如果用户拥有这个角色，则显示该div内的内容，如果没有则不显示-->
   <div class="div" sec:authorize="hasRole('vip1')">
     <a th:href="@{/level1/1}">level1-1</a><br/>
     <a th:href="@{/level1/2}">level1-2</a>
   </div>
   <div class="div" sec:authorize="hasRole('vip2')">
     <a th:href="@{/level2/1}">level2-1</a><br/>
     <a th:href="@{/level2/2}">level2-2</a>
   </div>
   <div class="div" sec:authorize="hasRole('vip3')">
     <a th:href="@{/level3/1}">level3-1</a><br/>
     <a th:href="@{/level3/2}">level3-2</a>
   </div>
   12345678910111213141516171819202122232425
   ```

4. 如果注销404了，就是因为它默认防止csrf跨站请求伪造，因为会产生安全问题，我们可以将请求改为post表单提交，或者在spring security中关闭csrf功能；我们试试：在 配置中增加 `http.csrf().disable();`

## 记住我

1. 开启记住我功能

   ```java
   //定制请求的授权规则
   @Override
   protected void configure(HttpSecurity http) throws Exception {
   //。。。。。。。。。。。
      //记住我,保存2周
      http.rememberMe();
   }
   1234567
   ```

2. 测试，关闭浏览器再次打开用户依旧存在

   **本质上是保存到cookie，通过浏览器审查元素的application中可以看到**

3. 如果使用自己的页面中的按钮，可以给按钮设置name，再在配置后面加上如下方法

   ```java
   http.rememberMe().rememberMeParameter("remember");
   1
   ```

## 定制登录页

1. 在配置中设置，用`.loginProcessingUrl("/login")`并将前端`form`表单的`action`设置为括号内相同即可，但如果前端用户名和密码前后端不一样，则需要进行设置，括号内的属性为前端页面的`name`属性

   ```java
   http.formLogin().loginPage("/toLogin").usernameParameter("username").passwordParameter("password").loginProcessingUrl("/login");
   1
   ```

# 16、Shiro

## shiro简介

### 基本功能点

Shiro 可以非常容易的开发出足够好的应用，其不仅可以用在 JavaSE 环境，也可以用在 JavaEE 环境。Shiro 可以帮助我们完成：认证、授权、加密、会话管理、与 Web 集成、缓存等。其基本功能点如下图所示：

![image-20201220220037818](../SpringBoot.assets/image-20201220220037818.png)

- Authentication：身份认证 / 登录，验证用户是不是拥有相应的身份；
- Authorization：授权，即权限验证，验证某个已认证的用户是否拥有某个权限；即判断用户是否能做事情，常见的如：验证某个用户是否拥有某个角色。或者细粒度的验证某个用户对某个资源是否具有某个权限；
- Session Manager：会话管理，即用户登录后就是一次会话，在没有退出之前，它的所有信息都在会话中；会话可以是普通 JavaSE 环境的，也可以是如 Web 环境的；
- Cryptography：加密，保护数据的安全性，如密码加密存储到数据库，而不是明文存储；
- Web Support：Web 支持，可以非常容易的集成到 Web 环境；
- Caching：缓存，比如用户登录后，其用户信息、拥有的角色 / 权限不必每次去查，这样可以提高效率；
- Concurrency：shiro 支持多线程应用的并发验证，即如在一个线程中开启另一个线程，能把权限自动传播过去；
- Testing：提供测试支持；
- Run As：允许一个用户假装为另一个用户（如果他们允许）的身份进行访问；
- Remember Me：记住我，这个是非常常见的功能，即一次登录后，下次再来的话不用登录了。

记住一点，Shiro 不会去维护用户、维护权限；这些需要我们自己去设计 / 提供；然后通过相应的接口注入给 Shiro 即可。

## Shiro的架构

### 外部

我们从外部来看 Shiro ，即从应用程序角度的来观察如何使用 Shiro 完成工作。如下图：

![image-20201220220053410](SpringBoot.assets/image-20201220220053410.png)

可以看到：应用代码直接交互的对象是 Subject，也就是说 Shiro 的对外 API 核心就是 Subject；其每个 API 的含义：

**Subject**：主体，代表了当前 “用户”，这个用户不一定是一个具体的人，与当前应用交互的任何东西都Subject，如网络爬虫，机器人等；即一个抽象概念；所有 Subject 都绑定到 SecurityManager，与 Subject 的所有交互都会委托给 SecurityManager；可以把 Subject 认为是一个门面；SecurityManager 才是实际的执行者；

**SecurityManager**：安全管理器；即所有与安全有关的操作都会与 SecurityManager 交互；且它管理着所有 Subject；可以看出它是 Shiro 的核心，它负责与后边介绍的其他组件进行交互，如果学习过 SpringMVC，你可以把它看成 DispatcherServlet 前端控制器；

**Realm**：域，Shiro 从 Realm 获取安全数据（如用户、角色、权限），就是说 SecurityManager 要验证用户身份，那么它需要从 Realm 获取相应的用户进行比较以确定用户身份是否合法；也需要从 Realm 得到用户相应的角色 / 权限进行验证用户是否能进行操作；可以把 Realm 看成 DataSource，即安全数据源。

也就是说对于我们而言，最简单的一个 Shiro 应用：

1. 应用代码通过 Subject 来进行认证和授权，而 Subject 又委托给 SecurityManager；
2. 我们需要给 Shiro 的 SecurityManager 注入 Realm，从而让 SecurityManager 能得到合法的用户及其权限进行判断。

**从以上也可以看出，Shiro 不提供维护用户 / 权限，而是通过 Realm 让开发人员自己注入。**

### 内部

接下来我们来从 Shiro 内部来看下 Shiro 的架构，如下图所示：

![image-20201220220106403](SpringBoot.assets/image-20201220220106403.png)

**Subject**：主体，可以看到主体可以是任何可以与应用交互的 “用户”；

**SecurityManager**：相当于 SpringMVC 中的 DispatcherServlet 或者 Struts2 中的 FilterDispatcher；是 Shiro 的心脏；所有具体的交互都通过 SecurityManager 进行控制；它管理着所有 Subject、且负责进行认证和授权、及会话、缓存的管理。

**Authenticator**：认证器，负责主体认证的，这是一个扩展点，如果用户觉得 Shiro 默认的不好，可以自定义实现；其需要认证策略（Authentication Strategy），即什么情况下算用户认证通过了；

**Authrizer**：授权器，或者访问控制器，用来决定主体是否有权限进行相应的操作；即控制着用户能访问应用中的哪些功能；

**Realm**：可以有 1 个或多个 Realm，可以认为是安全实体数据源，即用于获取安全实体的；可以是 JDBC 实现，也可以是 LDAP 实现，或者内存实现等等；由用户提供；注意：Shiro 不知道你的用户 / 权限存储在哪及以何种格式存储；所以我们一般在应用中都需要实现自己的 Realm；

**SessionManager**：如果写过 Servlet 就应该知道 Session 的概念，Session 呢需要有人去管理它的生命周期，这个组件就是 SessionManager；而 Shiro 并不仅仅可以用在 Web 环境，也可以用在如普通的 JavaSE 环境、EJB 等环境；所有呢，Shiro 就抽象了一个自己的 Session 来管理主体与应用之间交互的数据；这样的话，比如我们在 Web 环境用，刚开始是一台 Web 服务器；接着又上了台 EJB 服务器；这时想把两台服务器的会话数据放到一个地方，这个时候就可以实现自己的分布式会话（如把数据放到 Memcached 服务器）；

**SessionDAO**：DAO 大家都用过，数据访问对象，用于会话的 CRUD，比如我们想把 Session 保存到数据库，那么可以实现自己的 SessionDAO，通过如 JDBC 写到数据库；比如想把 Session 放到 Memcached 中，可以实现自己的 Memcached SessionDAO；另外 SessionDAO 中可以使用 Cache 进行缓存，以提高性能；

**CacheManager**：缓存控制器，来管理如用户、角色、权限等的缓存的；因为这些数据基本上很少去改变，放到缓存中后可以提高访问的性能

**Cryptography**：密码模块，Shiro 提高了一些常见的加密组件用于如密码加密 / 解密的。

## shiro组件

### 身份验证

**身份验证**，即在应用中谁能证明他就是他本人。一般提供如他们的身份 ID 一些标识信息来表明他就是他本人，如提供身份证，用户名 / 密码来证明。

在 shiro 中，用户需要提供 principals （身份）和 credentials（证明）给 shiro，从而应用能验证用户身份：

**principals**：身份，即主体的标识属性，可以是任何东西，如用户名、邮箱等，唯一即可。一个主体可以有多个 principals，但只有一个 Primary principals，一般是用户名 / 密码 / 手机号。

**credentials**：证明 / 凭证，即只有主体知道的安全值，如密码 / 数字证书等。

最常见的 principals 和 credentials 组合就是用户名 / 密码了。接下来先进行一个基本的身份认证。

另外两个相关的概念是之前提到的 **Subject** 及 **Realm**，分别是主体及验证主体的数据源。

## 快速开始（helloworld）

1. 导入依赖

   ```xml
   <dependency>
     <groupId>org.apache.shiro</groupId>
     <artifactId>shiro-core</artifactId>
     <version>1.4.1</version>
   </dependency>
   <dependency>
     <groupId>org.slf4j</groupId>
     <artifactId>slf4j-log4j12</artifactId>
     <version>1.7.21</version>
   </dependency>
   <dependency>
     <groupId>org.slf4j</groupId>
     <artifactId>jcl-over-slf4j</artifactId>
     <version>1.7.21</version>
   </dependency>
   <dependency>
     <groupId>log4j</groupId>
     <artifactId>log4j</artifactId>
     <version>1.2.17</version>
   </dependency>
   <dependency>
     <groupId>commons-logging</groupId>
     <artifactId>commons-logging</artifactId>
     <version>1.1.1</version>
   </dependency>
   12345678910111213141516171819202122232425
   ```

2. 配置文件（shiro.ini）

   ```ini
   [users]
   # user 'root' with password 'secret' and the 'admin' role
   root = secret, admin
   # user 'guest' with the password 'guest' and the 'guest' role
   guest = guest, guest
   # user 'presidentskroob' with password '12345' ("That's the same combination on
   # my luggage!!!" ;)), and role 'president'
   presidentskroob = 12345, president
   # user 'darkhelmet' with password 'ludicrousspeed' and roles 'darklord' and 'schwartz'
   darkhelmet = ludicrousspeed, darklord, schwartz
   # user 'lonestarr' with password 'vespa' and roles 'goodguy' and 'schwartz'
   lonestarr = vespa, goodguy, schwartz
   
   [roles]
   # 'admin' role has all permissions, indicated by the wildcard '*'
   admin = *
   # The 'schwartz' role can do anything (*) with any lightsaber:
   schwartz = lightsaber:*
   # The 'goodguy' role is allowed to 'drive' (action) the winnebago (type) with
   # license plate 'eagle5' (instance specific id)
   goodguy = winnebago:drive:eagle5
   123456789101112131415161718192021
   ```

3. log4j

   ```properties
   log4j.rootLogger=INFO, stdout
   
   log4j.appender.stdout=org.apache.log4j.ConsoleAppender
   log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
   log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m %n
   
   # General Apache libraries
   log4j.logger.org.apache=WARN
   
   # Spring
   log4j.logger.org.springframework=WARN
   
   # Default Shiro logging
   log4j.logger.org.apache.shiro=INFO
   
   # Disable verbose logging
   log4j.logger.org.apache.shiro.util.ThreadContext=WARN
   log4j.logger.org.apache.shiro.cache.ehcache.EhCache=WARN
   123456789101112131415161718
   ```

4. Quickstart.java

   ```java
   import org.apache.shiro.SecurityUtils;
   import org.apache.shiro.authc.*;
   import org.apache.shiro.config.IniSecurityManagerFactory;
   import org.apache.shiro.mgt.SecurityManager;
   import org.apache.shiro.session.Session;
   import org.apache.shiro.subject.Subject;
   import org.apache.shiro.util.Factory;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   /**
    * @author lee
    * @date 2020/8/11 - 6:24 下午
    */
   
   public class Quickstart {
   
   
     private static final transient Logger log = LoggerFactory.getLogger(Quickstart.class);
   
     public static void main(String[] args) {
   
   
       Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");
       SecurityManager securityManager = factory.getInstance();
   
       SecurityUtils.setSecurityManager(securityManager);
   
       //获取当前的用户对象 Subject
       Subject currentUser = SecurityUtils.getSubject();
   
       // 通过当前用户拿到Session
       Session session = currentUser.getSession();
       session.setAttribute("someKey", "aValue");
       String value = (String) session.getAttribute("someKey");
       if (value.equals("aValue")) {
         log.info("Subject=>session[" + value + "]");
       }
   
       //判断当前用户是否被认证
       if (!currentUser.isAuthenticated()) {
         //Token： 令牌
         UsernamePasswordToken token = new UsernamePasswordToken("lonestarr", "vespa");
         token.setRememberMe(true);//设置记住我
         try {
           currentUser.login(token);//执行登陆操作
         } catch (UnknownAccountException uae) {
           log.info("There is no user with username of " + token.getPrincipal());
         } catch (IncorrectCredentialsException ice) {
           log.info("Password for account " + token.getPrincipal() + " was incorrect!");
         } catch (LockedAccountException lae) {
           log.info("The account for username " + token.getPrincipal() + " is locked.  " +
                    "Please contact your administrator to unlock it.");
         }
         // ... catch more exceptions here (maybe custom ones specific to your application?
         catch (AuthenticationException ae) {
           //unexpected condition?  error?
         }
       }
   
       //say who they are:
       //print their identifying principal (in this case, a username):
       log.info("User [" + currentUser.getPrincipal() + "] logged in successfully.");
   
       //test a role:
       if (currentUser.hasRole("schwartz")) {
         log.info("May the Schwartz be with you!");
       } else {
         log.info("Hello, mere mortal.");
       }
   
       //test a typed permission (not instance-level)
       if (currentUser.isPermitted("lightsaber:wield")) {
         log.info("You may use a lightsaber ring.  Use it wisely.");
       } else {
         log.info("Sorry, lightsaber rings are for schwartz masters only.");
       }
   
       //a (very powerful) Instance Level permission:
       if (currentUser.isPermitted("winnebago:drive:eagle5")) {
         log.info("You are permitted to 'drive' the winnebago with license plate (id) 'eagle5'.  " +
                  "Here are the keys - have fun!");
       } else {
         log.info("Sorry, you aren't allowed to drive the 'eagle5' winnebago!");
       }
   
       //all done - log out!
       currentUser.logout();
   
       System.exit(0);
     }
   }
   
   123456789101112131415161718192021222324252627282930313233343536373839404142434445464748495051525354555657585960616263646566676869707172737475767778798081828384858687888990919293
   ```

以下方法Spring Security都有

```java
Subject currentUser = SecurityUtils.getSubject();
Session session = currentUser.getSession();
currentUser.isAuthenticated()
currentUser.getPrincipal()
currentUser.hasRole("schwartz")
currentUser.isPermitted("lightsaber:wield")
currentUser.logout();
1234567
```

## 在SpringBoot中集成Shiro

1. 创建springboot项目，创建时选择导入`springboot web`和`thmyeleaf`

2. 编写UserRealm类

   ```java
   //自定义的UserRealm
   public class UserRealm extends AuthorizingRealm {
     //授权
     @Override
     protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
       System.out.println("执行了=》授权");
       return null;
     }
     //认证
     @Override
     protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken authenticationToken) throws AuthenticationException {
       System.out.println("执行了=》认证");
       return null;
     }
   }
   123456789101112131415
   ```

3. 编写Shiroconfig类(三个方法，从下往上写)

   ```java
   @Configuration
   public class ShiroConfig {
     //shiroFilterFactoryBean：3
     public ShiroFilterFactoryBean getShiroFilterFactoryBean(@Qualifier("securityManager") DefaultWebSecurityManager defaultWebSecurityManager){
       ShiroFilterFactoryBean bean = new ShiroFilterFactoryBean();
       //设置安全管理器
       bean.setSecurityManager(defaultWebSecurityManager);
       return bean;
     }
     //DefaultWebSecurityManager：2
     @Bean(name="securityManager")
     public DefaultWebSecurityManager getdefaultWebSecurityManager(@Qualifier("userRealm") UserRealm userRealm){
       DefaultWebSecurityManager securityManager = new DefaultWebSecurityManager();
       securityManager.setRealm(userRealm);
       return securityManager;
     }
   
     //创建realm对象：1
     @Bean
     public UserRealm userRealm(){
       return new UserRealm();
     }
   }
   
   123456789101112131415161718192021222324
   ```

## 实现登陆拦截

1. 配置ShiroConfig配置类

   ```java
   //添加shiro的内置过滤器
           /*
               anon:无需认证
               authc:必须认证了才能访问
               user:必须拥有记住我功能才能用
               perms:拥有对某个资源的权限才能访问
               role:拥有某个角色权限才能访问
            */
           Map<String, String> filterMap = new LinkedHashMap<>();
           filterMap.put("/add","authc");
           filterMap.put("/update","authc");
        bean.setFilterChainDefinitionMap(filterMap);
   
           //如果没有权限就调到登陆页面
           bean.setLoginUrl("/toLogin");
   123456789101112131415
   ```

2. 在controller类实现`/toLogin`请求

   ```java
   @RequestMapping("/toLogin")
   public String toLogin(){
   
     return "login";
   }
   12345
   ```

## 实现用户认证

1. 在controller配置请求

   ```java
   @RequestMapping("/login")
   public String login(String username ,String password,Model model){
   
     //获取当前的用户
     Subject subject = SecurityUtils.getSubject();
   
     //封装用户的登陆数据
     UsernamePasswordToken token = new UsernamePasswordToken(username,password);
   
     try {
       subject.login(token);//执行登陆方法，如果没有异常就说明登陆成功
       return "index";
     }catch (UnknownAccountException e){//用户名不存在
       model.addAttribute("msg","用户名不存在");
       return "login";
     }catch (IncorrectCredentialsException e){
       model.addAttribute("msg","密码错误");
       return "login";
     }
   
   }
   123456789101112131415161718192021
   ```

2. 在UserRealm类中配置认证

   ```java
   //认证
   @Override
   protected AuthenticationInfo doGetAuthenticationInfo(AuthenticationToken token) throws AuthenticationException {
     System.out.println("执行了=》认证");
   
     //用户名密码   数据库取
     String name = "root";
     String password = "123";
   
     UsernamePasswordToken userToken = (UsernamePasswordToken) token;
     System.out.println(userToken.toString());
     if(!userToken.getUsername().equals(name)){
       return null; //抛出异常  UnknownAccountException
     }
   
     return new SimpleAuthenticationInfo("",password,"");
   }
   1234567891011121314151617
   ```

   用户名验证自己来做，密码验证shiro来做

## 整合Mybatis

1. 配置properties(yaml),和日志配置

   ```java
   mybatis.type-aliases-package=com.shirospringboot.pojo
   mybatis.mapper-locations=classpath:mapper/*.xml
   12
   ```

   ```yaml
   spring:
     datasource:
       username: codekitty
       password: lihaiyang
       url: jdbc:mysql://codekitty.cn:3306/study?serverTimezone=UTC&useUnicode=true&characterEncoding=utf-8
       driver-class-name: com.mysql.cj.jdbc.Driver
       type: com.alibaba.druid.pool.DruidDataSource # 自定义数据源
   
       #Spring Boot 默认是不注入这些属性值的，需要自己绑定
       #druid 数据源专有配置
       initialSize: 5
       minIdle: 5
       maxActive: 20
       maxWait: 60000
       timeBetweenEvictionRunsMillis: 60000
       minEvictableIdleTimeMillis: 300000
       validationQuery: SELECT 1 FROM DUAL
       testWhileIdle: true
       testOnBorrow: false
       testOnReturn: false
       poolPreparedStatements: true
   
       #配置监控统计拦截的filters，stat:监控统计、log4j：日志记录、wall：防御sql注入
       #如果允许时报错  java.lang.ClassNotFoundException: org.apache.log4j.Priority
       #则导入 log4j 依赖即可，Maven 地址：https://mvnrepository.com/artifact/log4j/log4j
       filters: stat,wall,log4j
       maxPoolPreparedStatementPerConnectionSize: 20
       useGlobalDataSourceStat: true
       connectionProperties: druid.stat.mergeSql=true;druid.stat.slowSqlMillis=500
   1234567891011121314151617181920212223242526272829
   ```

2. 编写mapper接口和mapper.xml

   ```java
   @Repository
   @Mapper
   public interface UserMapper {
   
       public User queryUserByName(String name);
   }
   123456
   ```

   ```xml
   <?xml version="1.0" encoding="UTF-8" ?>
   <!DOCTYPE mapper
           PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
           "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
   <!--namespace=绑定一个对应的Dao/Mapper接口-->
   <mapper namespace="com.shirospringboot.mapper.UserMapper">
       <!--    查询语句 id相当与要重写的方法名-->
       <select id="queryUserByName" resultType="User" parameterType="String">
           select * from study.User where username = #{username}
       </select>
   
   </mapper>
   123456789101112
   ```

3. 写service层

   ```java
   public interface UserService {
       public User queryUserByName(String name);
   }
   123
   ```

   ```java
   @Service
   public class UserServiceImpl implements UserService {
     @Autowired
     UserMapper userMapper;
   
     @Override
     public User queryUserByName(String username) {
   
       return userMapper.queryUserByName(username);
     }
   }
   1234567891011
   ```

   测试项目可以直接调用dao，不写service层，但公司项目一般要求写service层

## 实现授权

1. 对资源设置权限

   ```java
   //拦截
   Map<String, String> filterMap = new LinkedHashMap<>();
   filterMap.put("/add","perms[user:add]");
   filterMap.put("/update","perms[user:update]");
   bean.setFilterChainDefinitionMap(filterMap);
   
   //未授权就跳转到此请求
   bean.setUnauthorizedUrl("/noauth");
   12345678
   ```

2. 对登陆用户进行授权,该用户拥有的权限从数据库取得

   ```java
   //授权
   @Override
   protected AuthorizationInfo doGetAuthorizationInfo(PrincipalCollection principalCollection) {
     System.out.println("执行了=》授权");
   
     SimpleAuthorizationInfo info = new SimpleAuthorizationInfo();
   
     //拿到当前登陆的对象
     Subject subject = SecurityUtils.getSubject();
     User currentUser = (User)subject.getPrincipal();//拿到User
     info.addStringPermission(currentUser.getPerms());//授权
   
     return info;
   }
   1234567891011121314
   ```

## 整合thymeleaf

1. 导入shiro整合thymeleaf的maven资源

   ```xml
   <!--        shiro-thymeleaf整合-->
   <dependency>
     <groupId>com.github.theborakompanioni</groupId>
     <artifactId>thymeleaf-extras-shiro</artifactId>
     <version>2.0.0</version>
   </dependency>
   123456
   ```

2. 导入命名空间（不导没有提示，但不影响使用）

   ```html
   xmlns:shiro="http://www.thymeleaf.org/thymeleaf-extras-shiro"
   1
   ```

3. 配置bean

   ```java
   @Bean
   //整合shiroDialect ：用来整合shiro和thymeleaf
   public ShiroDialect getShiroDialect(){
   
     return new ShiroDialect();
   }
   123456
   ```

4. 实现登陆后只显示有用户权限的页面的链接

   ```html
   <div shiro:hasPermission="user:add">
     <a th:href="@{/add}">add</a>
   </div>
   <div shiro:hasPermission="user:update">
     <a th:href="@{/update}">update</a>
   </div>
   123456
   ```

# 17、Swagger

接口文档对于前后端开发人员都十分重要。尤其近几年流行前后端分离后接口文档又变成重中之重。接口文档固然重要，但是由于项 目周期等原因后端人员经常出现无法及时更新，导致前端人员抱怨接 口文档和实际情况不一致。

很多人员会抱怨别人写的接口文档不规范，不及时更新。当时当 自己写的时候确实最烦去写接口文档。这种痛苦只有亲身经历才会牢 记于心。

如果接口文档可以实时动态生成就不会出现上面问题。

**Swagger** 可以完美的解决上面的问题。

## Swagger 简介：

Swagger 是一套围绕 Open API 规范构建的开源工具，可以帮助设 计，构建，记录和使用 REST API。

Swagger 工具包括的组件：

- Swagger Editor ：基于浏览器编辑器，可以在里面编写 Open API规范。类似 Markdown 具有实时预览描述文件的功能。
- Swagger UI：将 Open API 规范呈现为交互式 API 文档。用可视化UI 展示描述文件。
- Swagger Codegen：将 OpenAPI 规范生成为服务器存根和客户端 库。通过 Swagger Codegen 可以将描述文件生成 html 格式和 cwiki 形 式的接口文档，同时也可以生成多种言语的客户端和服务端代码。

Swagger Inspector：和 Swagger UI 有点类似，但是可以返回更多 信息，也会保存请求的实际参数数据。

Swagger Hub：集成了上面所有项目的各个功能，你可以以项目 和版本为单位，将你的描述文件上传到 Swagger Hub 中。在 Swagger Hub 中可以完成上面项目的所有工作，需要注册账号，分免费版和收费版。

使用 Swagger，就是把相关的信息存储在它定义的描述文件里面（yml 或 json 格式），再通过维护这个描述文件可以去更新接口文档， 以及生成各端代码。

## Swagger集成

1. 导入maven依赖

   ```xml
   <!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
   <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger-ui</artifactId>
     <version>2.9.2</version>
   </dependency>
   <!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
   <dependency>
     <groupId>io.springfox</groupId>
     <artifactId>springfox-swagger2</artifactId>
     <version>2.9.2</version>
   </dependency>
   123456789101112
   ```

2. 创建SwaggerConfig.java

   ```java
   @Configuration
   @EnableSwagger2   //开启Swagger2
   public class SwaggerConfig{
   
   }
   12345
   ```

3. 运行访问`http://localhost:8080/swagger-ui.html`进行测试

## Swagger配置

在SwaggerConfig进行如下配置即可自定义Swagger配置

```java
@Configuration
@EnableSwagger2   //开启Swagger2
public class SwaggerConfig{
  @Bean
  public Docket docket(){

    return new Docket(DocumentationType.SWAGGER_2).apiInfo(apiInfo());
  }
  private ApiInfo apiInfo(){
    //作者信息
    Contact contact = new Contact("李海洋", "codekitty.cn:8000", "L18249290950@126.com");

    return new ApiInfo("codekitty's Swagger API Documentation", "千里之行，始于足下", "1.0", "codekitty.cn:8000",contact , "Apache 2.0", "http://www.apache.org/licenses/LICENSE-2.0", new ArrayList());
  }
}
123456789101112131415
```

## Swagger扫描接口

1. Docket(DocumentationType.SWAGGER_2).select()

```java
new Docket(DocumentationType.SWAGGER_2)
  .apiInfo(apiInfo())
  .enable(b)//是否启用Swagger，false则不启用
  .select()
  //RequestHandlerSelectors,配置要扫描接口的方式
  //basePackage，指定扫描包
  //                .apis(RequestHandlerSelectors.any()),扫描全部
  //                .apis(RequestHandlerSelectors.none()),不扫描
  //                withMethodAnnotation(GetMapping.class)) //扫描类上的注解
  //                withClassAnnotation(GetMapping.class)) //扫描方法上的注解
  .apis(RequestHandlerSelectors.basePackage("com.controller"))
  //Path过滤路径
  //                .paths(PathSelectors.ant("/com/**"))

  .build();
123456789101112131415
```

1. 实现开发环境中使用Swagger，运行上线环境中不使用Swagger

```java
public Docket docket(Environment environment){
//设置要显示的Swagger环境
Profiles profiles = Profiles.of("dev","test");
//获取项目的环境：判断是否处在自己设定的环境中
boolean flag = environment.acceptsProfiles(profiles);
}
123456
```

在properties中选择使用的环境,将flag传入`Enable()`

1. 通过`groupName("")`配置多个Docket，(在多人开发中，每个开发者配置一个自己的Swagger，方便管理)

```java
@Bean
public Docket docket1(){
  return new Docket(DocumentationType.SWAGGER_2).groupName("A");
}
@Bean
public Docket docket2(){
  return new Docket(DocumentationType.SWAGGER_2).groupName("B");
}
@Bean
public Docket docket3(){
  return new Docket(DocumentationType.SWAGGER_2).groupName("C");
}
123456789101112
```

## 实体类配置

```java
@ApiModel("用户实体类")
public class User {
    @ApiModelProperty("用户名")
    private String username;
    @ApiModelProperty("密码")
    private String password;
123456
```

在Controller进行配置请求

```java
@ApiOperation("user请求")
    //只要接口中返回值存在实体类，它就会被扫描到Swagger中
    @PostMapping(value = "/user")
    public String user(@ApiParam("用户名")String username){
        return "hello" + username;
    }
123456
```

就可以在Swagger显示实体类的信息，如果属性是private需要加get,set方法

**总结：**

1. 我们可以通过Swagger给一些比较难理解的属性或接口增加注释信息
2. 接口文档实时更新
3. 可以在线测试

【注意】在正式发布时要关闭Swagger！！！可以保证安全和避免浪费性能