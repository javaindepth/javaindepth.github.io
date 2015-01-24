---
layout: post
title:  "RESTful web service with Jersey !"
date:   2015-01-03 14:03:17
categories: jekyll update
comments: true
---
The purpose of this tutorial is to get acquaintance with RESTfull web service. We are using Jersy API to help implement a RESTful web service.
With apache tomacat as the web server.We are using maven to build the project and delpoy the project archive to tomcat. 

TOPIC

* Download and install required tools
 * [maven](http://maven.apache.org/)
 * [java](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html)
 * [eclipse](https://eclipse.org/downloads/)
 * [tomcat](http://tomcat.apache.org/download-70.cgi)

* Create a maven project with the following command
{% highlight java %}
mvn archetype:generate -DgroupId=com.javaindepth.rest -DartifactId=resthelloworld -DarchetypeArtifactId=maven-archetype-webapp -DinteractiveMode=false
{% endhighlight %}

* Add eclipes capabality to maven project

{% highlight java %}
mvn eclipse:eclipse -Dwtpversion=2.0
{% endhighlight %}


* Update the pom.xml with the following dependency for jersey liberaries

{% highlight xml %}
<dependencies> 
    <dependency>
        <groupId>com.sun.jersey</groupId>
        <artifactId>jersey-server</artifactId>
        <version>1.8</version>
    </dependency>
</dependencies>
{% endhighlight %}

* Service Class
{% highlight java %}
    package com.javaindepth.resthelloworld;
    import javax.ws.rs.GET;
    import javax.ws.rs.Path;
    import javax.ws.rs.PathParam;
    import javax.ws.rs.core.Response;
    @Path("/hellorest")
    public class HelloWorld {
        @GET
        @Path("/{params}")
        public Response getMessage(@PathParam("params") String message){
            String text="Hello "+message;
            return (Response) Response.status(200).entity(text).build();
    }
    }
{% endhighlight %}

* Update web.xml
{% highlight xml %}
<servlet>
    <servlet-name>jersey-serlvet</servlet-name>
    <servlet-class>
                 com.sun.jersey.spi.container.servlet.ServletContainer
            </servlet-class>
    <init-param>
         <param-name>com.sun.jersey.config.property.packages</param-name>
         <param-value>com.javaindepth.resthelloworld</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
    <servlet-name>jersey-serlvet</servlet-name>
    <url-pattern>/rest/*</url-pattern>
</servlet-mapping>
{% endhighlight %}

* Deploy the project in tomcat

 * Update tomcat-users.xml
{% highlight xml%}
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>
 
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<user username="admin" password="password" roles="manager-gui,manager-script" />
 
</tomcat-users>
{% endhighlight %}

 * update maven settings.xml
{% highlight xml%}
<?xml version="1.0" encoding="UTF-8"?>
<settings >
	<servers>
 
		<server>
			<id>TomcatServer</id>
			<username>admin</username>
			<password>password</password>
		</server>
 
	</servers>
</settings>
{% endhighlight %}
 * Update project pom.xml
{% highlight xml%}
	<plugin>
		<groupId>org.apache.tomcat.maven</groupId>
		<artifactId>tomcat7-maven-plugin</artifactId>
		<version>2.2</version>
		<configuration>
			<url>http://localhost:8080/manager/text</url>
			<server>TomcatServer</server>
			<path>/helloworldrest</path>
		</configuration>
	</plugin>
{% endhighlight %}

 * Deploying undeploy and redeploy the appplication archive
{% highlight java %}
mvn tomcat7:deploy 
mvn tomcat7:undeploy 
mvn tomcat7:redeploy
{% endhighlight %}

* Project Demo

 [http://localhost:8080/helloworldrest/rest/hellorest/javaindepth](http://localhost:8080/helloworldrest/rest/hellorest/javaindepth)

* Clone the complete project source code from the repo

[https://github.com/javaindepth/resthelloworld](https://github.com/javaindepth/resthelloworld)

