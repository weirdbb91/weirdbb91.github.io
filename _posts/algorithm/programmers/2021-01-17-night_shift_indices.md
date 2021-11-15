---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 야간 근무 지수 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-01-17 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 야간 근무 지수](https://programmers.co.kr/learn/courses/30/lessons/12927)

사용 언어 자바

### 입력

- 남은 작업량 배열 int[] works
- 가능 작업 처리량 int n

야근을 하면 야근 피로도가 쌓입니다.  
야근 피로도는 남은 일들의 작업량을 각각 제곱하여 합한 값입니다.  
가능 작업 처리량만큼의 작업 후 가능한 최소 야근 피로도를 리턴.
 

### 제한사항

- works는 길이 1 이상, 20,000 이하인 배열입니다.
- works의 원소는 50000 이하인 자연수입니다.
- n은 1,000,000 이하인 자연수입니다.



n이 그리 크지도 않고 복잡한 연산이 없어 깊게 생각 않고 1씩 처리했다

### 제출 답안

```java
public long solution(int n, int[] works) {
    long answer = 0;
    PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder());
    for (int i : works) {
        pq.add(i);
    }

    for (int i = 0; i < n; i++) {
        if (pq.peek() <= 0) {
            return 0;
        }
        pq.add(pq.poll() - 1);
    }

    while (!pq.isEmpty()) {
        answer += pq.peek() * pq.poll();
    }
    return answer;
}
```