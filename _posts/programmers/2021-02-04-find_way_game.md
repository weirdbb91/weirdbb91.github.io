---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 길 찾기 게임 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-02-04 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 길 찾기 게임](https://programmers.co.kr/learn/courses/30/lessons/42892)

사용 언어 자바

### 문제 설명

노드들을 입력받아 이진트리로 만들어 전위, 후위 순회 결과를 반환

- 트리를 구성하는 모든 노드의 x, y 좌표 값은 정수이다.  
- 모든 노드는 서로 다른 x값을 가진다.  
- 같은 레벨(level)에 있는 노드는 같은 y 좌표를 가진다.  
- 자식 노드의 y 값은 항상 부모 노드보다 작다.  
- 임의의 노드 V의 왼쪽 서브 트리(left subtree)에 있는 모든 노드의 x값은 V의 x값보다 작다.  
- 임의의 노드 V의 오른쪽 서브 트리(right subtree)에 있는 모든 노드의 x값은 V의 x값보다 크다.  

입력 예 :
[[5,3],[11,5],[13,3],[3,5],[6,1],[1,3],[8,6],[7,2],[2,2]]

출력 예 :
[[7,4,6,9,1,8,5,2,3],[9,6,5,8,1,4,3,2,7]]

### 제한사항
- nodeinfo는 이진트리를 구성하는 각 노드의 좌표가 1번 노드부터 순서대로 들어있는 2차원 배열이다.
- nodeinfo의 길이는 1 이상 10,000 이하이다.
- nodeinfo[i] 는 i + 1번 노드의 좌표이며, [x축 좌표, y축 좌표] 순으로 들어있다.
- 모든 노드의 좌표 값은 0 이상 100,000 이하인 정수이다.
- 트리의 깊이가 1,000 이하인 경우만 입력으로 주어진다.
- 모든 노드의 좌표는 문제에 주어진 규칙을 따르며, 잘못된 노드 위치가 주어지는 경우는 없다.

### 입력

- x, y 정보를 가진 노드 배열 nodeinfo


혹시나 굉장한 풀이방법이 있지않을까해서 고민하다가 포기했다 


### 제출 답안

```java
import java.util.*;
import java.util.stream.Collectors;

class Solution {
    public int[][] solution(int[][] nodeinfo) {
        List<Node> nodes = new ArrayList<>();
        for (int i = 0; i < nodeinfo.length; i++) {
            nodes.add(new Node(i + 1, nodeinfo[i][0], nodeinfo[i][1]));
        }
        
        nodes.sort(nodes, (a, b) -> b.y - a.y);
        
        List<Integer> pre = new ArrayList<>();
        List<Integer> post = new ArrayList<>();
        order(divide(nodes), pre, post);
        
        return new int[][]{ pre.stream().mapToInt(i->i).toArray(),
                            post.stream().mapToInt(i->i).toArray() };
    }
    
    public void order(Node p, List<Integer> pre, List<Integer> post) {
        pre.add(p.num);
        if (p.left != null) order(p.left, pre, post);
        if (p.right != null) order(p.right, pre, post);
        post.add(p.num);
    }
    
    public Node divide(List<Node> nodes) {
        if (nodes.size() <= 0) return null;
        
        Node parent = nodes.get(0);
        parent.left = divide(nodes.stream()
            .filter(a -> a.x < parent.x).collect(Collectors.toList()));
        parent.right = divide(nodes.stream()
            .filter(a -> a.x > parent.x).collect(Collectors.toList()));
        
        return parent;
    }
}

class Node {
    Node left = null;
    Node right = null;
    int num;
    int x;
    int y;
    
    Node(int num, int x, int y) {
        this.num = num;
        this.x = x;
        this.y = y;
    }
}
```