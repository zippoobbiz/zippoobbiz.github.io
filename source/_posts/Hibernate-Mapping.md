---
title: Hibernate Mapping
date: 2017-02-22 09:34:09
tags: [Hibernate, JPA]
categories: [Framework, Hibernate]
---

{% qnimg hibernate.jpeg %}

# A mapping example using xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE hibernate-mapping PUBLIC 
 "-//Hibernate/Hibernate Mapping DTD//EN"
 "http://www.hibernate.org/dtd/hibernate-mapping-3.0.dtd"> 

<hibernate-mapping>
   <class name="Employee" table="EMPLOYEE">
      <meta attribute="class-description">
         This class contains the employee detail. 
      </meta>
      <id name="id" type="int" column="id">
         <generator class="native"/>
      </id>
      <property name="firstName" column="first_name" type="string"/>
      <property name="lastName" column="last_name" type="string"/>
      <property name="salary" column="salary" type="int"/>
   </class>
</hibernate-mapping>
```

The file name should be <classname>.hbm.xml

# Mapping type
### Primitive types
|Mapping Type|Java Type|ANSI SQL type|
|:-|:-|:-|
|integer|int/java.lang.Integer|INTEGER|
|long|long/java.lang.Long|BIGINT|
|short|short/java.lang.Short|SMALLINT|
|float|float/java.lang.Float|FLOAT|
|double|double/java.lang.Double|DOUBLE|
|big_decimal|java.math.BigDecimal|NUMERIC|
|character|java.lang.String|CHAR(1)|
|string|java.lang.String|VARCHAR|
|byte|byte/java.lang.Byte|TINYINT|
|boolean|boolean/java.lang.Boolean|BIT|
|yes/no|boolean/java.lang.Boolean|CHAR(1) ('Y' or 'N')|
|true/false|boolean/java.lang.Boolean|CHAR(1) ('T' or 'F')|

### Date types
|Mapping Type|Java Type|ANSI SQL type|
|:-|:-|:-|
|date|java.util.Date/java.sql.Date|DATE|
|time|java.util.Date/java.sql.Time|TIME|
|timestamp|java.util.Date/java.sql.Timestamp|TIMESTAMP|
|calendar|java.util.Calendar|TIMESTAMP|
|calendar_date|java.util.Calendar|DATE|

### Binary and BLOB types
|Mapping Type|Java Type|ANSI SQL type|
|:-|:-|:-|
|binary|byte[]|VARBINARY (or BLOB)|
|text|java.lang.String|CLOB|
|serializable|any Java class that implements java.io.Serializable|VARBINARY (or BLOB)|
|clob|java.sql.Clob|CLOB|
|blob|java.sql.Blob|BLOB|

### JDK arelated types
|Mapping Type|Java Type|ANSI SQL type|
|:-|:-|:-|
|class|java.lang.Class|VARCHAR|
|locale|java.util.Locale|VARCHAR|
|timezone|java.util.TimeZone|VARCHAR|
|currency|java.util.Currency|VARCHAR|

# Annotations

@Entity @Table @id @GeneratedValue @Column

An example 
```Java
import javax.persistence.*;

@Entity
@Table(name = "EMPLOYEE")
public class Employee {
   @Id @GeneratedValue
   @Column(name = "id")
   private int id;

   @Column(name = "first_name")
   private String firstName;

   @Column(name = "last_name")
   private String lastName;

   @Column(name = "salary")
   private int salary;  

   public Employee() {}
   public int getId() {
      return id;
   }
   public void setId( int id ) {
      this.id = id;
   }
   public String getFirstName() {
      return firstName;
   }
   public void setFirstName( String first_name ) {
      this.firstName = first_name;
   }
   public String getLastName() {
      return lastName;
   }
   public void setLastName( String last_name ) {
      this.lastName = last_name;
   }
   public int getSalary() {
      return salary;
   }
   public void setSalary( int salary ) {
      this.salary = salary;
   }
}
```
