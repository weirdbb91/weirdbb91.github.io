---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 생성 패턴 # 제목
excerpt             : Creational Pattern # 썸네일 한줄 요약
categories          : DesignPattern Creational
tags                : DesignPattern GoF Creational
---

출처: [Refactoring Guru - Singleton pattern](https://refactoring.guru/design-patterns/creational-patterns)  
🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

## Creational Pattern<br>(생성 패턴)

디자인 패턴 중에 생성 패턴들은 다양한 객체들을 생성하는 매커니즘을 제공하고,  
기존 코드에 유연성과 재사용성을 향상시켜준다.  

## 종류

생성 패턴의 종류는 다음과 같다.

- [팩토리 메소드 패턴(Factory Method Pattern)](../factory_method/)
  - 생성할 객체의 클래스를 정확하게 지정하지 않고 객체를 생성하는 패턴
- [추상 팩토리 패턴(Abstract Factory Pattern)](../abstract_factory/)
  - 팩토리 메소드 패턴에서 한단계 더 캡슐화해, 팩토리를 추상화한 패턴
- [빌더 패턴(Builder Pattern)](../builder/)
  - 복잡한 객체를 생성할 때 쓰는 패턴
- [프로토타입 패턴(Prototype Pattern)](../prototype/)
  - 기존의 객체로부터 복제를 통해 새 객체를 생성하는 패턴
- [싱글톤 패턴(Singleton Pattern)](../singleton/)
  - 객체를 하나만 생성하는 패턴
