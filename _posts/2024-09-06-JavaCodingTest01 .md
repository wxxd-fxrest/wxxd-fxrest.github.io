---
title: Day01 | CodingTest JAVA
date: 2024-09-11 01:03:00 +09:00
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

## 문자열 출력하기
```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        System.out.println(a);
    }
}
```

<br/>
* * *
<br/>

## a와 b 출력하기
```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();

        System.out.println("a = " + a);
        System.out.println("b = " + b);
    }
}
```

<br/>
* * *
<br/>

## n개 간격의 원소들 [* ArrayList]
배열에서 n개 간격으로 원소를 추출하는 방법에 대해 알아보자. 이 문제를 해결하기 위해 나는 `ArrayList`를 활용했다. 

### 코드 설명
```java
import java.util.ArrayList;

class Solution {
    public int[] solution(int[] num_list, int n) {
        ArrayList<Integer> answerList = new ArrayList<>();
        
        for (int i = 0; i < num_list.length; i += n) {
            answerList.add(num_list[i]);
        }
        
        int[] answer = new int[answerList.size()];
        
        for (int i = 0; i < answerList.size(); i++) {
            answer[i] = answerList.get(i);
        }
        
        return answer;
    }
}
```

### 1. 클래스 및 메서드 정의
**클래스 선언**: `Solution` 클래스 정의. 
**메서드 정의**: `public int[] solution(int[] num_list, int n)` 메서드는 두 개의 매개변수를 받는다. 
  - 01) `num_list`: 원본 배열
  - 02) `n`       : 원소를 추출할 간격  

### 2. ArrayList 초기화
```java
ArrayList<Integer> answerList = new ArrayList<>();
```

- `ArrayList`를 사용하여 결과를 저장할 리스트를 초기화했다.  
> `ArrayList`는 동적으로 크기를 조정할 수 있어, 필요한 만큼 원소를 추가할 수 있는 장점이 있다.  

### 3. n개 간격으로 원소 추출
```java
for (int i = 0; i < num_list.length; i += n) {
    answerList.add(num_list[i]);
}
```

- `for` 루프를 사용해 `num_list`의 각 원소를 순회한다. 인덱스 `i`는 `n`만큼 증가하므로, `num_list[i]`는 n개 간격으로 원소를 선택하게 된다.
- 선택된 원소는 `answerList`에 추가된다.

### 4. 배열로 변환
```java
int[] answer = new int[answerList.size()];
```

- 추출한 원소들을 담을 배열 `answer`를 생성한다. 이 배열의 크기는 `answerList`의 크기와 동일하다.

### 5. ArrayList에서 배열로 복사
```java
for (int i = 0; i < answerList.size(); i++) {
    answer[i] = answerList.get(i);
}
```

- `answerList`의 각 원소를 `answer` 배열로 복사한다. 
- `get(i)` 메서드를 사용하여 리스트의 원소를 가져온다.

### 6. 결과 반환
```java
return answer;
```

- 최종적으로 n개 간격으로 추출된 원소들이 담긴 배열을 반환한다.  

<br/>
* * *
<br/>

## 문자열 반복해서 출력하기 [* repeat()]
문자열을 지정한 횟수만큼 반복 출력하는 방법. 이 코드는 `Scanner` 클래스를 활용하여 입력을 받고, `String` 클래스의 `repeat` 메서드를 사용하여 문자열을 반복한다. 

### 코드 설명
```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.next();
        int n = sc.nextInt();
        System.out.println(str.repeat(n));
    }
}
``` 
  
### 1. 사용자 입력 받기
```java
Scanner sc = new Scanner(System.in);
```

- `Scanner` 클래스는 Java에서 입력을 읽기 위해 사용된다. 
- `System.in`을 매개변수로 전달하여 키보드 입력을 받을 수 있도록 설정한다.  

### 2. 문자열 및 정수 입력
```java
String str = sc.next();
int n = sc.nextInt();
```

