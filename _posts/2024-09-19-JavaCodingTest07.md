---
title: Day07 | CodingTest JAVA
date: 2024-09-19 16:40:00 +09:00
categories: [코딩테스트(Coding Test), JAVA]
tags:
  [
    코딩테스트,
    CodingTest,
    Programmers,
    수열과 구간 쿼리 4,
    배열 만들기 2,
    카운트 업,
    콜라츠 수열 만들기,
    배열 만들기 4,
   ]
---

<br/>
<br/>

## 수열과 구간 쿼리 4
> **문제**  
정수 배열 `arr`와 2차원 정수 배열 `queries`이 주어집니다. `queries`의 원소는 각각 하나의 `query`를 나타내며, `[s, e, k]` 꼴입니다.
각 `query`마다 순서대로 `s` ≤ `i` ≤ `e`인 모든 `i`에 대해 `i`가 `k`의 배수이면 `arr[i]`에 1을 더합니다.
위 규칙에 따라 `queries`를 처리한 이후의 `arr`를 return 하는 solution 함수를 완성해 주세요.  

> **문제 분석**
1. **입력**:
   - 정수 배열 `arr`: 수정해야 할 배열
   - 2차원 정수 배열 `queries`: 각 쿼리는 `[s, e, k]` 형태로, `s`부터 `e`까지의 인덱스 중 `k`의 배수 인덱스 찾기  
2. **출력**:
   - 수정된 `arr` 배열 반환  
3. **작업**:
   - 각 쿼리에 대해:
     - `k`가 0일 경우 쿼리를 무시(0으로 나누는 것은 정의되지 않으므로)
     - `s`부터 `e`까지의 모든 인덱스를 순회하면서 인덱스 `i`가 `k`의 배수인지 확인
     - 배수라면 `arr[i]`의 값을 1 증가  
  
```java
public class Solution {
    public int[] solution(int[] arr, int[][] queries) {
        // 각 쿼리를 처리합니다.
        for (int[] query : queries) {
            int s = query[0]; // 시작 인덱스
            int e = query[1]; // 종료 인덱스
            int k = query[2]; // 배수
            
            if (k == 0) continue; // k가 0이면 쿼리 무시
            
            // 인덱스 s부터 e까지 반복
            for (int i = s; i <= e; i++) {
                // i가 k의 배수인지 확인
                if (i % k == 0) {
                    arr[i] += 1; // 배수일 경우 arr[i]에 1을 더함
                }
            }
        }
        return arr; // 수정된 arr 반환
    }
}
```

### 코드 설명  
1. **쿼리 반복**: `for (int[] query : queries)`를 통해 각 쿼리 처리
2. **변수 초기화**: 각 쿼리에서 `s`, `e`, `k` 추출
3. **k가 0인지 확인**: 만약 `k`가 0이라면 `continue`로 현재 쿼리 건너뛰기
4. **인덱스 반복**: `for (int i = s; i <= e; i++)`를 통해 `s`부터 `e`까지의 인덱스 반복
5. **배수 체크**: `if (i % k == 0)`를 통해 `i`가 `k`의 배수인지 확인하고, 맞다면 `arr[i]` 1 증가
6. **결과 반환**: 모든 쿼리를 처리한 후 수정된 `arr` 반환  


<br/>
* * *
<br/>

## 배열 만들기 2
> **문제**  
정수 `l`과 `r`이 주어졌을 때, `l` 이상 `r`이하의 정수 중에서 숫자 "0"과 "5"로만 이루어진 모든 정수를 오름차순으로 저장한 배열을 return 하는 solution 함수를 완성해 주세요. 만약 그러한 정수가 없다면, -1이 담긴 배열을 return 합니다.    

> **문제 분석**
1. **입력**:
   - 두 정수 `l`과 `r`: 범위의 시작과 끝을 나타냅니다. (1 ≤ l ≤ r ≤ 1,000,000)
2. **출력**:
   - 범위 내에서 "0"과 "5"로만 이루어진 정수들의 배열. 조건을 만족하는 정수가 없으면 `-1`이 담긴 배열 반환
