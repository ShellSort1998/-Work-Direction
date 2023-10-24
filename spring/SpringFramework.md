# SpringFramework



### 一、技术体系结构

#### 1.1. 总体技术体系

- 单一架构

一个项目、一个工程、导出为war包，在一个Tomcat上运行，==> all in one

<img src="C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231023184248913.png" alt="image-20231023184248913" style="zoom:80%;" />

​		单一架构，项目应用技术：SSM 即 Spring, SpringMVC, Mybatis



- 分布式架构

  一个项目，可以拆分成很多个模块，每个模块是IDEA中的一个module，每个工程都运行在自己的Tomcat上，模块之间可以互相调用，每个模块也可以看作是一个单一架构的应用

  <img src="C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231023184837191.png" alt="image-20231023184837191" style="zoom:100%;" />

  分布式架构，项目主要应用技术框架：SpringBoot (SSM), SpringCloud, 中间件等

  

#### 1.2. 框架概念和理解

- ​	优点：

  - 提高开发效率

  - 降低开发成本

  - 提高应用程序的稳定性

  - 提高标准化解决方案

- 框架可以总结理解为：**框架 = jar包 + 配置文件**

 





## 

## 

## 

## 

### 二、SpringFramework介绍

#### 2.1. Spring 和 SpringFramework

- 广义的Spring：是一个技术栈：Spring Framework、Spring MVC、 SpringBoot、 Spring Data、Spring Security等，Spring Framework是其他的基础

- 狭义的Spring：Spring Framework（基础框架）

  

#### 2.2. SpringFramework主要功能模块

![image-20231023192414971](C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231023192414971.png)

| 功能模块          | 功能介绍                                              |
| ----------------- | ----------------------------------------------------- |
| Core Container  * | 核心容器，在Spring环境下使用任何功能都必须基于IoC容器 |
| AOP 和 Aspects    | 面向切面编程                                          |
| TX                | 声明式事务管理                                        |
| Spring MVC        | 提供了面向Web应用程序的集成功能                       |



#### 2.3. SpringFramework优势

- 丰富的生态 
- 模块化设计
- 简化开发
- 不断更新迭代







## 

## 

## 

## 

### 三、SpringIoC容器 & 核心概念

#### 3.1.组件和组件管理概念

- 组件：可以复用的Java对象

  ![image-20231023193447701](C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231023193447701.png)

- Spring 充当组件管理的角色（IoC)

  - **组件**可以完全交给Spring框架进行管理，Spring框架代替了原有 new对象和对象属性赋值动作等
  - Spring具体的组件管理动作包含：
    1. 组件对象实例化
    2. 组件属性赋值
    3. 组件对象之间的引用
    4. 组件对象存货周期管理
    5. ....... 

  总结：Spring是一个组件的容器，用来创建、管理、存储组件。

  

- 组件交给Spring管理的优势

  - 降低了组件的耦合性
  - 提高可复用性
  - 方便配置和管理
  - 交给Spring管理的组件，可以使用Spring框架的AOP、声明式事务等功能







#### 3.2.Spring IoC容器和容器实现

##### 3.2.1 普通和复杂容器

- 普通容器：数据、集合（List、Set）
- 复杂容器：Spring IoC 



##### 3.2.2 SpringIoC容器

- Spring IoC容器，负责实例化、配置和组装bean（组件）。容器通过 **读取** *<u>配置元数据 </u>*来获取有关实例化、配置和组装组件的指令。配置元数据以 ***XML，Java注解或Java代码***

![image-20231024145517189](C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231024145517189.png)



##### 3.2.3 SpringIoC容器具体接口和实现类

- SpringIoC容器接口：

  ***BeanFactory*** 接口提供了一种高级配置机制，能够管理任何类型的对象，他是SpringIoC容器标准化超接口

  ***ApplicationContext*** 是 ***BeanFactory* **的子接口，拓展了如下功能：

  - 更容易与Spring的AOP功能集成
  - 消息资源处理（国际化）
  - 特定于应用程序给予接口实现，例如Web应用程序的WebApplicationContext

​		![image-20231024150338131](C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231024150338131.png)

###### <u>**常见的容器对象**</u>

| 类型名                               | 简介                                                         |
| ------------------------------------ | :----------------------------------------------------------- |
| ClassPathXmlApplicationContext *     | 通过读取**类路径**下的XML格式的配置文件，来创建IoC容器对象   |
| FileSystemXmlApplicationContext      | 通过文件**系统路径**读取XML格式的配置文件，来创建IoC容器对象 |
| AnnotationConfigApplicationContext * | 通过读取Java配置类创建IoC容器对象                            |
| WebApplicationContext *              | 基于Web环境创建IoC容器对象，并将对象引入存入ServletContext域中 |

