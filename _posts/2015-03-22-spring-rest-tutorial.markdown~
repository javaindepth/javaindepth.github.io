---
layout: post
title:  "Spring-rest web service!"
date:   2015-03-22 14:03:17
categories: jekyll update
comments: true
---

Spring is an integral part of any java devlopment and the api is widely used in the industy,and hence cant be ignored. The spring rest tutorial gives you a basic introduction to string rest api with maven. 

TOPIC

* Download and install required tools
 * [maven](http://maven.apache.org/)
 * [java](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
 * [eclipse](https://eclipse.org/downloads/)

Create a maven project with the following command
{% highlight java %}
mvn archetype:generate -DgroupId=com.javaindepth.springrest -DartifactId=spring-rest -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
{% endhighlight %}	

Add eclipse capablity to your maven project
{% highlight java %}
mvn eclipse:eclipse	
{% endhighlight %}

update your pom.xml with the bellow mentioned spring dependencies dependencies 
{% highlight java%}
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>org.springframework</groupId>
    <artifactId>gs-rest-service</artifactId>
    <version>0.1.0</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.2.2.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
		<dependency>
		      <groupId>junit</groupId>
		      <artifactId>junit</artifactId>
		      <version>3.8.1</version>
		      <scope>test</scope>
		</dependency>
    </dependencies>

    <properties>
        <java.version>1.7</java.version>
    </properties>


    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

    <repositories>
        <repository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </repository>
    </repositories>
    <pluginRepositories>
        <pluginRepository>
            <id>spring-releases</id>
            <url>https://repo.spring.io/libs-release</url>
        </pluginRepository>
    </pluginRepositories>
</project>
{% endhighlight %}

Controller Class

the @RestController annotation defines the controller class, this is new addition in spring-4 which is the same as using @controller and @responsebody annotations. The @requestmapping annotation has the mapping string "greeting", which by default accepts any methods unless specified. Eg: @RequestMapping("/greetings",method="GET") , here the method is mentioned to allow only GET requests.

{% highlight java%}
@RestController
public class MyAppController {
	AtomicInteger counter=new AtomicInteger();
	private String format="Hello %s";
	@RequestMapping("/greetings")
	public Greeting greetings(@RequestParam(value="name",defaultValue="javaindepth")String name){
		return new Greeting(counter.incrementAndGet(),String.format(format, name));
		}
}
{% endhighlight %}

Model class

The greeting model class has the set of variables which are used in the controller.
{% highlight java %}
public class Greeting implements Serializable{
	private static final long serialVersionUID = 1L;
	private int count;
	private String context;
	public Greeting(int count,String context) {
	this.count=count;
	this.context=context;
	}
	public int getCount() {
	return count;
	}
	public void setCount(int count) {
	this.count = count;
	}
	public String getContext() {
	return context;
	}
	public void setContext(String context) {
	this.context = context;
	}
}
	
{% endhighlight %}


SpringBootApplication

the webservice can be deployed with out packaging it to a war, with the help of springbootapplication annotation. The bellow code will deploy the application in the internal tomcat server and make it available in port 8080. 

{% highlight java %}
@SpringBootApplication
public class App
{
public static void main( String[] args )
{
SpringApplication.run(App.class, args);
}
}
{% endhighlight %} 

Application URL 

The application can now be accessed with the below url. Also we are using the jackson liberaries to convert the greeting objects returned back in the json format, which will be taken care of automatically. 

[http://localhost:8080/greeting](http://localhost:8080/greeting)

Source code

The complete source code can be found here

[https://github.com/javaindepth/spring-rest.git](https://github.com/javaindepth/spring-rest.git)



