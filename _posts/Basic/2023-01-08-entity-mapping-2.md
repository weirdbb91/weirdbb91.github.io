---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Entity Column Mapping # 제목
excerpt             : JPA Entity Column Mapping # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Database Entity Mapping
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity Mapping에 사용되는 주요 애노테이션에 대한 내용

- 객체와 테이블 매핑: @Entity, @Table
- 필드와 컬럼 매핑: @Column
- 기본 키 매핑: @Id
- 타입 매핑: @Enumerated, @Temporal

---

## 내용

### 애노테이션 소개

- @Entity
  - @Entity 애노테이션이 붙은 클래스는 JPA가 관리한다
  - JPA를 사용해서 테이블과 매핑할 클래스는 @Entity 필수
  - **주의사항**
    - 기본 생성자 필수(인수 없는 public or protected)  
    - final, enum, interface, inner class는 사용 불가
    - DB에 저장할 field에는 final 사용 불가
  - **애노테이션 속성**
    - name
      - JPA에서 사용할 엔티티 이름(기본값은 클래스명)을 지정함
- @Table
  - 엔티티와 매핑할 테이블을 지정함
  - **애노테이션 속성**
    - name
      - 매핑할 테이블 이름(기본값은 엔티티 이름)을 지정함
    - catalog
      - DB의 catalog 매핑
    - schema
      - DB의 schema 매핑
    - uniqueConstraints
      - DDL 생성 시에 유니크 제약 조건 생성
- @Column
  - 해당 필드가 테이블의 컬럼과 매핑된다고 명시함
  - **애노테이션 속성**
    - name
      - 매핑할 테이블 이름(기본값은 엔티티 이름)을 지정함
    - insetable
      - 컬럼 값의 등록 가능여부를 지정 - D: true
    - updatable
      - 컬럼 값의 변경 가능여부를 지정 - D: true
    - nullable
      - null 값이 할당 될 수 있는지를 지정 - D: true
    - unique
      - unique 키 여부를 지정 - D: false
      - 컬럼에서 지정하기보다는 unique 키의 이름을 지정할 수 있는  
        @Table의 uniqueConstraints를 사용하는걸 권장
    - columnDefinition
      - DB column 정의를 직접 함
      - ex) "varchar(100) default 'EMPTY'"
    - length
      - 문자 길이 제한 - D: 255
      - String 타입에만 적용됨
    - precision
      - BigDecimal 또는 BigInteger 타입에서 사용 - D: 0
        - double, float 불가
      - 소수점을 포함한 전체 자릿수를 지정
    - scale
      - BigDecimal 또는 BigInteger 타입에서 사용 - D: 0
        - double, float 불가
      - 아주 정밀한 소수의 자릿수를 지정
- @Id
  - 테이블의 pk를 매핑함
- @Enumerated
  - Enum 타입의 객체임을 명시함
  - **애노테이션 속성**
    - value
      - 어떤 타입의 Enum 형식인지 지정
        - EnumType.STRING: String 타입
          - Enum의 이름을 저장
        - EnumType.ORDINAL: 숫자 타입
          - Enum의 순서를 저장
          - 권장하지 않음, 추후에 순서가 변경되면 매우 위험
- @Temporal
  - 시간 타입의 객체임을 명시함
  - **필드 타입 LocalDate, LocalDateTime을 사용하면 생략 가능!**
  - java.util.Date 객체에는 날짜와 시간이 모두 포함되어 있으나  
    DB에는 구분되어 저장되므로 명시적인 매핑이 필요함
  - **애노테이션 속성**
    - value
      - 어떤 타입의 시간 형식인지 지정
        - TemporalType.DATE: java.sql.Date로 날짜를 포함
        - TemporalType.TIME: java.sql.Time으로 시간을 포함
        - TemporalType.TIMESTAMP: java.sql.Timestamp으로 시간과 날짜 모두 포함
  - 필드 타입 LocalDate, LocalDateTime 사용을 권장
- @Lob
  - 매핑하는 필드 타입에 따라 다르게 지정 됨
    - CLOB: String, char[], java.sql.CLOB
    - BLOB: byte[], java.sql.BLOB
- @Transient
  - 해당 필드는 DB에 컬럼으로 저장/생성/매핑되지 않음
  - DB와는 별개로 객체에서만 임시로 사용할 용도임을 명시
