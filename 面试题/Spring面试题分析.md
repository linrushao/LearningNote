# Spring面试题分析

## 1 开发中主要使用Spring的什么技术?

①.IOC容器管理各层的组件

②.使用AOP配置声明式事务

③.整合其他框架.

## 2 简述AOP和IOC概念

**AOP**:Aspect Oriented Program,面向(方面)切面的编程;Filter(过滤器)也是一种AOP.AOP是一种新的方法论,是对传统OOP(Object-Oriented Programming,面向对象编程)的补充.AOP的主要编程对象是切面(aspect),而切面模块化横切关注点.可以举例通过事务说明.

**IOC**:InvertOfControl,控制反转.也成为DI(依赖注入)其思想是反转资源获取的方向.传统的资源查找方式要求组件向容器发起请求查找资源.作为回应,容器适时的返回资源.而应用了IOC之后,则是容器主动地将资源推送给它所管理的组件,组件所要做的仅是选择一种合适的方式来接受资源.这种行为也被称为查找的被动形式

## 3 在Spring中如何配置Bean?

Bean的配置方式:通过全类名（反射）、通过工厂方法（静态工厂方法&实例工厂方法）、FactoryBean

## 4 IOC容器对Bean的生命周期

①.通过构造器或工厂方法创建Bean实例

②.为Bean的属性设置值和对其他Bean的引用

③.将Bean实例传递给Bean后置处理器的postProcessBeforeInitialization方法

④.调用Bean的初始化方法(init-method)

⑤.将Bean实例传递给Bean后置处理器的postProcessAfterInitialization方法

⑦.Bean可以使用了

⑧.当容器关闭时,调用Bean的销毁方法(destroy-method)

## 5 Spring如何整合Struts2?

整合Struts2,即由**IOC容器**管理Struts2的Action:

- 安装Spring插件:把struts2-spring-plugin-2.2.1.jar复制到当前WEB应用的WEB-INF/lib目录下
- 在Spring的配置文件中配置Struts2的Action实例
- 在Struts配置文件中配置action,但其class属性不再指向该Action的实现类,而是指向Spring容器中Action实例的ID

## 6 Spring如何整合Hibernate

整合Hibernate,即由**IOC容器**生成SessionFactory对象,并使用Spring的声明式事务

- 利用LocalSessionFactoryBean工厂Bean,声明一个使用XML映射文件的SessionFactory实例.
- 利用HibernateTransactionManager配置Hibernate的事务管理器

## 7 SpringMVC比较Struts2

①.SpringMVC的入口是Servlet,而Struts2是Filter

②.SpringMVC会稍微比Struts2快些.SpringMVC是基于方法设计,而Sturts2是基于类,每次发一次请求都会实例一个Action.

③.SpringMVC使用更加简洁,开发效率SpringMVC确实比struts2高:支持JSR303,处理ajax的请求更方便

④.Struts2的OGNL表达式使页面的开发效率相比SpringMVC更高些.

## 8 SpringMVC的运行流程

①.在整个SpringMVC框架中，DispatcherServlet处于核心位置，负责协调和组织不同组件以完成请求处理并返回响应的工作

②.SpringMVC处理请求过程：

- 若一个请求匹配DispatcherServlet的请求映射路径(在web.xml中指定),WEB容器将该请求转交给DispatcherServlet处理
- DispatcherServlet接收到请求后,将根据请求信息(包括URL、HTTP方法、请求头、请求参数、Cookie等)及HandlerMapping的配置找到处理请求的处理器(Handler).可将HandlerMapping看成路由控制器，将Handler看成目标主机。
- 当DispatcherServlet根据HandlerMapping得到对应当前请求的Handler后，通过HandlerAdapter对Handler进行封装，再以统一的适配器接口调用Handler。
- 处理器完成业务逻辑的处理后将返回一个ModelAndView给3DispatcherServlet,ModelAndView包含了视图逻辑名和模型数据信息
- DispatcherServlet借助ViewResoler完成逻辑视图名到真实视图对象的解析>得到真实视图对象View后,DispatcherServlet使用这个View对ModelAndView中的模型数据进行视图渲染

## 9 说出SpringMVC常用的5个注解

>  @RequestMapping、@PathVariable、@RequestParam、@RequestBoy、@ResponseBody

## 10 如何使用SpringMVC完成JSON操作

①.配置MappingJacksonHttpMessageConverter

②.使用@RequestBody注解或ResponseEntity作为返回值