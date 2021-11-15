---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 일급 객체 # 제목
excerpt             : first class object # 썸네일 한줄 요약
last_modified_at    : 2020-11-26 # 마지막 수정일
categories          : OOP
tags                : OOP FirstClassObject
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---
---
이 글은 아래의 출처에서 내용을 참고하여 작성하였습니다.  
출처 : [https://en.wikipedia.org/wiki/First-class_citizen](https://en.wikipedia.org/wiki/First-class_citizen)  
[https://isooo.github.io/etc/2019/11/13/%EC%9D%BC%EA%B8%89%EA%B0%9D%EC%B2%B4.html](https://isooo.github.io/etc/2019/11/13/%EC%9D%BC%EA%B8%89%EA%B0%9D%EC%B2%B4.html)


---
---

## 일급 객체의 정의

위키에서는 일급 객체의 정의를 다음과 같이 내리고 있다  

```
Robin Popplestone gave the following  
definition: All items have certain fundamental rights.

1. All items can be the actual parameters of functions
2. All items can be returned as results of functions
3. All items can be the subject of assignment statements
4. All items can be tested for equality.
```

---

이를 통해 내가 이해한 바에 따르면,  
모든 일급 객체의 요소들은 다음과 같은 권리를 가져야한다

1. 함수의 실제 매개변수가 될 수 있어야 한다
2. 함수의 결과 값으로 반환 될 수 있어야 한다
3. 할당문의 할당 값이 될 수 있어야 한다
4. 동일한지 서로 비교할 수 있어야 한다

즉 객체의 요소들이 모두 저 권리들을 갖춰야 일급 객체라고 부를수 있다

---
---

다음은 모던 자바의 장점에 대해 기술한 글의 일부이다.

---

## 일급 객체 (First-class citizen)

---

<br>

해당 언어에서 어떤 개체가 다음 조건을 만족하면 일급 객체로 간주한다.  

 * 파라미터로 전달할 수 있다.
 * 반환값(return value)로 사용할 수 있다.
 * 변수나 데이터 구조 안에 담을 수 있다.
 * 할당에 사용된 이름과 관계없이 고유한 구별이 가능하다.

위 조건들을 만족한다면,
그 개체를 해당 언어의 First-class citizen이라 부를 수 있다.

---

중략

---

**모던 자바**  
Java 8은 다양한 라이브러리 제공과 함수형 프로그래밍 컨셉을 도입하였기에  
패러다임이 전환되어 일명 모던 자바라고 불리고 있다.  
이 모던 Java부터는 Java에서 함수형 프로그래밍을 할 수 있도록 설계되었다.  
Java 8부터는 Function을 일급 객체로 사용할 수 있게 된 것이다.  

`Function이 일급 객체로 사용되는 언어를 First-class function를 지원하는 언어라 한다.`  


**장점**  
 * 메소드의 파라미터와 바디에만 집중할 수 있다.
 * 테스트에 용이하다.
 * 코드를 읽기 쉽다.
 * 사이드 이펙트가 없다(상태 값을 가지지 않으므로, 다른 변경을 일으키지 않는다).
 * OOP로 구현하는 것보다 간편하게 메소드 레벨에서 작업할 수 있다.

**맛보기**

계산 기능이 있는 프로그램을 만들었다.
```
interface Calculation {
    int calculate(int x, int y);
}

class Addition implements Calculation {
    @Override
    public int calculate(final int x, final int y) {
        return x + y;
    }
}

class Subtraction implements Calculation {
    @Override
    public int calculate(final int x, final int y) {
        return x - y;
    }
}
```

```
class CalculatorService {
    private final Calculation calculation;

    public CalculatorService(final Calculation calculation) {
        this.calculation = calculation;
    }

    public int calculator(final int x, final int y) {
        return this.calculation.calculate(x, y);
    }
}
```

위 Calculation에서 만약 다른 기능이 추가된다면(e.g. 곱셈, 나눗셈..),  
그에 대한 구현체를 만들어줘야 한다.  

그리고 CalculatorService를 생성할 때 하나의 구현체만 주입할 수 있어,  
덧셈과 뺄셈에 대한 기능이 필요할 땐 CalculatorService 인스턴스를 2개 만들어줘야 한다.

```
final CalculatorService calculatorService1 = new CalculatorService(new Addition());
calculatorService1.calculator(10, 20);

final CalculatorService calculatorService2 = new CalculatorService(new Subtraction());
calculatorService2.calculator(10, 20);
```

이를 FP(Functional Programming)로 나타내면 훨씬 간편하게 구현할 수 있다.  
Java 8에서는 Function은 일급 객체로 사용할 수 있도록 함수형 인터페이스를 제공하고 있다.  
이를 이용하여 구현해보자.

```
class FpCalculatorService {
    public int calculator(final Calculation calculation, final int x, final int y) {
        return calculation.calculate(x, y);
    }
}
```

이제 FpCalculatorService를 호출하는 쪽에서 Calculation 인스턴스를 넘겨주면 된다.

```
final FpCalculatorService fpCalculatorService = new FpCalculatorService();
fpCalculatorService.calculator((x, y) -> x - y, 10, 20);
fpCalculatorService.calculator((x, y) -> x * y, 10, 20);    
```
입맛에 맞게 기능을 구현하여, 해당 functional interface를 파라미터로 넘겨줄 수 있다.

---
---

정말 어떤 분께서 쓰셨는지 만나게 된다면 감사 인사를 드리고 싶다.  
덕분에 개념을 잡는데 아주 큰 도움이 되었습니다.

---
