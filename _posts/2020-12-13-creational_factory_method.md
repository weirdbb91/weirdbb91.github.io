---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 팩토리 메소드 패턴 # 제목
excerpt             : Creational Factory Method Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-13 # 마지막 수정일
categories          : gof
tags                : DesignPattern GoF Creational FactoryMethod
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## Factory Method Pattern<br>(팩토리 메소드 패턴)
생성 패턴(Object Creational)

호출시에 `적절한 객체를 반환하는 메소드`로  

객체 생성 목적의 인터페이스 또는 추상 클래스를 정의하고  
객체 `생성의 책임`을 구체화하는 `하위 클래스로 넘긴다`  

```java
class SuperClass {
    public void otherMethod() {
        Product p = factoryMethod();
        p.productMethod();
    }

    protected Product factoryMethod() {
        return new NormalProduct();
    }
}

class SubClass extends SuperClass {
    protected Product factoryMethod() {
        return new SpecialProduct();
    }
}
```
---
---
## 추상 팩토리 패턴과의 차이

팩토리 메소드는 호출시에 `적절한 객체를 반환하는 메소드`이고

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  



---
---