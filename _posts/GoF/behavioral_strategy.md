---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 전략 패턴 # 제목
excerpt             : Behavioral Strategy Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-11 # 마지막 수정일
categories          : gof
tags                : DesignPattern GoF Behavioral Strategy
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## Strategy Pattern<br>(전략 패턴)
행위 패턴(Object Behavioral)


`추상화`한 전략 `객체`에게 `수행을 위임`시키기 때문에  
전략 객체를 상속받아 `구체화`된 `객체`군은 `상호교환`이 가능해진다  
즉, `요청의 변경없이` 객체의 `행동`들이 통째로 `변경`된다  

상황에 따라 유연하게 대응할 수 있지만, `생성되는 객체의 수가 많아`지고  
객체군의 성격에 맞게 `일반화에 신경써`서 구현해야만한다  


```java
// 추상화한 전략 객체
public interface Animal {
    public String say();
}

...

// 전략 객체를 상속받아 구체화된 객체군
public class Dog implements Animal {
    @Override
    public String say() { return "왈왈"; }
}

public class Retriever implements Animal {
    @Override
    public String say() { return "안녕하세요"; }
}

public class Human implements Animal {
    @Override
    public String say() { return "배고파"; }
}

...

public class ZooCage {
    private Animal animal;

    public void setAnimal(Animal animal) {
        this.animal = animal;
    }

    public void sound() {
        // 요청 수행을 위임
        System.out.println(animal.say());
    }
}

...

public class Main {
    public static void main(String[] args) {
        ZooCage zooCage = new ZooCage();

        // 요청의 변경없이 객체의 행동들이 통째로 변경 됨
        zooCage.setAnimal(new Dog());
        zooCage.sound(); // "왈왈"

        zooCage.setAnimal(new Retriever());
        zooCage.sound(); // "안녕하세요"

        zooCage.setAnimal(new Human());
        zooCage.sound(); // "배고파"
    }
}
```