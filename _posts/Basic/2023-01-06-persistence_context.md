---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Persistence Context # 제목
excerpt             : Persistence Context # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Java JPA PersistenceContext
---

출처 : 인프런 김영한님의 강의 "자바 ORM 표준 JPA 프로그래밍 - 기본편" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

JPA의 영속성 컨텍스트에 대한 내용  

---

## 내용

PersistenceContext는 Entity 영속에 사용되는 논리적인 개념  
EntityManager를 통해 PersistenceContext에 접근한다  

### Entity의 생명주기

- 비영속(new/transient)
  - 영속성 컨텍스트와 전혀 관계가 없는 새로운 상태
  - Entity 객체를 생성하기만 하고,  
    EntityManager의 영속성 컨텍스트에 넣지 않은 상태
- 영속(managed)
  - 영속성 컨텍스트에 관리되는 상태
  - em.persist(...) 메소드로 Entity 객체를 저장(영속)한 상태
- 준영속(detached)
  - 영속성 컨텍스트에 저장되었다가 분리된 상태
  - em.detach(...) 메소드로 Entity 객체를  
    영속성 컨텍스트에서 분리한 상태
- 삭제(removed)
  - 삭제된 상태
  - em.remove(...) 메소드로 Entity 객체를 삭제한 상태

### 영속성 컨텍스트의 이점

- 1차 캐시
  - 영속성 컨텍스트에 Entity들을 저장하면서 캐싱을 하고,  
    DB에 질의하기 전에 영속성 컨텍스트 안에 해당 Entity가  
    캐싱되어 있는지 먼저 확인해서 불필요한 DB 연결을 최소화 함
- 동일성(identity) 보장
  - 1차 캐시로 반복 가능한 읽기(REPEATABLE READ) 등급의  
    트랜잭션 격리 수준을 DB가 아닌 Application 차원에서 제공
- 트랙잭션을 지원하는 쓰기 지연(transactional write-behind)
  - 1차 캐시에 Entity 객체가 저장되면,  
    JPA가 INSERT Query를 작성해서 쓰기 지연 SQL 저장소에 저장
- 변경 감지(Dirty checking)
  - 트랜잭션을 커밋하는 시점에 1차 캐시에 저장된 Entity와  
    DB에서 읽어온 원본(스냅샷)을 비교해 차이가 있다면  
    UPDATE Query를 작성해서 쓰기 지연 SQL 저장소에 저장  
    쓰기 지연 SQL 저장소의 Query들을 DB에 전송하고 커밋
- 지연 로딩(Lazy loading)

---

### 플러시란?

영속성 컨텍스트의 변경내용을 DB에 반영  

플러시가 발생했을 때 일어나는 일들

- 변경 감지
- 수정된 엔티티 쓰기 지연 SQL 저장소에 등록
- 쓰기 지연 SQL 저장소의 쿼리를 DB에 전송

#### 영속성 컨텍스트를 플러시 하는 방법

1. em.flush() - 직접 호출
2. 트랜잭션 커밋 - 플러시 자동 호출
3. JPQL 쿼리 실행 - 플러시 자동 호출

#### 플러시 모드 옵션

em.setFlushMode(FlushModeType);

- FlushModeType.AUTO
  - (기본값) 커밋이나 쿼리를 실행할 때 플러시
- FlushModeType.COMMIT
  - 쿼리가 아닌 커밋할 때만 플러시

> 웬만하면 플러시 모드 옵션은 건드리지 말고 기본값을 사용

### 플러시 주의사항

1. 플러시는 영속성 컨텍스트를 비우지 않음
2. 영속성 컨텍스트의 변경내용을 DB에 동기화
3. 트랜잭션이라는 작업 단위가 중요
   - 커밋 직전에만 동기화하면 됨

---

### 준영속 상태

Entity를 준영속 상태로 만드는 방법

- em.detach(...)
  - Entity 객체를 영속성 컨텍스트에서 분리하면  
    관리를 받지 않아 해당 객체는 Dirty check 하지 않음

- em.clear()
  - 엔티티 매니저의 영속성 컨텍스트를 초기화

- em.close()
  - 영속성 컨텍스트를 종료
