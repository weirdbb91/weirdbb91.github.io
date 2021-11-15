---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 등굣길 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-26 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 등굣길](https://programmers.co.kr/learn/courses/30/lessons/42898)

사용 언어 자바

### 입력

- 지도 가로 m
- 지도 세로 n
- 침수지 좌표 배열


집 좌표는 (1, 1), 학교 좌표는 (m, n)으로 나타냅니다.

격자의 크기 m, n과 침수지 좌표를 담은 2차원 배열 puddles이 주어집니다.  
오른쪽과 아래쪽으로만 움직여 집에서 학교까지 갈 수 있는 최단경로의 개수를  
1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.  

### 제한사항

- 격자의 크기 m, n은 1 이상 100 이하인 자연수입니다.
- m과 n이 모두 1인 경우는 입력으로 주어지지 않습니다.
- 물에 잠긴 지역은 0개 이상 10개 이하입니다.
- 집과 학교가 물에 잠긴 경우는 입력으로 주어지지 않습니다.


재귀로 풀다가 막혔다  
한참 고민하다가 경우의 수가 파스칼의 삼각형과 일치한다는걸 알아냈고  
침수지 기준으로 좌상단, 우하단 상자들의 경우의 수(침수지를 지나는 경우의 수)를  
전체 경우의 수에서 빼봤다  

침수지가 다수라 중복되는 경우의 수들이 생겨, 반환값이 음수로 나오기도 했다

또 한참 막히다가 침수지를 0으로 치환해서 계속 계산하면 된다는걸 발견했고  
정답인줄 알았는데 벽쪽의 침수지 이후로는 경우의 수가 생기지 않는다는걸 몰랐다

### 제출 답안

```java
public int solution(int m, int n, int[][] puddles) {
    int[][] cases = new int[m][n];        
    for (int[] p : puddles) cases[p[0] - 1][p[1] - 1] = -1;
    int outLine = 1;
    for (int i = 0; i < m; i++) {
        if (cases[i][0] == -1) outLine = 0;
        cases[i][0] = outLine;
    }
    outLine = 1;
    for (int j = 1; j < n; j++) {
        if (cases[0][j] == -1) outLine = 0;
        cases[0][j] = outLine;
    }

    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (cases[i][j] == -1) {
                cases[i][j] = 0;
                continue;
            }
            cases[i][j] = (cases[i - 1][j] + cases[i][j - 1]) % 1000000007;
        }
    }
    return cases[m - 1][n - 1] % 1000000007;
}
```

통과 이후 다른 사람의 풀이를 봤더니 정말 깔끔한 코드들이 많았다