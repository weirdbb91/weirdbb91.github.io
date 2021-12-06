---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 두 개 뽑아서 더하기 # 제목
excerpt             : 프로그래머스 문제(파이썬) # 썸네일 한줄 요약
last_modified_at    : 2021-04-05 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Python
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 두 개 뽑아서 더하기](https://programmers.co.kr/learn/courses/30/lessons/68644)

사용 언어 파이썬

### 문제 설명
정수 배열 numbers가 주어집니다. numbers에서 서로 다른 인덱스에 있는 두 개의 수를 뽑아 더해서 만들 수 있는 모든 수를 배열에 오름차순으로 담아 return 하도록 solution 함수를 완성해주세요.

### 제한사항
numbers의 길이는 2 이상 100 이하입니다.
numbers의 모든 수는 0 이상 100 이하입니다.

### 입출력 예

| numbers     | result        |
| ----------- | ------------- |
| [2,1,3,4,1] | [2,3,4,5,6,7] |
| [5,0,2,7]   | [2,5,7,9,12]  |

---

컴프리헨션을 공부할 겸 최대한 불편하게 풀어봤다  
막상 몇번 써보니 생각보다 편한것 같다

### 제출 답안

```py
def solution(numbers):
    return sorted({numbers[i] + numbers[j] for i in range(len(numbers) - 1) for j in range(i + 1, len(numbers))})
```