3. **작업**:
   - `l`에서 `r`까지의 모든 정수를 순회하며, 각 정수가 "0"과 "5"로만 이루어져 있는지 확인
   - 유효한 정수를 리스트에 추가
   - 리스트가 비어있으면 `-1`을 반환하고, 그렇지 않으면 리스트를 정수 배열로 변환하여 반환  

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public int[] solution(int l, int r) {
        List<Integer> result = new ArrayList<>();
        
        for (int i = l; i <= r; i++) {
            if (isValidNumber(i)) {
                result.add(i); // 유효한 숫자 추가
            }
        }
        
        if (result.isEmpty()) {
            return new int[]{-1}; // 결과가 없을 경우 -1 반환
        }
        
        return result.stream().mapToInt(i -> i).toArray(); // 리스트를 정수 배열로 변환
    }

    private boolean isValidNumber(int number) {
        String str = String.valueOf(number);
        for (char c : str.toCharArray()) {
            if (c != '0' && c != '5') {
                return false; // "0"과 "5"가 아닌 숫자가 포함된 경우
            }
        }
        return true; // 유효한 숫자
    }
}
```

### 코드 설명
1. **리스트 초기화**: `List<Integer> result = new ArrayList<>();`를 통해 결과를 저장할 리스트 초기화
2. **정수 순회**: `for (int i = l; i <= r; i++)`를 사용하여 `l`부터 `r`까지의 모든 정수 순회
3. **유효성 검사**: `isValidNumber(i)` 메서드를 호출하여 현재 숫자가 "0"과 "5"로만 이루어져 있는지 확인
4. **리스트에 추가**: 유효한 숫자일 경우 `result.add(i);`를 통해 리스트에 추가
5. **결과 확인**: 리스트가 비어있으면 `return new int[]{-1};`로 `-1`을 반환하고, 그렇지 않으면 `result`를 정수 배열로 변환하여 반환
6. **유효성 검사 메서드**: `isValidNumber` 메서드는 주어진 숫자를 문자열로 변환한 후, 각 문자에 대해 "0" 또는 "5"인지 확인하여 유효성을 검사  

<br/>
* * *
<br/>

## 카운트 업
> **문제**  
정수 start_num와 end_num가 주어질 때, start_num부터 end_num까지의 숫자를 차례로 담은 리스트를 return하도록 solution 함수를 완성해주세요.  

> **문제 분석**
1. **입력**:
   - 두 정수 `start_num`과 `end_num`: 이 범위의 시작과 끝을 나타냅니다. (0 ≤ start_num ≤ end_num)
2. **출력**:
   - `start_num`부터 `end_num`까지의 모든 정수를 포함하는 리스트
3. **작업**:
   - `start_num`부터 `end_num`까지의 정수를 생성하여 리스트에 담아 반환  

```java
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Solution {
    public List<Integer> solution(int start_num, int end_num) {
        return IntStream.rangeClosed(start_num, end_num) // start_num부터 end_num까지의 스트림 생성
                        .boxed() // IntStream을 Integer Stream으로 변환
                        .collect(Collectors.toList()); // 리스트로 변환하여 반환
    }
}
```

### 코드 설명
1. **IntStream.rangeClosed**: 
   - `IntStream.rangeClosed(start_num, end_num)` 메서드는 `start_num`부터 `end_num`까지의 모든 정수를 포함하는 스트림을 생성, 이 메서드는 `end_num`도 포함함  
2. **boxed()**:
   - `boxed()` 메서드는 `IntStream`을 `Stream<Integer>`로 변환, 기본형 `int`를 객체형 `Integer`로 변환하여 리스트에 담을 수 있게 함   
3. **collect(Collectors.toList())**:
   - `collect(Collectors.toList())` 메서드는 스트림의 요소를 리스트로 수집, 최종적으로 `List<Integer>` 형태로 결과를 반환    

<br/>
* * *
<br/>

## 콜라츠 수열 만들기
> **문제**  
모든 자연수 `x`에 대해서 현재 값이 `x`이면 `x`가 짝수일 때는 2로 나누고, `x`가 홀수일 때는 `3 * x + 1`로 바꾸는 계산을 계속해서 반복하면 언젠가는 반드시 `x`가 1이 되는지 묻는 문제를 콜라츠 문제라고 부릅니다. 그리고 위 과정에서 거쳐간 모든 수를 기록한 수열을 콜라츠 수열이라고 부릅니다. 계산 결과 1,000 보다 작거나 같은 수에 대해서는 전부 언젠가 1에 도달한다는 것이 알려져 있습니다. 임의의 1,000 보다 작거나 같은 양의 정수 `n`이 주어질 때 초기값이 `n`인 콜라츠 수열을 return 하는 solution 함수를 완성해 주세요.   

> **문제 분석**
1. **입력**:
   - 하나의 자연수 `n`: (1 ≤ n ≤ 1,000)
2. **출력**:
   - `n`으로 시작하는 콜라츠 수열을 담은 리스트
3. **작업**:
   - `n`이 1이 될 때까지 다음 규칙에 따라 반복
     - `n`이 짝수이면 `n`을 2로 나누고,
     - `n`이 홀수이면 `3 * n + 1`로 변경
   - 각 단계에서 `n`의 값을 리스트에 추가
   - 최종적으로 1을 리스트에 추가하고 반환   

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<Integer> solution(int n) {
        List<Integer> collatzSequence = new ArrayList<>();
        
        // n이 1이 될 때까지 반복
        while (n != 1) {
            collatzSequence.add(n); // 현재 값을 리스트에 추가
            if (n % 2 == 0) { // 짝수인 경우
                n /= 2; // n을 2로 나누기
            } else { // 홀수인 경우
                n = 3 * n + 1; // n을 3 * n + 1로 변경
            }
        }
        
        collatzSequence.add(1); // 마지막 값 1 추가
        return collatzSequence; // 결과 리스트 반환
    }
}
```

