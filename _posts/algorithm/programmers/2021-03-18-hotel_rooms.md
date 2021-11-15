---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 호텔 방 배정 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-03-18 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 호텔 방 배정](https://programmers.co.kr/learn/courses/30/lessons/64063)

사용 언어 자바

### 문제 설명
"스노우타운"에서 호텔을 운영하고 있는 "스카피"는 호텔에 투숙하려는 고객들에게 방을 배정하려 합니다. 호텔에는 방이 총 k개 있으며, 각각의 방은 1번부터 k번까지 번호로 구분하고 있습니다. 처음에는 모든 방이 비어 있으며 "스카피"는 다음과 같은 규칙에 따라 고객에게 방을 배정하려고 합니다.

- 한 번에 한 명씩 신청한 순서대로 방을 배정합니다.
- 고객은 투숙하기 원하는 방 번호를 제출합니다.
- 고객이 원하는 방이 비어 있다면 즉시 배정합니다.
- 고객이 원하는 방이 이미 배정되어 있으면 원하는 방보다 번호가 크면서 비어있는 방 중 가장 번호가 작은 방을 배정합니다.

예를 들어, 방이 총 10개이고, 고객들이 원하는 방 번호가 순서대로 [1, 3, 4, 1, 3, 1] 일 경우 다음과 같이 방을 배정받게 됩니다.

| 원하는 방 번호 | 배정된 방 번호 |
| -------------- | -------------- |
| 1              | 1              |
| 3              | 3              |
| 4              | 4              |
| 1              | 2              |
| 3              | 5              |
| 1              | 6              |


전체 방 개수 k와 고객들이 원하는 방 번호가 순서대로 들어있는 배열 room_number가 매개변수로 주어질 때, 각 고객에게 배정되는 방 번호를 순서대로 배열에 담아 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- k는 1 이상 1012 이하인 자연수입니다.
- room_number 배열의 크기는 1 이상 200,000 이하입니다.
- room_number 배열 각 원소들의 값은 1 이상 k 이하인 자연수입니다.
- room_number 배열은 모든 고객이 방을 배정받을 수 있는 경우만 입력으로 주어집니다.

예를 들어, k = 5, room_number = [5, 5] 와 같은 경우는 방을 배정받지 못하는 고객이 발생하므로 이런 경우는 입력으로 주어지지 않습니다.

### 입출력 예

| k   | room_number   | result        |
| --- | ------------- | ------------- |
| 10  | [1,3,4,1,3,1] | [1,3,4,2,5,6] |

---

유니온 파인드 알고리즘이었다  

3단계는 주로 뭔가 만들어야 되는게 있는 있는가 한 반면에  
4단계는 가끔씩 이렇게 특정 알고리즘을 알고 있는지만 확인하는듯한 경우가 있어서 맥빠질 때가 있다  
생각하는 맛에 푸는건데 생각할게 없었다  

### 제출 답안

```java
import java.util.*;

class Solution {
    HashMap<Long, Long> hotel = new HashMap<>();
    
    public long[] solution(long k, long[] room_number) {
        long[] answer = new long[room_number.length];
        
        for (int i = 0; i < room_number.length; i++) {
            answer[i] = findRoom(room_number[i]);
        }
        return answer;
    }
    
    private long findRoom(long room) {
        if (!hotel.containsKey(room)) {
            hotel.put(room, room + 1L);
            return room;
        }
        long num = findRoom(hotel.get(room));
        hotel.put(room, num + 1);
        return num;
    }
}
```