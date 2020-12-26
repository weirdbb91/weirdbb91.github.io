---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 여행경로 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-25 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 여행경로](https://programmers.co.kr/learn/courses/30/lessons/43164)

사용 언어 자바

### 입력

- \{\{출발지, 도착지\}가 담긴 배열 형태의 항공권, ... \} 배열

주어진 항공권을 모두 이용하여 여행경로를 짜라.  
항상 ICN 공항에서 출발합니다.  

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때,  
방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한사항
- 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
- 주어진 공항 수는 3개 이상 10,000개 이하입니다.
- tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
- 주어진 항공권은 모두 사용해야 합니다.
- 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
- 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.


### 제출 답안

```java
class Solution {
    public String[] solution(String[][] tickets) {
        // 알파벳 순으로 우선순위(출발지 > 도착지) 정렬
        Arrays.sort(tickets, (a, b) -> a[0].compareTo(b[0]) == 0 ? a[1].compareTo(b[1]) : a[0].compareTo(b[0]));
        Queue<String[]> ticketQ = new LinkedList<>();
        Stack<String[]> route = new Stack<>();
        route.add(new String[]{"", "ICN"});
        ticketQ.addAll(Arrays.asList(tickets));
        flight(ticketQ, route);

        return route.stream().map(i -> i[1]).toArray(String[]::new);
    }

    public void flight(Queue<String[]> ticketQ, Stack<String[]> route) {
        // 항공권 모두 사용시 종료
        if (route.size() == ticketQ.size() + 1) return;     // <- !! 삭제가능 중복코드 
        int startedIdx = route.size();      // 현 위치 저장
        List<String[]> choices = new ArrayList<>();
        // 이동 가능 경로 선별
        ticketQ.stream().filter(i -> i[0].equals(route.peek()[1]) && !route.contains(i)).forEach(choices::add);
        if (choices.isEmpty()) return;      // 이동불가시 종료

        for (String[] way : choices) {
            route.add(way);
            flight(ticketQ, route);
            // 항공권 모두 사용시 종료
            if (route.size() == ticketQ.size() + 1) return;
            // 항공권이 남은채 이동불가시 저장된 위치로 귀환
            while (route.size() > startedIdx) route.pop();
        }
    }
}
```