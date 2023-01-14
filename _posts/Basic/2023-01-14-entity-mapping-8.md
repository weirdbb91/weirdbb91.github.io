---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Entity FetchType # 제목
excerpt             : JPA DB 즉시로딩과 지연로딩 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Entity FetchType
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity 매핑에서 즉시로딩과 지연로딩에 대한 내용

## 정의

- 즉시로딩
  - **FetchType.EAGER**
  - 엔티티 조회시, 엔티티와 연관관계에 있는 다른 엔티티들을 함께 조회  
- 지연로딩
  - **FetchType.LAZY**
  - 엔티티 조회시, 해당 엔티티만 조회하고  
    엔티티와 연관관계에 있는 다른 엔티티들을 프록시 객체로 생성해  
    해당 프록시 객체가 사용되는 시점에 추가로 조회

## 사용예시

```java
@Entity
public class Team {

    // 즉시로딩(EAGER)의 경우, 조회하는 Team의 수 N 만큼  
    // 각 embers를 추가로 조회하는 SQL 쿼리가 발생
    // Team들의 각 members 조회 N번 + Team 조회 1번 = N + 1
    @OneToMany(fetch = FetchType.EAGER)
    private List<Member> members;
    ...
}
```

## 주의사항

- 즉시로딩은 실무에서 사용하기에 부적합
- 즉시로딩을 사용하면 예상하지 못한 SQL이 발생
- 즉시로딩은 JPQL에서 N + 1 문제를 일으킨다
- @...ToOne 애노테이션은 즉시로딩이 기본값
  - @...ToOne(fetch = FetchType.LAZY)로 변경해야함
- @...ToMany 애노테이션은 지연로딩이 기본값
