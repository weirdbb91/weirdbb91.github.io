---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 정수 삼각형 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-24 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 정수 삼각형](https://programmers.co.kr/learn/courses/30/lessons/43105)

사용 언어 자바

### 입력

- 정삼각형 모양 정수 배열

### 제한사항
- 삼각형의 높이는 1 이상 500 이하입니다.
- 삼각형을 이루고 있는 숫자는 0 이상 9,999 이하의 정수입니다.

꼭대기에서 바닥까지 이어지는 경로 중, 대각선으로만 거쳐내려간 숫자의 합이 가장 큰 경우를 반환  

이건 왜 레벨 3인지 모르겠다
아랫줄에서부터 이동 가능한 경로의 숫자중 더 큰 수를 골라 저장해 올라가는 방식으로 풀었다

### 제출 답안
```java
public int solution(int[][] triangle) {
    for (int i = triangle.length - 2; i >= 0; i--) {
        for (int j = triangle[i].length - 1; j >= 0; j--) {
            triangle[i][j] += Math.max(triangle[i + 1][j], triangle[i + 1][j + 1]);
        }
    }
    return triangle[0][0];
}
```