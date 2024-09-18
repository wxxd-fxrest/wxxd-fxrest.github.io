---
title: Day06 | CodingTest JAVA
date: 2024-09-18 17:03:00 +09:00
categories: [코딩테스트(Coding Test), JAVA]
tags:
  [
    코딩테스트,
    CodingTest,
    Programmers,
    마지막 두 원소,
    수 조작하기 1,
    수 조작하기 2,
    수열과 구간 쿼리 3,
    수열과 구간 쿼리 2,
   ]
---

<br/>
<br/>

## 마지막 두 원소
> **문제**  
정수 리스트 num_list가 주어질 때, 마지막 원소가 그전 원소보다 크면 마지막 원소에서 그전 원소를 뺀 값을 마지막 원소가 그전 원소보다 크지 않다면 마지막 원소를 두 배한 값을 추가하여 return하도록 solution 함수를 완성해주세요. 

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

class Solution {
    public List<Integer> solution(int[] num_list) {
        int last = num_list[num_list.length - 1]; // 마지막 원소
        int secondLast = num_list[num_list.length - 2]; // 그 전 원소

        // 기존 배열을 리스트로 변환
        List<Integer> result = Arrays.stream(num_list)
                                      .boxed() // int를 Integer로 변환
                                      .collect(Collectors.toList());

        // 조건에 따라 값 추가
        if (last > secondLast) {
            result.add(last - secondLast); // 마지막 원소에서 그 전 원소를 뺀 값
        } else {
            result.add(last * 2); // 마지막 원소를 두 배한 값
        }

        return result; // 수정된 리스트 반환
    }
}
```
### 풀이
- 주어진 정수 리스트 `num_list`에서 마지막 원소와 그 전 원소를 비교 
- 마지막 원소가 더 크면 두 값을 뺀 결과를 리스트에 추가, 그렇지 않으면 마지막 원소를 두 배하여 추가 
- 이 과정은 리스트의 원본 순서를 유지하며, 최종적으로 수정된 리스트를 반환  

<br/>
* * *
<br/>

## 수 조작하기 1
> **문제**  
정수 `n`과 문자열 `control`이 주어집니다. `control`은 "w", "a", "s", "d"의 4개의 문자로 이루어져 있으며, `control`의 앞에서부터 순서대로 문자에 따라 `n`의 값을 바꿉니다.
- "w" : `n`이 1 커집니다.
- "s" : `n`이 1 작아집니다.
- "d" : `n`이 10 커집니다.
- "a" : `n`이 10 작아집니다.
위 규칙에 따라 `n`을 바꿨을 때 가장 마지막에 나오는 `n`의 값을 return 하는 solution 함수를 완성해 주세요.  

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public int solution(int n, String control) {
        Map<Character, Integer> changeMap = new HashMap<>();
        changeMap.put('w', 1);
        changeMap.put('s', -1);
        changeMap.put('d', 10);
        changeMap.put('a', -10);
        
        for (char command : control.toCharArray()) {
            n += changeMap.getOrDefault(command, 0); // 기본값 0으로 설정
        }

        return n; // 최종 결과 반환
    }
}
```
### 풀이
- 정수 `n`과 문자열 `control`이 주어질 때, `control`의 각 문자에 따라 `n`의 값을 조정 
- "w"는 `n`을 1 증가, "s"는 1 감소, "d"는 10 증가, "a"는 10 감소 
- 모든 문자를 처리한 후, 최종적으로 변경된 `n`의 값을 반환    

<br/>
* * *
<br/>

## 수 조작하기 2
> **문제**  
정수 배열 `numLog`가 주어집니다. 처음에 `numLog[0]`에서 부터 시작해 "w", "a", "s", "d"로 이루어진 문자열을 입력으로 받아 순서대로 다음과 같은 조작을 했다고 합시다.  
- "w" : 수에 1을 더한다.
- "s" : 수에 1을 뺀다.
- "d" : 수에 10을 더한다.
- "a" : 수에 10을 뺀다.  
그리고 매번 조작을 할 때마다 결괏값을 기록한 정수 배열이 `numLog`입니다. 즉, `numLog[i]`는 `numLog[0]`로부터 총 `i`번의 조작을 가한 결과가 저장되어 있습니다.
주어진 정수 배열 `numLog`에 대해 조작을 위해 입력받은 문자열을 return 하는 solution 함수를 완성해 주세요.

