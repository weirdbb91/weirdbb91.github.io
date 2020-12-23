---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 자물쇠와 열쇠 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-22 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 자물쇠와 열쇠](https://programmers.co.kr/learn/courses/30/lessons/60059)

사용 언어 자바

### 입력

- M x M 배열(열쇠)
- N x N 배열(자물쇠)

### 제한사항
- key는 M x M(3 ≤ M ≤ 20, M은 자연수)크기 2차원 배열입니다.
- lock은 N x N(3 ≤ N ≤ 20, N은 자연수)크기 2차원 배열입니다.
- M은 항상 N 이하입니다.
- key와 lock의 원소는 0 또는 1로 이루어져 있습니다.
- 0은 홈 부분, 1은 돌기 부분을 나타냅니다.

열쇠를 움직이고 돌려가며(열쇠가 자물쇠 범위 밖으로 나가도 됨)  
자물쇠 범위에 모든 값이 전부 1이 될 수 있는지 boolean 반환  

### 풀이과정

한 30분 동안 뭘 놓친건지 한참을 찾아 헤맸지만  
못찾아서 그냥 무식하게 풀기로 했다  

유효한 범위(자물쇠)는 고정시키고 가중치를 이용해서  
열쇠의 좌표를 바꿔가며 확인해보기로 했다  

우선 열쇠 끝 - 자물쇠 시작부터 열쇠 시작 - 자물쇠 끝의 범위인  
열쇠 길이 + 자물쇠 길이 - 1을 가중치의 범위로 정했다  

keyHas 메소드로 확인 중인 자물쇠의 좌표와 가중치를 받아  
결과 값이 열쇠의 좌표 범위 내에 있는지 반환했다

그리고 rotate 메소드로 열쇠를 회전시켰다  
꽤 복잡할 줄 알았는데  
[y][x] 위치에 [(길이 - 1) - x][y] 값을 저장하면 됐다  

실행해보고 잘 되는것 같길래 출력문들만 주석처리하고  
제출했는데 바로 통과했다 한번에 통과한건 처음이었다   

### 제출 답안
```java
class Solution {
    public boolean solution(int[][] key, int[][] lock) {
        for (int i = 0; i < 4; i++) {
            if (check(key, lock)) return true;
            key = rotate(key);
        }
        return false;
    }

    // rotate the key 90 degrees
    public int[][] rotate(int[][] key) {
        int len = key.length;
        int[][] newKey = new int[len][len];
        for (int y = 0; y < len; y++) {
            for (int x = 0; x < len; x++) {
                newKey[y][x] = key[len - 1 - x][y];
            }
        }
        return newKey;
    }

    // yx [weight boundary] 0 to lock.length + key.length - 1
    public boolean check(int[][] key, int[][] lock) {
        int maxWeight = lock.length + key.length;
        for (int y = 0; y < maxWeight; y++) {
            for (int x = 0; x < maxWeight; x++) {
                if (match(key, lock, y, x)) return true;
                // System.out.println("fail");
            }
        }
        return false;
    }

    public boolean match(int[][] key, int[][] lock, int y, int x) {
        // System.out.println("Weight y[" + y + "] x[" + x + "]");
        int pad = key.length - 1;
        int point;
        for (int i = 0; i < lock.length; i++) {
            for (int j = 0; j < lock.length; j++) {
                point = lock[i][j];
                if (keyHas(pad, i, y) && keyHas(pad, j, x)) {
                    point += key[i + pad - y][j + pad - x];
                }
                // System.out.print(point);
                if (point != 1) return false;
            }
            // System.out.println();
        }
        return true;
    }

    public boolean keyHas(int pad, int base, int weight) {
        return (0 <= base + pad - weight) && (base + pad - weight <= pad);
    }
}
```