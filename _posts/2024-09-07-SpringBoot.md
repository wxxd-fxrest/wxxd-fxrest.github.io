---
title: Spring Boot에 대하여
date: 2024-09-07 17:40:00 +09:00
categories: [Java&Spring, Spring]
tags:
  [
    Spring,
    Java,
    SpringBoot,
    SpringFramework
  ]
---

<br/>
<br/>

# Spring Boot에 대하여

## 1. Spring Boot란?
Spring Boot는 Java 기반의 오픈 소스 프레임워크로, Spring Framework를 쉽게 사용할 수 있도록 도와준다. 복잡한 설정을 줄이고, 빠르고 효율적으로 애플리케이션을 개발할 수 있는 환경을 제공하며, 특히, 웹 애플리케이션과 RESTful API를 만드는 데 적합하다.  

<br/>
* * *
<br/>

## 1.1. Spring과 Spring Boot의 차이점

### Spring Framework란?
Spring Framework는 Java 플랫폼을 위한 애플리케이션 프레임워크로, 주로 엔터프라이즈급 애플리케이션을 개발하는 데 사용된다. Spring은 의존성 주입(Dependency Injection)과 관점 지향 프로그래밍(Aspect-Oriented Programming) 등의 기능을 제공하여, 코드의 모듈화와 테스트를 수월하게 할 수 있도록 도와준다.  

<br/>

### Spring Boot란?
Spring Boot는 Spring Framework의 확장으로, 개발자가 보다 간편하게 애플리케이션을 만들 수 있도록 돕는 도구이다. 자동 설정, 내장 서버, 스타터 의존성 등의 기능을 통해 복잡한 설정을 줄이고, 빠른 개발을 할 수 있도록 도와준다.  

<br/>

### 주요 차이점
**설정 방식**
- Spring Framework: XML 파일이나 Java Config를 통해 복잡한 설정이 필요하며, 개발자가 직접 설정을 관리해야 하므로 시간이 많이 소요된다.
- Spring Boot: 자동 설정 기능을 제공하여, 필요한 라이브러리와 환경을 자동으로 구성한다. 이를 통해 설정 시간을 크게 줄일 수 있다.  

**실행 방식**
- Spring Framework: 외부 서버(예: Tomcat, Jetty)에 배포해야 실행할 수 있다.
- Spring Boot: 내장형 서버를 제공하여, JAR 파일로 실행할 수 있다. 별도의 서버 환경 없이도 애플리케이션을 쉽게 실행할 수 있다.  

**의존성 관리**
- Spring Framework: 필요한 라이브러리를 수동으로 관리해야 하며, 각 라이브러리의 버전 호환성을 직접 체크해야 한다.
- Spring Boot: 스타터 의존성을 통해 관련 라이브러리를 간편하게 추가할 수 있으며, 버전 호환성 문제를 자동으로 관라힌다.  

**프로덕션 준비 기능**
- Spring Framework: 프로덕션 환경을 위한 기능은 별도로 구현해야 한다.
- Spring Boot: 헬스 체크, 모니터링, 메트릭 수집 등의 기능이 기본적으로 제공되어 프로덕션 환경에 쉽게 배포할 수 있다.  

<br/>

**결론**  
Spring Framework는 매우 강력한 기능을 제공하지만, 설정과 관리가 복잡할 수 있다. 반면, Spring Boot는 이러한 복잡성을 줄이고, 빠르고 효율적인 개발 환경을 제공한다. 따라서, 새로운 프로젝트를 시작할 때는 Spring Boot를 사용하는 것이 더 유리할 수 있다.   

<br/>
* * *
<br/>

## 2. Spring Boot의 필요성
전통적인 Spring Framework는 설정이 복잡하고 많은 XML 파일이 필요하고, 이로 인해 개발 시간이 길어지고 유지보수가 어려워졌다. Spring Boot는 이러한 문제를 해결하기 위해 다음과 같은 기능을 제공한다.

<br/>
* * *
<br/>

## 3. 주요 특징

### 3.1. 자동 설정
Spring Boot는 애플리케이션의 클래스 경로에 있는 라이브러리를 자동으로 인식하여 필요한 설정을 처리한다. 예를 들어, Spring Boot를 사용하면 웹 서버 설정이나 데이터베이스 연결을 위한 복잡한 코드를 작성할 필요가 없다. 

### 3.2. 독립 실행형 애플리케이션
Spring Boot로 만든 애플리케이션은 내장형 서버를 포함하고 있어, 별도의 서버 환경을 구축하지 않고도 실행할 수 있다. 즉, JAR 파일을 실행하는 것만으로도 애플리케이션을 시작할 수 있다.

### 3.3. 스타터 의존성
스타터 의존성은 Spring Boot의 핵심 기능 중 하나이다. 필요한 기능에 따라 `spring-boot-starter-xxx` 형태로 의존성을 추가하면, 관련된 라이브러리와 설정이 자동으로 포함된다. 예를 들어, 웹 애플리케이션을 만들고 싶으면 다음과 같이 의존성을 추가한다.

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

### 3.4. 프로덕션 준비 기능
Spring Boot는 애플리케이션의 상태를 모니터링하고, 성능을 측정할 수 있는 기능을 제공한다. 예를 들어, 헬스 체크 기능을 통해 애플리케이션이 정상적으로 작동하는지 확인할 수 있다.

<br/>
* * *
<br/>

## 4. Spring Boot의 사용 예

### 4.1. RESTful API 개발
Spring Boot는 RESTful API를 쉽게 개발할 수 있도록 해준다. REST는 웹상에서 자원을 표현하고 조작하기 위한 아키텍처 스타일로, HTTP 프로토콜을 사용합니다. 아래는 간단한 사용자 정보를 반환하는 REST API 예제이다.

```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/users")
    public List<User> getUsers() {
        return userService.findAll();
    }
}
```

이 코드는 `/api/users` 경로로 GET 요청을 보내면 모든 사용자 정보를 반환한다.

### 4.2. 데이터베이스 연동
Spring Boot는 JPA(Java Persistence API)와 함께 사용할 수 있어 데이터베이스 연동이 간편하다. JPA는 객체와 데이터베이스의 관계를 매핑해주는 기술이며, 다음은 사용자 정보를 데이터베이스에서 CRUD(Create, Read, Update, Delete) 작업을 수행하는 예제이다.

#### 4.2.1. 의존성 추가
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

#### 4.2.2. 사용자 엔티티 생성
```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;

    // Getters and Setters
}
```

#### 4.2.3. 리포지토리 인터페이스 생성
```java
@Repository
public interface UserRepository extends JpaRepository<User, Long> {
}
```

이제 `UserRepository`를 통해 데이터베이스와 상호작용할 수 있다.

### 4.3. 애플리케이션 실행
Spring Boot 애플리케이션은 `@SpringBootApplication` 어노테이션이 붙은 메인 클래스를 통해 실행된다. 아래는 간단한 실행 예제이다.

```java
@SpringBootApplication
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

## 5. 결론
Spring Boot는 현대 웹 애플리케이션 개발에 있어 매우 유용한 도구이다. 자동 설정, 독립 실행형 기능, 스타터 의존성 등의 특징 덕분에 개발자는 더 빠르고 효율적으로 애플리케이션을 구축할 수 있다. 