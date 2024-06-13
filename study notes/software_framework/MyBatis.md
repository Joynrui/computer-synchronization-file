# MyBatis

- `MyBatisPlus` dependency, MySQL 

```xml
<!--MyBatisPlus dependency-->
        <dependency>
            <groupId>com.baomidou</groupId>
            <artifactId>mybatis-plus-boot-starter</artifactId>
            <version>3.4.3.1</version>
        </dependency>
        <!--mysql driver-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
        <!--database connector pool-->
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid-spring-boot-starter</artifactId>
            <version>1.2.18</version>
        </dependency>
```

- 配置数据源

```properties
#数据源类型
spring.datasource.type=com.alibaba.druid.pool.DruidDataSource
#数据库驱动 MySQL 3.8.X
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
#数据库地址
spring.datasource.url=jdbc:mysql://localhost:3306/springboottestdb?useSSL=false
spring.datasource.username=root
spring.datasource.password=root1234
#mybatis日志输出
mybatis-plus.configuration.log-impl=org.apache.ibatis.logging.stdout.StdOutImpl
```

- `@MapperScan("com")`:`MapperScan` annotation is `MyBatis` mapping directory. Write on boot class name generally.

- mybatis CRUD annotation 

| annotation | function                              |
| ---------- | ------------------------------------- |
| @Insert    | 插入                                  |
| @Delete    | 删除                                  |
| @Update    | 更新                                  |
| @Select    | 选择                                  |
| @Result    | 结果集封装                            |
| @Results   | 可以与@Result一起使用，封装多个结果集 |
| @One       | 一对一结果集封装                      |
| @Many      | 一对多结果集封装                      |



eg.,MyBatis CRUD

```java
@Mapper
public interface UserBatisTestMapper {
    // return 1 means success, else return 0 means fail.
    @Insert("insert into user values(#{id},#{username}, #{password})")
    int add(UserBatisTest userBatisTest);

    // return 1 means success, else return 0 means fail.
    @Delete("delete from user where id=#{id}")
    int delete(int id);

    // return 1 means success, else return 0 means fail.
    @Update("update user set username=#{username}, password=#{password} where id=#{id}")
    int update(UserBatisTest userBatisTest);

    // return 1 means success, else return 0 means fail.
    @Select("select * from user where id=#{id}")
    int selectById(int id);

    @Select("select * from user")
    List<UserBatisTest> getAll();
}
```

- `MyBatisPlus CRUD`

`MyBatisPlus` has more convenient method to operating data

Like this:

```java
// User is a bean object
public interface UserMapper extends BaseMapper<User> {
	// you will undo any base CRUD on the bean object, BaseMapper implement it.   
}
```



