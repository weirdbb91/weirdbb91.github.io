---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : N으로 표현 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-21 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - N으로 표현](https://programmers.co.kr/learn/courses/30/lessons/42895)

사용 언어 자바

### 입력

- N
- number

### 제한사항

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.

문제는 number를 최소한의 N을 써서 표현하는 것이 목적이다  
N은 붙여서 쓰거나 괄호와 사칙연산을 이용해서 표현이 가능하다  

### 예시 

- 12 = 5 + 5 + (5 / 5) + (5 / 5)
- 12 = 55 / 5 + 5 / 5
- 12 = (55 + 5) / 5

N = 5, number = 12 일 때, N은 각각 6,5,4번씩 사용했고  
이 중 가장 작은 경우인 4를 반환하면 된다  

### 풀이과정

처음에는 number 이하의 수 중에 최대한 큰 수를 만들어서 빼는 것을 반복했고  
결과를 보고 나서 문제를 잘못 이해했다는 것을 깨달았다  

number 보다 큰 수에서 더 작은 수를 빼서 number를 만들 수도 있었고  
제곱수로 나누거나 빼는 것도 가능했다  

너무 많은 이 모든 경우의 수를 하나하나 다 만들어 주는것은 너무 난해했다

#### 첫번째 힌트
첫번째 힌트는 최솟값이 8이하라는 것에서 찾았다  

모든 경우의 수는  
```java
int number(int N의 갯수) {
    return number(N의 갯수 - i) 사칙연산 number(i);
}
```  
위의 형태로 만들어진다고 생각했다

#### 두 번째 힌트
두 번째로 찾은 힌트는 2개의 N으로 만들 수 있는 수에는 제한이 있다는 점이었다  

이것은 N 두 개로 만들 수 있는 모든 경우의 수다  
```
NN, 2N, 0, N^2, 1
```

이것들의 재료는 N이다  
정확히 말하자면 N 한개로 만들수 있는 수로 만들어졌다  

즉, N 3개로 만들수 있는 수는 (N 2개 수) 사칙연산 (N 1개 수)이다  
4개는 (3, 1), (2, 2)  
5개는 (4, 1), (3, 2)  
6개는 (5, 1), (4, 2), (3, 3)  
...  

피보나치 수처럼 N의 사용 횟수별 경우의 수들로  
다음 횟수의 경우의 수를 만들 수 있었다  

#### 놓친점
앞 뒤 순서가 상관있는 사칙연산들( -, / )이 있다는 것을 생각 못했다


### 제출 답안
```java
import java.util.*;

class Solution {
    public int solution(int N, int number) {
        Set<Integer>[] sets = new Set[8];
        for (int i = 0; i < 8; i++) {
            sets[i] = new HashSet<>();
            sets[i].add(repeatN(N, i));
            for (int j = 0; j < (i + 1) / 2; j++) {
                for (int iNum : sets[j]) {
                    for (int jNum : sets[i - 1 - j]) {
                        sets[i].add(iNum + jNum); // 순서영향 없는 연산
                        sets[i].add(iNum * jNum); // 순서영향 없는 연산
                        sets[i].add(iNum - jNum);
                        sets[i].add(jNum - iNum);
                        sets[i].add(iNum / jNum);
                        sets[i].add(jNum / iNum);
                    }
                }
            }
            sets[i].removeIf(num -> num <= 0);
            if (sets[i].contains(number)) return i + 1;
        }
        return -1;
    }

    public int repeatN(int N, int digit) {
        return digit <= 0 ? N : repeatN(N * 10, digit - 1) + N;
    }
}
```