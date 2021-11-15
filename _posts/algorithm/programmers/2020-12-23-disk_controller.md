---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 디스크 컨트롤러 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-23 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 디스크 컨트롤러](https://programmers.co.kr/learn/courses/30/lessons/42627)

사용 언어 자바

### 입력

- 작업 배열
  - 작업은 new int[]{요청 시점, 소요시간}의 형태이다

### 제한사항

- jobs의 길이는 1 이상 500 이하입니다.
- jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
- 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
- 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
- 하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.

각 작업들의 처리 순서를 바꿔 요청부터 작업 완료까지 최소 평균시간을 구해라  

문제를 잘못 읽은줄 알았다  
작업의 소요시간에 변경이 없는데 순서를 바꾼다고 평균시간이 변하나?  
시작 기준이 요청시간이라 평균시간에 차이가 생겼다  

우선순위 큐로 소요시간이 짧은 작업 먼저 처리를 해봤지만  
요청시간을 고려하지 않아서 실패했다  

우선순위 큐를 하나 더 만들어서 현시간 기준 요청 확인된 작업들을 걸러내  
소요시간이 짧은 작업 먼저 처리를 했더니 통과했다

그냥 왠지 당연하게 짧은 작업 먼저 끝내야겠다고 생각하면서 풀었는데  
통과하고 갑자기 왜 짧은 작업 먼저해야 평균 시간이 줄어드는지 궁금해졌다  
봐도 모르겠다 이해가 잘 안된다  

이번 문제는 우연히 통과한것 같다  


생각보다 기본제공되는 기능들이 많은데 아직도 모르는게 많다  

```java
new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
```

이건 정말 좋다  

### 제출 답안
```java
public int solution(int[][] jobs) {
    int answer = 0;
    PriorityQueue<int[]> waiting = new PriorityQueue<>(Comparator.comparingInt(a -> a[0]));
    PriorityQueue<int[]> processing = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
    waiting.addAll(Arrays.asList(jobs));
    int time = !waiting.isEmpty() ? waiting.peek()[0] : 0;

    while (!waiting.isEmpty() || !processing.isEmpty()) {
        while (!waiting.isEmpty() && waiting.peek()[0] <= time) processing.add(waiting.poll());
        if (processing.isEmpty()) {
            time++;
            continue;
        }
        time += processing.peek()[1];
        answer += time - processing.poll()[0];
    }
    return answer / jobs.length;
}
```