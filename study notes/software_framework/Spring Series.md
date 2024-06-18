# 1 Spring Series



##  1.1 Spring boot feature introduction

**Spring Boot** makes it easy to create **stand-alone,** production-grade Spring based Applications that you can "just run".

Most Spring Boot applications need **minimal Spring configuration**.



- **dependency management ** 

![image-20230318154215191](assets/Spring%20Series.assets/image-20230318154215191.png)

- **Auto-configuration**

- **Packaging and Runtime**

- **Integration Testing**



## 1.2 The First Spring boot project

- Use Spring initalizr to create project, official website has this method and IDEA also integrated. (remember add dependencies(like <font color="red">spring web</font>)) 

attentions:

- project structure

![image-20230318191602118](assets/Spring%20Series.assets/image-20230318191602118.png)



-  An example of pom.xml 

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
    <!--The most important part of spring boot-->
    <!--begin-->
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>2.7.5</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
    <!--end-->
	<groupId>com.max</groupId>
	<artifactId>maxspring</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>maxspring</name>
	<description>Demo project for Spring Boot</description>
    <!--attention on java version, it's should being allows to spring boot version.
		(spring boot 3.0.0 only support java 17 and later version, 
		if you use java 8, make sure the version of spring-boot-starter-parent version before the 3.0.0 )-->
	<properties>
		<java.version>8</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
                <!--if you change version after build, and then rebuild, spring-boot-maven-plugin maybe report error.
 					in this case, you can add the version here, and clear cache,restart IDEA-->
                <!--it haven't version tag here by default.-->
				<version>2.7.5</version>
			</plugin>
		</plugins>
	</build>

</project>

```

[IntelliJ IDEA 配置 Maven 最全说明 | 程序员笔记 (knowledgedict.com)](https://www.knowledgedict.com/tutorial/idea-config-maven.html)

##  1.3 Create Spring project in IDEA



- create spring project in IDEA 

![image-20230319105058331](assets/Spring%20Series.assets/image-20230319105058331.png)



- change banner

banner is the logo in console. Create banner.txt in **resources**.

![image-20230319105901362](assets/Spring%20Series.assets/image-20230319105901362.png)

![image-20230319112631050](assets/Spring%20Series.assets/image-20230319112631050.png)

attention: It will appear the spring logo on file brand like this:

![image-20230319112308914](assets/Spring%20Series.assets/image-20230319112308914.png)

the "shut down" button is spring boot logo. 



- change project port

```properties
#application.properties
#change tomcat server port
#8080 by default
server.port=8081 

```



## 1.4 Controller

### 1.4.1 `@Controller`与 `@RestController`

`@Controller`用于非前后端分离的项目类型，`@Controller`中返回的参数是MVC中的视图层View，而`@RestController`用于前后端分离的项目，控制器层的方法返回的是一个字符串，并将字符串转换为JOSN格式数据发送给前端。



### 1.4.2 `@RequestParam`

用于处理方法接收的参数与方法的形参不一致的情况

usage example:

```java
@RequestMapping(value = "/getTest3",method = RequestMethod.GET)
    public String getTest3(@RequestParam(value = "nickname", required = false)String name) {
        System.out.println(name);
        return "get request";
    }
