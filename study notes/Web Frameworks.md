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

**cfg.xml doctype**

```xml
<!DOCTYPE hibernate-configuration PUBLIC
    "-//Hibernate/Hibernate Configuration DTD//EN"
    "http://hibernate.sourceforge.net/hibernate-configuration-3.0.dtd">
```

**hbm.xml doctype**

```xml
<!DOCTYPE hibernate-mapping PUBLIC
    "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
    "http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
```











**Hibernate ORM** (or simply **Hibernate**) is an [object–relational mapping](https://en.wikipedia.org/wiki/Object–relational_mapping) tool for the [Java](https://en.wikipedia.org/wiki/Java_(programming_language)) programming language. It provides a [framework](https://en.wikipedia.org/wiki/Software_framework) for mapping an [object-oriented](https://en.wikipedia.org/wiki/Object-oriented_programming) domain model to a [relational database](https://en.wikipedia.org/wiki/Relational_database). Hibernate handles [object–relational impedance mismatch](https://en.wikipedia.org/wiki/Object–relational_impedance_mismatch) problems by replacing direct, [persistent](https://en.wikipedia.org/wiki/Persistence_(computer_science)) database accesses with high-level object handling functions.

The mapping of Java classes to database tables is implemented by the configuration of an [XML](https://en.wikipedia.org/wiki/XML) file or by using [Java Annotations](https://en.wikipedia.org/wiki/Java_annotation). When using an XML file, Hibernate can [generate](https://en.wikipedia.org/wiki/Program_synthesis) [skeleton](the structure consisting of all the bones) [source code](https://en.wikipedia.org/wiki/Source_code) for the persistence classes. This is [auxiliary]( auxiliary workers provide additional help for another group of workers) when annotations are used. Hibernate can use the XML file or the Java annotations to maintain the [database schema](https://en.wikipedia.org/wiki/Database_schema).



Use the Hibernate, you should import the jars it needs. (from official website)



How Hibernate works (before version 5.0)

![Lightbox](assets/Web%20Frameworks.assets/HBArchi.png)



[hibernate bootastrapping ways](https://www.baeldung.com/hibernate-5-bootstrapping-api)

 [What is the difference between Configuration vs ServiceRegistry vs StandardServiceRegistry?](https://stackoverflow.com/questions/67300459/what-is-the-difference-between-configuration-vs-serviceregistry-vs-standardservi)



#### H1 Hibernate Query Language (HQL)

- Database Independent Query

HQL (Hibernate Query Language) is the object-oriented version of SQL. It generates the database independent queries. So you don't need to write database specific queries. Before Hibernate, if database is changed for the project, we need to change the SQL query as well that leads to the maintenance problem.



It is an object oriented representation of Hibernate Query. The object of Query can be obtained by calling the createQuery() method Session interface.

The query interface provides many methods. There is given commonly used methods:

1. **public int executeUpdate()** is used to execute the update or delete query.
2. **public List list()** returns the result of the ralation as a list.
3. **public Query setFirstResult(int rowno)** specifies the row number from where record will be retrieved.
4. **public Query setMaxResult(int rowno)** specifies the no. of records to be retrieved from the relation (table).
5. **public Query setParameter(int position, Object value)** it sets the value to the JDBC style query parameter.
6. **public Query setParameter(String name, Object value)** it sets the value to a named query parameter.



- Example of HQL to get all the records

```java
//here persistent class name is Emp 
Query query=session.createQuery("from Emp"); 
List list=query.list();  
```

- Example of HQL to get records with pagination

```java
Query query=session.createQuery("from Emp");  
query.setFirstResult(5);  
query.setMaxResult(10);  
//will return the records from 5 to 10th number
List list=query.list();
```

- Example of HQL update query

```java
Transaction tx=session.beginTransaction();  
Query q=session.createQuery("update User set name=:n where id=:i");  
q.setParameter("n","Udit Kumar");  
q.setParameter("i",111);  
  
int status=q.executeUpdate();  
System.out.println(status);  
tx.commit();  
```

- Example of HQL delete query

```java
Query query=session.createQuery("delete from Emp where id=100");  
//specifying class name (Emp) not tablename  
query.executeUpdate();  
```

- HQL with Aggregate functions

    You may call avg(), min(), max() etc. aggregate functions by HQL. Let's see some common examples:

    - Example to get total salary of all the employees

    ```java
    Query q=session.createQuery("select sum(salary) from Emp");  
    List<Integer> list=q.list();  
    System.out.println(list.get(0)); 
    ```

    - Example to get **maximum** salary of employee

    ```java
    Query q=session.createQuery("select max(salary) from Emp");  
    ```

    - Example to get **minimum** salary of employee

    ```java
    Query q=session.createQuery("select min(salary) from Emp"); 
    ```

    - Example to count **total** number of employee ID

    ```java
    Query q=session.createQuery("select count(id) from Emp");  
    ```

    - Example to get **average** salary of each employees

    ```java
    Query q=session.createQuery("select avg(salary) from Emp");  
    ```

    



------



**The Hibernate architecture is categorized in four layers:**

- Java application layer
- Hibernate framework layer
- Backhand api layer
- Database layer



high level architecture of Hibernate with **mapping file** and **configuration file**.

![hibernate architecture](assets/Web%20Frameworks.assets/architecture.jpg)





#### H2 Elements of Hibernate Architecture

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





##### H2.1 Elements in hbm.xml

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



##### H2.2 `HibernateUtil`



`StandtardHibernateUtil`

```java
package com.max.util;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.boot.Metadata;
import org.hibernate.boot.MetadataSources;
import org.hibernate.boot.registry.StandardServiceRegistry;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;

/**
 * Hibernate utility  StandardHibernateUtil implement by StandardServiceRegistry
 */
public class StandardHibernateUtil {
    // declare StandServiceRegistry
    public static final StandardServiceRegistry ssr;
    // declare Metadata
    public static final Metadata metadata;

    // initialize ssr and metadata
    static {
        ssr = new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();
        metadata = new MetadataSources(ssr).getMetadataBuilder().build();
    }

    // initialize sessionFactory, get data from metadata object
    public static final SessionFactory sf = metadata.getSessionFactoryBuilder().build();

    // openSession() method from sf object (encapsulate original openSession())
    public static Session openSession() {
        return sf.openSession();
    }

}

```



`HibernateUtil`

```java
package com.max.util;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.cfg.Configuration;

public class HibernateUtil {
    // declare Configuration to get the hibernate config information
    private static final Configuration cf;
    // declare SessionFactory
    private static final SessionFactory sf;
    // initialize Configuration and SessionFactory object
    static {
        cf = new Configuration().configure();
        sf = cf.buildSessionFactory();
    }
    // openSession() method from sf object (encapsulate original openSession())
    public static Session openSession() {
        return sf.openSession();
    }
}

```





#### H3 Implementation with XML

You can create the ".hbm.xml"  file to mapping persistent class, such as the example shows before. 

Hibernate mapping Generator tools :**XDoclet, Middlegen, AndroMDA** 





#### H4 Implementation with Java Annotation

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





#### H5 Generator Class

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





#### H6 SQL Dialect

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





#### H7 Hibernate logging by Log4j

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







#### H8 Inheritance Mapping

We can map the inheritance hierarchy classes with the table of the database. There are three inheritance mapping strategies defined in the hibernate.

check the [link](https://poshichao.github.io/2018/05/07/entity-inhetitance/): another inheritance strategy reference



##### H8.1 Table Per Hierarchy

In table per hierarchy mapping, single table is required to map the whole hierarchy, an extra column (known as discriminator column) is added to identify the class. But nullable values are stored in the table.



###### H8.1.1 TPH with xml file

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



###### H8.1.2 TPH with Annotation

Here, we need to use <font color="gree">@Inheritance(strategy=InheritanceType.SINGLE_TABLE)</font>, <font color="gree">@DiscriminatorColumn</font> and <font color="gree">@DiscriminatorValue </font>annotations for mapping table per hierarchy strategy.

In case of table per hierarchy, **only one table is required to map the inheritance hierarchy.** Here, an extra column (also known as **discriminator column**) is created in the table to identify the class.

You need to follow the following steps to create simple example:

- Create the persistent classes

com/max/domain/annotation/EmployeeAnno.java

```java
package com.max.domain.annotation;


import javax.persistence.*;

// Annottaion of Entity, declare the class is a entity
@Entity
// mapping class to the table you want
@Table(name = "emp")
// declare inheritance strategy for single table (单表继承映射)
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
// declare discriminator column which used to distingish the class
@DiscriminatorColumn(name = "discriminator_type", discriminatorType = DiscriminatorType.STRING)
// declate discrminator column value
@DiscriminatorValue(value = "employee")
public class EmployeeAnno {
    // declare the member variable for primary key 'id'  
    @Id
    // declare id generate strategy 
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private int id;

    @Column(name = "name")
    private String name;

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}

```

com/max/domain/annotation/ContractEmployeeAnno.java

```java
package com.max.domain.annotation;

import javax.persistence.Column;
import javax.persistence.DiscriminatorValue;
import javax.persistence.Entity;

/**
 * Child class only needs to set the DiscriminatorValue. 
 * For single table inheritance strategy, child class needn't id column because 
 * all the child classes and ancestor class data is in one table 
 */
@Entity
@DiscriminatorValue("contract_employee")
public class ContractEmployeeAnno extends EmployeeAnno{
    @Column(name="pay_per_hour")
    private float payPerHour;
    @Column(name = "contract_duration")
    private String contractDuration;

    public float getPayPerHour() {
        return payPerHour;
    }

    public void setPayPerHour(float payPerHour) {
        this.payPerHour = payPerHour;
    }

    public String getContractDuration() {
        return contractDuration;
    }

    public void setContractDuration(String contractDuration) {
        this.contractDuration = contractDuration;
    }
}

```

com/max/domain/annotation/RegularEmployeeAnno.java

```java
package com.max.domain.annotation;

import javax.persistence.Column;
import javax.persistence.DiscriminatorValue;
import javax.persistence.Entity;

@Entity
@DiscriminatorValue("regular_employee")
public class RegularEmployeeAnno extends EmployeeAnno {
    @Column(name = "salary")
    private float salary;
    @Column(name = "bonus")
    private int bonus;

    public float getSalary() {
        return salary;
    }

    public void setSalary(float salary) {
        this.salary = salary;
    }

    public int getBonus() {
        return bonus;
    }

    public void setBonus(int bonus) {
        this.bonus = bonus;
    }
}

```

- Edit pom.xml file

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.max</groupId>
    <artifactId>hibernatepractice</artifactId>
    <version>1.0-SNAPSHOT</version>

    <properties>
        <maven.compiler.source>8</maven.compiler.source>
        <maven.compiler.target>8</maven.compiler.target>
    </properties>

    <dependencies>
        <!--dependency of hibernate core-->
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-core</artifactId>
            <version>5.6.14.Final</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.28</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>RELEASE</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.junit.jupiter</groupId>
            <artifactId>junit-jupiter</artifactId>
            <version>RELEASE</version>
            <scope>test</scope>
        </dependency>

    </dependencies>

</project>
```



- Create the configuration file

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>
    <session-factory>
        <property name="dialect">org.hibernate.dialect.MySQLDialect</property>
        <property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/hibernate5</property>
        <property name="hibernate.connection.username">root</property>
        <property name="hibernate.connection.password">123456</property>
        <property name="show_sql">true</property>
        <property name="format_sql">true</property>
        <!--resource attribute used to the way of xml -->
		<!-- <mapping  resource="employee.hbm.xml"/> -->
        <!--class attribute used to the way of annotation-->
        <mapping class="com.max.domain.annotation.EmployeeAnno"></mapping>
        <mapping class="com.max.domain.annotation.ContractEmployeeAnno"></mapping>
        <mapping class="com.max.domain.annotation.RegularEmployeeAnno"></mapping>
    </session-factory>
</hibernate-configuration>
```

- Create the class to store the fetch the data(Test class)

```java
import com.max.domain.annotation.ContractEmployeeAnno;
import com.max.domain.annotation.EmployeeAnno;
import com.max.domain.annotation.RegularEmployeeAnno;
import com.max.domain.xml.ContractEmployee;
import com.max.domain.xml.Employee;
import com.max.domain.xml.RegularEmployee;
import com.max.util.HibernateUtil;
import com.max.util.StandardHibernateUtil;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.boot.Metadata;
import org.hibernate.boot.MetadataSources;
import org.hibernate.boot.registry.StandardServiceRegistry;
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;
import org.junit.jupiter.api.Test;

import java.math.BigDecimal;

public class baseTest {
    @Test
    public void mainTest() {
        // Use HibernateUtil class to openSession(). It's via Configuration class to get
        // hibernate.cfg.xml file information and create session factory.
        // The way of Configuration deprecated after hibernate 5.x;
        Session session = HibernateUtil.openSession();
        Transaction transaction = session.beginTransaction();
        Employee employee = new Employee();
        employee.setName("MaxCroft");

        RegularEmployee regularEmployee = new RegularEmployee();
        regularEmployee.setSalary(2000.50F);
        regularEmployee.setBonus(BigDecimal.valueOf(2200.12));

        ContractEmployee contractEmployee = new ContractEmployee();
        contractEmployee.setPayPerHour(10.5F);
        contractEmployee.setContractDuration("seven month");

        session.persist(employee);
        session.persist(regularEmployee);
        session.persist(contractEmployee);

        transaction.commit();
        session.close();
        System.out.println("success");
    }

    @Test
    public void AnnotationTest() {
        // Use StandardHibernateUtil class to openSession. StandardHibernateUtil via StandardServiceRegistry and
        // Metadata to build session factory. StandardServiceRegistryBuilder.configure() to get information from hibernate.cfg.xml.
        Session session = StandardHibernateUtil.openSession();
        Transaction transaction = session.beginTransaction();
        // 瞬时态 session does not control object
        EmployeeAnno employeeAnno = new EmployeeAnno();
        employeeAnno.setName("焦垠睿");

        RegularEmployeeAnno regularEmployeeAnno = new RegularEmployeeAnno();
        regularEmployeeAnno.setName("Sunshine");
        regularEmployeeAnno.setSalary(10000.5F);
        regularEmployeeAnno.setBonus(3000);

        ContractEmployeeAnno contractEmployeeAnno = new ContractEmployeeAnno();
        contractEmployeeAnno.setName("小华");
        contractEmployeeAnno.setPayPerHour(20.8F);
        contractEmployeeAnno.setContractDuration("6个月");
        // 持久态 session control objects
        session.persist(employeeAnno);
        session.persist(regularEmployeeAnno);
        session.persist(contractEmployeeAnno);

        transaction.commit();
        // 脱管态 session release the object and don't control them anyway
        session.close();
        System.out.println("success");
    }
}

```



<font color=red>ERROR: Incorrect string value: '\xE9\x90\x92\xEF\xB9\x80...' for column 'name' at row 1</font>

When database charset, table character set and hibernate input string isn't utf8 (project default encoding, set encoding in idea/setting/editor ), it will report this error.

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

##### H8.2 Table Per Concrete class

In case of table per concrete class, **tables are created as per class**. But **duplicate column is added** in subclass tables.

Also refers to **tables will be created for every class**, and child class table has the ancestor class table's column. Data is **not intercommunication**.



###### H8.2.1 TPC with xml file

In case of Table Per Concrete class, there will be three tables in the database **having no relations to each other**, each representing a particular class. There are two ways to map the table with table per concrete class strategy.

- By `<union-subclass>` element
- By self creating the table for each class

Class Hierarchy as well as before.

- mapping file for persistent classes employee.hbm.xml file:

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC 
  "-//Hibernate/Hibernate Configuration DTD 3.0//EN" 
  "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
  
  <hibernate-mapping>  
  <class name="com.max.mypackage.Employee" table="emp122">  
  	<id name="id">  
  		<generator class="increment"></generator>  
  	</id>  
           
  	<property name="name"></property>  
            
  	<union-subclass name="com.max.mypackage.Regular_Employee" table="regemp122">  
  		<property name="salary"></property>  
  		<property name="bonus"></property>  
  	</union-subclass>  
            
  	<union-subclass name="com.max.mypackage.Contract_Employee" table="contemp122">  
  		<property name="pay_per_hour"></property>  
  		<property name="contract_duration"></property>  
  	</union-subclass>          
  </class>  
  </hibernate-mapping>  
```

- Table structure for Employee class

![table per concrete class ](assets/Web%20Frameworks.assets/concretetable1.jpg)

- Table structure for Regular_Employee class

![table per concrete class ](assets/Web%20Frameworks.assets/concretetable2.jpg)

- #### Table structure for Contract_Employee class

![table per concrete class ](assets/Web%20Frameworks.assets/concretetable3.jpg)



- Persistent classes

Employee.java

```java
package com.max.mypackage;  
  
public class Employee {  
private int id;  
private String name;  
  
//getters and setters  
}  
```

Contract_Employee.java

```java
package com.max.mypackage;  
  
public class Contract_Employee extends Employee{  
    private float pay_per_hour;  
    private String contract_duration;  
  
//getters and setters  
}  
```

Regular_Employee.java

```java
package com.max.mypackage;  
  
public class Regular_Employee extends Employee{  
private float salary;  
private int bonus;  
  
//getters and setters  
}  
```

- configuration file: as well as before, needs resource:

```xml
<mapping resource="employee.hbm.xml"/>  
```

- fetch data test:

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
  
    StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
    Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  
      
    SessionFactory factory=meta.getSessionFactoryBuilder().build();  
    Session session=factory.openSession();  
      
    Transaction t=session.beginTransaction();  
      
    Employee e1=new Employee();    
    e1.setName("Gaurav Chawla");    
        
    Regular_Employee e2=new Regular_Employee();    
    e2.setName("Vivek Kumar");    
    e2.setSalary(50000);    
    e2.setBonus(5);    
        
    Contract_Employee e3=new Contract_Employee();    
    e3.setName("Arjun Kumar");    
    e3.setPay_per_hour(1000);    
    e3.setContract_duration("15 hours");    
        
    session.persist(e1);    
    session.persist(e2);    
    session.persist(e3);    
        
    t.commit();    
    session.close();    
    System.out.println("success");    
}     
}  
```





###### H8.2.2 TPC with annotation

It needs to use <font color=gree>@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)</font> annotation in the parent class and <font color=gree>@AttributeOverrides </font>annotation in the subclasses.

<font color=gree>@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)</font> specifies that we are using table per concrete class strategy. It should be specified in the parent class only.

<font color=gree>@AttributeOverrides</font> defines that parent class attributes will be overridden in this class. In table structure, parent class table columns will be added in the subclass table.

All the file as well as before

- persistent classes

Employee.java

```java
package com.max.mypackage;  
import javax.persistence.*;  
  
@Entity  
@Table(name = "employee102")  
@Inheritance(strategy = InheritanceType.TABLE_PER_CLASS)  
  
public class Employee {  
@Id  
@GeneratedValue(strategy=GenerationType.AUTO)  
      
@Column(name = "id")  
private int id;  
  
@Column(name = "name")  
private String name;  
  
//setters and getters  
}  
```

Contract_Employee.java

```java
package com.max.mypackage;  
import javax.persistence.*;  
@Entity  
@Table(name="contractemployee102")  
@AttributeOverrides({  
    @AttributeOverride(name="id", column=@Column(name="id")),  
    @AttributeOverride(name="name", column=@Column(name="name"))  
})  
public class Contract_Employee extends Employee{  
      
    @Column(name="pay_per_hour")  
    private float pay_per_hour;  
      
    @Column(name="contract_duration")  
    private String contract_duration;  
  
    public float getPay_per_hour() {  
        return pay_per_hour;  
    }  
    public void setPay_per_hour(float payPerHour) {  
        pay_per_hour = payPerHour;  
    }  
    public String getContract_duration() {  
        return contract_duration;  
    }  
    public void setContract_duration(String contractDuration) {  
        contract_duration = contractDuration;  
    }  
} 
```

Regular_Employee.java

```java
package com.javatpoint.mypackage;  
import javax.persistence.*;  
  
@Entity  
@Table(name="regularemployee102")  
@AttributeOverrides({  
    @AttributeOverride(name="id", column=@Column(name="id")),  
    @AttributeOverride(name="name", column=@Column(name="name"))  
})  
public class Regular_Employee extends Employee{  
      
@Column(name="salary")    
private float salary;  
  
@Column(name="bonus")     
private int bonus;  
  
//setters and getters  
}  
```



- hibernate.cfg.xml (Oracle database)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>  
    <session-factory>  
        <property name="hbm2ddl.auto">update</property>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
<property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property>  
          
        <mapping class="com.javatpoint.mypackage.Employee"/>  
        <mapping class="com.javatpoint.mypackage.Contract_Employee"/>  
        <mapping class="com.javatpoint.mypackage.Regular_Employee"/>  
    </session-factory>  
</hibernate-configuration>  
```



- Store test

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
      
        StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
        Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  
          
        SessionFactory factory=meta.getSessionFactoryBuilder().build();  
        Session session=factory.openSession();  
          
        Transaction t=session.beginTransaction();  
          
        Employee e1=new Employee();  
        e1.setName("Gaurav Chawla");  
          
        Regular_Employee e2=new Regular_Employee();  
        e2.setName("Vivek Kumar");  
        e2.setSalary(50000);  
        e2.setBonus(5);  
          
        Contract_Employee e3=new Contract_Employee();  
        e3.setName("Arjun Kumar");  
        e3.setPay_per_hour(1000);  
        e3.setContract_duration("15 hours");  
          
        session.persist(e1);  
        session.persist(e2);  
        session.persist(e3);  
          
        t.commit();  
        session.close();  
        System.out.println("success");        
    }  
}  
```









##### H8.3 Table Per Subclass

In this strategy, **tables are created as per class but related by foreign key**. So there are **no duplicate columns**.





###### H8.3.1 TPS with xml

The `<joined-subclass>` element of class is used to map the child class with parent using the primary key and foreign key relation.

e.g.,

structure of  hierarchy:

![table per concrete class](assets/Web%20Frameworks.assets/inheritance1-16809236286651.jpg)

- hbm.xml

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC 
  "-//Hibernate/Hibernate Configuration DTD 3.0//EN" 
  "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-mapping>  
  <class name="com.max.mypackage.Employee" table="emp123">  
      <!--primary key-->
  <id name="id">  
 	 <generator class="increment"></generator>  
  </id>  
  
  <property name="name"></property>  
  
  <joined-subclass name="com.max.mypackage.Regular_Employee" table="regemp123">  
  	  <!--foregin key-->
      <key column="eid"></key>  
      <property name="salary"></property>  
      <property name="bonus"></property>  
  </joined-subclass>  
   
  <joined-subclass name="com.max.mypackage.Contract_Employee" table="contemp123">  
      <!--foregin key-->
      <key column="eid"></key>  
      <property name="pay_per_hour"></property>  
      <property name="contract_duration"></property>  
  </joined-subclass>  
  </class>  
  </hibernate-mapping>  
```

- Table structure 

Employee class

![table per subclass class ](assets/Web%20Frameworks.assets/concretetable1-16809237525144.jpg)

Regular_Employee class

![table per subclass class ](assets/Web%20Frameworks.assets/subclasstable2.jpg)

Contract_Employee class

![table per subclass class ](assets/Web%20Frameworks.assets/subclasstable3.jpg)

- persistent class

Emploee.java

```java
package com.max.mypackage;  
  
public class Employee {  
	private int id;  
	private String name;  
  
//getters and setters  
}  
```

Contract_Employee.java

```java
package com.max.mypackage;  
  
public class Contract_Employee extends Employee{  
    private float pay_per_hour;  
    private String contract_duration;  
  
//getters and setters  
}  
```

Regular_Employee.java

```java
package com.max.mypackage;  
public class Regular_Employee extends Employee{  
	private float salary;  
	private int bonus;  
  
//getters and setters  
}  
```



- hibernate.cfg.xml (Oracle)

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

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



- store test

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
          
	StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
	Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  
  
	SessionFactory factory=meta.buildSessionFactory();  
	Session session=factory.openSession();  
  
	Transaction t=session.beginTransaction();    
  
	Employee e1=new Employee();    
	e1.setName("Gaurav Chawla");    
    
	Regular_Employee e2=new Regular_Employee();    
	e2.setName("Vivek Kumar");    
	e2.setSalary(50000);    
	e2.setBonus(5);    
    
	Contract_Employee e3=new Contract_Employee();    
	e3.setName("Arjun Kumar");    
	e3.setPay_per_hour(1000);    
	e3.setContract_duration("15 hours");    
    
	session.persist(e1);    
	session.persist(e2);    
	session.persist(e3);    
    
	t.commit();    
	session.close();    
	System.out.println("success");    
  
}  
}  
```



###### H8.3.2 TPS with annotation

As we have specified earlier, in case of table per subclass strategy, tables are created as per persistent classes but they are treated using primary and foreign key. So there will not be any duplicate column in the relation.

It need to specify <font color=gree>@Inheritance(strategy=InheritanceType.JOINED)</font> in the parent class and <font color=gree>@PrimaryKeyJoinColumn</font> annotation in the subclasses.



table structure, class hierarchy same as before.

- persistent class

Employee.java

```java
package com.max.mypackage;  
import javax.persistence.*;  
  
@Entity  
@Table(name = "employee103")  
@Inheritance(strategy=InheritanceType.JOINED)  
  
public class Employee {  
@Id  
@GeneratedValue(strategy=GenerationType.AUTO)  
      
@Column(name = "id")  
private int id;  
  
@Column(name = "name")  
private String name;  
  
//setters and getters  
}  
File: Regular_Employee.java
package com.javatpoint.mypackage;  
  
import javax.persistence.*;  
  
@Entity  
@Table(name="regularemployee103")  
@PrimaryKeyJoinColumn(name="ID")  
public class Regular_Employee extends Employee{  
      
@Column(name="salary")    
private float salary;  
  
@Column(name="bonus")     
private int bonus;  
  
//setters and getters  
}  
```

Contract_Employee.java

```java
package com.javatpoint.mypackage;  
  
import javax.persistence.*;  
  
@Entity  
@Table(name="contractemployee103")  
@PrimaryKeyJoinColumn(name="ID")  
public class Contract_Employee extends Employee{  
      
    @Column(name="pay_per_hour")  
    private float pay_per_hour;  
      
    @Column(name="contract_duration")  
    private String contract_duration;  
  
    //setters and getters  
}  
```

Regular_Employee.java

```java
package com.max.mypackage;  
  
import javax.persistence.*;  
  
@Entity  
@Table(name="regularemployee103")  
@PrimaryKeyJoinColumn(name="ID")  
public class Regular_Employee extends Employee{  
      
@Column(name="salary")    
private float salary;  
  
@Column(name="bonus")     
private int bonus;  
  
//setters and getters  
}  
```

- hibernate.cfg.xml (Oracle)

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
  
<!-- Generated by MyEclipse Hibernate Tools.                   -->  
<hibernate-configuration>  
  
    <session-factory>  
        <!--The hbm2ddl.auto property is defined for creating automatic table in the database.-->
        <property name="hbm2ddl.auto">update</property>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
<property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property>  
          
        <mapping class="com.javatpoint.mypackage.Employee"/>  
        <mapping class="com.javatpoint.mypackage.Contract_Employee"/>  
        <mapping class="com.javatpoint.mypackage.Regular_Employee"/>  
    </session-factory>  
  
</hibernate-configuration>  
```

- store test

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
  
    public static void main(String args[])  
    {  
        StandardServiceRegistry ssr = new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
        Metadata meta = new MetadataSources(ssr).getMetadataBuilder().build();  
          
        SessionFactory factory=meta.getSessionFactoryBuilder().build();  
        Session session=factory.openSession();  
          
         Transaction t=session.beginTransaction();    
            
            Employee e1=new Employee();    
            e1.setName("Gaurav Chawla");    
                
            Regular_Employee e2=new Regular_Employee();    
            e2.setName("Vivek Kumar");    
            e2.setSalary(50000);    
            e2.setBonus(5);    
                
            Contract_Employee e3=new Contract_Employee();    
            e3.setName("Arjun Kumar");    
            e3.setPay_per_hour(1000);    
            e3.setContract_duration("15 hours");    
                
            session.persist(e1);    
            session.persist(e2);    
            session.persist(e3);    
                
            t.commit();    
            session.close();    
            System.out.println("success");        
    }  
}  
```



#### H9 Collection Mapping in Hibernate

We can map collection elements of Persistent class in Hibernate. You need to declare the type of collection in Persistent class from one of the following types:

- `java.util.List`
- `java.util.Set`
- `java.util.SortedSet`
- `java.util.Map`
- `java.util.SortedMap`
- `java.util.Collection`
- or write the implementation of `org.hibernate.usertype.UserCollectionType`



The persistent class should be defined like this for collection element.

```java
package com.max;  
  
import java.util.List;  
  
public class Question {  
	private int id;  
	private String qname;  
    //List can be of any type  
	private List<String> answers;
  
	//getters and setters
}  
```



##### H9.1 Mapping collection in mapping file

hbm.xml content:

```xml
<class name="com.max.Question" table="q100">  
	<id name="id">  
          <generator class="increment"></generator>  
	</id>  
	<property name="qname"></property>  
    
	<list name="answers" table="ans100">  
        <key column="qid"></key>  
        <index column="type"></index>  
        <element column="answer" type="string"></element>  
	</list>  
</class>  
```

- <font color=green><key></font>element is used to define the **foreign key** in this table based on the Question class identifier.
- <font color=green><index></font>element is used to **identify the type**. List and Map are indexed collection.
- <font color=green><element></font>is used to define the **element of the collection**.



Instance e.g.



- persistent class

Question.java

```java
package com.max;  
  
import java.util.List;  
  
public class Question {  
	private int id;  
	private String qname;  
    //Here, List stores the objects of Answer class  
	private List<Answer> answers;
  
	//getters and setters  
}  
```

Answer.java

```java
package com.max;  

import java.util.List;  

public class Answer {  
	private int id;  
	private String answer;  
	private String posterName;  

    //getters and setters  
}  
```



- hbm.xml mapping file

```xml
<class name="com.max.Question" table="q100">  
	<id name="id">  
		<generator class="increment"></generator>  
	</id>  
	<property name="qname"></property>  
            
    <list name="answers" >  
		<key column="qid"></key>  
		<index column="type"></index>  
		<one-to-many class="com.max.Answer" />  
	</list>  
</class>  
```

*Here, List is mapped by one-to-many relation. In this scenario, there can be many answers for one question.*



##### H9.2 key element

The key element is used to define the foreign key in the joined table based on the original identity. The foreign key element is nullable by default. So for non-nullable foreign key, we need to specify not-null attribute such as:

```xml
<key column="qid" not-null="true"></key>
```

All of the key attributes:

```xml
<key column="column_name"
     on-delete="noaction | cascade"
     not-null="true | false"
     property-ref="property_name"
     update="true | false"
     unique="true | false"
```



##### H9.3 Indexed Collection

The collection elements can be categorized in two forms:

- **indexed** ,and
- **non-indexed**

The **List and Map collection are indexed** whereas set and **bag collections are non-indexed**. Here, indexed collection means List and Map requires an additional element <font color=green><index></font>.



##### H9.4 Collection Elements

The collection elements can have value or entity reference (another class object). We can use one of the 4 elements

- **element**
- **component-element**
- **one-to-many**, or
- **many-to-many**

The element and component-element are used for normal value such as string, int etc. whereas one-to-many and many-to-many are used to map entity reference.

------



##### H9.5 Mapping List

If our persistent class has List object, we can map the List easily either by <list> element of class in mapping file or by annotation.

Use `java.util.List`

 **It needs index column** in the mapping class  



- How to fetch data from list (bag, Set, Map are the same way)

```java
package com.max;    
    
import javax.persistence.TypedQuery;  
import java.util.*;  
import org.hibernate.*;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;  
    
public class FetchData {    
public static void main(String[] args) {    
        
    StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
    Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  
      
    SessionFactory factory=meta.getSessionFactoryBuilder().build();  
    Session session=factory.openSession();  
    
    // Create query to getResultList
    TypedQuery query=session.createQuery("from Question");    
    List<Question> list=query.getResultList();   
    
    // Create an iterator to store temp data 
    Iterator<Question> itr=list.iterator();  
    
    // Traverse list by iterator
    while(itr.hasNext()){    
        Question q=itr.next();    
        System.out.println("Question Name: "+q.getQname());    
            
        //printing answers    
        List<String> list2=q.getAnswers();    
        Iterator<String> itr2=list2.iterator();    
        while(itr2.hasNext()){    
            System.out.println(itr2.next());    
        }          
    }    
    session.close();    
    System.out.println("success");         
}    
}    
```



------



##### H9.6 Mapping Bag

If our persistent class has *List object*, we can map the List by **list or bag** element in the mapping file. The bag is just like List but it doesn't require index element.

Also use `java.util.List`

**Don't needs index column** in the mapping class.

------



##### H9.7 Mapping Set

If our persistent class has Set object, we can map the Set by set element in the mapping file. The **set element doesn't require index element**. The one difference between List and Set is that, it **stores only unique values**.



e.g. for set element:

```xml
<class name="com.max.Question" table="q1002">  
       ...        
          <set name="answers" table="ans1002">  
          <key column="qid"></key>  
          <element column="answer" type="string"></element>  
          </set>  
            
       ...  
</class>  
```



------



##### H9.8 Mapping Map

Hibernate allows you to map Map elements with the RDBMS. As we know, list and map are index-based collections. In case of map, **index column works as the key** and **element column works as the value**.

use `java.util.Map`

e.g.  of Map method:



- persistent class Question.java

``` java
package com.max;  
  
import java.util.Map;  
  
public class Question {  
    private int id;  
    private String name,username;  
    private Map<String,String> answers;  
  
    public Question() {
    }  
    public Question(String name, String username, Map<String, String> answers) {  
        super();  
        this.name = name;  
        this.username = username;  
        this.answers = answers;  
    }  
    public int getId() {  
        return id;  
    }  
    public void setId(int id) {  
        this.id = id;  
    }  
    public String getName() {  
        return name;  
    }  
    public void setName(String name) {  
        this.name = name;  
    }  
    public String getUsername() {  
        return username;  
    }  
    public void setUsername(String username) {  
        this.username = username;  
    }  
    public Map<String, String> getAnswers() {  
        return answers;  
    }  
    public void setAnswers(Map<String, String> answers) {  
        this.answers = answers;  
    }  
}  
```

- question.hbm.xml

```xml
<?xml version='1.0' encoding='UTF-8'?>  
<!DOCTYPE hibernate-configuration PUBLIC 
  "-//Hibernate/Hibernate Configuration DTD 3.0//EN" 
  "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-mapping>  
<class name="com.javatpoint.Question" table="question736">  
    <id name="id">  
    	<generator class="native"></generator>  
    </id>  
    <property name="name"></property>  
    <property name="username"></property>  

    <map name="answers" table="answer736" cascade="all">  
    	<key column="questionid"></key>  
        <index column="answer" type="string"></index>  
    	<element column="username" type="string"></element>  
    </map>  
</class>  
</hibernate-mapping>     
```

- hibernate.cfg.xml

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>  
    <session-factory>  
        <property name="hbm2ddl.auto">update</property>  
        <property name="dialect">org.hibernate.dialect.Oracle9Dialect</property>  
        <property name="connection.url">jdbc:oracle:thin:@localhost:1521:xe</property>  
        <property name="connection.username">system</property>  
        <property name="connection.password">jtp</property>  
        <property name="connection.driver_class">oracle.jdbc.driver.OracleDriver</property>  
      
    <mapping resource="question.hbm.xml"/>  
    </session-factory>  
  
</hibernate-configuration>  
```

- StoreTest.java

```java
package com.max;    
    
import java.util.HashMap;    
import org.hibernate.*;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;    
  
  
public class StoreTest {    
	public static void main(String[] args) {    
   
        StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
        Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  

        SessionFactory factory=meta.getSessionFactoryBuilder().build();  
        Session session=factory.openSession();  

        Transaction t=session.beginTransaction();    

        HashMap<String,String> map1=new HashMap<String,String>();    
        map1.put("Java is a programming language","John Milton");    
        map1.put("Java is a platform","Ashok Kumar");    

        HashMap<String,String> map2=new HashMap<String,String>();    
        map2.put("Servlet technology is a server side programming","John Milton");    
        map2.put("Servlet is an Interface","Ashok Kumar");    
        map2.put("Servlet is a package","Rahul Kumar");    

        Question question1=new Question("What is Java?","Alok",map1);    
        Question question2=new Question("What is Servlet?","Jai Dixit",map2);    

        session.persist(question1);    
        session.persist(question2);    

        t.commit();    
        session.close();    
        System.out.println("successfully stored");    
	}    
}    
```



output:

![Hibernate Mapping Map Example 1](assets/Web%20Frameworks.assets/mapping-map-in-collection-mapping1.jpeg)

![Hibernate Mapping Map Example 2](assets/Web%20Frameworks.assets/mapping-map-in-collection-mapping2.jpeg)





- FetchTest.java

```java
package com.javatpoint;    
import java.util.*;  
  
import javax.persistence.TypedQuery;  
  
import org.hibernate.*;  
import org.hibernate.boot.Metadata;  
import org.hibernate.boot.MetadataSources;  
import org.hibernate.boot.registry.StandardServiceRegistry;  
import org.hibernate.boot.registry.StandardServiceRegistryBuilder;  
   
public class FetchTest {    
    public static void main(String[] args) {    
        StandardServiceRegistry ssr=new StandardServiceRegistryBuilder().configure("hibernate.cfg.xml").build();  
        Metadata meta=new MetadataSources(ssr).getMetadataBuilder().build();  

        SessionFactory factory=meta.getSessionFactoryBuilder().build();  
        Session session=factory.openSession();    

     	TypedQuery query=session.createQuery("from Question ");    
        List<Question> list=query.getResultList();    
        
        Iterator<Question> iterator=list.iterator();   
        
        while(iterator.hasNext()){    
            Question question=iterator.next();   
            
            System.out.println("question id:"+question.getId());    
            System.out.println("question name:"+question.getName());    
            System.out.println("question posted by:"+question.getUsername());    
            System.out.println("answers.....");    
            
            Map<String,String> map=question.getAnswers();    
            Set<Map.Entry<String,String>> set=map.entrySet();    
            Iterator<Map.Entry<String,String>> iteratoranswer=set.iterator();    
            
            while(iteratoranswer.hasNext()){    
                Map.Entry<String,String> entry=(Map.Entry<String,String>)iteratoranswer.next();   
                
                System.out.println("answer name:"+entry.getKey());    
                System.out.println("answer posted by:"+entry.getValue());    
            }    
        }    
        session.close();    
    }    
}    
```



 output:

![Hibernate Mapping Map Example 3](assets/Web%20Frameworks.assets/mapping-map-in-collection-mapping3.jpeg)





#####  H9.9 One to Many



##### H9.10 Many to Many



##### H9.11 One to one



##### H9.12 Many to One



##### H9.13 Bidirectional Association (bi-directional (bi, two) )

Bidirectional association allows us to fetch details of dependent object from both side. In such case, we have the reference of two classes in each other.

Let's take an example of Employee and Address, if Employee class has-a reference of Address and Address has a reference of Employee. Additionally, you have applied one-to-one or one-to-many relationship for the classes in mapping file as well, it is known as bidirectional association.



[Change Bidirectional Association to Unidirectional](https://refactoring.guru/change-bidirectional-association-to-unidirectional)

- Why refactor

A bidirectional association is generally harder to maintain than a unidirectional one, requiring additional code for properly creating and deleting the relevant objects. This makes the program more complicated.

In addition, an improperly implemented bidirectional association can cause problems for garbage collection (in turn leading to memory bloat by unused objects).

- Benefits

    - Simplifies the class that doesn’t need the relationship. Less code equals less code maintenance.

    - Reduces dependency between classes. Independent classes are easier to maintain since any changes to a class affect only that class.





##### H9.14 Hibernate Lazy Collection

Lazy collection loads the child objects on demand, it is used to improve performance. Since Hibernate 3.0, lazy collection is enabled by default.

To use lazy collection, you may optionally use lazy="true" attribute in your collection. It is by default true, so you don't need to do this. If you set it to false, all the child objects will be loaded initially which will decrease performance in case of big data.

e.g.

```xml
<list name="answers" lazy="true">  
          <key column="qid"></key>  
          <index column="type"></index>  
          <one-to-many class="com.javatpoint.Answer"/>  
</list>  
```





##### H9.15 Component mapping

In component mapping, we will map the dependent object as a component. **An component is an object that is stored as an value rather than entity reference.** This is mainly used if the dependent object **doesn't have primary key**. It is used in case of composition (HAS-A relation), that is why it is termed as component.

e.g.,

Address.java

```java
package com.max;  
  
public class Address {  
private String city,country;  
private int pincode;  
  
//getters and setters  
}  
```

Employee.java

```java
package com.max;  
public class Employee {  
private int id;  
private String name;  
private Address address;//HAS-A  
  
//getters and setters  
}  
```



Here, address is a dependent object. Hibernate framework provides the facility to map the dependent object as a component. Let's see how can we map this dependent object in mapping file.

```xml
<class name="com.max.Employee" table="emp177">  
<id name="id">  
<generator class="increment"></generator>  
</id>  
<property name="name"></property>  
  
<component name="address" class="com.max.Address">  
    <property name="city"></property>  
    <property name="country"></property>  
    <property name="pincode"></property>  
</component>  
  
</class>  

```



#### H10 Named Query

There are two ways to define the named query in hibernate:

- by annotation
- by mapping file.





#### H11 Caching in Hibernate

Hibernate caching improves the performance of the application by pooling the object in the cache. It is useful when we have to fetch the same data multiple times.

There are mainly two types of caching:

- First Level Cache, and
- Second Level Cache



#### H12 Hibernate Lifecycle

In Hibernate, either we create an object of an entity and save it into the database, or we fetch the data of an entity from the database. Here, each entity is associated with the lifecycle. The entity object passes through the different stages of the lifecycle.



The Hibernate lifecycle contains the following states: -

- Transient state

    - The transient state is the initial state of an object.

    - Once we create an instance of POJO class, then the object entered in the transient state.

    - Here, an object is not associated with the Session. So, the transient state is not related to any database.

    - Hence(Thus), modifications in the data don't affect any changes in the database.

    - The transient objects exist in the heap memory. They are independent of Hibernate.

```java
//Here, object enters in the transient state.  
Employee e=new Employee(); 
e.setId(101);  
e.setFirstName("Gaurav");  
e.setLastName("Chawla");  
```



- Persistent state
    - As soon as the object associated with the Session, it entered in the persistent state.
    - Hence, we can say that an object is in the persistence state when we save or persist it.
    - Here, each object represents the row of the database table.
    - So, modifications in the data make changes in the database.

We can use any of the following methods for the persistent state.

```java
session.save(e);  
session.persist(e);  
session.update(e);  
session.saveOrUpdate(e);  
session.lock(e);  
session.merge(e);  
```



- Detached state
    - Once we either close the session or clear its cache, then the object entered into the detached state.
    - As an object is no more associated with the Session, modifications in the data don't affect any changes in the database.
    - However, the detached object still has a representation in the database.
    - If we want to persist the changes made to a detached object, it is required to reattach the application to a valid Hibernate session.
    - To associate the detached object with the new hibernate session, use any of these methods - load(), merge(), refresh(), update() or save() on a new session with the reference of the detached object.

We can use any of the following methods for the detached state.

```java
session.close();  
session.clear();  
session.detach(e);  
session.evict(e);  
```





![Hibernate Lifecycle](assets/Web%20Frameworks.assets/hibernate-lifecycle.png)







### Mybatis





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
