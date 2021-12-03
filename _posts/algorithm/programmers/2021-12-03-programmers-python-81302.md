---
title               : 거리두기 확인하기 # 제목
excerpt             : 프로그래머스 문제(파이썬) # 썸네일 한줄 요약
categories          : Algorithm 문제풀이
tags                : Programmers Solution Python
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 거리두기 확인하기](https://programmers.co.kr/learn/courses/30/lessons/81302)

사용 언어 파이썬

### 문제 설명
개발자를 희망하는 죠르디가 카카오에 면접을 보러 왔습니다.

코로나 바이러스 감염 예방을 위해 응시자들은 거리를 둬서 대기를 해야하는데 개발 직군 면접인 만큼, 아래와 같은 규칙으로 대기실에 거리를 두고 앉도록 안내하고 있습니다.

대기실은 5개이며, 각 대기실은 5x5 크기입니다.
거리두기를 위하여 응시자들 끼리는 맨해튼 거리1가 2 이하로 앉지 말아 주세요.
단 응시자가 앉아있는 자리 사이가 파티션으로 막혀 있을 경우에는 허용합니다.

5개의 대기실을 본 죠르디는 각 대기실에서 응시자들이 거리두기를 잘 기키고 있는지 알고 싶어졌습니다. 자리에 앉아있는 응시자들의 정보와 대기실 구조를 대기실별로 담은 2차원 문자열 배열 places가 매개변수로 주어집니다. 각 대기실별로 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 배열에 담아 return 하도록 solution 함수를 완성해 주세요.

### 제한사항
- places의 행 길이(대기실 개수) = 5
- places의 각 행은 하나의 대기실 구조를 나타냅니다.
- places의 열 길이(대기실 세로 길이) = 5
- places의 원소는 P,O,X로 이루어진 문자열입니다.
- places 원소의 길이(대기실 가로 길이) = 5
- P는 응시자가 앉아있는 자리를 의미합니다.
- O는 빈 테이블을 의미합니다.
- X는 파티션을 의미합니다.
- 입력으로 주어지는 5개 대기실의 크기는 모두 5x5 입니다.
- return 값 형식
- 1차원 정수 배열에 5개의 원소를 담아서 return 합니다.
- places에 담겨 있는 5개 대기실의 순서대로, 거리두기 준수 여부를 차례대로 배열에 담습니다.
- 각 대기실 별로 모든 응시자가 거리두기를 지키고 있으면 1을, 한 명이라도 지키지 않고 있으면 0을 담습니다.

### 입출력 예

|places|result|
|--|--|
|[<br>["POOOP", "OXXOX", "OPXPX", "OOXOX", "POXXP"],<br>["POOPX", "OXPXP", "PXXXO", "OXXXO", "OOOPP"],<br>["PXOPX", "OXOXP", "OXPOX", "OXXOP", "PXPOX"],<br>["OOOXX", "XOOOX", "OOOXX", "OXOOX", "OOOOO"],<br>["PXPXP", "XPXPX", "PXPXP", "XPXPX", "PXPXP"]<br>]|[1, 0, 1, 1, 1]|


---


### 제출 답안

```py
from collections import deque

MAX_RANGE = 5
MAX_DISTANCE = 2

PERSON = "P"
EMPTY = "O" # 테이블
PARTITION = "X"

VALID = 1
INVALID = 0

# 거리두기 규칙 위반시 0, 준수시 1 반환
def is_valid_distance(place):
    # 응시자 위치 파악
    persons = []
    for y in range(MAX_RANGE):
        for x in range(MAX_RANGE):
            if place[y][x] == PERSON:
                persons.append([y, x])
    
    # 응시자 전원 점검
    for person in persons:
        have_to_visit = deque([person, ])
        visited = [[0] * MAX_RANGE for i in range(MAX_RANGE)]
        visited[person[0]][person[1]] = 1
        
        # 4방향 좌표 변경값
        dir_y = [0, 1, 0, -1]
        dir_x = [1, 0, -1, 0]
        
        # BFS
        while have_to_visit:
            y, x = have_to_visit.popleft()
            distance = visited[y][x]
            
            # 점검 범위 초과
            if distance > MAX_DISTANCE:
                continue
            
            # 4방향 점검
            for i in range(4):
                next_y = y + dir_y[i]
                next_x = x + dir_x[i]
                
                # 대기실 범위 초과 or 파티션위치 or 이미 점검 완료
                if 0 > next_y or next_y >= MAX_RANGE \
                    or 0 > next_x or next_x >= MAX_RANGE \
                    or place[next_y][next_x] == PARTITION \
                    or visited[next_y][next_x]:
                    continue
                
                # 거리두기 규칙 위반
                if place[next_y][next_x] == PERSON:
                    return INVALID
                
                # 방문 필요 목록에 추가
                visited[next_y][next_x] = distance + 1
                have_to_visit.append([next_y, next_x])
    
    # 응시자 전원 점검 결과 거리두기 규칙 준수            
    return VALID

def solution(places):
    answer = []
    for place in places:
        answer.append(is_valid_distance(place))
    return answer
```