### 코드 설명
1. **리스트 초기화**: `List<Integer> collatzSequence = new ArrayList<>();`를 통해 콜라츠 수열을 저장할 리스트를 초기화
2. **반복문**: `while (n != 1)`을 사용하여 `n`이 1이 될 때까지 반복
   - 현재 `n`의 값을 리스트에 추가합니다: `collatzSequence.add(n);`
   - `n`이 짝수인지 홀수인지 확인하여 다음 값을 결정
     - 짝수일 경우: `n /= 2;`를 통해 `n`을 2로 나눔  
     - 홀수일 경우: `n = 3 * n + 1;`을 통해 `n`을 `3 * n + 1`로 변경
3. **마지막 값 추가**: `while` 루프가 종료되면 `n`은 1이 되므로, `collatzSequence.add(1);`로 리스트에 1 추가
4. **결과 반환**: 최종적으로 `collatzSequence`를 반환하여 콜라츠 수열 제공  

<br/>
* * *
<br/>

## 배열 만들기 4
> **문제**  
정수 배열 `arr`가 주어집니다. `arr`를 이용해 새로운 배열 `stk`를 만드려고 합니다.
변수 `i`를 만들어 초기값을 0으로 설정한 후 `i`가 `arr`의 길이보다 작으면 다음 작업을 반복합니다.
- 만약 `stk`가 빈 배열이라면 `arr[i]`를 `stk`에 추가하고 `i`에 1을 더합니다.
- `stk`에 원소가 있고, `stk`의 마지막 원소가 `arr[i]`보다 작으면 `arr[i]`를 `stk`의 뒤에 추가하고 `i`에 1을 더합니다.
- `stk`에 원소가 있는데 `stk`의 마지막 원소가 `arr[i]`보다 크거나 같으면 `stk`의 마지막 원소를 `stk`에서 제거합니다.
위 작업을 마친 후 만들어진 `stk`를 return 하는 solution 함수를 완성해 주세요.  

> **문제 분석**
1. **입력**:
   - 정수 배열 `arr`: 주어진 배열에서 작업 수행
2. **출력**:
   - 새로운 배열 `stk`: 주어진 규칙에 따라 생성된 배열
3. **작업 규칙**:
   - 변수 `i`를 0으로 초기화하고, `i`가 `arr`의 길이보다 작으면 다음 작업을 반복
   - `stk`가 비어 있으면 `arr[i]`를 `stk`에 추가하고, `i`를 1 증가
   - `stk`에 원소가 있고, `stk`의 마지막 원소가 `arr[i]`보다 작으면 `arr[i]`를 `stk`에 추가하고, `i`를 1 증가
   - `stk`의 마지막 원소가 `arr[i]`보다 크거나 같으면 `stk`의 마지막 원소를 제거  

```java
import java.util.ArrayList;
import java.util.List;

public class Solution {
    public List<Integer> solution(int[] arr) {
        List<Integer> stk = new ArrayList<>();
        int i = 0; // 초기값 설정

        // 배열의 끝까지 반복
        while (i < arr.length) {
            // stk가 비어있거나, stk의 마지막 원소가 arr[i]보다 작은 경우
            if (stk.isEmpty() || stk.get(stk.size() - 1) < arr[i]) {
                stk.add(arr[i]); // arr[i]를 stk에 추가
                i++; // i 증가
            } else {
                // stk의 마지막 원소가 arr[i]보다 크거나 같은 경우
                stk.remove(stk.size() - 1); // stk의 마지막 원소 제거
            }
        }

        return stk; // 결과 반환
    }
}
```

### 코드 설명
1. **리스트 초기화**: `List<Integer> stk = new ArrayList<>();`를 통해 `stk` 초기화 
2. **변수 초기화**: `int i = 0;`를 통해 인덱스 `i`를 0으로 설정
3. **반복문**: `while (i < arr.length)`를 사용하여 배열의 끝까지 반복
   - **첫 번째 조건**: `if (stk.isEmpty() || stk.get(stk.size() - 1) < arr[i])`
     - `stk`가 비어있거나, `stk`의 마지막 원소가 `arr[i]`보다 작으면 `arr[i]`를 `stk`에 추가
     - `i`를 1 증가
   - **두 번째 조건**: `else`
     - `stk`의 마지막 원소가 `arr[i]`보다 크거나 같으면, `stk`의 마지막 원소를 제거
4. **결과 반환**: 반복이 끝나면 `stk`를 반환하여 최종 결과 반환  

<br/>
* * *
<br/>