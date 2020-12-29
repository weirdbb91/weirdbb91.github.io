---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 베스트앨범 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-25 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 베스트앨범](https://programmers.co.kr/learn/courses/30/lessons/42579)

사용 언어 자바

장르 별 최다 재생 곡들을 최대 두 개씩 모아 정수 배열로 반환  
노래는 고유 번호(인덱스)로 구분, 수록기준은 다음과 같습니다.

1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
   
### 입력

(곡은 인덱스로 구분함)

- 노래 장르 배열
- 노래 재생 수 배열

### 제한사항

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.

최우선 순위부터 나열하자면  
최다 재생 장르 -> 최다 재생곡 -> 낮은 인덱스  

최소 단위(노래)는 인덱스와 재생수를 가지며,  
장르는 해당 장르의 노래 리스트와 전체 재생수를 가져야했다.  

구현하고나니 왜 해시맵을 쓴건지 납득이 안간다  
저렇게 따로 정렬해버릴거면 장르 클래스를 만들어  
전체 재생수와 노래 리스트를 넣는게 나았을것 같다  
역시 아직도 부족한게 정말 터무니없이 많다  

문제를 차분하게 봐야되는데 그러질 못한다  
시간제한이 있는것도 아닌데 항상 다급하다  
경험부족이 초조함을 부르는것 같다  
반복숙달이 요구됨  

### 제출 답안

```java
class Solution {
    public int[] solution(String[] genres, int[] plays) {
        HashMap<String, HashMap<Integer, Integer>> total = new HashMap<>();
        for (int i = 0; i < genres.length; i++) {
            if (!total.containsKey(genres[i])) {
                total.put(genres[i], new HashMap<Integer, Integer>(){{ put(-1, 0); }});
            }
            HashMap<Integer, Integer> temp = total.get(genres[i]);
            temp.put(-1, (temp.get(-1) + plays[i]));
            temp.put(i, plays[i]);
        }

        List<Integer> answer = new ArrayList<>();
        List<String> totalList = new ArrayList<>(total.keySet());
        totalList.sort((a, b) -> total.get(b).get(-1) - total.get(a).get(-1));
        for (String i : totalList) {
            HashMap<Integer, Integer> temp = total.get(i);
            List<Integer> songs = new ArrayList<>(temp.keySet());
            songs.sort((a, b) -> temp.get(b) - temp.get(a));
            for (int j = 1; j < temp.size() && j <= 2; j++) {
                answer.add(songs.get(j));
            }
        }
        return answer.stream().mapToInt(Integer::intValue).toArray();
    }
}
```