---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Entity Relationship # 제목
excerpt             : JPA DB 매핑 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Database Entity Relationship
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity Mapping 중 연관관계 설정에 대한 내용

### 용어 정리

- 방향(Direction)
  - 단방향, 양방향
- 다중성(Multiplicity)
  - 일대일(1:1), 일대다(1:N), 다대일(N:1), 다대다(N:N)
- 연관관계의 주인(Owner)
  - 객체 양방향 연관관계에서 관리를 하는 주인

---

### 객체와 테이블의 괴리

- 테이블은 외래 키로 JOIN을 사용해 연관된 테이블을 찾는다
- 객체는 참조를 사용해 연관된 객체를 찾는다
- 테이블은 한쪽에만 외래 키를 가지고 있다(연관관계 1개)
- 객체는 양쪽의 단방향 관계로 양방향 관계를 완성한다(연관관계 2개)
  - 사실 양방향은 없다 -> 양쪽에 단방향이 있다

#### 연관관계의 주인(Owner)

양방향 매핑 규칙

- 객체의 두 관계 중 하나를 연관관계의 주인으로 지정
- 연관관계의 주인만이 외래 키를 관리(등록, 수정)
- 주인이 아닌쪽은 읽기만 가능
- 주인은 mappedBy 속성 사용 X
- 주인이 아니면 mappedBy 속성으로 주인을 명시

#### 주인 선정 방법

- 비즈니스 로직을 기준으로 선택하면 안됨
- 외래 키가 있는 쪽이 주인
- 다수(N)쪽이 주인

---

### 관계 예시

#### 단방향 다대일 관계 예시

```java
// Member.java

@ManyToOne // 현재 객체가 다(N), Team 객체가 일(1)인 관계임을 명시
@JoinColumn(name = "TEAM_ID") // Team 객체의 테이블과 JOIN 할 때 사용할 컬럼("TEAM_ID")을 명시
private Team team;
```

#### 양방향 다대일 관계 예시

```java
// Member.java (위 단방향 다대일 관계 예시와 동일)

@ManyToOne // 현재 객체가 다(N), Team 객체가 일(1)인 관계임을 명시
@JoinColumn(name = "TEAM_ID") // Team 객체의 테이블과 JOIN 할 때 사용할 컬럼("TEAM_ID")을 명시
private Team team;
```

```java
// Team.java

@OneToMany(mappedBy = "team") // 상대편 객체의 어떤 필드와 매핑이 되는건지 명시
private List<Member> members;
```

---

### 주의사항

- 양방향 매핑시에 무한루프를 주의
  - toString(), lombok, JSON 생성 라이브러리 등
- 어느 한쪽에는 관계의 생성 또는 수정 사항을 반영했더라도 반대편에는 하지 않을 수 있다  

    ```java
    team.getMembers().add(member);
    em.persist(member); // member에는 변경 사항이 없기 때문에 반영되지 않는다.
    ```

- 연관관계 편의 메소드 사용을 권장

    ```java
    // Member class method
    public void changeTeam(Team team) {
        this.team = team;
        team.getMembers().add(this);
    }

    // 또는

    // Team class method
    public void addMember(Member member) {
        member.setTeam(this);
        this.members.add(member);
    }
    ```

- 단방향 연관관계만 잘 매핑 설정해두면,  
    양방향은 필요할 때 추가해도 된다
