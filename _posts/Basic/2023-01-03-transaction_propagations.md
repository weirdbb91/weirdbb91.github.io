---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Transaction propagations # 제목
excerpt             : Transaction propagations # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Transaction Propagation
---

출처 : 인프런 김영한님의 강의 "스프링 DB 2편 - 데이터 접근 활용 기술" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

Spring의 Transation Propagation(전파) 전략에 대한 내용  

---

## 내용

### 요약

주로 쓰이는 전파 전략으로는  
기본값인 REQUIRED와 REQUIRES_NEW가 있다.  

REQUIRED는 기존 트랜잭션이 없으면 새로 생성하고,  
기존 트랜잭션이 있다면 참여하는 옵션이다.

REQUIRES_NEW는 기존 트랜잭션의 유무와는 무관하게  
항상 새로운 트랙잭션을 생성하는 옵션이다.  

---

### 설명

스프링에서 제공하는 트랜잭션 전파 옵션들은 아래와 같다.  

- REQUIRED
  - 기존 트랜잭션이 없으면 새로 생성하고,  
    기존 트랜잭션이 있다면 참여하는 옵션이다.
- REQUIRES_NEW
  - 기존 트랜잭션이 없으면 새로 생성하고,  
    기존 트랜잭션이 있어도 새로 생성하는 옵션이다.
- SUPPORT
  - 기존 트랜잭션이 없으면 트랜잭션이 없는 채로 진행하고,  
    기존 트랜잭션이 있다면 참여하는 옵션이다.
- NOT_SUPPORT
  - 기존 트랜잭션이 없으면 트랜잭션이 없는 채로 진행하고,  
    기존 트랜잭션이 있다면 보류해두고 트랜잭션이 없는 채로 진행하는 옵션이다.
- MANDATORY
  - 기존 트랜잭션이 없으면 IllegalTransactionStateException 예외가 발생하고,  
    기존 트랜잭션이 있다면 참여하는 옵션이다.
- NEVER
  - 기존 트랜잭션이 없으면 트랜잭션이 없는 채로 진행하고,  
    기존 트랜잭션이 있다면 IllegalTransactionStateException 예외가 발생하는 옵션이다.
- NESTED
  - 기존 트랜잭션이 없으면 새로 생성하고,  
    기존 트랜잭션이 있다면 중첩 트랜잭션을 생성하는 옵션이다.
    - 중첩 트랜잭션
      - 외부 트랜잭션의 영향을 받는다.
        - 외부 트랜잭션이 롤백 되면, 중첩 트랜잭션도 롤백된다.
      - 외부 트랜잭션에는 영향을 주지 못한다.
        - 중첩 트랜잭션이 롤백 되어도 외부 트랜잭션은 커밋할 수 있다.
  - JDBC savepoint 기능을 사용하기 때문에 DB Driver가 해당 기능을 지원하는지 확인 필요
  - 중첩 트랜잭션은 JPA에서는 사용할 수 없다.

---

## 주의사항

'isolation', 'timeout', readOnly'  
상기 옵션들은 트랜잭션이 시작 될 때만 적용되고,  
기존 트랜잭션에 참여하는 경우에는 적용되지 않는다.  
그러므로 SUPPORT 같은 경우에는 참여만 하기 때문에 적용 받을 일이 없고,  
REQUIRES_NEW 같은 경우에는 반대로 매번 새로 생성하기 때문에 항상 적용을 받는다.  
