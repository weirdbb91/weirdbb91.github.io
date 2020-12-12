---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 클래스 다이어그램 # 제목
excerpt             : UML Class Diagram # 썸네일 한줄 요약
last_modified_at    : 2020-12-12 # 마지막 수정일
categories          : etc
tags                : ETC ClassDiagram
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---
클래스 다이어그램의 표기 방법에 대해  
특히 연관관계과 집합연관 관계에 있어 논란이 많고  
출처마다 다른 주장을 하는 경우가 많아  
참고 정도만 하시길 권장합니다.

---

## 구성

|클래스의 구성|위치|
|:-:|:-:|
|일반 class name<br>추상적 객체<\<class name\>>|첫줄|
|멤버변수 attributes|중간|
|메소드 methods|마지막|
<br>

## 변수, 메소드 작성 방법

|접근제한자|기호|
|:-:|:-:|
|public|+|
|default|~|
|protected|#|
|private|-|
<br>

|예시|
|-|
|- age : int = 0|
|- name : String|
|+ setName(String)|
|+ getName() : String|
<br>

## 관계의 표기방법

|관계|기호|설명|
|:-:|:-:|:-:|
|일반화<br>(Generalization)|─▷|상속받는 경우, is a 관계|
|실체화<br>(Realization)|···▷|구현하는 경우, 오버라이딩|
|의존<br>(Dependency)|···>|사용은 하지만 멤버변수는 아님|
|직접연관<br>(Association)|─>|사용도하고 멤버변수이기도 함|
|집합연관<br>(Aggregation)|◇─|멤버변수지만 new는 안함, has a 관계|
|복합연관<br>(Composition)|◆─|멤버변수이고 new도 함, own a 관계|
|관계간의<br>다중성 표현|n ─ n<br>n ··· n|n : 수, .. : 또는, * : 이상<br>(1 : n의 관계, n : n의 관계 등)|
