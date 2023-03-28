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





#### Elements of Hibernate Architecture

- <font color=red>`SessionFactory`</font>: The `SessionFactory`is a factory of session and client of <font color=red>`ConnectionProvider`</font>. It holds second level cache *(optional)* of data. The `org.hibernate.SessionFactory` interface provides factory method to get the object of Session.
- <font color=red>`Session`</font>: The `session` object provides an interface between the application and data stored in the database. It is a short-lived object and wraps the JDBC connection. It is factory of Transaction, Query and Criteria. It holds a first-level cache *(mandatory)* of data. The `org.hibernate.Session` interface provides methods to **insert, update and delete the object**. It also provides factory methods for Transaction, Query and Criteria.
- <font color=red>`transacton`</font>: The `transaction` object specifies the atomic unit of work. It is *optional*. The `org.hibernate.Transaction` interface provides methods for transaction management.
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







2. Create the mapping file for Persistent class

The mapping file name conventionally, should be **class_name.hbm.xml.** There are many elements of the mapping file.

- **hibernate-mapping :** It is the root element in the mapping file that contains all the mapping elements.
- **class :** It is the sub-element of the hibernate-mapping element. It specifies the Persistent class.
- **id :** It is the subelement of class. It specifies the primary key attribute in the class.
- **generator :** It is the sub-element of id. It is used to generate the primary key. There are many generator classes such as assigned, increment, hilo, sequence, native etc. We will learn all the generator classes later.
- **property :** It is the sub-element of class that specifies the property name of the Persistent class.



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
          "-//Hibernate/Hibernate Configuration DTD 5.3//EN"  
          "http://hibernate.sourceforge.net/hibernate-configuration-5.3.dtd">  
  
<hibernate-configuration>  
  
    <session-factory>  
        <property name="hbm2ddl.auto">update</property>  
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

        session.save(e1);  
        t.commit();  
        System.out.println("successfully saved");    
        // close the stream 
        factory.close();  
        session.close();    
	}    
}   
```





5. Load the jar file

    For successfully running the hibernate application, you should have the **hibernate5.jar** file.

6. in this way you can run the example that you accessing the oracle database and loading the hibernate jar package.(load the jar packages without IDE, it should put the jars to the JRE 'JRE/lib/ext' folder ) 



#### Implementation with XML

You can create the ".hbm.xml"  file to mapping persistent class, such as the example shows before. 



#### Implementation with Java Annotation

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













### Mybatis





### JPA
