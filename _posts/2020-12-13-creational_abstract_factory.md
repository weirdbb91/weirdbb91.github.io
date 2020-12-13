---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 추상 팩토리 패턴 # 제목
excerpt             : Creational Abstract Factory Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-13 # 마지막 수정일
categories          : gof
tags                : DesignPattern GoF Creational AbstractFactory
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## Abstract Factory Pattern<br>(추상 팩토리 패턴)
객체 생성 패턴(Object Creational)

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  

팩토리만 교체하면 생산 제품군 전체가 바뀌기 때문에  
객체의 표현, 구현 정보, 의존성 등을 은닉해 `플랫폼 종속성이 제거`되고  
추상 클래스에서 결합도를 정의하거나 계층화시켜 `결합도를 낮출 수 있다`  

생성제품군의 `변경은 쉬워`지지만, `새로운` 제품의 `추가는 어려워`진다

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

---
---
## 팩토리 메소드와의 차이

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  

팩토리 메소드는 공장처럼 호출시에 `적절한 객체를 반환하는 메소드`이고  
추상 팩토리 외에도 다방면으로 활용되는 더 작은 개념이라고 볼 수 있다  

---
---