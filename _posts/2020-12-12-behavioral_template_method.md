---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 템플릿 메소드 패턴 # 제목
excerpt             : Behavioral Template Method Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-12 # 마지막 수정일
categories          : gof
tags                : DesignPattern GoF Behavioral TemplateMethod
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## Template Method Pattern<br>(템플릿 메소드 패턴)
행위 패턴(Object Behavioral)

`일정한 단계`가 있는 알고리즘들을 나눠 `공통된 절차를 제외`한  
`변경 가능성`이 있는 부분들을 `하위 클래스에서 구체화`하는 패턴  



```java
// 단계별 구성
public abstract class Life {
    protected abstract String wakeUp();
    protected abstract String eat();
    protected abstract String sleep();

    // 공통된 절차를 지정해 코드 중복 지양
    public void daily() {
        System.out.print(wakeUp());
        System.out.print(eat());
        System.out.print(sleep());
    }
}

...


// 하위 클래스에서 구체화
public class DogLife extends Life {
    @Override
    protected String wakeUp() { return "왈왈"; }
    @Override
    protected String eat() { return "찹찹"; }
    @Override
    protected String sleep() { return "..."; }
}

...

public class Main {
    public static void main(String[] args) {
        Life myDog = new DogLife();
        myDog.daily(); // 왈왈찹찹...
    }
}
```