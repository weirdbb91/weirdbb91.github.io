---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 섬 연결하기 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-23 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 섬 연결하기](https://programmers.co.kr/learn/courses/30/lessons/42861)

사용 언어 자바

### 입력

- 브릿지

최소신장트리를 구현하시오

### 풀이과정

문제가 너무 직설적이어서 별 생각없이 바로 풀었다
프림 알고리즘을 이용했다

### 제출 답안
```java
public int solution(int n, int[][] costs) {
    int answer = 0;
    List<int[]> bridgeList = new ArrayList<>();
    List<Integer> connected = new ArrayList<>();

    int firstIsland = 0;
    connected.add(firstIsland);
    for (int[] i : costs) {
        if (i[0] == firstIsland || i[1] == firstIsland) bridgeList.add(i);
    }

    while (connected.size() < n) {
        // sort bridgeList by lowest cost
        Collections.sort(bridgeList, (a, b) -> a[2] - b[2]);

        // pop the lowest cost bridge from bridgeList
        int[] temp = bridgeList.remove(0);

        // islands in temp are all already connected
        if (connected.contains(temp[0]) && connected.contains(temp[1])) continue;

        // take the temp bridge
        int newIsland = -1;
        if (connected.contains(temp[0])) {
            newIsland = temp[1];
        }
        if (connected.contains(temp[1])) {
            newIsland = temp[0];
        }

        // pay the temp bridge's cost
        answer += temp[2];
        connected.add(newIsland);

        for (int[] i : costs) {
            // put all reachable bridges in bridgeList
            if (!bridgeList.contains(i) && (connected.contains(i[0]) && !connected.contains(i[1]) ||
                    connected.contains(i[1]) && !connected.contains(i[0]))) {
                bridgeList.add(i);
            }
        }
    }

    return answer;
}
```