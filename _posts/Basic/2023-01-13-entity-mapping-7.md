---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : JPA Hibernate Proxy class # 제목
excerpt             : JPA 프록시 # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA Hibernate Proxy
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA에서 즉시로딩과 지연로딩 이해에 필요한 HibernateProxyClass에 대한 내용

## 정의

DB를 통해 실제 엔티티 객체를 조회하는 em.find() 메소드와는 다르게  
DB 조회를 미루기 위한 가짜(프록시) 엔티티 객체를 조회하는  
**em.getReference()** 메소드를 호출하면 반환되는 객체의 class  
{PACKAGE}.Entity\$HibernateProxy\${RANDOM}라는 이름으로 생성된다  

### 특징

- 실제 클래스를 상속 받는다
- 실제 클래스와 겉 모양이 같다
- 사용자 입장에서는 진짜와 프록시 객체를  
    구분하지 않고 사용하면 된다

### 작동 흐름

- 프록시 객체는 실제 객체의 참조(target)를 보관할 수 있다  
    (처음 생성된 시점에는 실제 객체를 보관하지 않는다)
- 프록시 객체의 메소드를 호출하면 프록시 객체는  
    실제 객체의 메소드를 대신 호출한다
- 프록시 객체가 실제 객체를 보관하고 있지 않거나,  
    반환값을 구할수 없으면 영속성 컨텍스트를 통해  
    DB의 실제 Entity를 받아와 보관(참조)한다

> 실제 객체의 내용이 당장 필요하지 않으면  
> 프록시 객체를 통해 조회를 미룬다  
>
> JPA에 구현된 기능이 아님  
> JPA에는 표준만 있고 구현은 Hibernate 같은데서 한다  

### 프록시 확인 방법

- 프록시 인스턴스의 초기화 여부 확인
  - PersistenceUnitUtil.isLoaded(Object entity)
- 프록시 클래스 확인 방법
  - entity.getClass().getName() 출력
- 프록시 강제 초기화(JPA 표준에는 없는 기능)
  - org.hibernate.Hibernate.initialize(entity)

### 주의사항

- 프록시 객체는 DB 조회 전후가 다르지 않다  
    target이 null에서 실제 객체의 참조로 할당되는것 뿐
- 프록시 객체는 원본 객체를 상속받기 때문에 타입체크시 유의  
  - == 비교시에는 실패
  - instanceof를 사용해야 함
- 찾는 엔티티가 이미 영속성 컨텍스트에 있으면  
    em.getReference()를 호출해도 실제 엔티티를 반환
  - JPA에서는 이미 영속성 컨텍스트에 있는 엔티티 객체와  
    em.getReference()의 반환값을 == 비교했을 때  
    항상 true를 반환해야하기 때문
- 반대로 영속성 컨텍스트에 없는 엔티티의 프록시 객체를  
    먼저 생성하고 em.find()로 실제 객체를 조회하면  
    em.find()의 반환값이 프록시 객체가 된다  
  - JPA는 ㄹㅇ루다가 == 비교에 진심인 편
- em.getReference()으로 조회하려는 대상이  
    영속성 컨텍스트에 없거나(clear) 관리 대상이 아니거나(detach)  
    영속성 컨텍스트가 꺼져있으면(close) 예외가 발생한다  
    (LazyInitializationException)  
