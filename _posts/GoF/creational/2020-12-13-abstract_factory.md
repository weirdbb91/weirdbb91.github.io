---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 추상 팩토리 패턴 # 제목
excerpt             : Creational Abstract Factory Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-13 # 마지막 수정일
categories          : DesignPattern Creational
tags                : DesignPattern GoF Creational AbstractFactory
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

## Abstract Factory Pattern<br>(추상 팩토리 패턴)

객체 생성 패턴(Object Creational)

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  

객체의 생성의 세부사항과 의존성을 다른객체로부터 보호하고  
생성에 대한 결합도를 모듈 단위로 계층화 시키는게 가능해진다  

## Class diagram

<img src="/assets/images/posts/2020-12-13-abstract_factory/diagram.png" alt="클래스_다이어그램">

## 예시

```java
class ExampleClass {
    private Factory factory;

    public ExampleClass(Factory factory) {
        this.factory = factory;
    }

    public void otherMethod() {
        // food의 구현은 전달받은 Factory에 따라 달라진다
        Food food = factory.getFood();
        food.productMethod();
    }
}

interface Food { ... }
interface Cloth { ... }

// 말 그대로 추상화된 팩토리
interface Factory {
    Food getFood();
    Cloth getCloth();
}
```

## 팩토리 메소드와의 차이

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  

팩토리 메소드는 호출시에 `적절한 객체를 반환하는 메소드`이고  
추상 팩토리 외에도 다방면으로 활용되는 더 작은 개념이라고 볼 수 있다  
