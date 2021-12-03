---
title               : 괄호 회전하기 # 제목
excerpt             : 프로그래머스 문제(파이썬) # 썸네일 한줄 요약
categories          : Algorithm 문제풀이
tags                : Programmers Solution Python
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 괄호 회전하기](https://programmers.co.kr/learn/courses/30/lessons/76502)

사용 언어 파이썬

### 문제 설명
다음 규칙을 지키는 문자열을 올바른 괄호 문자열이라고 정의합니다.

- (), [], {} 는 모두 올바른 괄호 문자열입니다.
- 만약 A가 올바른 괄호 문자열이라면, (A), [A], {A} 도 올바른 괄호 문자열입니다. 예를 들어, [] 가 올바른 괄호 문자열이므로, ([]) 도 올바른 괄호 문자열입니다.
- 만약 A, B가 올바른 괄호 문자열이라면, AB 도 올바른 괄호 문자열입니다. 예를 들어, {} 와 ([]) 가 올바른 괄호 문자열이므로, {}([]) 도 올바른 괄호 문자열입니다.

대괄호, 중괄호, 그리고 소괄호로 이루어진 문자열 s가 매개변수로 주어집니다.  
이 s를 왼쪽으로 x (0 ≤ x < (s의 길이)) 칸만큼 회전시켰을 때 s가 올바른 괄호 문자열이 되게 하는 x의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한사항
- s의 길이는 1 이상 1,000 이하입니다.

### 입출력 예

|s|result|
|--|--|
|"[](){}"|3|
|"}]()[{"|2|
|"[)(]"|0|
|"}}}"|0|

---


### 제출 답안

```py
BRAKETS = {
    "(": ")",
    "{": "}",
    "[": "]"
}

# 올바른 괄호 문자열이면 1을 반환, 아니면 0
def is_valid_parentheses(string) -> int:
    stack = []
    for d in string:
        if d in BRAKETS:
            stack.append(d)
            continue
        if not stack or d != BRAKETS[stack.pop()]:
            return 0
    return int(not stack)
    
def solution(s):
    answer = 0
    # 문자열을 회전하며 순회
    for i in range(len(s)):
        answer += is_valid_parentheses(s[i:] + s[:i])
    return answer
```