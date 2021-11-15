---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 줄 서는 방법 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-01-20 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 줄 서는 방법](https://programmers.co.kr/learn/courses/30/lessons/12936)

사용 언어 자바

### 문제 설명
n명의 사람이 일렬로 줄을 서고 있습니다.  
n명의 사람들에게는 각각 1번부터 n번까지 번호가 매겨져 있습니다.  
n명이 사람을 줄을 서는 방법은 여러가지 방법이 있습니다.  
예를 들어서 3명의 사람이 있다면 다음과 같이 6개의 방법이 있습니다.

- [1, 2, 3]
- [1, 3, 2]
- [2, 1, 3]
- [2, 3, 1]
- [3, 1, 2]
- [3, 2, 1]

사람을 나열 하는 방법을 사전 순으로 나열 했을 때,  
k번째 방법을 return하는 solution 함수를 완성해주세요.

### 제한사항
- n은 20이하의 자연수 입니다.
- k는 n! 이하의 자연수 입니다.

### 입력

- 사람 수 n
- 방법 번호 k

제출하고 후기 작성하면서 k가 long 타입이라는걸 알았다  
글을 읽는게 어려운건지 참 안타깝다  

첫번째 자리의 숫자는 두 번째 숫자가 가진 경우의 수만큼 지나야 바뀐다  
즉 k번째 방법의 첫번째 자리의 인덱스는  
(k - 1) / 두 번째 숫자가 가진 경우의 수가 된다  

이런 나열 방법의 규칙을 그대로 표현해봤다  

원래 전부 int형이었는데 처음 제출 후  
효율성 테스트에서 실패와 함께 런타임 오류가 나와서 고민하다가  
20 팩토리얼이면 인트 범위를 넘기겠다는 생각이 들어 롱타입으로 바꿨다


cases에는 각 자릿수가 가진 경우의 수를 담았고  
list에는 1부터 n까지 순서로 담았다


### 제출 답안

```java
public int[] solution(int n, long k) {
    ArrayList<Long> cases = new ArrayList<>();
    ArrayList<Long> list = new ArrayList<>();
    long a = 1;
    for (int i = 1; i <= n; i++) {
        a *= i;
        cases.add((long) a);
        list.add((long) i);
    }
    int[] answer = new int[n];
    int targetIdx;
    Long partCases;
    k--;
    for (int i = 0; i < n - 1; i++) {
        partCases = cases.get(n - i - 2);
        targetIdx = (int) (k / partCases);
        answer[i] = list.remove(targetIdx).intValue();
        k -= (int) targetIdx * partCases;
    }
    answer[n - 1] = list.get(0).intValue();
    return answer;
}
```