---
title: Day04-05 | CodingTest JAVA
date: 2024-09-17 19:03:00 +09:00
categories: [코딩테스트(Coding Test), JAVA]
tags:
  [
    코딩테스트,
    CodingTest,
    Programmers,
    n의 배수,
    공배수,
    홀짝에 따라 다른 값 반환하기,
    조건 문자열,
    flag에 따라 다른 값 반환하기,
    코드 처리하기,
    등차수열의 특정한 항만 더하기,
    주사위 게임 2,
    원소들의 곱과 합,
    이어 붙인 수
  ]
---

<br/>
<br/>

# Day04
## n의 배수
> 문제  
정수 num과 n이 매개 변수로 주어질 때, num이 n의 배수이면 1을 return n의 배수가 아니라면 0을 return하도록 solution 함수를 완성해주세요.  

```java
class Solution {
    public int solution(int num, int n) {
        return num % n == 0 ? 1 : 0;
    }
}
```
### 설명
- `num % n`은 `num`을 `n`으로 나눈 나머지를 계산
- 나머지가 0이면 `num`은 `n`의 배수이므로 `1`을 반환하고, 그렇지 않으면 `0`을 반환

<br/>
* * *
<br/>

## 공배수
> 문제  
정수 number와 n, m이 주어집니다. number가 n의 배수이면서 m의 배수이면 1을 아니라면 0을 return하도록 solution 함수를 완성해주세요.  

```java
class Solution {
    public int solution(int number, int n, int m) {
        return (number % n == 0 && number % m == 0) ? 1 : 0;
    }
}
```
### 설명
- `number % n == 0`와 `number % m == 0`을 통해 `number`가 각각 `n`과 `m`의 배수인지 확인
- 두 조건이 모두 참이면 `1`을 반환하고, 그렇지 않으면 `0`을 반환
- 논리 연산자 `&&`를 사용하여 두 조건을 동시에 확인

<br/>
* * *
<br/>

## 홀짝에 따라 다른 값 반환하기
> 문제  
양의 정수 n이 매개변수로 주어질 때, n이 홀수라면 n 이하의 홀수인 모든 양의 정수의 합을 return 하고 n이 짝수라면 n 이하의 짝수인 모든 양의 정수의 제곱의 합을 return 하는 solution 함수를 작성해 주세요.  
 
```java
class Solution {
    public int solution(int n) {
        int answer = 0;

        if (n % 2 != 0) { // n이 홀수인 경우
            for (int i = 1; i <= n; i += 2) { // 1부터 n까지 홀수만 더함
                answer += i;
            }
        } else { // n이 짝수인 경우
            for (int i = 2; i <= n; i += 2) { // 2부터 n까지 짝수의 제곱을 더함
                answer += i * i;
            }
        }

        return answer;
    }
}
```
### 설명
- `n`이 홀수일 경우, 1부터 `n`까지 홀수만을 더함
- `n`이 짝수일 경우, 2부터 `n`까지 짝수의 제곱을 더함
- 각각의 경우에 따라 반복문을 사용하여 조건에 맞는 값을 계산

<br/>
* * *
<br/>

## 조건 문자열
> 문제  
문자열에 따라 다음과 같이 두 수의 크기를 비교하려고 합니다.
- 두 수가 `n`과 `m`이라면
    - ">", "=" : `n` >= `m`
    - "<", "=" : `n` <= `m`
    - ">", "!" : `n` > `m`
    - "<", "!" : `n` < `m`
두 문자열 `ineq`와 `eq`가 주어집니다. `ineq`는 "<"와 ">"중 하나고, `eq`는 "="와 "!"중 하나입니다. 그리고 두 정수 `n`과 `m`이 주어질 때, `n`과 `m`이 `ineq`와 `eq`의 조건에 맞으면 1을 아니면 0을 return하도록 solution 함수를 완성해주세요.  
 
```java
class Solution {
    public int solution(String ineq, String eq, int n, int m) {
        boolean comparison = false;

        // ineq와 eq에 따라 비교 결과를 결정
        if (ineq.equals("<")) {
            comparison = eq.equals("=") ? n <= m : n < m;
        } else if (ineq.equals(">")) {
            comparison = eq.equals("=") ? n >= m : n > m;
        }

        return comparison ? 1 : 0; // 비교 결과에 따라 1 또는 0 반환
    }
}
```
### 설명
- `ineq`와 `eq`에 따라 `n`과 `m`의 비교 결과를 결정
- `equals` 메서드를 사용하여 문자열 비교
- 비교 결과에 따라 `1` 또는 `0`을 반환

<br/>
* * *
<br/>