- `sc.next()`를 사용하여 사용자로부터 문자열을 입력받는다. 이때, 공백이 포함된 문자열은 첫 번째 단어만 읽어온다.
- `sc.nextInt()`를 사용하여 사용자로부터 정수를 입력받는다. 이 정수는 문자열을 반복할 횟수를 나타낸다.  

### 3. 문자열 반복 및 출력
```java
System.out.println(str.repeat(n));
```

- `String` 클래스의 `repeat(int count)` 메서드를 사용하여 입력받은 문자열 `str`을 `n`번 반복한다. 
> 이 메서드는 Java 11부터 추가된 기능으로, 문자열을 간편하게 반복할 수 있게 해줌.
- 반복된 문자열은 `System.out.println()`을 통해 출력된다.  

<br/>
* * *
<br/>

# 대소문자 바꿔서 출력하기 [* toCharArray(), isUpperCase(), toLowerCase(), toUpperCase()]
이번에는 문자열의 대소문자를 반전시키는 프로그램을 구현하는 방법에 대해 알아보자. 이 코드는 `Scanner` 클래스를 사용하여 사용자 입력을 받고, `Character` 클래스를 활용하여 각 문자의 대소문자를 변환한다.

#### 코드 설명 
```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        
        char[] ch = a.toCharArray();
        
        for (char c : ch) {
            if (Character.isUpperCase(c)) {
                c = Character.toLowerCase(c);
            } else {
                c = Character.toUpperCase(c);
            }
            System.out.print(c);
        }
    }
}
```

### 1. 사용자 입력 받기
```java
Scanner sc = new Scanner(System.in);
String a = sc.next();
```

- `Scanner` 클래스를 사용하여 사용자로부터 입력을 받는다. 
- `next()` 메서드를 통해 공백을 포함하지 않는 문자열을 받는다.

### 2. 문자열을 문자 배열로 변환

```java
char[] ch = a.toCharArray();
```

- 입력받은 문자열 `a`를 `toCharArray()` 메서드를 사용하여 문자 배열 `ch`로 변환한다. 이를 통해 **각 문자를 개별적으로 처리**할 수 있다.

### 3. 대소문자 변환 및 출력
```java
for (char c : ch) {
    if (Character.isUpperCase(c)) {
        c = Character.toLowerCase(c);
    } else {
        c = Character.toUpperCase(c);
    }
    System.out.print(c);
}
```

- `for-each` 루프를 사용하여 문자 배열 `ch`의 각 문자를 순회한다.
- `Character.isUpperCase(c)` 메서드를 사용하여 현재 문자가 대문자인지 확인한다. 대문자인 경우 `Character.toLowerCase(c)`를 통해 소문자로 변환한다.
- 대문자가 아닌 경우, `Character.toUpperCase(c)`를 사용하여 소문자를 대문자로 변환한다.
- 변환된 문자는 `System.out.print(c)`를 통해 출력된다.  

<br/>
* * *
<br/>

## 특수문자 출력하기 [* 이스케이프 시퀀스]
마지막으로, 특수문자를 출력하는 간단한 프로그램을 구현하는 방법에 대해 알아보자.

### 코드 설명
```java
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        System.out.println("!@#$%^&*(\\'\"<>?:;");
    }
}
```

### 1. 특수문자 출력

```java
System.out.println("!@#$%^&*(\\'\"<>?:;");
```

- `System.out.println()` 메서드를 사용하여 문자열을 출력한다. 이 문자열은 다양한 특수문자로 구성되어 있다.
- 문자열 내에서 특수문자를 포함할 때, 일부 문자들은 **이스케이프 시퀀스를 사용**해야 한다. 예를 들어, `\'`는 작은따옴표를, `\"`는 큰따옴표를 출력하기 위해 사용된다. 

<br/>
* * *
<br/>

오늘부터 코딩테스트 가보자고! 코테가 이렇게 재밌는 건 또 처음이야, 자바 짱이잖아?