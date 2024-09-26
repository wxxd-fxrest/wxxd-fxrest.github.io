---
title: Bean Overview - Spring 공식문서 뿌시기 
date: 2024-09-26 15:30:00 +09:00
categories: [Java&Spring, Spring]
tags:
  [
    Spring,
    Java,
    Spring 공식문서,
    Bean Overview,
    Bean 정의,
  ]
---

<br/>
<br/>

# Spring Bean 개요 - Bean Overview
## Spring IoC 컨테이너
Spring IoC 컨테이너는 하나 이상의 Bean을 관리하며, 이들은 컨테이너에 공급하는 구성 메타데이터로 생성된다.  

## BeanDefinition
Bean 정의는 `BeanDefinition` 객체로 표현되며, 주요 메타데이터 항목은 다음과 같다.
- **패키지 적절한 클래스 이름**: Bean의 실제 구현 클래스.
- **Bean 행동 구성 요소**: Bean의 동작 방식(범위, 생명주기 콜백 등).
- **종속성**: Bean이 필요로 하는 다른 Bean에 대한 참조.
- **기타 설정**: 예를 들어, 연결 풀의 크기 제한.

### 예시
```xml
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource">
    <property name="driverClassName" value="com.mysql.cj.jdbc.Driver"/>
    <property name="url" value="jdbc:mysql://localhost:3306/mydb"/>
    <property name="username" value="user"/>
    <property name="password" value="password"/>
</bean>
```

<br/>
* * *
<br/>

## Bean 정의의 속성
Bean 정의는 여러 속성으로 구성되며, 각 속성의 설명은 다음과 같다.

| 속성                     | 설명                      |
|------------------------|-------------------------|
| Class                  | Bean의 클래스           |
| Name                   | Bean의 이름             |
| Scope                  | Bean의 범위             |
| Constructor arguments   | 생성자 인수             |
| Properties             | 속성 주입               |
| Autowiring mode        | 자동 주입 모드          |
| Lazy initialization mode| 지연 초기화 모드        |
| Initialization method   | 초기화 메서드           |
| Destruction method      | 파괴 메서드             |

## 기존 객체 등록
`ApplicationContext`는 외부에서 생성된 기존 객체를 등록할 수 있다. `getBeanFactory()` 메서드를 통해 `DefaultListableBeanFactory`에 접근하여 `registerSingleton(..)` 및 `registerBeanDefinition(..)` 메서드를 사용해 등록할 수 있다.

### 예시
```java
ApplicationContext context = new AnnotationConfigApplicationContext(MyConfig.class);
MyService myService = new MyService();
context.getBeanFactory().registerSingleton("myService", myService);
```

<br/>
* * *
<br/>

## Bean 재정의
- **Bean 재정의 정의**: 이미 할당된 식별자를 사용하여 Bean을 등록할 때 발생.
- **재정의 비활성화**: `allowBeanDefinitionOverriding` 플래그를 `false`로 설정하여 Bean 재정의를 비활성화할 수 있다.

### 예시
```java
@Bean
public static void setAllowBeanDefinitionOverriding(ApplicationContext context) {
    ((ConfigurableApplicationContext) context).getBeanFactory().setAllowBeanDefinitionOverriding(false);
}
```

<br/>
* * *
<br/>

## Bean 이름 짓기
- 모든 Bean은 하나 이상의 식별자를 가지며, 이 식별자는 컨테이너 내에서 고유해야 한다.
- XML 기반 구성에서 `id` 속성과 `name` 속성을 사용하여 Bean의 식별자를 지정할 수 있다.

### 예시
```xml
<bean id="userService" class="com.example.UserService"/>
<bean name="accountService" class="com.example.AccountService"/>
```

<br/>
* * *
<br/>

## 특정 Bean의 이름을 다른 이름으로 참조하기
빈 정의 내에서 ID 속성으로 지정된 하나의 이름과 이름 속성에서 지정된 다른 이름의 조합으로 빈에 대해 두 개 이상의 이름을 제공할 수 있다. 이는 대규모 시스템에서 유용하다.

### 예시
```xml
<alias name="userService" alias="userSvc"/>
```

<br/>
* * *
<br/>

## Bean 인스턴스화
Bean 정의는 하나 이상의 객체를 생성하기 위한 레시피로 기능하다. XML 기반 구성에서 `<bean/>` 요소의 `class` 속성으로 객체의 유형을 지정한다.

### 예시
```xml
<bean id="exampleBean" class="com.example.ExampleBean"/>
```

<br/>
* * *
<br/>

## 생성자를 통한 인스턴스화
생성자 접근 방식으로 Bean을 생성할 경우, 모든 일반 클래스를 Spring에서 사용할 수 있으며, 기본 생성자가 필요할 수 있다.

### 예시
```xml
<bean id="clientService" class="com.example.ClientService"/>
```

<br/>
* * *
<br/>

## 스태틱 팩토리 방식으로 인스턴스화
정적 공장 메서드를 사용하여 Bean을 정의할 때, `class` 속성에는 정적 공장 메서드를 포함하는 클래스를 지정하고, `factory-method` 속성에는 공장 메서드의 이름을 지정한다.

### 예시
```xml
<bean id="clientService" class="com.example.ClientService" factory-method="createInstance"/>
```

<br/>
* * *
<br/>

## 인스턴스 팩토리 방법을 사용한 인스턴스화
인스턴스 팩토리 메서드를 사용하여 Bean을 생성할 때, 기존 Bean의 비정적 메서드를 호출하여 새로운 Bean을 생성한다.

### 예시
```xml
<bean id="serviceLocator" class="com.example.DefaultServiceLocator"/>
<bean id="clientService" factory-bean="serviceLocator" factory-method="createClientServiceInstance"/>
```

<br/>
* * *
<br/>

## Bean의 런타임 유형 결정
특정 Bean의 런타임 유형은 결정하기가 쉽지 않다. `BeanFactory.getType` 메서드를 호출하여 실제 런타임 유형을 확인하는 것이 권장된다.

### 예시
```java
Class<?> beanType = beanFactory.getType("clientService");
```

<br/>
<br/>
<br/>
* * *
<br/>
<br/>
<br/>

> **Reference**  
<a href="https://docs.spring.io/spring-framework/reference/core/beans/definition.html" style="text-decoration: none; color: #757575;">Bean Overview</a>