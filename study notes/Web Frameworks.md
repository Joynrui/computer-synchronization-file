# Web Frameworks

**Most popular backend frameworks** 

![image-20230317173226297](assets/Web%20Frameworks.assets/image-20230317173226297.png)









First, learn <font color="red">spring boot</font>, than begin to learn <font color="red">spring MVC</font> and <font color="red">SSM</font> (*Spring  +  SpringMVC + Mybatis*)  

##  1 Spring Boot



###  1.1 Spring boot feature introduction

**Spring Boot** makes it easy to create **stand-alone,** production-grade Spring based Applications that you can "just run".

Most Spring Boot applications need **minimal Spring configuration**.



- **dependency management ** 

![image-20230318154215191](assets/Web%20Frameworks.assets/image-20230318154215191.png)

- **Auto-configuration**

- **Packaging and Runtime**

- **Integration Testing**



### 1.2 The First Spring boot project

- Use Spring initalizr to create project, official website has this method and IDEA also integrated. (remember add dependencies(like <font color="red">spring web</font>)) 

attentions:

- project structure

![image-20230318191602118](assets/Web%20Frameworks.assets/image-20230318191602118.png)



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

###  1.3 Create Spring project in IDEA



- create spring project in IDEA 

![image-20230319105058331](assets/Web%20Frameworks.assets/image-20230319105058331.png)



- change banner

banner is the logo in console. Create banner.txt in **resources**.

![image-20230319105901362](assets/Web%20Frameworks.assets/image-20230319105901362.png)

![image-20230319112631050](assets/Web%20Frameworks.assets/image-20230319112631050.png)

attention: It will appear the spring logo on file brand like this:

![image-20230319112308914](assets/Web%20Frameworks.assets/image-20230319112308914.png)

the "shut down" button is spring boot logo. 



- change project port

```properties
#application.properties
#change tomcat server port
#8080 by default
server.port=8081 

```











## ORM

**Object-relational mapping** (ORM) is a mechanism that makes it possible to address, access and manipulate objects without having to consider how those objects relate to their data sources.

ORM has many frameworks such as Hibernate, Mybatis.



### Hibernate