```java
import java.util.HashMap;
import java.util.Map;

class Solution {
    public String solution(int[] numLog) {
        StringBuilder result = new StringBuilder();
        Map<Integer, Character> changeMap = new HashMap<>();
        changeMap.put(1, 'w');
        changeMap.put(-1, 's');
        changeMap.put(10, 'd');
        changeMap.put(-10, 'a');

        for (int i = 1; i < numLog.length; i++) {
            int difference = numLog[i] - numLog[i - 1];
            result.append(changeMap.get(difference)); // 변화량에 따라 문자 추가
        }

        return result.toString(); // 최종 결과 반환
    }
}
```
### 풀이
- 주어진 정수 배열 `numLog`와 조작 문자열을 기반으로, 초기 값 `numLog[0]`에서 시작하여 각 문자에 따름 
- "w", "a", "s", "d"에 따라 값을 변경한 후, 각 조작 결과를 배열에 저장 
- 최종적으로, 이 조작을 통해 생성된 문자열을 반환  

<br/>
* * *
<br/>

## 수열과 구간 쿼리 3
> **문제**  
정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[i, j]` 꼴입니다.
각 `query`마다 순서대로 `arr[i]`의 값과 `arr[j]`의 값을 서로 바꿉니다.
위 규칙에 따라 `queries`를 처리한 이후의 `arr`를 return 하는 solution 함수를 완성해 주세요. 

```java
class Solution {
    public int[] solution(int[] arr, int[][] queries) {
        for (int[] query : queries) {
            int i = query[0]; // i 값
            int j = query[1]; // j 값

            // arr[i]와 arr[j]의 값 교환
            int temp = arr[i];
            arr[i] = arr[j];
            arr[j] = temp;
        }
        return arr; // 최종 결과 반환
    }
}
```
### 풀이
- 정수 배열 `arr`와 2차원 배열 `queries`가 주어질 때, 각 쿼리에 대해 `arr`의 두 원소의 인덱스를 교환 
- 이 과정은 주어진 쿼리 순서에 따라 순차적으로 진행되며, 모든 쿼리 처리가 완료된 후의 배열 `arr`을 반환

<br/>
* * *
<br/>

## 수열과 구간 쿼리 2
> **문제**  
정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[s, e, k]` 꼴입니다.
각 `query`마다 순서대로 `s` ≤ `i` ≤ `e`인 모든 `i`에 대해 `k`보다 크면서 가장 작은 `arr[i]`를 찾습니다.
각 쿼리의 순서에 맞게 답을 저장한 배열을 반환하는 solution 함수를 완성해 주세요.
단, 특정 쿼리의 답이 존재하지 않으면 -1을 저장합니다.  

```java
class Solution {
    public int[] solution(int[] arr, int[][] queries) {
        int[] result = new int[queries.length];

        for (int q = 0; q < queries.length; q++) {
            int s = queries[q][0];
            int e = queries[q][1];
            int k = queries[q][2];
            int min = Integer.MAX_VALUE; // k보다 큰 값 중 최소값 초기화
            boolean found = false;

            for (int i = s; i <= e; i++) {
                if (arr[i] > k) {
                    found = true;
                    if (arr[i] < min) {
                        min = arr[i];
                    }
                }
            }

            result[q] = found ? min : -1; // 결과 저장
        }

        return result; // 최종 결과 반환
    }
}
```
### 풀이
- 정수 배열 `arr`와 2차원 배열 `queries`가 주어질 때, 
  각 쿼리에 대해 주어진 인덱스 범위 내에서 `k보`다 큰 원소 중 가장 작은 값을 찾음  
- 만약 해당 조건을 만족하는 원소가 없다면 -1을 반환  
- 모든 쿼리에 대한 결과를 배열에 저장 후 반환  