```



## 1.5 Set static file access directory

```properties
# 设置默认静态资源访问路径格式，如设置为"/images/**"路径,要访问static目录中的文件则必须加上images前缀，即"http://localhost:8080/images/test.jpg"
# 默认值为 "/**"
spring.mvc.static-path-pattern=/**
# 设置编译完成时，静态资源的路径名称。源代码包路径保持一致。必须加前缀"classpath:"。
spring.web.resources.static-locations=classpath:/filename
```



## 1.6 File Upload

**文件上传原理**

- 表单的 `enctype` 属性规定在发送到服务器之前应该如何对表单数据进行编码。
- 当表单的`enctype="application/x-www-form-urlencoded"`（default）时，form表单中的数据格式为：`key=value&key=value`。
- 当表单的`enctype="multipart/form-data"`时，其传输数据的形式如何下：

![image-20230726214649767](assets/Spring%20Series.assets/image-20230726214649767.png)

- Spring Boot 工程嵌入的tomcat限制了请求的文件大小，每个文件的配置最大为1MB，单次请求的文件总数不能大于10MB。
- 要更改这个默认值需要在配置文件（`application.properties`）中加入两个配置。

```properties
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
```

- 当表单的`enctype="multipart/form-data"`时，可以使用``MultipartFile`获取上传文件数据，在通过`transferTo`方法将其写入磁盘当中。

eg.,

```java
@RestController
public class FileController {
    /**
     * UPLOADED_FOLDER为上传文件所在的项目地址
     */
    private static final String UPLOADED_FOLDER = System.getProperty("user.dir") + "/upload/";

    @PostMapping("/upload")
    public String upload(String nickname, MultipartFile f, HttpServletRequest request) throws IOException {
        System.out.println(nickname);
        // 获取图片原始名称
        System.out.println("文件名称：" + f.getOriginalFilename());
        // 获取文件大小
        System.out.println("文件大小：" + f.getSize());
        // 获取文件类型
        System.out.println("文件类型：" + f.getContentType());
        // 获取上传文件的项目文件地址
        System.out.println(UPLOADED_FOLDER);
        // 获取系统真实路径
        String path = request.getServletContext().getRealPath("/upload/");
        System.out.println(path);
        saveFile(f, path);
        return "upload success";
    }

    /**
     * Take the file that you want upload to the server. (request --> server directory)
     * @param f
     * @param path
     * @throws IOException
     */
    public void saveFile(MultipartFile f, String path) throws IOException {
        // 判断路径是否存在，不存在则创建路径
        File upDir = new File(path);
        if (!upDir.exists()) {
            upDir.mkdir();
        }
        // 创建file对象存储路径
        File file = new File(path + f.getOriginalFilename());
        // 使用transferTo()方法将网络上传输的文件存储到此目录当中
        f.transferTo(file);
    }
}
```

focus：开发阶段每次tomcat存储上文件的路径都会改变，所以每次上传文件前要先重启服务器。





## 1.7 Spring Boot Interceptor

拦截器适用于全局操作，应用场景如下：

- 权限查看：登录检测，进入处理程序检测是否登录，如果没有，则直接返回登录页面。
- 性能监控：有时系统运行缓慢，可以通过拦截器在进入处理程序之前记录开始时间，在处理完后记录结束时间，从而得到该请求的处理时间
- 通用行为：读取cookie得到用户信息并将用户对象放入请求，从而方便后续流程使用。还有哦Locale, Theme信息等，只要时多个处理程序都需要的，即可使用拦截器实现。



Spring Boot 中的拦截器：

- Spring Boot 定义了`HandlerInterceptor`接口来实现自定义拦截器的功能。
- `HandlerInterceptor`接口定义了`preHandle`、`postHandle`、`afterCompletion`三种方法，通过重写这三种方法实现请求前，请求后等操作。

![image-20230801160614993](assets/Spring%20Series.assets/image-20230801160614993.png) 



an implementation example of interceptor

- definition:

```java
public class LoginInterceptor implements HandlerInterceptor {
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("Prehandle in LoginInterceptor");
        return true;
    }
}
```

### 1.7.1 Interceptor registry

- `addPathPatterns`方法定义拦截器地址
- `excludePathPatterns`定义排除某些地址不被拦截
- 添加的一个拦截器没有`addPathPattern`任何一个`url`则默认拦截所有请求。
- 如果没有`excludePathPatterns`任何一个请求，则默认不放过任何一个请求。

an implementation example of interceptor registry 

```java
@Configuration
public class WebConfigurer implements WebMvcConfigurer {

    /**
     *  This method add the interceptor which you create, and put it on specified directory. And the interceptor
     *  will work on this directory.
     * @param registry
     */
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoginInterceptor()).addPathPatterns("/user/**");
    }
}
```



### 1.7.2 Interceptor data localized question

- `request.getAttribute`表示从request范围取得设置的属性，必须要先`setAttribute`设置属性，才能通过`getAttribute`来取得，设置与取得的为Object对象类型 。

- `request.getParameter`表示接收参数，参数为页面提交的参数，包括：表单提交的参数、URL重写（就是xxx?id=1中的id）传的参数等，因此这个并没有设置参数的方法（没有`setParameter`），而且接收参数返回的不是Object，而是String类型。

- `setAttribute`的参数是String 和 Object ,

​		1.放的时候：`Double res = new Double(result)`;//包装

​				`request.setAttribute(“result”, res);`//再设置进去

​		2.取的时候：``Double res = (Double)request.getAttribute(“result”);``

​				`double result = res.doublue();`

- 另外，需要注意的是使用request.setAttribute时不能使redirect而是forward。即是将请求转发而不是重定向.

[link](https://developer.aliyun.com/article/861741)



# 2 Spring Data JPA

