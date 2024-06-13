# Web Frameworks List







# Front end Framework

## Vue.js





# Back end Framework

**Most popular backend frameworks** 

![image-20230317173226297](assets/Web%20Frameworks.assets/image-20230317173226297.png)





First, learn <font color="red">spring boot</font>, then begin to learn <font color="red">spring MVC</font> and <font color="red">SSM</font> (*Spring  +  SpringMVC + Mybatis*) 

 

## Spring Boot



# ORM: Object Related Mapping

**Object-relational mapping** (ORM) is a mechanism that makes it possible to address, access and manipulate objects without having to consider how those objects relate to their data sources.

ORM has many frameworks such as Hibernate, Mybatis.



## Hibernate

## MyBatis





### JPA

A JPA (Java Persistence API) is a specification of Java which is used to access, manage, and persist data between Java object and relational database. It is considered as a standard approach for Object Relational Mapping.

JPA can be seen as a bridge between object-oriented domain models and relational database systems. Being a specification, JPA doesn't perform any operation by itself. Thus, it requires implementation. So, ORM tools like Hibernate, TopLink, and iBatis implements JPA specifications for data persistence.





#### Need of JPA

As we have seen so far, JPA is a specification. It provides common prototype and functionality to ORM tools. By implementing the same specification, all ORM tools (like Hibernate, TopLink, iBatis) follows the common standards. In the future, if we want to switch our application from one ORM tool to another, we can do it easily.



#### JPA VS Hibernate



| JPA                                                          | Hibernate                                                    |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| Java Persistence API (JPA) defines the management of relational data in the Java applications. | Hibernate is an Object-Relational Mapping (ORM) tool which is used to save the state of Java object into the database. |
| It is just a specification. Various ORM tools implement it for data persistence. | It is one of the most frequently used JPA implementation.    |
| It is defined in **`javax.persistence`**package.             | It is defined in **`org.hibernate`** package.                |
| The **`EntityManagerFactory`** interface is used to interact with the entity manager factory for the persistence unit. Thus, it provides an entity manager. | It uses **`SessionFactory`** interface to create Session instances. |
| It uses **`EntityManager`** interface to create, read, and delete operations for instances of mapped entity classes. This interface interacts with the persistence context. | It uses **`Session`** interface to create, read, and delete operations for instances of mapped entity classes. It behaves as a runtime interface between a Java application and Hibernate. |
| It uses **`Java Persistence Query Language`** (JPQL) as an object-oriented query language to perform database operations. | It uses **`Hibernate Query Language`** (HQL) as an object-oriented query language to perform database operations. |





# RESTful

- 一种流行的互联网软件服务架构设计风格。

- 全称Representational State Transfer, 表述性状态转移。

- RESTful不是一个标准，而是一组Client 与 Server 交互时的架构理念和设计原则，基于这个架构理念和设计原则的Web API更加简洁，更有层次。



## features of RESTful

- 每一个URL代表一种资源
- Client使用GET,POST,PUT,DELETE四种表示操作的动词对Server资源进行操作：

>- GET用于获取资源， 或称 C 从 S 获取资源。
>- POST用于新建资源，或称 C 向 S 发送资源。
>- PUT用于更新资源， 或称 C 向 S 发送 S 中已存在资源的新版本，更新资源。
>- DELETE用于删除资源。

- 通过操作资源的表现形式实现服务端请求操作。

- 资源的表现形式为JSON or HTML。
- C 与 S 之间的交互在请求之间是无状态的，从C到S的每个请求都包含必须的信息。



**符合RESTful规范的Web API需要具备以下两个关键特性：**

- 安全性：安全的方法被期望不会产生任何副作用，当我们使用GET操作获取资源时，不会引起资源本身的改变，也不会引起服务器状态改变。
- 幂等性：幂等的方法保证了重复进行一个请求和一次请求的效果相同（并不是指响应总是相同的，而是指服务器上的资源状态从第一次请求后就不在改变了），在数学上幂等性时指N次变换的结果和一次变换相同。

