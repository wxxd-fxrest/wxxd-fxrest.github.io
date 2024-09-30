---
title: Dependency Injection - Spring 공식문서 뿌시기 
date: 2024-09-30 20:50:00 +09:00
categories: [Java&Spring, Spring]
tags:
  [
    Spring,
    Java,
    Spring 공식문서,
    Dependency Injection,
    의존성 주입,
  ]
---

<br/>
<br/>

# 스프링의 의존성 주입
의존성 주입(Dependency Injection, DI)은 객체가 의존성을 정의하는 과정이다. 이는 생성자 인수, 팩토리 메서드에 대한 인수, 또는 팩토리 메서드에서 반환된 후 객체 인스턴스에 설정되는 속성을 포함한다. 빈이 생성될 때 컨테이너는 의존성을 주입한다.  
이 과정은 빈이 스스로 제어되는 것의 역순이다. 클래스의 직접 구성이나 서비스 로케이터 패턴을 사용해 의존성을 인스턴스화하거나 위치를 스스로 제어하는 것이다.  
DI 원칙을 사용하면 코드가 깨끗해지고, 객체가 의존성을 가지고 공급될 때 분리되는 것이 더 효과적이다. 객체는 의존성을 찾지 않으며, 의존성과 위치, 또는 클래스를 알지 못한다. 이로 인해 특히 인터페이스나 추상 기반 클래스에 의존성이 있는 경우, stub이나 mock 구현을 사용한 유닛 테스트가 더 쉬워진다.  

<br/>

## 생성자 기반 의존성 주입
생성자 기반 DI는 컨테이너가 각각의 의존성을 가진 인수를 사용해 생성자를 호출할 때 이루어진다. 빈을 구성하는 것은 특정 인수와 함께 정적 팩토리 메서드를 호출하는 것과 유사하다.   

다음 예제는 오직 생성자 주입으로만 의존성을 주입할 수 있는 클래스를 보여준다.  
```java
public class SimpleMovieLister {
	private final MovieFinder movieFinder;

	public SimpleMovieLister(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// 비즈니스 로직은 생략...
}
```  
이 클래스는 컨테이너의 특정 인터페이스, 기본 클래스 또는 주석에 의존하지 않는 POJO이다.  

<br/>

### 생성자 인수 결정
생성자 인수 결정은 사용하는 인수의 타입에 의해 매칭된다. 빈 정의의 생성자 인수에 잠재적 모호성이 없을 경우, 생성자 인수는 빈 인스턴스화 시 해당 인수가 적절한 생성자에게 제공되는 순서에 따라 제공된다.  
```java
public class ThingOne {
	public ThingOne(ThingTwo thingTwo, ThingThree thingThree) {
		// ...
	}
}
```  
`ThingTwo`와 `ThingThree` 클래스가 상속과 관련이 없다면, 잠재적 모호성은 없다. 따라서 다음 구성은 잘 작동한다.  

<br/>

```xml
<beans>
	<bean id="beanOne" class="x.y.ThingOne">
		<constructor-arg ref="beanTwo"/>
		<constructor-arg ref="beanThree"/>
	</bean>
	<bean id="beanTwo" class="x.y.ThingTwo"/>
	<bean id="beanThree" class="x.y.ThingThree"/>
</beans>
```  
다른 빈이 참조되었을 때, 타입이 알려져 매칭할 수 있다.  

<br/>

### 생성자 인수 타입 매칭
간단한 타입을 사용했을 때, 스프링은 그 값의 타입을 결정할 수 없다. 다음 클래스를 고려하자.  
```java
public class ExampleBean {
	private final int years;
	private final String ultimateAnswer;

	public ExampleBean(int years, String ultimateAnswer) {
		this.years = years;
		this.ultimateAnswer = ultimateAnswer;
	}
}
```  
이 경우, 유형 속성을 통해 생성자 인수의 유형을 명시적으로 지정할 수 있다.

```xml
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg type="int" value="7500000"/>
	<constructor-arg type="java.lang.String" value="42"/>
</bean>
```  

<br/>

### 생성자 인수 인덱스
인덱스 속성을 사용하여 생성자 인수의 인덱스를 명시적으로 지정할 수 있다.  
```xml
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg index="0" value="7500000"/>
	<constructor-arg index="1" value="42"/>
</bean>
```  

