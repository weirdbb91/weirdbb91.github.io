---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 보행자 천국 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-26 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 보행자 천국](https://programmers.co.kr/learn/courses/30/lessons/1832)

사용 언어 자바

지도는 m × n 크기의 격자 모양 배열 city_map으로 주어진다.  
자동차는 오른쪽 또는 아래 방향으로 한 칸씩 이동 가능하다.  

city_map[i][j]에는 도로의 상황을 나타내는 값이 저장되어 있다.  

도로 상황 종류
- 0 : 자동차가 자유롭게 지나갈 수 있다.
- 1 : 자동차 통행이 금지되어 지나갈 수 없다.
- 2 : 진입한 방향 그대로 한칸 더 간다.

좌상단 끝에서 우하단 끝까지 이동 가능한 전체 가능한 경로 수를 반환하라.  
가능한 경로 수를 20170805로 나눈 나머지 값을 출력하라.  

### 입력

- 지도 가로 m
- 지도 세로 n
- 도로 상황 배열 city_map
  
### 제한사항

- 1 <= m, n <= 500
- city_map의 크기는 m × n이다.
- 배열의 모든 원소의 값은 0, 1, 2 중 하나이다.
- 출발점의 좌표는 (0, 0), 도착점의 좌표는 (m - 1, n - 1)이다.
- 출발점과 도착점의 city_map[i][j] 값은 0이다.

도로 상황 2(진입방향 그대로 한칸더)를 제외하면  
바로 전에 했던 등굣길과 흡사해서 비교적 수월했다  


### 제출 답안

```java
public int solution(int m, int n, int[][] cityMap) {
    int[][] map = new int[m + 1][n + 1];
    map[1][0] = 1;      // map idx = cityMap idx + 1
    int up, left, straight;
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            if (cityMap[i][j] != 0) continue;
            
            straight = 1;
            while (i - straight > 0 && cityMap[i - straight][j] == 2) straight++;
            up = map[i + 1 - straight][j + 1];

            straight = 1;
            while (j - straight > 0 && cityMap[i][j - straight] == 2) straight++;
            left = map[i + 1][j + 1 - straight];

            map[i + 1][j + 1] = (up + left) % 20170805;
        }
    }
    return map[m][n] % 20170805;
}
```