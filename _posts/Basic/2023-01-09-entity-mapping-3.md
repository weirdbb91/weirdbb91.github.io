---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Id Mapping # 제목
excerpt             : JPA DB 기본 키 매핑 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Database Schema
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity Mapping 중 기본 키(pk) 매핑에 대한 내용

### 직접 할당

@Id 애노테이션 만으로 직접 할당임을 명시  

```java
@Id
private String id;
```

### 자동 생성

@GeneratedValue 애노테이션을 사용  

@GeneratedValue 애노테이션 사용시의 id 생성 전략  

- IDENTITY
  - 데이터베이스에 생성을 위임
  - ex) MySQL auto_increment
  - INSERT SQL이 실행되어야 ID 값을 알 수 있음
- SEQUENCE
  - DB 시퀀스 오브젝트 사용
    - 테이블 마다 다른 시퀀스 오브젝트 사용을 원한다면
        @SequenceGenerator 사용

        ```java
        @Entity
        @SequenceGenerator(
            name = "MEMBER_SEQ_GENERATOR",
            sequenceName = "MEMBER_SEQ", // 매핑할 DB 시퀀스 이름
            initialValue = 1, // 초기 값
            allocationSize = 1) // 시퀀스 한 번 호출에 증가하는 크기
        public class Member {

            @Id
            @GeneratedValue(
                strategy = GenerationType.SEQUENCE,
                generator = "MEMBER_SEQ_GENERATOR")
            private Long id;
        }
        ```

- TABLE
  - 키 생성용 테이블을 하나 만들어서 DB 시퀀스를 흉내내는 전략
  - 모든 DB에 적용 가능
  - 상대적으로 성능이 좀 떨어진다는 이슈가 있음
  - @TableGenerator 사용

    ```java
    @Entity
    @TableGenerator(
        name = "MEMBER_SEQ_GENERATOR",
        table = "MY_SEQUENCES", // 테이블 이름
        pkColumnValue = "MEMBER_SEQ", // pk 컬럼 명
        allocationSize = 1) // 시퀀스 한 번 호출에 증가하는 크기
    public class Member {

        @Id
        @GeneratedValue(
            strategy = GenerationType.TABLE,
            generator = "MEMBER_SEQ_GENERATOR")
        private Long id;
    }
    ```

- AUTO
  - 방언(Dialect)에 따라 위 세 가지 중 자동 지정

> **allocationSize 옵션**  
> IDENTITY 전략의 INSERT SQL이 실행되어야만  
> id를 알 수 있다는 부분을 보완하는 옵션  
>  
> 시퀀스를 호출 할 때 마다 옵션 값만큼  
> 시퀀스 값을 증가 시켜 공간을 미리 확보해두고 사용  
>
> 확보 시점이 시퀀스 호출 시점이므로 동시성 이슈도 적다  

---

### 권장하는 식별자 생성 전략

기본 키 제약 조건

- null이 아님
- 유일성
- 불변

미래까지 이 조건들을 만족하는 자연키는 찾기 어렵다  
(자연키: 주민등록번호, 전화번호 등)  
주민번호도 완벽하지 않으니 대리키(대체키)를 사용하자  

권장하는 형태: Long형 + 대체키 + 키 생성전략 사용  

- auto_increment
- 시퀀스 오브젝트
- UUID
- 등등
