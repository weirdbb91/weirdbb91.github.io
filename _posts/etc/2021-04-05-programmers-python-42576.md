---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 완주하지 못한 선수 # 제목
excerpt             : 프로그래머스 문제(파이썬) # 썸네일 한줄 요약
last_modified_at    : 2021-04-05 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Python
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 완주하지 못한 선수](https://programmers.co.kr/learn/courses/30/lessons/42576)

사용 언어 파이썬


### 문제 설명
수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한사항
마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.

### 입출력 예
|participant|	completion|	return|
|-|-|
|["leo", "kiki", "eden"]|	["eden", "kiki"]|	"leo"|
|["marina", "josipa", "nikola", "vinko", "filipa"]|	["josipa", "filipa", "marina", "nikola"]|	"vinko"|
|["mislav", "stanko", "mislav", "ana"]|	["stanko", "ana", "mislav"]|	"mislav"|

---

단 한명의 선수만 제외했기 때문에 양쪽 정렬 후  
많은 쪽을 기준으로 같지 않은 첫번째를 반환했다

### 제출 답안

```py
def solution(participant, completion):
    participant = sorted(participant)
    completion = sorted(completion)
    for i in range(len(participant)):
        if participant[i] != completion[i]:
            return participant[i]
    return participant[0]
```