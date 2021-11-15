---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 멀리 뛰기 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-03-22 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 멀리 뛰기](https://programmers.co.kr/learn/courses/30/lessons/12914)

사용 언어 자바

### 문제 설명

효진이는 멀리 뛰기를 연습하고 있습니다.  
효진이는 한번에 1칸, 또는 2칸을 뛸 수 있습니다.  
칸이 총 4개 있을 때, 효진이는  
(1칸, 1칸, 1칸, 1칸)  
(1칸, 2칸, 1칸)  
(1칸, 1칸, 2칸)  
(2칸, 1칸, 1칸)  
(2칸, 2칸)  
의 5가지 방법으로 맨 끝 칸에 도달할 수 있습니다.  
멀리뛰기에 사용될 칸의 수 n이 주어질 때, 효진이가 끝에 도달하는 방법이 몇 가지인지 알아내, 여기에 1234567를 나눈 나머지를 리턴하는 함수, solution을 완성하세요. 예를 들어 4가 입력된다면, 5를 return하면 됩니다.  

### 제한 사항
n은 1 이상, 2000 이하인 정수입니다.  
입출력 예  
| n   | result |
| --- | ------ |
| 4   | 5      |
| 3   | 3      |

---

놀랍도록 직접적인 피보나치 문제였다  
수를 저장하면서 진행해 불필요한 연산을 줄였고  
1234567L로 나누면서 구했다  

### 제출 답안

```java
class Solution {
    private long[] cases = new long[2001];
    
    public long solution(int n) {
        if (n <= 2) return (long) n;
        cases[1] = 1L;
        cases[2] = 2L;
        return jump(n);
    }
    
    public long jump(int n) {
        if (cases[n] != 0) return cases[n];
        cases[n] = jump(n - 1) + jump(n - 2);
        return cases[n] % 1234567L;
    }
}
```