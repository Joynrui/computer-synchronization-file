# Spring Boot Pen Pal Diary Platform Developing Log

## 2023.7.22 before

- ES6 basic fundamental syntax.(ECMAScript)
- The integration of the TinyMCE Editor in fore-end page. 
- access cache question.

## 2023.7.22

- The different about Spring Boot annotation `@Controller` and `@RestController`.
- `GetMapping()`,`PostMapping()` and `@RequestMapping(value="directory", method="RequestMethod.GET"), @RequestMapping(value="directory", method="RequestMethod.POST")` is equivalent.
- Controller parameter transmit.



## 2023.7.23

- basic usage of GET request in Spring Boot
- basic usage of POST request in Spring Boot
- The usage of `@RequestParam()`
- json format data transmit by fore-end, how to receive in  back-end post request.
- apifox test devtools
- IDEA Http Client test



## 2023.7.26

- Set static resources file access directory in `application.properties`.

- Set static target access directory pattern.

- file upload





## 2023.8.1

- Spring Interceptor

- RESTful service(RESTful framework): a API developing design style.
-  http method



## 2023.8.5

- swagger
- `MyBatis` and `MyBatisPlus` base CRUD
- http request type post get put delete ... 





## 2023.8.9

- Vue basic application



## 2023.8.17

- Vue components
- different between Vue2 and Vue3
- `Element-ui` basic function
- `Axios` basic function: an Ajax framework  



## 2023.8.19

- diary front end **basic** structure design

- confirm develop process: front-end -> data dictionary -> back-end -> database 



## 2023.8.25

- beginning of `Vue Router`
- beginning of `Vuex`



## 2023.9.7

- certain user page container



## 2024.1.2

- feature: 识别登录状态，在start页面，点击start button, 若未登录，则跳转登录页面；若已登录，则直接跳转主页面；

> 解决方法：使用vue路由导航守卫，判断请求地址与本地token状态。



## 2024.1.14

- feature: front register page;
- feature: back-end register function;

## 2024.1.17 

- feature: complete register function, front and back; 



## 2024.1.19

- bug: 修改login功能相关bug;





# Question summary

- 查询用户信息时，使用uid作为参数安全还是使用user实体好？

```
1.使用用户实体作为参数：
	使用用户实体作为参数通常在需要更多查询条件的情况下使用，例如根据多个属性来筛选用户。
	这种方式更灵活，可以根据用户实体的属性来构建查询条件。
需要小心防止非法注入其他属性的风险，可以使用验证和过滤来确保传入的用户实体只包含必要的属性。

2.如果你选择使用用户实体作为参数，并担心非法注入其他属性的风险，可以考虑以下几种方式来加强安全性：
	使用验证：在接收到用户实体后，执行验证操作，确保只有合法的属性被使用。
	过滤属性：在接收到用户实体后，可以在服务层对属性进行过滤，只保留需要的属性。
	使用DTO（数据传输对象）：创建一个专门用于查询的DTO，只包含查询条件所需的属性，而不是整个用户实体。
无论你选择哪种方式，都需要根据具体的需求和安全要求来做出决策，并采取适当的安全措施以防止非法操作。
```

