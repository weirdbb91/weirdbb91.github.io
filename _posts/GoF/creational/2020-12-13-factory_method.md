---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 팩토리 메소드 패턴 # 제목
excerpt             : Creational Factory Method Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-13 # 마지막 수정일
categories          : DesignPattern Creational
tags                : DesignPattern GoF Creational FactoryMethod
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

## Factory Method Pattern<br>(팩토리 메소드 패턴)

생성 패턴(Object Creational)

호출시에 `적절한 객체를 반환하는 메소드`로  

객체 생성 목적의 인터페이스 또는 추상 클래스를 정의하고  
객체 `생성의 책임`을 구체화하는 `하위 클래스로 넘긴다`  

## Class diagram

<img src="/assets/images/posts/2020-12-13-factory_method/diagram.png" alt="클래스_다이어그램">

## 예시

```java
// 생성될 객체의 추상 클래스
public abstract class Pizza {
    // 구현체가 구현해야될 기능
    public abstract void addIngredients();

    // 공통된 기능
    public void bakePizza() {
        System.out.println("Pizza baked at 400 for 20 minutes.");
    }
}

// 구현체 - Cheese 피자
public class CheesePizza extends Pizza {
    @Override
    public void addIngredients() {
        System.out.println("Preparing ingredients for cheese pizza.");
    }
}

// 구현체 - Pepperoni 피자
public class PepperoniPizza extends Pizza {
    @Override
    public void addIngredients() {
        System.out.println("Preparing ingredients for pepperoni pizza.");
    }
}

// 구현체 - Veggie 피자
public class VeggiePizza extends Pizza {
    @Override
    public void addIngredients() {
        System.out.println("Preparing ingredients for veggie pizza.");
    }
}
```

```java
// 객체 생성 인터페이스를 제공하는 추상 클래스
public abstract class BasePizzaFactory {
    
    public abstract Pizza createPizza(String type);
}

// 적합한 객체를 생성하는 구현체
public class PizzaFactory extends BasePizzaFactory{
    @Override
    public  Pizza createPizza(String type){
        Pizza pizza;
        switch (type.toLowerCase())
        {
            case "cheese":
                pizza = new CheesePizza();
                break;
            case "pepperoni":
                pizza = new PepperoniPizza();
                break;
            case "veggie":
                pizza = new VeggiePizza();
                break;
            default: throw new IllegalArgumentException("No such pizza.");
        }
        pizza.addIngredients();
        pizza.bakePizza();
        return pizza;
    }
}
```

## 테스트

```java
public class PizzaFactoryTest {
    @Test
    public void testMakePizzas(){
        BasePizzaFactory pizzaFactory = new PizzaFactory();
        Pizza cheesePizza = pizzaFactory.createPizza("cheese");
        // Preparing ingredients for cheese pizza.
        // Pizza baked at 400 for 20 minutes.
        Pizza veggiePizza = pizzaFactory.createPizza("veggie");
        // Preparing ingredients for veggie pizza.
        // Pizza baked at 400 for 20 minutes.
    }
}
```

## 추상 팩토리 패턴과의 차이

팩토리 메소드는 호출시에 `적절한 객체를 반환하는 메소드`이고

생산 제품군 전체를 마치 테마를 바꾸듯 간단하게 교체하기위해  
`공통 테마의 팩토리 메소드들을 가지는 객체를` 주입할 수 있도록  
`추상적으로 정의한 것`이 추상 팩토리다  
