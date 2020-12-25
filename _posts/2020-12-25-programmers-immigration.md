---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 입국심사 # 제목
excerpt             : 프로그래머스 문제 # 썸네일 한줄 요약
last_modified_at    : 2020-12-25 # 마지막 수정일
categories          : etc
tags                : Programmers Solution Java
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 [프로그래머스 - 입국심사](https://programmers.co.kr/learn/courses/30/lessons/43238)

사용 언어 자바

### 입력

- 심사 받을 인원 수 n
- 심사관별 심사 소요시간 배열

### 제한사항
- 입국심사를 기다리는 사람은 1명 ~ 1,000,000,000명입니다.
- 각 심사관의 심사 소요시간은 1분 ~ 1,000,000,000분입니다.
- 심사관은 1명 ~ 100,000명입니다.

최소 심사 소요시간 반환


### 첫번째 제출 답안 (실패 : 시간초과)

```java
class Solution {
    public long solution(int n, int[] times) {
        long answer = 0;
        PriorityQueue<Examiner> examiners = new PriorityQueue<>(
            (a, b) -> Long.compare(a.endTime(), b.endTime()));
        
        Arrays.stream(times).forEach(i -> examiners.add(new Examiner(0, i)));
        
        for (int i = 0; i < n; i++) {
            answer = Math.max(answer, examiners.peek().endTime());
            examiners.peek().immigrate();
            examiners.add(examiners.poll());
        }
        
        return answer;
    }

}

class Examiner {
    private long ready;
    private int delayTime;

    public Examiner(long ready, int delayTime) {
        this.ready = ready;
        this.delayTime = delayTime;
    }
    
    public void immigrate() { ready += delayTime; }
    
    public long endTime() { return ready + delayTime; }
}
```

고친다고 통과될것 같지 않을 정도로 많이 시간초과됐다  
접근 자체가 잘못됐다는 것  

심사가 끝나도 다음심사 종료 예정시간이 다른 심사관보다 길면  
심사를 하지 않는다 휴식이 아닌 퇴근인 것이었다  

역시 뭔가 재귀나 특정 자료구조가 아닌 단순 연산 문제가 아닐까  
노트에 시간에 따른 두 심사관의 업무를 그려보니 공식이 있는것 같았다  

n = (정답 / 심사관1 소요시간) + (정답 / 심사관2 ..) + (답 / 심3) ...  

정답 시점의 시간에는 이미 퇴근한 심사관도 있으니 이 공식은 틀렸다  
그러나 소수점을 버린다면 정답에 부합했다  

정답의 조건을 찾은 것이다  

### 제출 답안

```java
public long solution(int n, int[] times) {
    long minTime = 1L;
    long maxTime = (long) times[times.length - 1] * n;
    long answer = maxTime;
    long average;
    long coverage;

    while (minTime <= maxTime) {
        average = (minTime + maxTime) / 2;
        coverage = 0;

        for (int time : times) coverage += average / time;

        if (coverage < n) minTime = average + 1;
        if (coverage >= n) {
            answer = Math.min(answer, average);
            maxTime = average - 1;
        }
    }
    return answer;
}
```

- maxTime 값을 롱형으로 캐스팅 안해줘서 인트 범위를 넘어버려 실패
- 반복문의 조건을 minTime < maxTime으로 해서 실패
- answer 초기값을 Integer.MAX_VALUE로 해서 인트 범위초과 답을 반환 못해 실패