## flag에 따라 다른 값 반환하기
> 문제  
두 정수 a, b와 boolean 변수 flag가 매개변수로 주어질 때, flag가 true면 a + b를 false면 a - b를 return 하는 solution 함수를 작성해 주세요.  
 
```java
class Solution {
    public int solution(int a, int b, boolean flag) {
        return flag ? (a + b) : (a - b);
    }
}
```
### 설명
- 삼항 연산자를 사용하여 flag가 true일 경우 `a + b`를, false일 경우 `a - b`를 계산하여 반환

<br/>
* * *
<br/>

# Day04
## 코드 처리하기
> 문제  
문자열 `code`가 주어집니다.
`code`를 앞에서부터 읽으면서 만약 문자가 "1"이면 `mode`를 바꿉니다. `mode`에 따라 `code`를 읽어가면서 문자열 `ret`을 만들어냅니다.
`mode`는 0과 1이 있으며, `idx`를 0 부터 `code의 길이 - 1` 까지 1씩 키워나가면서 `code[idx]`의 값에 따라 다음과 같이 행동합니다.
- `mode`가 0일 때
    - `code[idx]`가 "1"이 아니면 `idx`가 짝수일 때만 `ret`의 맨 뒤에 `code[idx]`를 추가합니다.
    - `code[idx]`가 "1"이면 `mode`를 0에서 1로 바꿉니다.
- `mode`가 1일 때
    - `code[idx]`가 "1"이 아니면 `idx`가 홀수일 때만 `ret`의 맨 뒤에 `code[idx]`를 추가합니다.
    - `code[idx]`가 "1"이면 `mode`를 1에서 0으로 바꿉니다.
문자열 `code`를 통해 만들어진 문자열 `ret`를 return 하는 solution 함수를 완성해 주세요.
단, 시작할 때 `mode`는 0이며, return 하려는 `ret`가 만약 빈 문자열이라면 대신 "EMPTY"를 return 합니다.  
 
```java
public class Solution {
    public String solution(String code) {
        StringBuilder ret = new StringBuilder();
        int mode = 0; // 초기 모드 설정

        for (int idx = 0; idx < code.length(); idx++) {
            char currentChar = code.charAt(idx);

            // 모드 전환
            if (currentChar == '1') {
                mode = 1 - mode; // 모드 전환
            } else {
                // 조건 체크를 위한 메서드 호출
                if (shouldAppend(mode, idx)) {
                    ret.append(currentChar);
                }
            }
        }

        return ret.length() == 0 ? "EMPTY" : ret.toString(); // 빈 문자열일 경우 "EMPTY" 반환
    }

    private boolean shouldAppend(int mode, int idx) {
        // 모드에 따라 문자열 추가 여부 결정
        return (mode == 0 && idx % 2 == 0) || (mode == 1 && idx % 2 == 1);
    }
}
```
### 설명
- mode가 `0`일 때는 짝수 인덱스의 문자만 추가하고, `1`일 때는 홀수 인덱스의 문자만 추가
- mode는 `1`을 만날 때마다 전환
- 최종적으로 ret가 비어 있으면 `EMPTY`를 반환

<br/>
* * *
<br/>

## 등차수열의 특정한 항만 더하기
> 문제  
두 정수 a, d와 길이가 n인 boolean 배열 included가 주어집니다. 첫째항이 a, 공차가 d인 등차수열에서 included[i]가 i + 1항을 의미할 때, 이 등차수열의 1항부터 n항까지 included가 true인 항들만 더한 값을 return 하는 solution 함수를 작성해 주세요.  
 
```java
import java.util.stream.IntStream;

class Solution {
    public int solution(int a, int d, boolean[] included) {
        return IntStream.range(0, included.length)
                        .filter(i -> included[i]) // 포함된 항만 필터링
                        .map(i -> a + i * d) // 항 계산
                        .sum(); // 합산
    }
}
```
### 설명
- `IntStream.range(0, included.length)`를 사용하여 인덱스 생성
- `filter`를 통해 `included`가 `true`인 인덱스만 필터링하고, map을 통해 해당 인덱스에 따라 등차수열의 항 계산
- 최종적으로 `sum`을 통해 합산

<br/>
* * *
<br/>

## 주사위 게임 2
> 문제  
1부터 6까지 숫자가 적힌 주사위가 세 개 있습니다. 세 주사위를 굴렸을 때 나온 숫자를 각각 `a`, `b`, `c`라고 했을 때 얻는 점수는 다음과 같습니다.
- 세 숫자가 모두 다르다면 `a` + `b` + `c` 점을 얻습니다.
- 세 숫자 중 어느 두 숫자는 같고 나머지 다른 숫자는 다르다면 (`a` + `b` + `c`) × (`a` + `b` + `c` )점을 얻습니다.
- 세 숫자가 모두 같다면 (`a` + `b` + `c`) × (`a` + `b` + `c` ) × (`a` + `b` + `c` )점을 얻습니다.
세 정수 `a`, `b`, `c`가 매개변수로 주어질 때, 얻는 점수를 return 하는 solution 함수를 작성해 주세요.  
 
