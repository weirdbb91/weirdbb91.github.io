---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : ThreadLocal # 제목
excerpt             : Java ThreadLocal # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java ThreadLocal
---

출처 : [[SpringBoot] ThreadLocal 간단 정리](https://jaimemin.tistory.com/2007)

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

ThreadLocal에 대한 내용  

---

## 내용

### 배경 설명

Spring의 bean들은 Spring Container에 의해 Singleton으로 관리된다.  
(static 같은 공용 필드 또한 마찬가지)  
이러한 방식은 다수의 Thread가 접근하게 되면 동시성 이슈가 발생할 가능성이 높다.  

위와 같은 문제들을 해결하기 위한 Java객체가 ThreadLocal이다.  

---

### ThreadLocal 설명

ThreadLocal은 Thread만 접근할 수 있는 일종의 저장소이다.  
ThreadLocal이 각 Thread들을 식별해, 각각의 저장소를 구분한다.  

ThreadLocal의 method list:

- get(): 조회
- set(): 저장
- remove(): 초기화

---

### 주의사항

1. **메모리 누수의 위험**이 있다.
2. **Tomcat같은 WAS**의 경우, Thread 생성 비용이 커서  
    자체적으로 Thread Pool을 운용하는데  
    이 때, **Thread를 재사용**하게 된다.
   - 재사용된 Thread의 경우, **이전 작업 데이터**가  
        저장소에 **그대로 남아있어 매우 위험**하다.
3. ThreadLocal은 Thread를 반환할 때
    remove() 메소드로 반드시 초기화 해야한다.
   - Thread가 반환될 때 Intercepter 또는 Filter에서  
        초기화하는 것이 바람직하다.
