---
title: Day02-03 | CodingTest JAVA
date: 2024-09-15 17:03:00 +09:00
categories: [코딩테스트(Coding Test), JAVA]
tags:
  [
    코딩테스트,
    CodingTest,
    Programmers,
    ArrayList, 
    repeat(), 
    toCharArray(), 
    isUpperCase(), 
    toLowerCase(), 
    toUpperCase(), 
    이스케이프 시퀀스
  ]
---

<br/>
<br/>

## 문자열 섞기

```java
class Solution {
    public String solution(String str1, String str2) {
        StringBuilder sb = new StringBuilder();
        
        char[] chars1 = str1.toCharArray();
        char[] chars2 = str2.toCharArray();
    
        for (int i = 0; i < chars1.length; i++) {
            sb.append(chars1[i]).append(chars2[i]);
        }
    
        return sb.toString();
    }
}
```

### 설명
두 개의 문자열 `str1`과 `str2`를 입력받아, 각 문자열의 문자를 번갈아 결합하여 새로운 문자열을 생성  

### 작동 원리
1. **문자열 변환**: `toCharArray()` 메서드를 사용하여 문자열을 문자 배열로 변환
2. **StringBuilder**: `StringBuilder` 객체를 생성하여 효율적인 문자열 결합
3. **반복문**: 두 문자 배열의 각 문자에 대해 반복하면서 각 문자를 `StringBuilder`에 추가
4. **결과 반환**: 최종적으로 `toString()` 메서드를 호출하여 `StringBuilder`의 내용을 문자열로 변환하고 반환

### 장점
- **효율성**: `StringBuilder`를 사용함으로써 문자열 결합 시 성능 향상
- **가독성**: 코드가 간결하고 이해하기 쉬움  

<br/>
* * *
<br/>

## 문자 리스트를 문자열로 변환하기

```java
import java.util.stream.Collectors;

class Solution {
    public String solution(String[] arr) {
        return java.util.Arrays.stream(arr)
                               .collect(Collectors.joining());
    }
}
```

### 설명
문자열 배열 `arr`을 입력받아, 배열의 모든 요소를 하나의 문자열로 결합하여 반환  

### 작동 원리
1. **Stream 변환**: `java.util.Arrays.stream(arr)`를 사용하여 배열을 스트림으로 변환
2. **Collecting**: `Collectors.joining()` 메서드를 사용하여 스트림의 요소를 하나의 문자열로 결합
3. **결과 반환**: 최종적으로 결합된 문자열을 반환  

### 장점
- **간결함**: 코드가 매우 간결하고 읽기 쉬우며, Java 8 이상에서 추가된 스트림 API 활용
- **유연성**: 다른 구분 기호를 사용하여 문자열을 결합할 수도 있음  

<br/>
* * *
<br/>

## 문자열 곱하기

```java
class Solution {
    public String solution(String my_string, int k) {
        return my_string.repeat(k);
    }
}
```

### 설명
주어진 문자열 `my_string`을 `k`번 반복하여 새로운 문자열을 생성  

### 작동 원리
1. **문자열 반복**: `String.repeat(int count)` 메서드를 사용하여 문자열을 지정한 횟수만큼 반복.
2. **결과 반환**: 반복된 문자열 반환  

### 장점
- **효율성**: 간단한 메서드 호출로 문자열을 반복할 수 있어 코드가 매우 간결 함
- **가독성**: 코드가 직관적이며, 한 줄로 명확한 작업   

### 지원 버전
- **Java 11 이상**에서 사용 가능  

<br/>
* * *
<br/>

## 더 크게 합치기

```java
class Solution {
    public int solution(int a, int b) {
        // b의 자릿수 계산
        int bDigits = String.valueOf(b).length();
        
        // a ⊕ b 계산
        int abValue = a * (int) Math.pow(10, bDigits) + b;
        
        // b ⊕ a 계산
        int baValue = b * (int) Math.pow(10, String.valueOf(a).length()) + a;
        
        // 더 큰 값을 반환, 같으면 abValue를 반환
        return Math.max(abValue, baValue);
    }
}
```

### 설명
두 개의 정수 `a`와 `b`를 입력받아, 두 숫자를 조합하여 만든 두 가지 경우 중 더 큰 값을 반환  

### 작동 원리
1. **자릿수 계산**: `String.valueOf(b).length()`를 사용하여 `b`의 자릿수 계산
2. **조합 계산**: 
   - `abValue`는 `a`와 `b`를 결합한 값입니다.
   - `baValue`는 `b`와 `a`를 결합한 값입니다.
3. **최대값 반환**: `Math.max()` 메서드를 사용하여 두 값을 비교하고 더 큰 값을 반환  

### 장점
- **효율성**: 문자열 변환 없이 수학적 계산으로 조합
- **직관성**: 두 숫자의 조합을 명확하게 계산하여 가독성이 좋음  

<br/>
* * *
<br/>

## 두 수의 연산값 비교하기

```java
class Solution {
    public int solution(int a, int b) {
        // b의 자릿수 계산
        int bDigits = String.valueOf(b).length();
        
        // a ⊕ b 계산
        int plusCase = a * (int) Math.pow(10, bDigits) + b;
        
        // 2 * a * b 계산
        int multiplyCase = 2 * a * b;
        
        // 더 큰 값을 반환, 같으면 plusCase를 반환
        return (plusCase >= multiplyCase) ? plusCase : multiplyCase;
    }
}
```

### 설명
두 정수 `a`와 `b`를 입력받아, 두 연산의 결과를 비교하여 더 큰 값을 반환  

### 작동 원리
1. **자릿수 계산**: `String.valueOf(b).length()`를 사용하여 `b`의 자릿수를 계산
2. **조합 계산**: `plusCase`는 `a`와 `b`를 조합한 값
3. **곱셈 계산**: `multiplyCase`는 `2 * a * b`를 계산
4. **최대값 반환**: 조건문을 사용하여 두 값을 비교하고 더 큰 값을 반환  
 
### 장점
- **효율성**: 수학적 계산으로 문자열 변환 없이 연산
- **가독성**: 조건문을 사용하여 명확하게 비교하고 결과를 반환  

<br/>
* * *
<br/>

2, 3일차 한 번에 포스팅! 아 자바 재밌는데 어려워🥲

