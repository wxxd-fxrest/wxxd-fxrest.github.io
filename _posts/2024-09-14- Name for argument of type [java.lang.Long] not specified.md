---
title: findById()메소드 사용에 대한 트러블 슈팅 - Name for argument of type [java.lang.Long] not specified
date: 2024-09-14 18:50:00 +09:00
categories: [Project, Bubbly-ToDo]
tags:
  [
    SideProject,
    TodoApp,
    트러블 슈팅,
    findById(),
    Spring,
    Spring Boot,
    Java 
  ]
---

<br/>
<br/>

# findById()메소드 사용에 대한 트러블 슈팅

## 문제 설명

Spring Boot 애플리케이션에서 `findById` 메소드를 사용하여 특정 사용자의 정보를 조회하는 과정에서 다음과 같은 오류가 발생했다.

```
java.lang.IllegalArgumentException: Name for argument of type [java.lang.Long] not specified, and parameter name information not available via reflection. Ensure that the compiler uses the '-parameters' flag.
```

이 오류는 Java 컴파일러가 메소드 매개변수의 이름 정보를 제공하지 않기 때문에 발생한 거였다.  

<br/>
* * *
<br/>

### 초기 코드

해결 전 `findById` 메소드는 다음과 같이 작성되어 있었다. 

```java
@GetMapping("/todo/{id}")
public String findById(@PathVariable Long id, Model model) {
    UserDTO userDTO = userService.findById(id);
    model.addAttribute("member", userDTO);
    return "detail";
}
```

<br/>
* * *
<br/>

### 시도한 방법들과 그 이유 및 실패 분석

### 1차 시도: @RequestParam 사용

- **목표**: `@PathVariable` 대신 `@RequestParam`을 사용하여 문제를 해결해보려 함.
- **조치**:
    
```java
@GetMapping("/todo/{id}")
public String findById(@RequestParam Long id, Model model) {
    UserDTO userDTO = userService.findById(id);
    model.addAttribute("member", userDTO);
    return "detail";
}
```
    
- **실패 이유**: `@RequestParam`은 URL 경로의 매개변수를 처리하지 않기 때문에, 경로 변수에서 ID를 가져오는 데 실패했다. 이로 인해 여전히 매개변수 이름 정보가 부족한 상태였다.

<br/>
* * *
<br/>

### 2차 시도: @RequestParam(value = "id") 사용

- **목표**: 매개변수 이름을 명시적으로 지정하여 문제를 해결해보려 함.
- **조치**:
    
```java
@GetMapping("/todo/{id}")
public String findById(@RequestParam(value = "id") Long id, Model model) {
    UserDTO userDTO = userService.findById(id);
    model.addAttribute("member", userDTO);
    return "detail";
}
```
    
- **실패 이유**: 여전히 `@RequestParam`을 사용하고 있었기 때문에 URL 경로에서 ID를 가져오는 데 실패했다. 매개변수 이름을 명시적으로 지정하더라도, 경로 변수는 처리되지 않았다.

<br/>
* * *
<br/>

### 3차 시도: @PathVariable 사용 및 디버깅 추가

- **목표**: 원래의 `@PathVariable` 방식으로 돌아가서 디버깅 정보를 추가.
- **조치**:
    
```java
@GetMapping("/todo/{id}")
public String findById(@PathVariable Long id, Model model) {
    System.out.println("Fetching user with ID: " + id); // 요청된 ID 출력

    UserDTO userDTO = userService.findById(id);

    if (userDTO == null) {
        System.out.println("User not found, redirecting to error page."); // 사용자 없음 출력
        return "error"; // 에러 페이지로 리다이렉트
    }

    model.addAttribute("member", userDTO);
    return "detail"; // 사용자 정보가 있는 detail 페이지로 이동
}
```
    
- **실패 이유**: 이 방법은 `@PathVariable`을 사용했지만, Java 컴파일러가 매개변수 이름 정보를 제공하지 않기 때문에 여전히 오류가 발생했다. 디버깅 정보는 유용했으나, 문제의 근본 원인을 해결하지 못했다.

<br/>
* * *
<br/>

### 4차 시도: Gradle 빌드 클린 및 재실행

- **목표**: 설정이 제대로 적용되었는지 확인하기 위해 클린 빌드 수행.
- **조치**: 다음 명령어를 실행했습니다:
    
```bash
./gradlew clean build
```
    

<br/>
* * *
<br/>

### 5차 시도: Java 버전 확인

- **목표**: Java 버전이 8 이상인지 확인하고, Toolchain 설정 확인.
- **조치**: Gradle Toolchain을 사용하여 Java 17을 명시적으로 설정했습니다:
    
```groovy
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(17)
    }
}
```
    

<br/>
* * *
<br/>

### 6차 시도: VS Code 설정 확인

- **목표**: VS Code에서 Java 컴파일러가 `parameters` 플래그를 사용하도록 설정하기.
- **조치**: `settings.json` 파일에서 잘못된 `"java.compile.settings"` 항목을 제거하고, 올바른 설정을 추가했다.
    
```json
{
    "java.home": "C:\\\\Program Files\\\\Java\\\\jdk-17",
    "java.configuration.runtimes": [
        {
            "name": "JavaSE-17",
            "path": "C:\\\\Program Files\\\\Java\\\\jdk-17"
        }
    ]
}
```

<br/>
* * *
<br/>

### <span style="color: #0550ae; font-weight: bold">최종 성공 코드</span>

### 추가 시도: 코드 수정 및 Gradle 및 VS Code 설정 수정

- **목표**: `parameters` 플래그가 설정되어 있는지 확인하기.
- **조치**: `build.gradle` 파일에서 다음과 같이 설정했다.
    
    ```groovy
    tasks.withType(JavaCompile) {
        options.compilerArgs += ['-parameters']
    }
    ```
    

최종적으로 다음과 같이 코드를 수정하여 오류를 해결했다.

```java
@GetMapping("/todo/{id}")
public String findById(@PathVariable(name = "id") Long id, Model model) {
    System.out.println("Fetching user with ID: " + id); // 요청된 ID 출력

    UserDTO userDTO = userService.findById(id);

    if (userDTO == null) {
        System.out.println("User not found, redirecting to error page."); // 사용자 없음 출력
        return "error"; // 에러 페이지로 리다이렉트
    }

    model.addAttribute("member", userDTO);
    return "detail"; // 사용자 정보가 있는 detail 페이지로 이동
}
```

### 성공 이유

- **매개변수 이름 명시**: `@PathVariable(name = "id")`을 명시적으로 지정하여 Java 컴파일러가 매개변수 이름 정보를 사용할 수 있게 했다. 이는 오류 메시지에서 요구했던 사항을 해결할 수 있었다.
- **디버깅 출력 추가**: 요청된 ID를 출력하는 로그를 추가하여 전체 흐름을 확인하고, 사용자 정보가 없을 경우의 처리도 명확하게 했다. 이러한 추가적인 디버깅 정보는 문제 해결 과정에서 도움이 됐다.  

<br/>
<br/>
<br/>
* * *
<br/>
<br/>
<br/>

> **Reference**  
<a href="https://yeonyeon.tistory.com/184" style="text-decoration: none; color: #757575;">[Spring] NestedServletException - Name for argument type [java.lang.Long] not available 에러</a>