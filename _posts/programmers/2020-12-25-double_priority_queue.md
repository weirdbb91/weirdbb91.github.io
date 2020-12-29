---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 이중우선순위큐 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-25 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 이중우선순위큐](https://programmers.co.kr/learn/courses/30/lessons/42628)

사용 언어 자바

### 입력

- 명령 문자 배열


이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.  

|명령어|수신 탑(높이)|
|-|-|
|I 숫자|큐에 주어진 숫자를 삽입합니다.|
|D 1|큐에서 최댓값을 삭제합니다.|
|D -1|큐에서 최솟값을 삭제합니다.|

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때,  
모든 연산을 처리한 후 큐가 비어있으면 [0,0]  
비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.  

### 제한사항

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.

### 제출 답안

```java
public int[] solution(String[] operations) {
    PriorityQueue<Integer> AscQ = new PriorityQueue();
    PriorityQueue<Integer> DescQ = new PriorityQueue(Collections.reverseOrder());

    for (String order : operations) {
        if (!DescQ.isEmpty() && order.equals("D 1")) {
            AscQ.remove(DescQ.poll());
        }
        if (!AscQ.isEmpty() && order.equals("D -1")) {
            DescQ.remove(AscQ.poll());
        }
        if (order.charAt(0) == 'I') {
            AscQ.add(Integer.parseInt(order.split(" ")[1]));
            DescQ.add(Integer.parseInt(order.split(" ")[1]));
        }
    }
    return AscQ.isEmpty() ? new int[]{0, 0} : new int[]{DescQ.poll(), AscQ.poll()};
}
```
