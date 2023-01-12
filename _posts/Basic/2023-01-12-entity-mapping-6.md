---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Entity Inheritance Mapping 2 # 제목
excerpt             : JPA DB 상속관계 매핑 2 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Entity Inheritance Mapping MappedSuperclass
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA Entity 매핑에서 상속관계에 대한 내용, 그 두 번째  
@MappedSuperclass 애노테이션에 관한 내용  

## 정의

Entity의 부모 클래스에 사용하는 애노테이션으로  
상속을 받은 자식 클래스에 부모 클래스의 매핑 정보만 제공  
상속관계를 매핑하는것이 아니라 상속 그 자체라  
부모 클래스는 테이블과 매핑이 되지 않는다  

### 사용 예시

```java
// 부모 클래스
@MappedSuperclass
public abstract class BaseEntity {
    private LocalDateTime createdAt;
    private LocalDateTime updatedAt;
    ...
}
```

```java
// 자식 클래스
@Entity
public class Member extends BaseEntity {
    // 부모 필드를 상속받음
    // private LocalDateTime createdAt;
    // private LocalDateTime updatedAt;
    // ...
    private String firstName;
    private String lastName;
    ...
}
```

### 주의사항

- Entity에 사용하는 것이 아님  
- 테이블과 매핑되지 않음  
- 조회, 검색 불가  
  - em.find(부모클래스) 불가  
- 직접 생성해서 사용할 일이 없으므로,  
    추상 클래스로 정의하는것을 권장  