```java
class Solution {
    public int solution(int a, int b, int c) {
        int sum = a + b + c; // a + b + c 계산
        int sumOfSquares = a * a + b * b + c * c; // a^2 + b^2 + c^2 계산
        int sumOfCubes = a * a * a + b * b * b + c * c * c; // a^3 + b^3 + c^3 계산

        // 모두 같은 경우
        if (a == b && b == c) {
            return sum * sumOfSquares * sumOfCubes;
        }
        // 두 개가 같고 하나가 다른 경우
        else if (a == b || b == c || a == c) {
            return sum * sumOfSquares;
        }
        // 모두 다른 경우
        return sum;
    }
}
```
### 설명
- 주사위의 값을 합산하여 `sum`을 계산
- 조건에 따라 점수를 계산하는 방식이 다름
- 같은 숫자가 모두 같을 경우, 두 개가 같을 경우, 모두 다른 경우에 대해 각각 다른 점수를 반환

<br/>
* * *
<br/>

## 원소들의 곱과 합
> 문제  
정수가 담긴 리스트 num_list가 주어질 때, 모든 원소들의 곱이 모든 원소들의 합의 제곱보다 작으면 1을 크면 0을 return하도록 solution 함수를 완성해주세요.  
 
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] num_list) {
        if (num_list.length == 0) return 0; // 배열이 비어있을 경우

        int sum = Arrays.stream(num_list).sum(); // 합계 계산
        int product = Arrays.stream(num_list).reduce(1, (a, b) -> a * b); // 곱 계산

        return (sum * sum > product) ? 1 : 0; // 조건에 따라 1 또는 0 반환
    }
}
```
### 설명
- 빈 배열 체크: `if (num_list.length == 0) return 0;`를 통해 배열이 비어있는 경우 0을 반환
- 합계 계산: `Arrays.stream(num_list).sum();`를 사용하여 배열의 모든 원소의 합을 계산
- 곱 계산: `Arrays.stream(num_list).reduce(1, (a, b) -> a * b);`를 사용하여 배열의 모든 원소의 곱을 계산, reduce 메서드는 초기값 1을 사용하여 배열의 각 요소를 곱함
- 비교 및 반환: `(sum * sum > product) ? 1 : 0;`를 통해 합의 제곱이 곱보다 큰지 비교하여 결과를 반환. 조건이 참이면 1, 거짓이면 0을 반환

<br/>
* * *
<br/>

## 이어 붙인 수
> 문제  
정수가 담긴 리스트 num_list가 주어집니다. num_list의 홀수만 순서대로 이어 붙인 수와 짝수만 순서대로 이어 붙인 수의 합을 return하도록 solution 함수를 완성해주세요.  
 
```java
import java.util.ArrayList;
import java.util.List;

class Solution {
    public int solution(int[] num_list) {
        StringBuilder oddBuilder = new StringBuilder();
        StringBuilder evenBuilder = new StringBuilder();

        // 홀수와 짝수 분리
        for (int num : num_list) {
            if (num % 2 == 0) {
                evenBuilder.append(num); // 짝수인 경우
            } else {
                oddBuilder.append(num); // 홀수인 경우
            }
        }

        // 홀수와 짝수를 정수로 변환하여 합산
        int oddSum = oddBuilder.length() > 0 ? Integer.parseInt(oddBuilder.toString()) : 0;
        int evenSum = evenBuilder.length() > 0 ? Integer.parseInt(evenBuilder.toString()) : 0;

        return oddSum + evenSum; // 두 수의 합 반환
    }
}
```
### 설명
- 문자열 빌더 초기화: StringBuilder 객체를 사용하여 홀수와 짝수를 각각 저장
    - `StringBuilder oddBuilder = new StringBuilder();`
    - `StringBuilder evenBuilder = new StringBuilder();`
- 홀수와 짝수 분리: `for (int num : num_list)`를 사용하여 배열을 순회하며 홀수와 짝수를 분리
    - `if (num % 2 == 0)` 조건을 통해 짝수를 확인하고, 그렇지 않은 경우 홀수로 처리
- 문자열 변환 및 합산:
    - `oddBuilder.length() > 0 ? Integer.parseInt(oddBuilder.toString()) : 0;`를 통해 홀수로 만들어진 문자열이 있을 경우 정수로 변환
    - 짝수도 같은 방식으로 처리
- 결과 반환: 홀수와 짝수의 합을 반환 
    - `return oddSum + evenSum;`

<br/>
* * *
<br/>