### Http Method

Http提供了POST,GET, PUT, DELETE等操作类型对某个Web资源进行**<font color="gree">Create、Read、Update和Delete操作。</font>**

一个HTTP请求除了利用URL标志目标资源之外，还需要通过HTTP Method指定针对该资源的操作类型，一些常见的HTTP方法及其在RESTful风格下的使用：

![image-20230801203457838](assets/Web%20Frameworks.assets/image-20230801203457838.png)

- focus:<font color=red>除POST以外，其他请求参数都在请求参数中而不在请求体中。</font>



# Swagger

- Swagger 是一个规范和完整的框架，用于生成、描述、调用和可视化RUSTful风格的Web服务器，是非常流行的API表达式工具。
- Swagger能够自动生成完善的RESTful API 文档，同时并根据后台代码的修改同步更新，同时提供完整的测试页面来调试API。

- 需求依赖

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

- Swagger的配置

```java
@Configuration
// enable Swagger function
@EnableSwagger2
public class Swagger2Config {
    @Bean
    public Docket CreateRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                // com包下所有API都交给Swager2管理
                .apis(RequestHandlerSelectors.basePackage("com"))
                .paths(PathSelectors.any()).build();

    }

    /**
     *  API文档页面显示信息
     * @return ApiInfoBuilder()
     */
    private ApiInfo apiInfo(){
        return new ApiInfoBuilder()
                .title("演示项目API")
                .description("学习Swagger1的演示项目")
                .build();
    }
}
```

- <font color=red>focus</font>: Spring Boot 2.6.X后与Swagger有版本冲突问题，需要在`application.properties`中添加以下配置”

```properties
spring.mvc.pathmatch.matching-strategy=ant_path_matcher
```

- access address: `http://127.0.0.1:8080/swagger-ui.html`

- swagger annotation

![image-20230805152722189](assets/Web%20Frameworks.assets/image-20230805152722189.png)





# Cross Origin Question

为了保证browser的安全，不同源的客户端脚本在没有明确授权的情况下，不能读写对方资源，称为同源策略，同源策略时浏览器安全的基石。

- 同源策略（`Sameoriginpolicy`）是一种约定，它是浏览器最核心也是最基本的安全功能。
- 同源是指在同一个域内，就是两个页面具有相同的<font color="red">协议，主机和端口号</font>。
- 当一个请求URL的协议，域名，端口三者之前任意一个与当前页面URL不同，即为跨域，此时无法读取非同源网页的Cookie，无法向非同源地址发送Ajax请求。

## CORS

- CORS, Cross-Origin Resource Sharing, 是由W3C制定的一种跨域资源共享技术标准，其目的是为解决前端的跨区请求。

- CORS可以在不破坏已有规则的情况下，通过后端服务器实现CORS接口，从而实现跨域通信。
- CORS将请求分为两种：**简单请求和非简单请求**， 分别对跨域通信提供了支持。



### 简单请求

