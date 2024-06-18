# BS Software Architecture

## Spring back-end architecture

### data persistence

- **Spring Data JPA**
- **Hibernate**
- **Spring Data MongoDB**

### Security

- **Spring Security**
- **JWT**

### Message queue

- **Spring AMQP**: Used to integrate RabbitMQ.
- **Spring Kafka**: Used to integrate Apache Kafka.

主要用于实现异步通信、解耦、负载均衡和弹性扩展等功能。

### REST API developing

- **Spring MVC**

- **Spring HATEOAS**: Used to construct the HATEOAS principle RESTful API.

- **Spring WebFlux**: Used to construct responsive Web applications. (适用于需要高并发和低延迟的应用场景)

### Service registry and discover

- **Spring Cloud Netflix Eureka**: 提供服务注册和发现功能。
- **Spring Cloud Consul**：另一种服务注册和发现工具，基于Consul。

### Configuration management

- **Spring Cloud Config**: 集中化的配置管理，支持动态更新配置。
- **Spring Boot Actuator**：提供监控和管理功能，包括健康检查、指标、审计等。

### Log and monitoring

- **SLF4J**：一个简单的日志门面，支持多种日志框架。

- **Logback**：一个流行的日志框架，常与SLF4J一起使用。

(SLF4J substitute for Commons Logging, Logback substitute for Log4J)

- **ELK Stack（Elasticsearch, Logstash, Kibana）**：用于日志收集、存储和分析。

- **Prometheus + Grafana**：用于监控和可视化应用指标。

#### Test

- JUnit
- Mockito: imitate objects and behaviors for convenient
- Spring Test: integration test supported.

### API Documentation

- **Springfox**：用于生成Swagger文档，便于API文档的自动化生成和管理。

- **OpenAPI**：与Swagger结合，提供标准化的API文档格式。

### Task Scheduling

- **Spring Batch**：用于处理批处理任务，支持大数据量的处理。

- **Quartz Scheduler**：一个功能强大的任务调度器，支持复杂的调度需求。

### Separation of front-end and back-end

- **Spring Boot Starter Websocket**：用于实现WebSocket通信，支持实时数据更新。

- **Spring Boot Starter Thymeleaf**：用于服务器端模板渲染，但在前后端分离项目中，通常会使用单页应用框架（如React、Angular、Vue.js）替代。

### DevOps and Containerization

- **Docker**：用于应用容器化，便于部署和扩展。
- **Kubernetes**：用于容器编排，支持自动化部署、扩展和管理。
- **Jenkins**：用于持续集成和持续部署（CI/CD）。





