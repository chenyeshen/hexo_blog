---
layout:     post
title:      SpringCloud入门学习
subtitle:   学习笔记
date:       2019-08-10
author:     chenyeshen
header-img: img/img20.jpg
catalog: true
tags:
    - SpringCloud
    - 微服务
---

## Eureka
### 父工程的pom.xml
```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.yeshen.cloud</groupId>
    <artifactId>demo</artifactId>
    <version>1.0-SNAPSHOT</version>
	
	
   // 这里关于  info的配置
   
    <build>
        <finalName>springcloud_demo</finalName>
        <resources>
            <resource>
                <directory>src/main/resources</directory>
                <filtering>true</filtering>
            </resource>
        </resources>
        <plugins>
           <plugin>
               <groupId>org.apache.maven.plugins</groupId>
               <artifactId>maven-resources-plugin</artifactId>
               <configuration>
                   <delimiters>
                       <delimit>$</delimit>
                   </delimiters>
               </configuration>

           </plugin>

        </plugins>

    </build>

    <modules>
        <module>eureka7001</module>
        <module>test</module>
    </modules>

</project>
```
### 服务端 EurekaServer

#### pom.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.6.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
        <spring-cloud.version>Greenwich.SR2</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```
### application.java 

```
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.server.EnableEurekaServer;

@SpringBootApplication
@EnableEurekaServer
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}

```

### yml的配置

```
server:
  port: 7001
eureka:
  instance:
    hostname: localhost
  client:
    fetch-registry: false
    register-with-eureka: false
    service-url:
       defaultZone: http://${eureka.instance.hostname}:${server.port}/eureka

```

 ## 客户端 EurekaClient
### pom.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.1.6.RELEASE</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.example</groupId>
    <artifactId>demo</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>demo</name>
    <description>Demo project for Spring Boot</description>

    <properties>
        <java.version>1.8</java.version>
        <spring-cloud.version>Greenwich.SR2</spring-cloud.version>
    </properties>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>

        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
            <version>2.1.6.RELEASE</version>
        </dependency>
    </dependencies>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>${spring-cloud.version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>

```
### application.java 
```
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}

```

### yml
```

spring:
  application:
    name: test
eureka:
  client:
    service-url:
      defaulZone: http://localhost:7001/eureka
  instance:
    instance-id: yeshen
    prefer-ip-address: true
info:
   app.name: yeshenApp
   company.name:  www.chenyeshen.com
   build.artifactId: $project.artifactId$
   build.version: $project.version$


```
** 或者**

### application.properties
```
spring.application.name=test

eureka.client.service-url.defaultZone=http://localhost:7001/eureka
eureka.instance.instance-id=yeshen
eureka.instance.prefer-ip-address=true

info.app.name=yeshenApp
info.company.name=www.yeshen.com
info.build.artifactId=demo
info.build.version=0.0.1-SNAPSHOT
```

###  效果如图：
![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190726165041085.png)

![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190726165102750.png)


## 服务的发现 

### provider 提供暴露服务的接口
**主程序  application**
```
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.netflix.eureka.EnableEurekaClient;

@SpringBootApplication
@EnableEurekaClient
@EnableDiscoveryClient  // 暴露发现
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

}

```

**TestController**
```
package com.example.demo;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cloud.client.ServiceInstance;
import org.springframework.cloud.client.discovery.DiscoveryClient;   //  cloud中得client
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.net.URI;
import java.util.List;

@RestController
public class TestController {

    @Autowired
    DiscoveryClient discoveryClient;

    @RequestMapping("/list")
    public Object list() {

        List<String> services = discoveryClient.getServices();
        System.out.println("==========" + services);

        List<ServiceInstance> yeshen = discoveryClient.getInstances("test");

        for (ServiceInstance instance : yeshen) {

            String host = instance.getHost();
            String instanceId = instance.getInstanceId();
            String uri = instance.getUri().toString();

            System.out.println("555" + host + "5555" + instanceId + "5555" + uri);


        }
        return  this.discoveryClient;
    }
}

```

