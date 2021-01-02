---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 가장 긴 팰린드롬 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-01-02 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 가장 긴 팰린드롬](https://programmers.co.kr/learn/courses/30/lessons/12904)

사용 언어 자바

### 입력

- 문자열 s

앞뒤를 뒤집어도 똑같은 문자열을 팰린드롬(palindrome)이라고 합니다.
문자열 s가 주어질 때, 가장 긴 s의 부분문자열(Substring)의 길이를 return.

문자열 s가 `abcdcba`이면 7, `aba`cde이면 3.

### 제한사항

- 문자열 s의 길이 : 2,500 이하의 자연수
- 문자열 s는 알파벳 소문자로만 구성


### 제출 답안

```java
public int solution(String s) {
    int answer = 1;
    int len = s.length();
    int dis = 0;
    int center = len / 2;

    // 검사 기준의 중심이 양쪽으로 멀어지는 방식

    while (center < len) {
        if (0 <= center - 1) {                              // 짝
            answer = Math.max(answer, comp(s, center - 1, center));
        }
        
        if (0 <= center - 1 && center + 1 < len) {          // 홀
            answer = Math.max(answer, comp(s, center - 1, center + 1));
        }

        if (answer >= len) break;

        if (dis <= 0) {         // 문자열의 중심으로부터 멀어질 거리
            dis *= -1;
            dis++;
        } else {
            dis *= -1;
        }
        center = len / 2 + dis;
    }
    return answer;
}

public int comp(String s, int head, int tail) {
    int len = s.length();
    while (s.charAt(head) == s.charAt(tail)) {
        head--;
        tail++;
        if (0 > head || tail >= len) break;
    }
    return tail - head - 1;
}
```