某些请求不会触发 [CORS 预检请求](https://developer.mozilla.org/zh-CN/docs/Glossary/Preflight_request)。在废弃的 [CORS 规范](https://www.w3.org/TR/2014/REC-cors-20140116/#terminology)中称这样的请求为*简单请求*，但是目前的 [Fetch 规范](https://fetch.spec.whatwg.org/)（CORS 的现行定义规范）中不再使用这个词语。

其动机是，HTML 4.0 中的 [form](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/form) 元素（早于跨站 [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 和 [`fetch`](https://developer.mozilla.org/zh-CN/docs/Web/API/fetch)）可以向任何来源提交简单请求，所以任何编写服务器的人一定已经在保护[跨站请求伪造攻击](https://developer.mozilla.org/zh-CN/docs/Glossary/CSRF)（CSRF）。在这个假设下，服务器不必选择加入（通过响应预检请求）来接收任何看起来像表单提交的请求，因为 CSRF 的威胁并不比表单提交的威胁差。然而，服务器仍然必须提供 [`Access-Control-Allow-Origin`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Access-Control-Allow-Origin) 的选择，以便与脚本*共享*响应。



若请求**满足所有下述条件**，则该请求可视为*简单请求*：

- 使用下列方法之一：

    - [`GET`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)
    - [`HEAD`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/HEAD)
    - [`POST`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/POST)

- 除了被用户代理自动设置的标头字段（例如`Connection`,`User-Agent`或其他在 Fetch 规范中定义为"禁用标头名称"的标头），允许人为设置的字段为 Fetch 规范定义的对 CORS 安全的标头字段集合

    。该集合为：

    - [`Accept`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept)
    - [`Accept-Language`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Accept-Language)
    - [`Content-Language`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Language)
    - [`Content-Type`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Content-Type)（需要注意额外的限制）
    - [`Range`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Headers/Range)（只允许[简单的范围标头值](https://fetch.spec.whatwg.org/#simple-range-header-value) 如 `bytes=256-` 或 `bytes=127-255`）

- `Content-Type`标头所指定的媒体类型的值仅限于下列三者之一：
    - `text/plain`
    - `multipart/form-data`
    - `application/x-www-form-urlencoded`
- 如果请求是使用 [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 对象发出的，在返回的 [`XMLHttpRequest.upload`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest/upload) 对象属性上没有注册任何事件监听器；也就是说，给定一个 [`XMLHttpRequest`](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 实例 `xhr`，没有调用 `xhr.upload.addEventListener()`，以监听该上传请求。
- 请求中没有使用 [`ReadableStream`](https://developer.mozilla.org/zh-CN/docs/Web/API/ReadableStream) 对象。



简单来说，简单请求使，CORS策略会在header中增加一个origin字段：

```
Origin:http://localhost:8081
```

服务端收到请求后，根据该字段判断是否允许该请求访问，如果允许，则在response HTTP header信息中添加Access-Control-Allow-Origin字段：

```
// * 代表所有的源域，也可以指定源域
Access-Control-Allow-Origin: *
```

### 预检请求

与简单请求不同，“需预检的请求”一般称为非简单请求，要求必须首先使用 [`OPTIONS`](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/OPTIONS) 方法发起一个预检请求到服务器，以获知服务器是否允许该实际请求。"预检请求“的使用，可以避免跨域请求对服务器的用户数据产生未预期的影响。

- 预检请求将真实请求的信息，包括请求方法，自定义字段，源信息，添加到http header信息字段中，询问服务器是否允许这样的操作。

eg.,

 browser request:

```
OPTION:/test HTTP:/1.1
Origin:http://localhost:8081
Access-Control-Request-Method:GET
Access-Control-Request-Headers:X-Costom-Header
Host:localhost:8081
```

Access-Control-Request-Headers 包含请求的自定义header字段

Server response:

```
Access-Control-Allow-Origin:http://localhost:8081
Access-Control-Allow-Methods:GET,POST,PUT,DELETE
Access-Control-Allow-Headers:X-Custom-Header
Access-Control-Allow-Credenticals:true
//Unit second
Access-Control-Max-Age: 1728000 
```

Access-Control-Allow-Headers: 是否允许用户发送，处理cookie

Access-Control-Max-Age：超过有效期重发预检请求



### CORS using in Spring Boot



Configuration Class: This direction used to  Mapping all of the project, and you needn't to add `@CrossOrigin` annotation at every Controller.(That's an another direction)

```java
public class CorsConfig implements WebMvcConfigurer {
    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOriginPatterns("*")
                .allowedMethods("POST","GET","PUT", "OPTION", "DELETE")
                .maxAge(168000)
                .allowedHeaders("*")
                // 是否发送cookie
                .allowCredentials(true);
    }
}
```



# SLF4J



![image-20231015210546114](assets/Web%20Frameworks.assets/image-20231015210546114.png)