### 发现服务
### 消费者发现服务

```
package com.example.demo.controller;

import java.util.List;

import com.example.demo.dao.Dept;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.client.RestTemplate;


@RestController
public class DeptController_Consumer
{

	//private static final String REST_URL_PREFIX = "http://localhost:8001";
	private static final String REST_URL_PREFIX = "http://localhost:8080";

	/**
	 * 使用 使用restTemplate访问restful接口非常的简单粗暴无脑。 (url, requestMap,
	 * ResponseBean.class)这三个参数分别代表 REST请求地址、请求参数、HTTP响应转换被转换成的对象类型。
	 */
	@Autowired
	private RestTemplate restTemplate;

	@SuppressWarnings("unchecked")
	@RequestMapping(value = "/consumer/dept/list")
	public Object list()
	{
		return restTemplate.getForObject(REST_URL_PREFIX + "/list", Object.class);
	}


}

```

### 效果如图：

 ![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190726214449940.png)


 ## 集群搭建

### Eureka7001.com

**配置文件**

```
server:
  port: 7001
eureka:
  instance:
    hostname: eureka7001.com
  client:
    fetch-registry: false
    register-with-eureka: false
    service-url:
       defaultZone: http://eureka8001.com:8001/eureka,http://eureka9001.com:9001/eureka

```

### Eureka8001.com

**配置文件**
```
server:
  port: 8001
eureka:
  instance:
    hostname: eureka8001.com
  client:
    fetch-registry: false
    register-with-eureka: false
    service-url:
       defaultZone: http://eureka7001.com:7001/eureka,http://eureka9001.com:9001/eureka

```

### Eureka9001.com

**配置文件**

```
server:
  port: 9001
eureka:
  instance:
    hostname: eureka8009.com
  client:
    fetch-registry: false
    register-with-eureka: false
    service-url:
       defaultZone: http://eureka7001.com:7001/eureka,http://eureka8001.com:8001/eureka

```

### 客户端0入驻集群

**配置**
```
server:
  port: 10000
eureka:
  client:
    service-url:
       defaultZone: http://eureka7001.com:7001/eureka,http://eureka8001.com:8001/eureka,http://eureka9001.com:9001/eureka
  instance:
      instance-id: yeshen
      prefer-ip-address: true
spring:
  profiles:
    active: dev
  application:
    name: provide

info:
  app:
     name: yeshenApp
  company:
     name: www.yeshen.com
  build:
     artifactId: demo
     version:  0.0.1-SNAPSHOT
```
### 客户端1入驻集群

**配置**

```
server:
  port: 10001
eureka:
  client:
    service-url:
       defaultZone: http://eureka7001.com:7001/eureka,http://eureka8001.com:8001/eureka,http://eureka9001.com:9001/eureka
  instance:
      instance-id: yeshen
      prefer-ip-address: true
spring:
  profiles:
    active: dev
  application:
    name: provide001

info:
  app:
     name: yeshenApp
  company:
     name: www.yeshen.com
  build:
     artifactId: demo
     version:  0.0.1-SNAPSHOT
```

### 客户端2入驻集群

**配置**
```
server:
  port: 10002
eureka:
  client:
    service-url:
       defaultZone: http://eureka7001.com:7001/eureka,http://eureka8001.com:8001/eureka,http://eureka9001.com:9001/eureka
  instance:
      instance-id: yeshen
      prefer-ip-address: true
spring:
  profiles:
    active: dev
  application:
    name: provide002

info:
  app:
     name: yeshenApp
  company:
     name: www.yeshen.com
  build:
     artifactId: demo
     version:  0.0.1-SNAPSHOT
```

 ### 效果如图：
 ![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190727154432706.png)![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190727154432806.png)![file](https://chenyeshen.oss-cn-shenzhen.aliyuncs.com/oneblog/article/20190727154432816.png)

 
