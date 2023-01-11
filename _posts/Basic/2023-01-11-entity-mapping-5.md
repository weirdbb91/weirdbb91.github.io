---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Entity Inheritance Mapping 1 # 제목
excerpt             : JPA DB 상속관계 매핑 1 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Entity Inheritance Mapping
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity 매핑에서 상속관계에 대한 내용, 그 첫번째

## 정의

- RDB에서는 상속관계를 표현할 수가 없다  
- 수퍼타입 서브타입 관계라는 모델링 기법이 객체 상속과 유사  

객체의 상속 구조와 DB의 수퍼타입 서브타입 관계를 매핑  

### 주요 애노테이션

- @Inheritance(strategy = {상속 전략 타입})
  - InheritanceType.JOINED
    - 공통 정보를 수퍼타입으로 정의하고,  
      부가 정보를 서브타입으로 각각의 테이블 정의
    - 타입 컬럼으로 서브타입을 특정 후 조인하는 전략  
    - 보편적으로 추천되는 방식
    - 정규화된 데이터
    - 효율적인 저장공간 활용
    - 조회시 JOIN이 많이 사용됨, 성능 저하
    - 조회 쿼리가 복잡함
    - 데이터 저장시 INSERT SQL이 두 번 실행됨
  - InheritanceType.SINGLE_TABLE
    - 정보들을 통합해 한 테이블에 모두 정의하는 전략
    - DTYPE 컬럼이 자동으로 추가된다
    - JOIN이 필요 없으므로 일반적으로 조회성능이 우수
    - 조회 쿼리가 단순함
    - 자식 엔티티가 매핑한 컬럼은 모두 nullable
    - 테이블이 너무 커지면 조회 성능이 오히려 떨어질 수 있다
  - InheritanceType.TALBE_PER_CLASS
    - 수퍼타입 없이, 수퍼타입의 컬럼들을  
        각 서브타입에 통합해 각각 정의하는 전략
    - 이 따위 방식은 사라지는게 맞다
    - 선택한다면 후회할 것이다
- @DiscriminatorColumn(name = "{DTYPE 컬럼 명}")
  - DTYPE은 서브타입 구분자로, 수퍼타입에 사용하며  
    수퍼타입 테이블에 서브타입 구분을 위한 컬럼을 추가한다
  - 기본값은 "DTYPE"
- @DiscriminatorValue("{DTYPE 값}")
  - 서브타입에 사용, 서브타입의 DTYPE 값을 명시한다
  - 기본값은 해당 클래스의 이름

---

### 예시

```java
@Entity
@Enheritance(strategy = InheritanceType.JOINED)
@DiscriminatorColumn(name = "type")
public abstract class Item {
```

```java
@Entity
@DiscriminatorValue("M")
public class Movie extends Item {
```
