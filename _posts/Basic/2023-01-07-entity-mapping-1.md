---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA auto generate database schema function # 제목
excerpt             : JPA DB 스키마 자동 생성 기능 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Database Schema
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA에서 제공하는 데이터베이스 스키마 자동 생성 기능에 대한 내용

---

## 내용

### 데이터베이스 스키마 자동 생성 기능

- 애플리케이션 실행 시점에 DDL을 자동 생성  
  - 개발 과정에서 애플리케이션 실행시,  
       DB 스키마들을 자동으로 생성해줌  
- 지정한 DB 방언(Dialect)을 활용, DB에 적합한 DDL 생성  
  - 개발 단계에서만 사용할 것.  
    운영서버에서 사용하려면 검토 필수  

#### **사용방법**

하이버네이트 설정 추가  

```java
// gradle application.properties
hibernate.hbm2ddl.auto={옵션 값}
```

옵션 종류

- create
  - 기존 테이블 DROP 후 CREATE
- create-drop
  - create과 동일하나, 종료시점에 DROP 추가
- update
  - 변경부분만 반영(ALTER) - 삭제 사항은 반영되지 않음
- validate
  - 엔티티와 테이블의 명세가 일치하는지 확인(불일치시 예외 발생)
- none
  - 사용안함(관례상 none, 안적거나 옵션이 아닌 값을 넣어도 동일)

> create, create-drop는 DROP을 실행한다  
> -> 안쓰는걸 권장  
>
> update 또한 직접적인 변경을 가한다  
> -> 매우 신중하게 사용하거나 안쓰는걸 권장

---

### DDL 생성 기능

엔티티에 제약 조건을 명시해두면 데이터베이스 스키마가  
자동 생성될 때 제약 조건에 맞게 생성해준다

제약 조건 예시

```java
@Column(nullable = false, length = 10)
private String userName;

@Column(unique = true)
private String nickName;
```

```java
@Table(uniqueConstaints = {
    @UniqueConstraints(
        name = "NAME_AGE_UNIQUE",
        columnNames = {"NAME", "AGE"}
    )
})
public class Member {
```

DDL 생성기능은 DDL을 자동 생성할 때만 사용되고,  
JPA의 실행 로직에는 영향을 주지 않음  
