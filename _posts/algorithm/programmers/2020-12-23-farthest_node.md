---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 가장 먼 노드 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-23 # 마지막 수정일
categories          : Algorithm 문제풀이
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 가장 먼 노드](https://programmers.co.kr/learn/courses/30/lessons/49189)

사용 언어 자바

### 입력

- 노드 갯수 n
- 양방향 간선 배열(가중치 없음)

### 제한사항

- 노드의 개수 n은 2 이상 20,000 이하입니다.
- 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
- vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.

1번 노드에서 출발했을때 가장 먼 거리에 해당하는 노드들의 갯수를 반환하시오  

이 문제는 생각없이 풀었다가 시간 복잡도가 초과되어 통과하지 못했었다  
쓸데없이 괜히 스트림을 써봤다

### 제출 답안
```java
public int solution(int n, int[][] edge) {
    int max = 0;
    int[] nodes = new int[n];
    for (int i = 1; i < n; i++) nodes[i] = 50000;
    List<Integer> visited = new ArrayList<>();
    List<Integer> willGo = new ArrayList<>();
    willGo.add(1);

    List<Integer>[] bridges = new ArrayList[n];
    for (int i = 0; i < n; i++) bridges[i] = new ArrayList<>();
    for (int[] i : edge) {
        bridges[i[0] - 1].add(i[1]);
        bridges[i[1] - 1].add(i[0]);
    }

    while (!willGo.isEmpty()) {
        int arrived = willGo.remove(0);
        for (int near : bridges[arrived - 1]) {
            nodes[arrived - 1] = Math.min(nodes[arrived - 1], (nodes[near - 1] + 1));
            if (!visited.contains(near) && !willGo.contains(near)) willGo.add(near);
        }
        visited.add(arrived);
        max = Math.max(max, nodes[arrived - 1]);
    }
    int finalMax = max;
    return (int) Arrays.stream(nodes).filter(i -> i == finalMax).count();
}
```