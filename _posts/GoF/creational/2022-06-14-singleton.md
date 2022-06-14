---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 싱글톤 패턴 # 제목
excerpt             : Creational Singleton Pattern # 썸네일 한줄 요약
categories          : DesignPattern Creational
tags                : DesignPattern GoF Creational Singleton
---

출처: [Springframework Guru - Singleton pattern](https://springframework.guru/gang-of-four-design-patterns/singleton-design-pattern/), [Refactoring Guru - Singleton pattern](https://refactoring.guru/design-patterns/singleton)  
🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

## Singleton Pattern<br>(싱글톤 패턴)

생성 패턴(Object Creational)

특정 클래스의 객체가 단 하나만 인스턴스화 되도록 하는 패턴이다.  
요청 이전의 인스턴스화 여부에 따라 주로 두 가지로 구현방법이 나뉜다.  

## Lazy initialization

요청을 받으면 그 때 인스턴스화하는 방법이다.  

### 예시 - Lazy initialization

```java
// Lazy initialization - 요청 받으면 그 때 인스턴스화
public class SingletonClass {
    private static SingletonClass instance = null; // 첫 요청 전까진 null

    private SingletonClass() {} // private 생성자로 외부에서 인스턴스화 불가

    public static SingletonClass getInstance() {
        if (instance == null) {
            instance = new SingletonClass(); // 처음이자 마지막으로 실행되는 로직
        }
        return instance;
    }
}
```

외부에서 클래스를 인스턴스화 할 수 없도록 생성자를 private으로 선언해두고,  
클래스 내부에 해당 클래스 타입의 정적 변수 null로 선언한다.  

인스턴스를 반환하는 정적 메소드에서는  
인스턴스를 반환하기 전에 정적 변수의 값이 null이면,  
인스턴스를 생성해 정적 변수에 할당하는 로직을 추가한다.  

위 로직으로 해당 클래스는 최대 단 한번만 인스턴스화 된다.  

## Eager initialization

요청 받기 전에 미리 인스턴스화하는 방법이다.

### 예시 - Eager initialization

```java
// Eager initialization - 요청 받기 전에 미리 인스턴스화
public class SingletonClass {
    private static final SingletonClass INSTANCE = new SingletonClass();
 
    private SingletonClass() {} // private 생성자로 외부에서 인스턴스화 불가
 
    public static SingletonClass getInstance() {
        return INSTANCE;
    }
}
```

마찬가지로 생성자를 private으로 선언해 외부에서의 인스턴스화를 막고,  
유일한 인스턴스를 담을 정적 필드를 미리 인스턴스화 해둔다.  

인스턴스를 반환하는 정적 메소드에서는  
미리 인스턴스화 해둔 정적 필드를 반환해주면 된다.  

애당초 미리 인스턴스화 해두었던 필드만 반환되니,  
위 로직에서 해당 클래스는 단 한번만 인스턴스화 된다.

## 테스트

```java
SingletonClass instance1 = SingletonClass.getInstance();
// instance1.hashCode(): 292938459
SingletonClass instance2 = SingletonClass.getInstance();
// instance2.hashCode(): 292938459
```

## 장점

- 클래스의 인스턴스를 단 하나만 생성된다고 확신할 수 있다
- 해당 인스턴스를 전역에서 접근할 수 있다(Global access point)
- 요청시에 단 한번만 싱글톤 객체를 초기화 할 수 있다

## 단점

- 단일책임원칙에 위배된다
- 해당 인스턴스를 전역에서 접근할 수 있다(Global access point)
  - Global state를 만드는것은 아무나 접근이 가능하기 때문에 넘모 위험함
  - 프로그램의 구성요소가 서로에 대해 너무 많은 정보를 아는 것은 올바른 디자인이 아님
- 멀티 쓰레드 환경에서는 여러개의 객체가 생성될 수 있다
- 유닛 테스트가 어려워질 수 있다
  - 많은 테스트 프레임워크에서 Mock 객체들을 생성할 때 상속에 의존하기 때문
  - 자바에서는 정적 메소드(인스턴스를 반환하는)를 재정의(Overriding)하는게 불가함
  - 테스트를 안하거나, 싱글톤 패턴을 사용하지 않는 것을 추천