![image-20231024160738042](C:\Users\wwx\AppData\Roaming\Typora\typora-user-images\image-20231024160738042.png)



##### 3.2.4 SpringIoC容器管理配置方式

**Spring**框架提供了多种配置方式：XML、注解、Java配置类

1. **XML**：是Spring框架最早的配置方式之一，通过在XML文件中定义Bean及依赖关系，Bean的作用域等信息，让Spring IoC容器管理Bean之间的依赖关系
2. **注解** *：从Spring2.5 开始提供，可以通过在Bean类上使用注解来代替XML配置文件的配置信息，通过在Bean类上加上相应的注解（@Component，@Service，@Autowired等），将Bean注册到Spring IoC容器中，这样Spring IoC容器就可以管理这些Bean之间的依赖关系
3. **Java配置类方式** *：从Spring3.0 开始提供，通过Java类来定义Bean、Bean之间的依赖关系和配置信息，从而代替XML配置文件方式。通过@Configuration、@Bean等注解来实现Bean和依赖关系的配置。



**推荐：**注解 + 配置类





#### 3.3.Spring IoC / DI 概念总结

##### 3.3.1 IoC 容器



##### 3.3.2 IoC （Inversion of Control） 控制反转

1. 当应用程序需要使用一个对象时，不再是应用程序直接创建该对象，而是交给IoC容器去创建和管理（即控制权由应用程序转移到IoC容器中了，实现了“反转”控制权的操作）。这种方式基本上是通过依赖查找的方式来实现

   （IoC容器创建实例是用到 反射机制）



##### 3.3.3 DI （Dependency Injection）依赖注入

1. DI 是指组件之间传递依赖关系的关系过程中，将**依赖关系**在容器内部进行处理，实现了对象之间的解耦合（因为不必在程序代码中硬编码对象之间的依赖关系）。Spring中，DI是通过XML文件或注解方式实现。
   - 三种DI（依赖注入）形式：
     - 构造函数注入
     - Setter方法注入
     - 接口注入





## 

## 

## 

## 

## 



### 四、SpringIoC实践和应用

 

#### 4.1 Spring IoC / DI 实现步骤	*

- **配置元数据（配置**）

  - 基于XML的配置元数据的基本结构：

    ```xml
    <bean id="..." [1] class="..." [2]>
    	<!-- collaborators and configuration for this bean go here-->
    </bean>
    ```

    ```xml
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xsi:schemaLocation="http://www.springframework.org/schema/beans
                               https://www.springframework.org/schema/beans/spring-beans.xsd">
    
        <bean id="..." [1] class="..." [2]>
    	<!-- collaborators and configuration for this bean go here-->
    	</bean>
        
        <bean id="..." class="...">
    	<!-- collaborators and configuration for this bean go here-->
    	</bean>
    </beans>
    ```

    Spring IoC 容器管理一个或多个组件。例如：在XML中<bean/>形式定义的

    - [**id：**]() 属性是标识单个Bean定义的字符串

    - [**class：**]()属性定义Bean的 *完全限定类名* -------为了IoC使用反射机制

      

- **实例化IoC容器**

​	提供给 **[ApplicationContext]()** 构造函数的位置路径是 资源字符串地址，允许容器从各种外部资源加载配置元数据。

​	IoC容器实例化工作：

```java 
// 实例化ioc容器
ApplicationContext context = new ClassPathXmlApplicationContext("service.xml","daos.xml");
```



- **获取Bean组件**  *

​	**[ApplicationContext]()** 是一个高级工厂接口，能够维护不同Bean以及其依赖项的注册表。通常使用方法 **[T getBean(String name, Class<T> requiredType)]()**，来得到Bean实例。

```java
//创建IoC容器对象，指定配置文件
ApplicationContext context = new ClassPathXmlApplicationContext("service.xml","daos.xml");
//获取ioc容器组件对象
PetStoreService service = context.getBean("petStore",PetStoreService.class);
//使用组件
List<String> userList = service.getUsernameList();
```





#### 4.2 基于XML配置方式组件的管理



#### 4.3 基于注解方式管理 Bean



#### 4.4 基于配置类方式管理 Bean



#### 4.5 三种配置方式的总结



#### 4.6 整合 Spring5-Test5 搭建测试环境



### 五、Spring AOP面向切面编程





### 六、Spring 声明式事务





### 七、Spring 核心掌握总结