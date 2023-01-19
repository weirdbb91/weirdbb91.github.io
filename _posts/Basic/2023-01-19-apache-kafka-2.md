---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Apache Kafka 기본 1 # 제목
excerpt             : 아파치 카프카의 주요 요소 1 # 썸네일 한줄 요약
categories          : Basic Apache Kafka
tags                : Basic Apache Kafka
---

출처 : 패스트캠퍼스 "Kafka 완전 정복 : 클러스터 구축부터 MSA 환경 활용까지" 중 일부

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 개요

아파치 카프카의 주요 요소들에 대해 알아본다  

---

## Topic

카프카 안에서 Message가 저장되는 장소, `논리적 요소`  

Topic 생성시 Partition 개수를 지정하고,  
각 Partition들은 Broker들에 의해 분산되며  
Segment File들로 구성됨  

---

## Partition

`변경없이 누적되어 쌓이는 Commit Log`,  

- Topic을 구성하는 물리적 구성요소  
- 하나의 Topic은 항상 하나 이상의 Partition으로 구성됨  
- 병렬처리(Throughput 처리량 향상)를 위해서 다수의 Partition을 사용
  - 다수의 Partition들을 Brocker들이 분산해 가져감
- Partition 번호는 0번부터 시작해 오름차순으로 생성됨  
  - 누적만 하기 때문에 Partition에 저장된 데이터는 변경 불가
- 이벤트의 위치를 나타내는 offset이 존재
- 각 Partition들은 서로 독립적
  - 이벤트(Message)의 순서는 하나의 Partition 내에서만 보장됨

---

## Segment

`Message(데이터)가 저장되는 실제 물리 File`  

- Partition을 구성하는 물리적 구성요소  
- Segment File이 지정된 크기보다 크거나 지정된 기간보다 오래되면  
    새 파일이 열리고 Message는 새로 열린 파일에 추가됨  

### **Rolling Strategy**

Segment 생성 전략으로 일정 기준을 초과하면  
Segment를 새로 생성한다

- 용량: log.segment.bytes(기본값 1기가)
- 기간: log.roll.hours(기본값 168시간)

Partition당 오직 하나의 Segment만 활성화 되어 데이터가 쓰여진다  

---

## Broker

- Partition에 대한 Read 및 Write를 관리하는 소프트웨어
- Kafka Server라고도 부름
- Topic 내의 Partition들을 분산, 배치, 유지 및 관리
- 각각의 Broker들은 ID(숫자)로 식별됨
- Topic의 일부 Partition들을 포함
  - Broker는 Topic 데이터의 전체가 아닌 일부분(Partition)만 가짐
- 전체 Broker들을 Bootstrap server라고 부름
- Client가 하나의 Broker에만 연결하면 Cluster 전체에 연결되어  
    Cluster 내 Broker들의 리스트를 알게됨(장애를 대비해 전체를 전달)
  - 자신이 필요한 Topic과 Partition의 위치를 알고 연결함

---

<!-- ## Zookeeper

Brocker들의 목록/설정을 관리하는 소프트웨어

- 변경사항에 대해 Kafka에 알림
  - Topic 생성/제거, Broker 추가/제거 등
- 과반수 산정을 위해 홀수개의 서버로 작동되게 설계됨(최소 3, 권장 5)
- 앞으로는 사라지게 될 컴포넌트(카프카에서 주키퍼를 제거 중)

--- -->

## Kafka Cluster

- 여러 개의 Broker들로 구성
- Client는 특정 Broker에 연결하면 전체 클러스터에 연결됨
- 4대 이상의 Broker로 Cluster를 구성하길 권장(최소 3대)
- Topic을 구성하는 Partition들은 여러 Broker 상에 분산됨
- Topic 생성시 Kafka가 자동으로 생성된 Topic의 Partition들을  
    모든 Broker에게 할당/분배해줌

---
