---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA 고아객체제거 orphanRemoval # 제목
excerpt             : JPA 고아객체제거 orphanRemoval # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA CASCADE
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity 매핑에서 @OneTo... 애노테이션의 orphanRemoval 옵션에 대한 내용  

## 정의

연관관계가 모두 끊어진(참조가 제거된) 자식 엔티티 객체를  
고아 객체로 식별하고 자동으로 삭제하는 옵션  

## 사용예시

```java
@Entity
public class Parent {
    ...
    // orphanRemoval 옵션을 활성화 한다
    @OneToMany(mappedBy = "parent", orphanRemoval = true)
    private List<Child> childList = new ArrayList<>();
    ...
}
```

## 자식객체의 생명주기 관리

- cascade = CascadeType.ALL  
- orphanRemoval = true  

위 두 옵션을 사용하면, 부모객체를 통해  
자식객체의 생명주기를 관리할 수 있다  

스스로(JPA를 통해) 생명주기를 관리하는 부모 엔티티는  
em.persist()로 영속화, em.remove()로 제거하며,  
이에 따라 종속된 자식 엔티티의 생명주기가 관리된다  
그렇게되면 자식 엔티티는 Repository가 없어도 된다

이는 도메인 주도 설계(DDD)의 Aggregate Root 개념을 구현할 때 유용하다  

> Repository는 Aggregate Root만 contact한다  
>  
> Aggregate Root 외에는 차라리 Repository를 만들지 않고,  
> Aggregate Root를 통해 생명주기를 관리하는것이 더 낫다  

## 주의사항

- 참조하는 곳이 하나(단일 소유자)일 때만 사용  
- @OneTo... 애노테이션만 가능  
- orphanRemoval 옵션을 활성화하면,  
    부모 객체가 제거 될 때 자식 객체들도 함께 제거 된다  
    이는 CascadeType.REMOVE와 동일하게 동작한다  
