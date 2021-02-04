---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 기둥과 보 설치 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2021-02-04 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 기둥과 보 설치](https://programmers.co.kr/learn/courses/30/lessons/60061)

사용 언어 자바

### 제한 사항

- n은 5 이상 100 이하인 자연수입니다.
- build_frame의 세로(행) 길이는 1 이상 1,000 이하입니다.
- build_frame의 가로(열) 길이는 4입니다.
- build_frame의 원소는 [x, y, a, b]형태입니다.
  - x, y는 기둥, 보를 설치 또는 삭제할 교차점의 좌표이며, [가로 좌표, 세로 좌표] 형태입니다.
  - a는 설치 또는 삭제할 구조물의 종류를 나타내며, 0은 기둥, 1은 보를 나타냅니다.
  - b는 구조물을 설치할 지, 혹은 삭제할 지를 나타내며 0은 삭제, 1은 설치를 나타냅니다.
  - 벽면을 벗어나게 기둥, 보를 설치하는 경우는 없습니다.
  - 바닥에 보를 설치 하는 경우는 없습니다.
- 구조물은 교차점 좌표를 기준으로 보는 오른쪽, 기둥은 위쪽 방향으로 설치 또는 삭제합니다.
- 구조물이 겹치도록 설치하는 경우와, 없는 구조물을 삭제하는 경우는 입력으로 주어지지 않습니다.
- 최종 구조물의 상태는 아래 규칙에 맞춰 return 해주세요.
  - return 하는 배열은 가로(열) 길이가 3인 2차원 배열로, 각 구조물의 좌표를 담고있어야 합니다.
  - return 하는 배열의 원소는 [x, y, a] 형식입니다.
  - x, y는 기둥, 보의 교차점 좌표이며, [가로 좌표, 세로 좌표] 형태입니다.
  - 기둥, 보는 교차점 좌표를 기준으로 오른쪽, 또는 위쪽 방향으로 설치되어 있음을 나타냅니다.
  - a는 구조물의 종류를 나타내며, 0은 기둥, 1은 보를 나타냅니다.
  - return 하는 배열은 x좌표 기준으로 오름차순 정렬하며, x좌표가 같을 경우 y좌표 기준으로 오름차순 정렬해주세요.
  - x, y좌표가 모두 같은 경우 기둥이 보보다 앞에 오면 됩니다.

- 기둥은 바닥 위에 있거나 보의 한쪽 끝 부분 위에 있거나, 또는 다른 기둥 위에 있어야 합니다.
- 보는 한쪽 끝 부분이 기둥 위에 있거나, 또는 양쪽 끝 부분이 다른 보와 동시에 연결되어 있어야 합니다.

### 입력

- 격자 가로 세로 길이 n
- [x, y, a, b]형태의 작업 배열 build_frame


끔찍한 경험이었다

### 제출 답안

```java
import java.util.*;

class Solution {
    public int[][] solution(int n, int[][] build_frame) {
        int[][] frame = new int[n + 1][n + 1];          // 설치 현황 지도
        ArrayList<int[]> result = new ArrayList<>();

        for (int[] temp : build_frame) {
            int type = temp[2] == 0 ? 1 : 10;           // 0(기둥) = 1, 1(보) = 10

            if (temp[3] == 1) {                         // -설치-
                // if (result.contains(temp)) continue;    // 이미 설치됨 -> 생략

                result.add(temp);                       // 임시 설치
                frame[temp[0]][temp[1]] += type;

                if (hasProblem(frame, result)) {        // 불합격 -> 철거
                    result.remove(temp);
                    frame[temp[0]][temp[1]] -= type;
                }
            }
            if (temp[3] == 0) {                         // -삭제-
                int[] target = result.stream()          // 삭제 대상 확인
                        .filter(a -> a[0] == temp[0] && a[1] == temp[1] && a[2] == temp[2])
                        .findFirst().orElse(null);

                // if (target == null) continue;           // 그런거 없음 -> 생략

                result.remove(target);                  // 임시 철거
                frame[temp[0]][temp[1]] -= type;

                if (hasProblem(frame, result)) {        // 불합격 -> 재설치
                    result.add(target);
                    frame[temp[0]][temp[1]] += type;
                }
            }
        }

        result.sort((a, b) -> a[0] - b[0] != 0 ? a[0] - b[0]
                            : a[1] - b[1] != 0 ? a[1] - b[1]
                            : a[2] - b[2]);

        int[][] answer = new int[result.size()][3];
        for (int i = 0; i < result.size(); i++) {
            int[] temp = result.get(i);
            answer[i] = new int[]{temp[0], temp[1], temp[2]};
        }
        return answer;
    }

    // 구조물 전체 확인
    public boolean hasProblem(int[][] frame, ArrayList<int[]> result) {
        for (int[] i : result) {
            if ((i[2] == 0 && !validP(frame, i)) ||
                (i[2] == 1 && !validB(frame, i))) return true;
        }
        return false;
    }

    // 기둥 적합성 확인
    public boolean validP(int[][] frame, int[] i) {
        int x = i[0];
        int y = i[1];
        // 바닥 위 || 다른 기둥 위 || 좌측 보 위 || 우측 보 위
        return (y <= 0) || (frame[x][y - 1] % 10 >= 1)
            || (x > 0 && frame[x - 1][y] >= 10) || (frame[x][y] >= 10);
    }

    // 보 적합성 확인
    public boolean validB(int[][] frame, int[] i) {
        int x = i[0];
        int y = i[1];
        int mLen = frame.length - 2;
        // 좌하단 기둥 || 우하단 기둥 || (좌표 범위 확인 && 양쪽 보)
        return (frame[x][y - 1] % 10 == 1) || (frame[x + 1][y - 1] % 10 == 1)
            || ((0 < x && x < mLen) && (frame[x - 1][y] >= 10) && (frame[x + 1][y] >= 10));
    }
}
```