**Hibernate ORM** (or simply **Hibernate**) is an [object–relational mapping](https://en.wikipedia.org/wiki/Object–relational_mapping) tool for the [Java](https://en.wikipedia.org/wiki/Java_(programming_language)) programming language. It provides a [framework](https://en.wikipedia.org/wiki/Software_framework) for mapping an [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming) domain model to a [relational database](https://en.wikipedia.org/wiki/Relational_database). Hibernate handles [object–relational impedance mismatch](https://en.wikipedia.org/wiki/Object–relational_impedance_mismatch) problems by replacing direct, [persistent](https://en.wikipedia.org/wiki/Persistence_(computer_science)) database accesses with high-level object handling functions.

The mapping of Java classes to database tables is implemented by the configuration of an [XML](https://en.wikipedia.org/wiki/XML) file or by using [Java Annotations](https://en.wikipedia.org/wiki/Java_annotation). When using an XML file, Hibernate can [generate](https://en.wikipedia.org/wiki/Program_synthesis) [skeleton](the structure consisting of all the bones) [source code](https://en.wikipedia.org/wiki/Source_code) for the persistence classes. This is [auxiliary]( auxiliary workers provide additional help for another group of workers) when annotations are used. Hibernate can use the XML file or the Java annotations to maintain the [database schema](https://en.wikipedia.org/wiki/Database_schema).



Use the Hibernate, you should import the jars it needs. (from official website)



How Hibernate works (before version 5.0)

![Lightbox](assets/Web%20Frameworks.assets/HBArchi.png)



[hibernate bootastrapping ways](https://www.baeldung.com/hibernate-5-bootstrapping-api)

 [What is the difference between Configuration vs ServiceRegistry vs StandardServiceRegistry?](https://stackoverflow.com/questions/67300459/what-is-the-difference-between-configuration-vs-serviceregistry-vs-standardservi)



**Hibernate Query Language (HQL)**

- Database Independent Query

HQL (Hibernate Query Language) is the object-oriented version of SQL. It generates the database independent queries. So you don't need to write database specific queries. Before Hibernate, if database is changed for the project, we need to change the SQL query as well that leads to the maintenance problem.



**The Hibernate architecture is categorized in four layers:**

- Java application layer
- Hibernate framework layer
- Backhand api layer
- Database layer



high level architecture of Hibernate with **mapping file** and **configuration file**.

![hibernate architecture](assets/Web%20Frameworks.assets/architecture.jpg)





#### H1.1 Elements of Hibernate Architecture

- <font color=red>`SessionFactory`</font>: The `SessionFactory`is a factory of session and client of <font color=red>`ConnectionProvider`</font>. It holds second level cache *(optional)* of data. The `org.hibernate.SessionFactory` interface provides factory method to get the object of Session.
- <font color=red>`Session`</font>: The `session` object provides an interface between the application and data stored in the database. It is a short-lived object and wraps the JDBC connection. It is factory of Transaction, Query and Criteria. It holds a first-level cache *(mandatory)* of data. The `org.hibernate.Session` interface provides methods to **insert, update and delete the object**. It also provides factory methods for Transaction, Query and Criteria.
- <font color=red>`transaction`</font>: The `transaction` object specifies the atomic unit of work. It is *optional*. The `org.hibernate.Transaction` interface provides methods for transaction management.
- <font color=red>`ConnectionProvider`</font>: It is a factory of JDBC connections. It abstracts the application from <font color=red>`DriverManager`</font>or <font color=red>`DataSource`.</font> It is *optional*.

- <font color=red>`TransactionFactory`</font>: It is a factory of Transaction. It is *optional*.





1. A simple Persistent class should follow some **rules:**

- **A no-arg constructor:** It is recommended that you have a default constructor at least package visibility so that hibernate can create the instance of the Persistent class by `newInstance()` method.
- **Provide an identifier property:** It is better to assign an attribute as id. This attribute behaves as a primary key in database.
- **Declare getter and setter methods:** The Hibernate recognizes the method by getter and setter method names by default.
- **Prefer non-final class:** Hibernate uses the concept of proxies, that depends on the persistent class. The application programmer will not be able to use proxies for lazy association fetching.

e.g.,    Employee.java

```java
package com.max.mypackage;  
  
public class Employee {  
private int id;  
private String firstName,lastName;  
  
public int getId() {  
    return id;  
}  
public void setId(int id) {  
    this.id = id;  
}  
public String getFirstName() {  
    return firstName;  
}  
public void setFirstName(String firstName) {  
    this.firstName = firstName;  
}  
public String getLastName() {  
    return lastName;  
}  
public void setLastName(String lastName) {  
    this.lastName = lastName;  
}  
  
  
}  
```





##### elements in hbm.xml

2. Create the mapping file for Persistent class

The mapping file name conventionally, should be **class_name.hbm.xml.** There are many elements of the mapping file.

- <font color=gree>**hibernate-mapping**</font>: It is the root element in the mapping file that contains all the mapping elements.
- <font color="gree">**class**</font> : It is the sub-element of the hibernate-mapping element. It specifies the Persistent class.
- <font color=gree>**id** </font>: It is the subelement of class. It specifies the primary key attribute in the class.
- <font color=gree>**generator**</font> : It is the sub-element of id. It is used to generate the primary key. There are many generator classes such as assigned, increment, hilo, sequence, native etc. We will learn all the generator classes later.（generator will be describing in *H1.4*）
- <font color=gree>**property**</font> : It is the sub-element of class that specifies the property name of the Persistent class.

>1. **`name`**: the name of the property, with an initial lowercase letter.
>2. **`column`** (optional - defaults to the property name): the name of the mapped database table column. This can also be specified by nested `<column>` element(s).
>3. **`type`** (optional): a name that indicates the Hibernate type.
>4. `update, insert` (optional - defaults to `true`): specifies that the mapped columns should be included in SQL `UPDATE` and/or `INSERT` statements. Setting both to `false` allows a pure "derived" property whose value is initialized from some other property that maps to the same column(s), or by a trigger or other application.
>5. `formula` (optional): an SQL expression that defines the value for a *computed* property. Computed properties do not have a column mapping of their own.
>6. **`unique`** (optional): enables the DDL generation of a unique constraint for the columns. Also, allow this to be the target of a `property-ref`.
>7. `lazy` (optional - defaults to `false`): specifies that this property should be fetched lazily when the instance variable is first accessed. It requires build-time bytecode instrumentation.
>8. **`not-null` **(optional): enables the DDL generation of a nullability constraint for the columns.
>9. **`optimistic-lock` **(optional - defaults to `true`): specifies that updates to this property do or do not require acquisition of the optimistic lock. In other words, it determines if a version increment should occur when this property is dirty.
>10. `generated` (optional - defaults to `never`): specifies that this property value is actually generated by the database. See the discussion of [generated properties](https://docs.jboss.org/hibernate/core/3.3/reference/en/html/mapping.html#mapping-generated) for more information.
>11. `access` (optional - defaults to `property`): the strategy Hibernate uses for accessing the property value.

- <font color=gree>**properties**</font>: The `<properties>` element allows the definition of a named, logical grouping of the properties of a class. The most important use of the construct is that it allows a combination of properties to be the target of a `property-ref`. It is also a convenient way to define a multi-column unique constraint. 

>1. `name`: the logical name of the grouping. It is *not* an actual property name.
>
>2. `insert`: do the mapped columns appear in SQL `INSERTs`?
>3. `update`: do the mapped columns appear in SQL `UPDATEs`?
>4. `optimistic-lock` (optional - defaults to `true`): specifies that updates to these properties either do or do not require acquisition of the optimistic lock. It determines if a version increment should occur when these properties are dirty.
>5. `unique` (optional - defaults to `false`): specifies that a unique constraint exists upon all mapped columns of the component.

e.g., simple properties

```xml
<class name="Person"> 
	<id name="personNumber"/> 
... 
	<properties name="name" unique="true" update="false"> 
		<property name="firstName"/> 
		<property name="initial"/> 
		<property name="lastName"/> 
	</properties> 
</class>
```



- <font color=gree>**discriminator**</font>：The `<discriminator>` element is required for polymorphic persistence using the <font color=red>table-per-class-hierarchy mapping strategy</font>. It declares a discriminator column of the table. The discriminator column contains marker values that tell the persistence layer what subclass to instantiate for a particular row. A restricted set of types can be used: string, character, integer, byte, short, boolean, yes_no, true_false.

e.g.,discriminator declared like this,

```xml
<discriminator column="discriminator_column" type="discriminator_type" force="true|false" insert="true|false" formula="arbitrary sql expression" />
```

>1. `column` (optional - defaults to `class`): the name of the discriminator column.
>2. type (optional - defaults to string): a name that indicates the Hibernate type
>3. `force` (optional - defaults to `false`): "forces" Hibernate to specify the allowed discriminator values, even when retrieving all instances of the root class.
>4. `insert` (optional - defaults to `true`): set this to `false` if your discriminator column is also part of a mapped composite identifier. It tells Hibernate not to include the column in SQL `INSERTs`.
>5. `formula` (optional): an arbitrary SQL expression that is executed when a type has to be evaluated. It allows content-based discrimination.

e.g.,  employee.hbm.xml

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-mapping PUBLIC  
 "-//Hibernate/Hibernate Mapping DTD 5.3//EN"  
 "http://hibernate.sourceforge.net/hibernate-mapping-5.3.dtd">  
  
 <hibernate-mapping>  
  <class name="com.max.mypackage.Employee" table="emp1000">  
    <id name="id">  
     <generator class="assigned"></generator>  
    </id>  
            
    <property name="firstName"></property>  
    <property name="lastName"></property>  
            
  </class>  
            
 </hibernate-mapping>  
```



3. Create the Configuration file

The configuration file contains information about the database and mapping file. Conventionally, its name should be **hibernate.cfg.xml**.

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC 
  "-//Hibernate/Hibernate Configuration DTD 3.0//EN" 
  "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">  
  
<hibernate-configuration>  
  
    <session-factory>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
        <property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property>  
    <mapping resource="employee.hbm.xml"/>  
    </session-factory>  
  
</hibernate-configuration>  
```

It's an Oracle database configuration.





4. Create the class that retrieves or stores the object

In this class, we are simply storing the employee object to the database.

Begin with `standardServiceRegistryBuilder().configurtion("hibernate.cfg.xml").build();`

```java
package com.max.mypackage;    
    
import org.hibernate.Session;    
import org.hibernate.SessionFactory;    
import org.hibernate.Transaction;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;  
  
    
public class StoreData {    
	public static void main(String[] args) {    
        
        //Create typesafe ServiceRegistry object    
        StandardServiceRegistry ssr = new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
		// Create metadata objectand to get ssr object
        Metadata meta = new MetadataSources(ssr).getMetadataBuilder().build();  

        SessionFactory factory = meta.getSessionFactoryBuilder().build();  
        Session session = factory.openSession();  
        Transaction t = session.beginTransaction();   

        Employee e1 = new Employee();    
        e1.setId(101);    
        e1.setFirstName("Max");    
        e1.setLastName("Croft");    

        // session.persist(e1);
        session.save(e1);  
        t.commit();  
        System.out.println("successfully saved");    
        // close the stream 
        factory.close();  
        session.close();    
	}    
}   
```

Attention: There are two methods to store the session, `save()` and `persist()`;

1. Save()

    1. **Returns** generated Id after saving. Its return type is **Serializable**;
    2. **Saves** the changes to the database outside of the transaction;
    3. Assigns the generated id to the entity you are persisting;
    4. `session.save()` for a detached object will **create a new row** in the table.
2. Persist()
    1. **Does not return** generated Id after saving. Its return type is **void**;
    2. **Does not save** the changes to the database outside of the transaction;
    3. Assigns the generated Id to the entity you are persisting;
    4. `session.persist()` for a detached object will throw a `PersistentObjectException`, as it is not allowed.



All these are tried/tested on Hibernate v4.0.1.








5. Load the jar file

    For successfully running the hibernate application, you should have the **hibernate5.jar** file.

6. in this way you can run the example that you accessing the oracle database and loading the hibernate jar package.(load the jar packages without IDE, it should put the jars to the JRE 'JRE/lib/ext' folder ) 



#### H1.2 Implementation with XML

You can create the ".hbm.xml"  file to mapping persistent class, such as the example shows before. 

Hibernate mapping Generator tools :**XDoclet, Middlegen, AndroMDA** 





#### H1.3 Implementation with Java Annotation

You can also use annotation to mapping the persistent class.

some annotation of hibernate should be used:

- **@Entity** annotation marks this class as an entity.

- **@Table** annotation specifies the table name where data of this entity is to be persisted. If you don't use @Table annotation, hibernate will use the class name as the table name by default.

- **@Id** annotation marks the identifier for this entity.

- **@Column** annotation specifies the details of the column for this property or field. If @Column annotation is not specified, property name will be used as the column name by default.



e.g., shows the example  we had created but within annotation

```java
package com.max.mypackage;  
  
import javax.persistence.Entity;  
import javax.persistence.Id;  
import javax.persistence.Table;  
  
@Entity  
@Table(name= "emp500")   
public class Employee {    
    @Id   
    private int id;    
    private String firstName,lastName;    
    
    public int getId() {    
        return id;    
    }    
    public void setId(int id) {    
        this.id = id;    
    }    
    public String getFirstName() {    
        return firstName;    
    }    
    public void setFirstName(String firstName) {    
        this.firstName = firstName;    
    }    
    public String getLastName() {    
        return lastName;    
    }    
    public void setLastName(String lastName) {    
        this.lastName = lastName;    
    }    
}   
```





#### H1.4 Generator Class

All the generator classes implements the **org.hibernate.id.IdentifierGenerator interface**.



**generator class value**

To set the values of generate class like this:

```xml
<id name="identify">
    <generator class="value"></generator>
    
</id>
```



1. **assigned**: It is the default generator strategy if there is no <generator> element . In this case, application assigns the id.
2. **increment**: It generates the unique id only if no other process is inserting data into this table. It generates **short**, **int** or **long** type identifier. If a table contains an identifier then the application considers its maximum value else the application consider that the first generated identifier is 1. 
3. **sequence**: It uses the sequence of the database. if there is no sequence defined, it creates **a sequence automatically** e.g. in case of Oracle database, it creates a sequence named HIBERNATE_SEQUENCE. *In case of Oracle, DB2, SAP DB, Postgre SQL or McKoi, it uses sequence but it uses generator in interbase.*

​		For defining your own sequence, use the param subelement of generator.

```xml
.....  
 <id ...>  
  <generator class="sequence">  
      <param name="sequence">your_sequence_name</param>  
  </generator>  
 </id>  
 .....  
```

4. **hilo**: It uses high and low algorithm to generate the id of type short, int and long. 

5. **native**: It uses identity, sequence or hilo depending on the database vendor.     Database ventor is a central repository of supplier information that can be accessed and shared by authorized users within an organization. 

6. identity: It is used in *Sybase*, *My SQL*, *MS SQL Server*, *DB2* and *HypersonicSQL* to support the id column. The returned id is of type short, int or long. It is responsibility of database to generate unique identifier.
7. seqhilo: It uses high and low algorithm on the specified sequence name. The returned id is of type short, int or long.
8. **uuid**: It uses 128-bit UUID algorithm to generate the id. The returned id is of type String, unique within a network (because IP is used). The UUID is represented in hexadecimal digits, 32 in length.
9. guid: It uses GUID generated by database of type string. It works on *MS SQL Server* and *MySQL*.
10. **select**: It uses the primary key returned by the database trigger.
11. **foreign**: It uses the id of another associated object, mostly used with <one-to-one> association.
12. sequence-identity: It uses a special sequence generation strategy. It is supported in Oracle 10g drivers only.





#### H1.5 SQL Dialect

The dialect specifies the **type of database used in hibernate so that hibernate generate appropriate type of SQL statements.** For connecting any hibernate application with the database, it is required to provide the configuration of SQL dialect.



Syntax of SQL Dialect(Oracle)

```xml
<property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
```

MySQL:

```xml
<property name="dialect">org.hibernate.dialect.MySQL8Dialect</property>  
```

Different type of the database has different dialect class.



There are many Dialects classes defined for RDBMS in the **org.hibernate.dialect** package. They are as follows: 

| RDBMS                | Dialect                                       |
| :------------------- | :-------------------------------------------- |
| Oracle (any version) | `org.hibernate.dialect.OracleDialect`         |
| Oracle9i             | `org.hibernate.dialect.Oracle9iDialect`       |
| Oracle10g            | `org.hibernate.dialect.Oracle10gDialect`      |
| MySQL                | `org.hibernate.dialect.MySQLDialect`          |
| MySQL with InnoDB    | `org.hibernate.dialect.MySQLInnoDBDialect`    |
| MySQL with MyISAM    | `org.hibernate.dialect.MySQLMyISAMDialect`    |
| DB2                  | `org.hibernate.dialect.DB2Dialect`            |
| DB2 AS/400           | `org.hibernate.dialect.DB2400Dialect`         |
| DB2 OS390            | `org.hibernate.dialect.DB2390Dialect`         |
| Microsoft SQL Server | `org.hibernate.dialect.SQLServerDialect`      |
| Sybase               | `org.hibernate.dialect.SybaseDialect`         |
| Sybase Anywhere      | `org.hibernate.dialect.SybaseAnywhereDialect` |
| PostgreSQL           | `org.hibernate.dialect.PostgreSQLDialect`     |
| SAP DB               | `org.hibernate.dialect.SAPDBDialect`          |
| Informix             | `org.hibernate.dialect.InformixDialect`       |
| HypersonicSQL        | `org.hibernate.dialect.HSQLDialect`           |
| Ingres               | `org.hibernate.dialect.IngresDialect`         |
| Progress             | `org.hibernate.dialect.ProgressDialect`       |
| Mckoi SQL            | `org.hibernate.dialect.MckoiDialect`          |
| Interbase            | `org.hibernate.dialect.InterbaseDialect`      |
| Pointbase            | `org.hibernate.dialect.PointbaseDialect`      |
| FrontBase            | `org.hibernate.dialect.FrontbaseDialect`      |
| Firebird             | `org.hibernate.dialect.FirebirdDialect`       |





#### H1.6 Hibernate logging by Log4j

Logging enables the programmer to write the log details into a file permanently. Log4j and Logback frameworks can be used in hibernate framework to support logging.

There are two ways to perform logging using log4j:

1. **By log4j.xml file (or)**
2. **By log4j.properties file**



- Levels of Logging

| Levels  | Description                                           |
| :------ | :---------------------------------------------------- |
| OFF     | This level is used to turn off logging.               |
| WARNING | This is a message level that indicates a problem.     |
| SEVERE  | This is a message level that indicates a failure.     |
| INFO    | This level is used for informational messages.        |
| CONFIG  | This level is used for static configuration messages. |





- There are two ways to perform logging using log4j using xml file:
    1. Load the log4j jar files with hibernate
    2. Create the log4j.xml file inside the src folder (parallel with hibernate.cfg.xml file)



log4j.xml 

All of the log details in this xml file.

```xml
<?xml version="1.0" encoding="UTF-8"?>  
<!DOCTYPE log4j:configuration SYSTEM "log4j.dtd">  
<log4j:configuration xmlns:log4j="http://jakarta.apache.org/log4j/"  
    debug="false">  
<appender name="CONSOLE" class="org.apache.log4j.ConsoleAppender">  
 <layout class="org.apache.log4j.PatternLayout">  
  <param name="ConversionPattern" value="[%d{dd/MM/yy hh:mm:ss:sss z}] %5p %c{2}: %m%n" />  
 </layout>  
</appender>  
    <appender name="ASYNC" class="org.apache.log4j.AsyncAppender">  
        <appender-ref ref="CONSOLE" />  
        <appender-ref ref="FILE" />  
</appender>  
<appender name="FILE" class="org.apache.log4j.RollingFileAppender">  
    <param name="File" value="C:/javatpointlog.log" />  
    <param name="MaxBackupIndex" value="100" />  
 <layout class="org.apache.log4j.PatternLayout">  
  <param name="ConversionPattern" value="[%d{dd/MM/yy hh:mm:ss:sss z}] %5p %c{2}: %m%n" />  
</layout>  
</appender>  
    <category name="org.hibernate">  
        <priority value="DEBUG" />  
    </category>  
    <category name="java.sql">  
        <priority value="debug" />  
    </category>  
    <root>  
        <priority value="INFO" />  
        <appender-ref ref="FILE" />  
    </root>  
</log4j:configuration>  
```



log4j.properties file

Use log4j properties

```properties
# Direct log messages to a log file  
log4j.appender.file=org.apache.log4j.RollingFileAppender  
log4j.appender.file.File=C:\\javatpointhibernate.log  
log4j.appender.file.MaxFileSize=1MB  
log4j.appender.file.MaxBackupIndex=1  
log4j.appender.file.layout=org.apache.log4j.PatternLayout  
log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n  
   
# Direct log messages to stdout  
log4j.appender.stdout=org.apache.log4j.ConsoleAppender  
log4j.appender.stdout.Target=System.out  
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout  
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n  
   
# Root logger option  
log4j.rootLogger=INFO, file, stdout  
   
# Log everything. Good for troubleshooting  
log4j.logger.org.hibernate=INFO  
   
# Log all JDBC parameters  
log4j.logger.org.hibernate.type=ALL  
```







#### H1.7 Inheritance Mapping

We can map the inheritance hierarchy classes with the table of the database. There are three inheritance mapping strategies defined in the hibernate:

##### Table Per Hierarchy

In table per hierarchy mapping, single table is required to map the whole hierarchy, an extra column (known as discriminator column) is added to identify the class. But nullable values are stored in the table.



###### TPH with xml file

Hierarchy structure use `<subclass>` to implement. One xml file record all of the Hierarchy class include parent class and subclasses.

It is mainly used to distinguish the record. To specify this, **discriminator** subelement of class must be specified.

e.g.,

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC 
  "-//Hibernate/Hibernate Configuration DTD 3.0//EN" 
  "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
  
<hibernate-mapping>  
<class name="com.max.mypackage.Employee" table="emp121" discriminator-value="emp">  
	<id name="id">  
		<generator class="increment"></generator>  
	</id>  
  
	<discriminator column="type" type="string"></discriminator>  
	<property name="name"></property>  
            
	<subclass name="com.max.mypackage.Regular_Employee" discriminator-value="reg_emp">  
		<property name="salary"></property>  
		<property name="bonus"></property>  
	</subclass>  
            
	<subclass name="com.max.mypackage.Contract_Employee" discriminator-value="con_emp">  
		<property name="pay_per_hour"></property>  
		<property name="contract_duration"></property>  
	</subclass>  
</class>  
</hibernate-mapping>  
```



Others,

Hierarchy strategy use only one table which mapping to the parent Class, it has all of columns of class have. e.g.,

inheritance hierarchy:

![table per class hierarchy using annotation](assets/Web%20Frameworks.assets/inheritance1.jpg)

Xml:

person.hbm.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-mapping PUBLIC
        "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd">
<hibernate-mepping>
	<class name="con.max.domain.Person" table="person">
    	<id name="id">
        	<generator class="native"></generator>
        </id>
        <discriminator column="discrimination" type="java.lang.String"></discriminator>
        <property name="name" column="name" type="java.long.String"></property>
        <subclass name="com.max.domain.Scientist" disciriminator-value="scientist">
            <property name="paperNmae" column="paper_name" type="java.long.String"></property>
            <property name+"department" column="department" type="java.long.String"></property>
        </subclass> 
        <subclass name="com.max.domain.Student" discriminator-value="student">
        	<property name="school" column="school" type="java.long.String"></property>
            <property name="teacher" column="teacher" type="java.long.String"></property>
        </subclass>
    </class>
</hibernate-mepping>
```



Person.java

```java
public class Person {
    private int id;
    private String name;
    private int age;
    
    public Person(){
    }
    public Person(int id,String name, int age){
        this.id = id;
        this.name = name;
        this.age = age;
    }
    public int getId(){
        return this.id;
    }
    public void setId(int id){
        this.id = id;
    }
    public String getName() {
    	return this.name;    
	}
    public void setName(String name) {
        this.name = name;
    }
   	public int getAge(){
        return this.age;
    }
    public void setAge(int age){
        this.age = age;
    }
}
```

Scientist.java

```java
public class Scientist extends Person {
    private String paperName;
    private String department;
    
    public Scientist(){
    }
    public Scientist(String paperName, String department) {
        this.paperNmae = paperName;
        this.deparment = department;
    } 
    public String getPaperName(){
        return this.paperName;
    }
 	public void setPaperName(String paperName){
        this.paperName = paperName; 
    }   
    public String getDepartment(){
        return this.depaperment;
    }
    public void setDeparment(String department){
        this.department = department;
    }
}
```

Student.java

```java
public class Student{
    private String school;
    private String teacher;
    public Student(){
    } 
    public Student(String school, String teacher){
        this.school = school;
        this.teacher = teacher;
    }
   	public String getSchool() {
        return this.school;
    }
    public void setSchool(){
        this.school = school;
    }
    public String getTeacher(){
        return this.teacher;
    }
    public void setTeacher(){
        this.teacher = teacher;
    }
}
```

describe table person

```sql
create table person if not exists (
	id int not null pirmary key auto_increment,
    name varchar(20) not null,
    age int not null,
    paperName varchar(30),
    department varchar(30),
    school varchar(30),
    teacher varchar(30)
)engine=InnoDB；
```

**All the data will be insert into the table.**



###### TPH with Annotation

Here, we need to use <font color="gree">@Inheritance(strategy=InheritanceType.SINGLE_TABLE)</font>, <font color="gree">@DiscriminatorColumn</font> and <font color="gree">@DiscriminatorValue </font>annotations for mapping table per hierarchy strategy.

In case of table per hierarchy, **only one table is required to map the inheritance hierarchy.** Here, an extra column (also known as **discriminator column**) is created in the table to identify the class.

You need to follow the following steps to create simple example:

- Create the persistent classes
- Edit pom.xml file
- Create the configuration file
- Create the class to store the fetch the data



<font color=red>ERROR: Incorrect string value: '\xE9\x90\x92\xEF\xB9\x80...' for column 'name' at row 1</font>

When database charset, table character set and hibernate input string isn't utf8, it will report this error.

You should convert the database charset and table character set to utf8 or utf8mb4;

>create database and set charset to utf8:
>
>```mysql
>CREATE DATABASE IF NOT EXISTS test CHARSET=utf8; 
>```
>
>change the database charset:
>
>```mysql
>ALTER DATABASE test CHARSET=UTF8MB4; 
>ALTER DATABASE bookdb DEFAULT CHARSET SET utf8mb4;
>```
>
>change the table character set:
>
>```mysql
>ALTER TABLE table_name CONVERT TO CHARACTER SET utf8mb4;
>```

##### Table Per Concrete class

In case of table per concrete class, tables are created as per class. But duplicate column is added in subclass tables.

##### Table Per Subclass

In this strategy, tables are created as per class but related by foreign key. So there are no duplicate columns.







### Mybatis





### JPA
