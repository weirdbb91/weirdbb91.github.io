---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Apache Kafka란? # 제목
excerpt             : 아파치 카프카란? # 썸네일 한줄 요약
categories          : Basic Apache Kafka
tags                : Basic Apache Kafka
---

출처 : 패스트캠퍼스 "Kafka 완전 정복 : 클러스터 구축부터 MSA 환경 활용까지" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

아파치 카프카가 무엇인지에 대해 가볍게 알아본다  

## 정의

한마디로 `Data in Motion Platform`(Event Streaming Platform)  
움직이는 데이터를 처리하는 플랫폼  

실시간으로 흐르는 이벤트 스트림을 받아 필요한 곳으로 데이터를 전달해줌  

- Event Stream
  - 비즈니스의 모든 영역에서 광범위하게 발생
  - 대용량의 데이터(Big Data) 발생
  - 연속적인 많은 이벤트들의 흐름
    - Event
      - 비즈니스에서 일어나는 모든 일(데이터)를 의미

## 개발 배경

링크드인에서 하루 4.5조 개 이상의 이벤트 스트림을 처리해야하는데  
기존의 Messaging Platform(ex. MQ)로는 처리할 수 없어서  
넘치는 이벤트 스트림을 처리하기 위해 개발

## 특징

1. `Pub`lish & `Sub`scribe
   - 이벤트 스트림을 안전하게 전송
2. ₩rite to `Disk`
   - 이벤트 스트림을 디스크에 저장
3. `Processing` & `Analysis`
   - 이벤트 스트림을 분석 및 처리

## 사용처

이벤트가 사용되는 모든 곳

- Messaging System
- IoT 디바이스로부터 데이터 수집
- 애플리케이션에서 발생하는 로그 수집
- Realtime Event Stream Processing(Fraud Detection, 이상 감지 등)
- DB 동기화(MSA 기반의 분리된 DB간 동기화)
- 실시간 ETL(`E`xtract & `T`ransform & `L`oad)
- Spark, Flick, Storm, Hadoop과 같은 빅데이터 기술과 같이 사용
