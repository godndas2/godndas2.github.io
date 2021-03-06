---
layout: post
current: post
cover:  assets/images/welcome.jpg
navigation: True
title: Welcome to ReSpace
date: 2019-01-08 10:30:00
tags: [daily-rec]
class: post-template
subclass: 'post tag-daily-rec'
author: ReSpace
---

**Spring Boot를 사용해보자**

주니어 개발자로서 신기술에 대한 호기심이 항상 넘쳐난다.
Spring Boot를 신기술이라 칭하기는 애매하지만 내가 모르는 모든 기술은 신기술이니까(...)

2019년 목표 중 하나인 <a href="#">Spring Boot를 사용해서 토이 프로젝트 만들기</a>를 하기 위해서 오늘 부터 Spring Boot를 파헤쳐보기로 했다.

### Spring Boot를 왜 사용해야하나?
1. 수작업으로 초기 셋업하는 과정 없이 간단히 프로젝트를 띄울 수 있다. 스프링에서 제공하는 Spring Tool Suite 개발 도구를 사용하면 마법사를 통해 기본적인 프로젝트 성격과 프로젝트에서 필요로 하는 라이브러리를 선택할 수 있다. 수작업으로 셋업하더라도 이전에 비해 반 이상이 단순해진다고 생각된다.
2. 프로젝트마다 일상적으로 설정하게 되는 사항들을 이미 내부적으로 가지고 있고 개별적으로 차이가 나는 부분만 설정 파일에 집어 넣으면 된다. 예를 들어 DB 연결 설정은 설정대로, 스프링 DB 설정은 설정대로 하지 않고 DB 연결 설정만 설정 파일에 적어놓으면 된다. DB 드라이버니, 트랜잭션이니 하는 것처럼 당연히 들어가야하는 것들은 알아서 처리된다.
3. 톰캣(Tomcat)이나 제티(Jetty)를 기본 내장할 수 있으며 웹 프로젝트 띄우는 시간이 독립적인 톰캣으로 띄우는 시간보다 반은 단축된다(예를 들어 30초 -> 15초). 또한 이렇게 서블릿 컨테이너가 내장될 수 있으므로 프로젝트를 .jar 파일 형태로 간단히 만들어 배포할 수 있다.
4. maven pom.xml에서 의존 라이브러리의 버전을 일일이 지정하지 않아도 된다. 스프링 부트가 권장 버전을 관리한다. 또한 Spring Tool Suite을 사용한다면 이클립스의 “컨텐트 어시스트” 기능을 통해 의존 라이브러리를 자동 완성 방식으로 입력할 수 있다.
<p style="font-size: 12px;"><a href="https://start.goodtime.co.kr/">이동련</a>님의 글 참조</p>

### Code

**Spring의 Pom.xml**

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.sivalabs</groupId>
    <artifactId>springmvc-jpa-demo</artifactId>
    <packaging>war</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>springmvc-jpa-demo</name>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>      
        <failOnMissingWebXml>false</failOnMissingWebXml>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-webmvc</artifactId>
            <version>4.2.4.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-jpa</artifactId>
            <version>1.9.2.RELEASE</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>1.7.13</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-api</artifactId>
            <version>1.7.13</version>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-log4j12</artifactId>
            <version>1.7.13</version>
        </dependency>
        <dependency>
            <groupId>log4j</groupId>
            <artifactId>log4j</artifactId>
            <version>1.2.17</version>
        </dependency>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>1.4.190</version>
        </dependency>
        <dependency>
            <groupId>commons-dbcp</groupId>
            <artifactId>commons-dbcp</artifactId>
            <version>1.4</version>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>5.1.38</version>
        </dependency>
        <dependency>
            <groupId>org.hibernate</groupId>
            <artifactId>hibernate-entitymanager</artifactId>
            <version>4.3.11.Final</version>
        </dependency>
        <dependency>
            <groupId>javax.servlet</groupId>
            <artifactId>javax.servlet-api</artifactId>
            <version>3.1.0</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>org.thymeleaf</groupId>
            <artifactId>thymeleaf-spring4</artifactId>
            <version>2.1.4.RELEASE</version>
        </dependency>
    </dependencies>
</project>
```


### Spring Boot의 Pom.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.sivalabs</groupId>
    <artifactId>hello-springboot</artifactId>
    <packaging>jar</packaging>
    <version>1.0-SNAPSHOT</version>
    <name>hello-springboot</name>
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>1.3.2.RELEASE</version>
    </parent>
    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
        <java.version>1.8</java.version>
    </properties>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-data-jpa</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-devtools</artifactId>
        </dependency>
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
        </dependency>
    </dependencies>
</project>
```


두 개의 pom.xml을 비교해보면 Spring Boot 코드의 양이 한 눈에 봐도 적다.

무엇보다 내가 Spring Boot를 search할 때 흥미롭게 봤던 점은 내장 된 Servlet Container를 지원한다는 점이다.

spring-boot-starter-tomcat을 자동으로 가져오는 spring-boot-startter-web이 추가되어있고 main 메소드를 실행할 때 Tomcat을 포함한 Container로 시작했으므로 외부에서 따로 Tomcat을 가져올 필요가 없다는 것이다 !

### 만약 Tomcat이 아닌 Jetty를 사용한다면?
<br>
spring-boot-starter-tomcat을 제외하고 spring-boot-starter-jetty를 포함시켜주면 된다.
 
<p><mark>To be continued...</mark></p>