<br/>

### 생성자 인수 이름
값 명확성 해제를 위해 생성자 매개변수 이름을 사용할 수 있다.  
```xml
<bean id="exampleBean" class="examples.ExampleBean">
	<constructor-arg name="years" value="7500000"/>
	<constructor-arg name="ultimateAnswer" value="42"/>
</bean>
```  
스프링이 생성자로부터 파라미터 이름을 찾을 수 있도록 매개변수 플래그를 활성화한 상태로 코드를 컴파일해야 한다. 만약 매개변수 플래그를 사용하고 싶지 않거나 할 수 없다면, `@ConstructorProperties` JDK 어노테이션을 사용하여 생성자 인수의 이름을 명시적으로 지정할 수 있다.  

<br/>
* * *
<br/>

## Setter 기반 의존성 주입
Setter 기반 DI는 컨테이너가 빈을 인스턴스화한 후, 빈의 setter 메서드를 호출함으로써 이루어진다.  
다음 예제는 순수 세터 주입을 사용해야만 의존성 주입이 가능한 클래스를 보여준다.  
```java
public class SimpleMovieLister {
	private MovieFinder movieFinder;

	public void setMovieFinder(MovieFinder movieFinder) {
		this.movieFinder = movieFinder;
	}

	// 비즈니스 로직은 생략...
}
```  
`ApplicationContext`는 생성자 기반과 Setter 기반 DI를 지원한다. Setter 기반 DI는 생성자 접근 방식으로 이미 주입된 일부 의존성 이후에 지원된다.  

<br/>
* * *
<br/>

## 의존성 해소 과정
컨테이너는 빈 의존성 해소를 다음과 같이 수행한다.  
1. `ApplicationContext`가 생성되고, 모든 빈을 설명하는 구성 메타데이터로 초기화된다. 구성 메타데이터는 XML, 자바 코드 또는 어노테이션으로 지정할 수 있다.
2. 각 빈에 대해 의존성은 속성, 생성자 인수 또는 정적 팩토리 메서드에 대한 인수 형태로 표현된다. 이러한 의존성은 빈이 실제로 생성될 때 빈에 제공된다.
3. 각 속성이나 생성자 인수는 설정할 값의 실제 정의이거나, 컨테이너의 다른 빈에 대한 참조이다.
4. 값인 각 속성이나 생성자 인수는 지정된 형식에서 해당 속성이나 생성자 인수의 실제 타입으로 변환된다. 기본적으로 스프링은 문자열 형식으로 제공된 값을 `int`, `long`, `String`, `boolean` 등과 같은 모든 기본 타입으로 변환할 수 있다.  
스프링 컨테이너는 컨테이너가 생성될 때 각 빈의 구성을 유효성 검사하지만, 빈의 속성은 빈이 실제로 생성될 때까지 설정되지 않는다. 싱글톤 범위의 빈은 사전 인스턴스화로 설정되면 컨테이너가 생성될 때 생성된다.  

<br/>
* * *
<br/>

## 결론
스프링은 빈이 실제로 생성될 때 속성과 의존성을 가능한 한 늦게 설정하고 해결한다. 이는 올바르게 로드된 스프링 컨테이너가 나중에 객체를 요청할 때, 해당 객체나 그 의존성을 생성하는 데 문제가 있을 경우 예외를 발생시킬 수 있음을 의미한다. 이러한 구성 문제의 가시성이 지연될 가능성이 있기 때문에, `ApplicationContext` 구현은 기본적으로 싱글톤 빈을 사전 인스턴스화한다.  
생성자 기반 DI와 Setter 기반 DI를 혼합할 수 있기 때문에, 필수 의존성에는 생성자를 사용하고 선택적 의존성에는 Setter 메서드를 사용하는 것이 좋은 규칙이다. 스프링 팀은 일반적으로 생성자 주입을 권장하는데, 이는 애플리케이션 구성 요소를 불변 객체로 구현할 수 있게 하고, 필수 의존성이 null이 아님을 보장하기 때문이다. 

<br/>
<br/>
<br/>
* * *
<br/>
<br/>
<br/>

> **Reference**  
<a href="https://docs.spring.io/spring-framework/reference/core/beans/dependencies/factory-collaborators.html" style="text-decoration: none; color: #757575;">Dependency Injection</a>