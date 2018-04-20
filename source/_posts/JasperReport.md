---
title: JasperReport
date: 2016-11-13 16:20:05
tags: [Java]
categories: [Language, Java]
---


> JasperReports is an open source Java reporting tool that can write to a variety of targets, such as: screen, a printer, into PDF, HTML, Microsoft Excel, RTF, ODT, Comma-separated values or XML files. It can be used in Java-enabled applications, including Java EE or web applications, to generate dynamic content. –Wikipedia


![Alt text](http://og2api1gp.bkt.clouddn.com/static/images/jasper.jpg "Optional title")

Download it, unzip it. JasperReport Lib cannot run alone and we don’t really need to install it, we only need to cp it to classpath directory with all other jar files.

JasperReport using AWT generate report, if using terminal and terminal only, then JasperReport is not a good choice.

Generate report

```
package jasperreport.javabean;  
  
import java.util.Date;  
  
public class User {  
    private String username;  
    private Date birthday;  
  
    public User(String username, Date birthday) {  
        this.username = username;  
        this.birthday = birthday;  
    }  
  
    public String getUsername() {  
        return username;  
    }  
  
    public void setUsername(String username) {  
        this.username = username;  
    }  
  
    public Date getBirthday() {  
        return birthday;  
    }  
  
    public void setBirthday(Date birthday) {  
        this.birthday = birthday;  
    }  
  
}
```

```
package jasperreport.javabean;  
  
import java.io.InputStream;  
import java.util.ArrayList;  
import java.util.Date;  
import java.util.HashMap;  
import java.util.List;  
import java.util.Map;  
  
import net.sf.jasperreports.engine.JRExporterParameter;  
import net.sf.jasperreports.engine.JasperFillManager;  
import net.sf.jasperreports.engine.JasperPrint;  
import net.sf.jasperreports.engine.data.JRBeanCollectionDataSource;  
import net.sf.jasperreports.engine.export.JRTextExporter;  
import net.sf.jasperreports.engine.export.JRTextExporterParameter;  
  
public class JasperReportWithJavaBean {  
    public static void export() throws Exception{  
          
        InputStream inputStream = JasperReportWithJavaBean.class.getResourceAsStream("JavaBeanReport.jasper");  
        Map<Object,Object> parameters = new HashMap<Object,Object>();  
          
        List<User> users = new ArrayList<User>();  
        users.add(new User("user_01",new Date()));  
        users.add(new User("user_02",new Date()));  
        users.add(new User("user_03",new Date()));  
          
        JRBeanCollectionDataSource dataSource = new JRBeanCollectionDataSource(users);  
        JasperPrint jasperPrint = JasperFillManager.fillReport(inputStream, parameters, dataSource);  
          
          
        JRTextExporter exporter = new JRTextExporter();  
          
        exporter.setParameter(JRExporterParameter.JASPER_PRINT, jasperPrint);    
        exporter.setParameter(JRExporterParameter.OUTPUT_FILE_NAME, "javabean.txt");    
        exporter.setParameter(JRTextExporterParameter.PAGE_WIDTH, 200);    
        exporter.setParameter(JRTextExporterParameter.PAGE_HEIGHT, 100);    
        exporter.exportReport();  
    }  
      
    public static void main(String[] args) throws Exception{  
        export();  
    }  
}
```

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">  
    <modelVersion>4.0.0</modelVersion>  
    <groupId>JasperReport</groupId>  
    <artifactId>JasperReport</artifactId>  
    <version>0.0.1-SNAPSHOT</version>  
  
    <dependencies>  
        <dependency>  
            <groupId>net.sf.jasperreports</groupId>  
            <artifactId>jasperreports</artifactId>  
            <version>3.7.2</version>  
        </dependency>  
          
        <dependency>  
            <groupId>org.codehaus.groovy</groupId>  
            <artifactId>groovy-all</artifactId>  
            <version>1.7.5</version>  
        </dependency>  
          
        <dependency>  
            <groupId>mysql</groupId>  
            <artifactId>mysql-connector-java</artifactId>  
            <version>5.1.13</version>  
        </dependency>  
    </dependencies>  
</project>
```