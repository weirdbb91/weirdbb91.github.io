---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA 영속성전이 # 제목
excerpt             : JPA 영속성전이 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA CASCADE
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA 영속성전이에 대한 내용

## 정의

엔티티객체의 영속을 전이시키는 옵션

### 문제 상황 예시

```java
@Entity
public class Parent {
    ...
    @OneToMany(mappedBy = "parent")
    private List<Child> childList = new ArrayList<>();
    ...
}
```

```java
Child child1 = new Child();
Child child2 = new Child();

Parent parent = new Parent();
parent.add(child1);
parent.add(child2);

// 각 엔티티 객체별로 전부 영속을 해줘야 함
em.persist(child1);
em.persist(child2);
em.persist(parent);
```

### 개선 상황 예시

```java
@Entity
public class Parent {
    ...
    // 하위 엔티티에 영속성전이 타입 지정
    @OneToMany(mappedBy = "parent", cascade = CascadeType.ALL)
    private List<Child> childList = new ArrayList<>();
    ...
}
```

```java
Child child1 = new Child();
Child child2 = new Child();

Parent parent = new Parent();
parent.add(child1);
parent.add(child2);

// 영속하는 엔티티와 연관된 객체들을 자동으로 영속해줌
em.persist(parent);
```

## 종류

- CascadeType.ALL
  - 모두 적용
- CascadeType.PERSIST
  - 연관된 하위 자식 엔티티까지 연쇄적으로 영속 수행
- CascadeType.REMOVE
  - 연관된 하위 자식 엔티티까지 연쇄적으로 삭제 수행
- CascadeType.MERGE
  - 연관된 하위 자식 엔티티까지 연쇄적으로 병합 수행
- CascadeType.REFRESH
  - 연관된 하위 자식 엔티티까지 연쇄적으로 새로고침 수행
- CascadeType.DETACH
  - 연관된 하위 자식 엔티티까지 연쇄적으로 준영속 수행

> **PERSIST와 MERGE의 차이**  
> 출처 : [umanking's blog](https://umanking.github.io/2019/04/12/jpa-persist-merge/)  
>  
> JpaRepository의 구현체 SimpleJpaRepository에서  
> save() 메소드의 파라미터가 **새로운 entity이면 persist()**를,  
> (entityInformation.isNew()에서 true)  
>  
> 그게 **아니면 merge()를 호출**한다.  
>  
> merge는 한번 persist 상태였다가 detached 된 상태에서  
> 다시 persist 상태가 될 때, merge 한다고 한다.
>  
> `요약 : 없던거면 persist, 있던거면 merge`

## 주의사항

- 영속성전이는 연관관계를 매핑하는것과 아무런 관련이 없음  
- 편의성 외에는 그 어떤 의미도 가지지 않는다  
- 엔티티가 특정 엔티티를 소유하는 관계(단일 소유자)일 때만 사용한다
  - 다른 제 3의 엔티티가 연관이 있다면,  
    의도치 않게 삭제되거나 생성되는 문제가 발생할 수 있다
