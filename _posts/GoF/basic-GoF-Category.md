---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : GoF # 제목
excerpt             : 한권 요약 # 썸네일 한줄 요약
last_modified_at    : 2020-12-06 # 마지막 수정일
categories          : DesignPattern GoF
tags                : DesignPattern GoF
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---
이 글은 아래의 출처에서 내용을 참고하여 작성하였습니다.  
출처 : [https://yrok.tistory.com/](https://yrok.tistory.com/)
[https://en.wikipedia.org/wiki/Design_Patterns#cite_note-1](https://en.wikipedia.org/wiki/Design_Patterns#cite_note-1)


---
---
생성 패턴 (Creational)

- ~~Abstract Factory Pattern<br>(추상 팩토리 패턴)~~
- Builder Pattern<br>(빌드 패턴)
- ~~Factory Method Pattern<br>(팩토리 메소드 함수)~~
- Prototype Pattern<br>(프로토타입 패턴) 원형
- Singleton Pattern<br>(싱글톤 패턴) 단일체

구조 패턴 (Structural)

- ~~Adapter Pattern<br>(어댑터 패턴) 적응자~~
- Bridge Pattern<br>(브릿지 패턴) 가교
- Composite Pattern<br>(복합체 패턴)
- Decorator Pattern<br>(데코레이터 패턴) 장식자
- Facade Pattern<br>(퍼사드 패턴)
- Flyweight Pattern<br>(플라이급 패턴)
- Proxy Pattern<br>(프록시 패턴)

행위 패턴 (Behavioral)

- Chain of Responsibility Pattern<br>(책임 연쇄 패턴)
- Command Pattern<br>(커맨드 패턴) 명령
- Interpreter Pattern<br>(인터프리터 패턴) 해석자
- Iterator Pattern<br>(반복자 패턴)
- Mediator Pattern<br>(중재자 패턴)
- Memento Pattern<br>(메멘토 패턴)
- Observer Pattern<br>(옵저버 패턴) 감시자
- State Pattern<br>(상태 패턴)
- ~~Strategy Pattern<br>(전략 패턴)~~
- ~~Template Method Pattern<br>(템플릿 메소드 패턴)~~
- Visitor Pattern<br>(방문자 패턴)


## 생성 패턴 (Creational)

생성 패턴은 각 상황에 `필요한 객체를 유연하게 결정`하기 위해  
직접 `인스턴스화하지않고 객체를 생성`하는 패턴들입니다.

생성(Creational) “클래스” 패턴은 객체를 생성하는 책임의 일부를 서브클래스가 담당하도록 넘깁니다. 그러나 생성 “객체” 패턴은 이를 다른 깨체에게 위임합니다.
추상 팩토리, 빌더, 팩토리 메서드, 원형 패턴(프로토타입) 및 단일체 패턴(싱글톤)에서는 구체 클래스에서 인스턴스를 생성하도록 하고 있다. 이들 패턴에서는 객체 생성의 과정을 추상화함으로써 인스턴스화할 때 인터페이스와 구현을 연결하는 다른 방법을 제시한다.


### Abstract Factory Pattern<br>(추상 팩토리 패턴)
- 다른 객체를 생성하는 책임만 있는 객체를 만들어 공장과 같이 부품을 조합해서 인스턴스 생성을 실행하는 패턴
- 특정 클래스에서 객체를 생성하는 문제를 방지하려면 객체를 직접 생성해서는 안된다.
- 하드웨어와 소프트웨어 플랫폼에 대한 의존성. 플랫폼 종속성을 제거한다.
- 객체의 표현이나 구현에 대한 의존성. 정보를 사용자에게 감춤
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 추상 팩토리 패턴의 참가 객체는 팩토리와 제품이다. 이 패턴은 클래스의 인스턴스를 직접 만들지 않고서도 관련된 제품 객체의 군을 생성하는 방법을 정의한다. 어떤 특정 팩토리를 지정하여 이를 통해서 제품을 생성하게 하는 방법으로 원하는 제품을 선택한다. 팩토리의 인스턴스만 바꾸면 전체 제품군을 바꿀 수 있다. 추상 팩토리 패턴은 동일 계열의 제품군을 다룰 수 있다는 점에서 다른 생성 패턴과 다르다.
- 여러 개의 룩앤필 표준을 지원하기 위한 추상 팩토리 패턴
- -CreateMaze가 방, 벽, 문을 생성하기 위해 생성 방법을 알고 있는 개체를 매개변수로 넘겨받을 수 있다면, 생성 방법이 바뀔 때마다 새로운 매개변수를 넘겨받음으로써 생성할 객체의 유형을 달리할 수 있다. ⇒ 추상 팩토리 패턴


### Builder Pattern<br>(빌드 패턴)
- 복잡한 인스턴스를 단계적으로 조립하는 패턴
- 퍼사드 패턴은 서브시스템을 어떻게 객체로 표현할 수 있는지 설명하고, 플라이급 패턴은 규모는 작지만 개수는 많은 객체를 다루는 방법을 설명한다. 추상팩토리 패턴과 빌더 패턴은 다른 객체를 생성하는 책임만 있는 객체를 만들어 낸다. 방문자 패턴과 명령 패턴은 요청을 자신이 처리하는 것이 아니라, 다른 객체나 객체 집합이 요청을 처리하여 구현하도록 책임지는 객체를 만들어 낸다.
- 알고리즘 의존성. 변경이 가능한 알고리즘은 분리해낸다.
- -CreateMaze가 생성하고자 하는 미로에 방, 문, 벽을 추가하는 연산을 사용해서 새로운 미로를 만들 수 있는 객체를 넘겨받는다면 미로를 만드는 방법이나 변경을 이 객체의 상속을 통해서 해결할 수 있다. ⇒ 빌더 패턴

### Factory Method Pattern<br>(팩토리 메소드 함수)
- 상위 클래스에서 인스턴스 작성법의 뼈대를 세우고  
  구체적인 작성은 하위 클래스에서 실행하는 패턴
- 특정 클래스에서 객체 생성. 이를 방지하려면 객체를 직접 생성해서는 안된다.
- -CreateMaze가 방, 벽, 문을 생성하기 위해서 생성자를 이용하지 않고 가상 함수를 호출하도록 구현되어 있다면, 이 가상 함수의 실제 구현을 다양한 방법으로 변경할 수 있다. ⇒ 팩토리 메서드 패턴

### Prototype Pattern<br>(프로토타입 패턴) 원형
- 모형이 되는 인스턴스를 복사해서 인스턴스 만드는 패턴
- 특정 클래스에서 객체 생성. 이를 방지하려면 객체를 직접 생성해서는 안된다.
- -CreateMaze를 이미 만든 다양한 방, 문, 벽 객체로 매개변수화하는 방법도 가능한데, 이미 만든 객체를 복사해서 미로에 추가하면, 이들 인스턴스를 교체하여 미로의 복합 방법을 변경할 수 있다. ⇒ 원형 패턴

### Singleton Pattern<br>(싱글톤 패턴) 단일체
- 인스턴스가 하나만 존재하게 하는 패턴
- -한 게임에 오로지 하나의 미로 객체만 존재할 수 있고 그 게임에서 돌아가는 모든 게임 객체들이 이 미로에 접근이 가능하도록 보장한다. 전역 변수, 전역 함수 의존할 필요가 없어진다. ⇒ 단일체 패턴


---
---
## 구조 패턴 (Structural)

구조패턴은 인터페이스의 `상속 구조`나 객체의 `기능`을 `추가`하는  
방식과 같은 `클래스나 객체의 구조`에 관한 패턴입니다.

구조(Structural) “클래스” 패턴은 상속을 이용해서 클래스를 복합하고, 구조 “객체” 패턴은 깨체를 합성하는 방법을 정의합니다.


### Adapter Pattern<br>(어댑터 패턴) 적응자
- 서로 다른 인터페이스(API)를 갖는 클래스들을 연결하는 패턴
- 클래스 변경이 편하지 못한 점.

### Bridge Pattern<br>(브릿지 패턴) 가교
- 두 종류의 확장이 혼재하는 프로그램을  
  기능의 계층과 구현의 계층으로 분리하고  
  그 사이를 연결하는 패턴
- 하드웨어와 소프트웨어 플랫폼에 대한 의존성. 플랫폼 종속성을 제거한다.
- 객체의 표현이나 구현에 대한 의존성. 정보를 사용자에게 감춤
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 서브클래싱을 통한 기능 확장. 일반적으로 객체 합성과 위임은 행동 조합을 위한 상속보다 훨씬 유연한 방법이다. 많은 디자인 패턴에서는 그냥 서브클래스를 정의하고 다른 인스턴스와 새로 정의한 클래스의 인스턴스를 합성해서 기능을 재정의하는 방법을 도입한다.
- 위임에 전적으로 의존하는 패턴들. 중재자 패턴은 객체 간의 교류를 중재하는 객체를 도입하여 중재자 객체가 다른 객체로 연산을 전달하도록 구현한다. 책임 연쇄 패턴은 한 객체에서 다른 객체로 고리를 따라서 요청의 처리를 계속 위임한다. 가교 패턴은 구현과 추상적 개념을 분리하는 패턴이다. 추상화와 특정 구현을 대응시키고 추상화는 단순히 자신의 연산을 구현에 전달한다.
- Window 클래스와 WindowImp 클래스 간의 관련성은 가교 패턴의 한 예이다. 서로 독립적으로 확장되지만 함께 동작해야 하는 개념들을 별도의 클래스 계층으로 분리하는 것이 가교 패턴의 목적이다. 이렇게 두 개의 계층으로 분리할 때는 두가지의 기준을 세워야 한다. 하나는 논리적 개념에 해당하는 윈도우이고, 다른 하나는 그 윈도우에 대한 서로 다른 물리적 구현이다. 가교 패턴을 적용하면, 윈도우 시스템에 종속적인 구현과 전혀 상관없이 논리적인 윈도우 추상화를 확장할 수 있고, 그 반대로 추상적 개념과 무관하게 새로운 윈도우 시스템의 구현도 추가할 수 있다.
- 여러 개의 윈도우 플랫폼을 허용하기 위한 가교 패턴



### Composite Pattern<br>(복합체 패턴)
- 그릇과 내용물을 동일시해서 재귀적인 구조를 구축하는 패턴
- 복합체 패턴에서 Component 클래스는 공통의 인터페이스를 정의하고, Composite 클래스는 공통의 구현을 정의한다.
-  복합체 패턴과 장식자 패턴은 복잡한 실행 구조를 구축하는 데 유용한 패턴이다.
-  복합체 패턴은 객체지향 관점에서 재귀적 합성을 표현하는 패턴이다.
-  문서의 물리적 구조를 표현하기 위한 복합체 패턴

### Decorator Pattern<br>(데코레이터 패턴) 장식자
- 장식과 내용물을 동일시해 장식을 여러 겹 중복되게 하는 패턴
- 장식자 패턴(데코레이터)과 프록시 패턴은 장식되고 중재되는 객체와 동일한 인터페이스를 갖도록 장식자 객체와 프록시 객체의 인터페이스를 요청한다.
- 서브클래싱을 통한 기능 확장. 일반적으로 객체 합성과 위임은 행동 조합을 위한 상속보다 훨씬 유연한 방법이다. 많은 디자인 패턴에서는 그냥 서브클래스를 정의하고 다른 인스턴스와 새로 정의한 클래스의 인스턴스를 합성해서 기능을 재정의하는 방법을 도입한다.
- 클래스 변경이 편하지 못한 점.
-  복합체 패턴과 장식자 패턴은 복잡한 실행 구조를 구축하는 데 유용한 패턴이다.
-  장식자 패턴은 “투명한 포함” 개념에 의해 장식을 지원하는 클래스와 포함되는 객체들 사이의 관계를 잡아낸 것이다. 장식자 패턴에서 “장식은”은, 객체에 추가할 수 있는 모든 책임에 해당한다. 장식에 해당하는 예로는, 처리부를 갖는 추상 구문 트리, 새로운 상태 전이를 갖는 유한 상태 오토마타(finite state automata), 속성 태그를 갖는 영속성 객체망 등이 있는데, 이것은 기본 객체에 추가적인 책임이 부여된 예들이다.
-  <투명한 포함(transparent enclosure) 개념>
  1. 단일 자식(다른 말로 단일 구성요소)에 기반을 둔 합성과
  2. 호환되는 인터페이스의 개념을 조합한 것
- 사용자 인터페이스를 꾸미기 위한 장식자 패턴





### Facade Pattern<br>(퍼사드 패턴)
- 복잡하게 얽힌 클래스를 개별적으로 제어하는 것이 아니라  
  창구 역할을 하는 클래스를 하나 배치해서 시스템  
  전체의 조작성을 좋게 하는 패턴
- 퍼사드 패턴은 서브시스템을 어떻게 객체로 표현할 수 있는지 설명하고, 플라이급 패턴은 규모는 작지만 개수는 많은 객체를 다루는 방법을 설명한다. 추상팩토리 패턴과 빌더 패턴은 다른 객체를 생성하는 책임만 있는 객체를 만들어 낸다. 방문자 패턴과 명령 패턴은 요청을 자신이 처리하는 것이 아니라, 다른 객체나 객체 집합이 요청을 처리하여 구현하도록 책임지는 객체를 만들어 낸다.
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.

### Flyweight Pattern<br>(플라이급 패턴)
- 복수의 장소에서 동일한 것이 등장할 때  
  그것들을 공유해서 낭비를 없애는 패턴
- 퍼사드 패턴은 서브시스템을 어떻게 객체로 표현할 수 있는지 설명하고, 플라이급 패턴은 규모는 작지만 개수는 많은 객체를 다루는 방법을 설명한다. 추상팩토리 패턴과 빌더 패턴은 다른 객체를 생성하는 책임만 있는 객체를 만들어 낸다. 방문자 패턴과 명령 패턴은 요청을 자신이 처리하는 것이 아니라, 다른 객체나 객체 집합이 요청을 처리하여 구현하도록 책임지는 객체를 만들어 낸다.

### Proxy Pattern<br>(프록시 패턴)
- 정말로 목적한 것이 필요하게 될 때까지  
  대리인을 사용해서 처리를 진행시키는 패턴
- 장식자 패턴과 프록시 패턴은 장식되고 중재되는 객체와 동일한 인터페이스를 갖도록 장식자 객체와 프록시 객체의 인터페이스를 요청한다.
- 객체의 표현이나 구현에 대한 의존성. 정보를 사용자에게 감춤


---
---
## 행위 패턴 (Behavioral)

행위패턴은 `객체간`의 `상호작용`과 `책임분산`에 관련된 패턴입니다.

행동(Behavioral) “클래스” 패턴은 상속을 이용해서 알고리즘과 제어 흐름을 기술하고, 행동 “객체” 패턴은 하나의 작업을 수행하기 위해 객체 집합이 어떻게 협력하는지를 기술합니다.


### Chain of Responsibility Pattern<br>(책임 연쇄 패턴)
- 복수의 오브젝트(객체)가 연결되어 있는  
  내부의 어딘가에서 일을 수행하는 패턴
- 첵임 연쇄 패턴에 나오는 객체들은 반드시 동일한 타입을 가져야 하지만, 이들이 구현을 공유할 부분은 없다.
- 특정 연산에 대한 의존성. 요청의 처리 방법을 직접 코딩하는 방식을 피한다.
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 서브클래싱을 통한 기능 확장. 일반적으로 객체 합성과 위임은 행동 조합을 위한 상속보다 훨씬 유연한 방법이다. 많은 디자인 패턴에서는 그냥 서브클래스를 정의하고 다른 인스턴스와 새로 정의한 클래스의 인스턴스를 합성해서 기능을 재정의하는 방법을 도입한다.
- 위임에 전적으로 의존하는 패턴들. 중재자 패턴은 객체 간의 교류를 중재하는 객체를 도입하여 중재자 객체가 다른 객체로 연산을 전달하도록 구현한다. 책임 연쇄 패턴은 한 객체에서 다른 객체로 고리를 따라서 요청의 처리를 계속 위임한다. 가교 패턴은 구현과 추상적 개념을 분리하는 패턴이다. 추상화와 특정 구현을 대응시키고 추상화는 단순히 자신의 연산을 구현에 전달한다.
- 책임 연쇄 패턴은 상속이 드러나지 않는 교류 패턴을 만들어 낸다.

### Command Pattern<br>(커맨드 패턴) 명령
- 요구나 명령을 형태로 만들어서 클래스로 표현하는 패턴
- 퍼사드 패턴은 서브시스템을 어떻게 객체로 표현할 수 있는지 설명하고, 플라이급 패턴은 규모는 작지만 개수는 많은 객체를 다루는 방법을 설명한다. 추상팩토리 패턴과 빌더 패턴은 다른 객체를 생성하는 책임만 있는 객체를 만들어 낸다. 방문자 패턴과 명령 패턴(커맨드)은 요청을 자신이 처리하는 것이 아니라, 다른 객체나 객체 집합이 요청을 처리하여 구현하도록 책임지는 객체를 만들어 낸다.
- 명령(커맨드), 감시자, 상태, 전략 패턴은 순수 인터페이스인 추상 클래스를 써서 구현될 때가 많다.
- 특정 연산에 대한 의존성. 요청의 처리 방법을 직접 코딩하는 방식을 피한다.
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 명령 패턴은 요청을 어떻게 캡슐화하는지 설명하는 패턴이다. 명령 패턴은 요청을 발생시키는 데 필요한 균일한 인터페이스를 규정해 주기 때문에, 사용자 쪽에서는 서로 다른 요청을 동일하게 처리할 수 있다. 또한, 이 패턴에는 취소와 재실행을 처리하는 인터페이스를 추가할 수도 있다.
- 취소 가능한 사용자 연산을 위한 명령 패턴

### Interpreter Pattern<br>(인터프리터 패턴) 해석자
- 문법 규칙을 클래스로 표현하는 패턴

### Iterator Pattern<br>(반복자 패턴)
- 복수의 요소가 모여 있는 집합에서  
  요소를 순서대로 지정해서 처리하는 패턴
- 알고리즘 의존성. 변경이 가능한 알고리즘은 분리해낸다.
- 반복자 패턴은 객체 구조에 대한 접근 및 순회 방법을 지원하기 위한 기법을 잡아낸 패턴이다. 반복자 패턴은 다양화될 수 있는 개념들을 캡슐화하면 어떻게 유연성과 재사용성 헤택을 취할 수 있는지 보여주는 예이다.
- 객체 구조를 접근하고 순회하기 위한 반복자 패턴

### Mediator Pattern<br>(중재자 패턴)
- 복수의 클래스가 서로 직접 의사 소통을 하는 것이 아니라  
  중개역을 하는 클래스를 하나 준비하고 그 클래스하고만  
  의사 소통을 하게 해서 프로그램을 단순하게 만드는 패턴
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 위임에 전적으로 의존하는 패턴들. 중재자 패턴은 객체 간의 교류를 중재하는 객체를 도입하여 중재자 객체가 다른 객체로 연산을 전달하도록 구현한다. 책임 연쇄 패턴은 한 객체에서 다른 객체로 고리를 따라서 요청의 처리를 계속 위임한다. 가교 패턴은 구현과 추상적 개념을 분리하는 패턴이다. 추상화와 특정 구현을 대응시키고 추상화는 단순히 자신의 연산을 구현에 전달한다.

### Memento Pattern<br>(메멘토 패턴)
- 현재의 상태를 저장해 두고 필요할 때 복귀시키는  
  undo 기능을 설정하는 패턴
- 메멘토 패턴은 객체의 내부 상태를 어떻게 저장하고 캡슐화해야 하는지를 정의함으로써 객체가 나중에 그 상태로 복구할 수 있는 방법을 알려준다.
- 객체의 표현이나 구현에 대한 의존성. 정보를 사용자에게 감춤

### Observer Pattern<br>(옵저버 패턴) 감시자
- 상태가 변화하는 클래스와 그 변화를 통지받는 클래스를  
  분리해서 생각하는 패턴
- 명령, 감시자(옵저버), 상태, 전략 패턴은 순수 인터페이스인 추상 클래스를 써서 구현될 때가 많다.
- 높은 결합도. 추상 클래스 수준에서 결합도를 정의한다거나 계층화시키는 방법으로 디자인 패턴은 낮은 결합도의 시스템을 만들도록 한다.
- 서브클래싱을 통한 기능 확장. 일반적으로 객체 합성과 위임은 행동 조합을 위한 상속보다 훨씬 유연한 방법이다. 많은 디자인 패턴에서는 그냥 서브클래스를 정의하고 다른 인스턴스와 새로 정의한 클래스의 인스턴스를 합성해서 기능을 재정의하는 방법을 도입한다.
- 감시자 패턴으로 만드는 런타임 구조는 이 패턴을 잘 알고 있지 않는 한 이해하기가 종종 까다롭다. 

### State Pattern<br>(상태 패턴)
- 상태를 클래스로 표현해서 상태에 맞는  
  분기문의 사용을 줄여주는 패턴
- 상태 패턴은 대상들의 각 상태를 객체로 표현합니다.
- 명령, 감시자, 상태, 전략 패턴은 순수 인터페이스인 추상 클래스를 써서 구현될 때가 많다.
- 상태 패턴에서 객체는 현재 상태를 표현하는 상태 객체에 요청의 처리를 위임한다.
- 이 두 패턴의 목적은 처리를 전달하는 객체를 변경하지 않고 객체의 행동을 변경할 수 있게 하자는 것이다.

### Strategy Pattern<br>(전략 패턴)
- 알고리즘을 전부 교체해서 수정하기 쉽도록 하는 패턴
- 전략 패턴은 상호교환이 가능한 알고리즘군을 어떻게 구현할지를 설명합니다.
- 명령, 감시자, 상태, 전략 패턴은 순수 인터페이스인 추상 클래스를 써서 구현될 때가 많다.
- 알고리즘 의존성. 변경이 가능한 알고리즘은 분리해낸다.
- 서브클래싱을 통한 기능 확장. 일반적으로 객체 합성과 위임은 행동 조합을 위한 상속보다 훨씬 유연한 방법이다. 많은 디자인 패턴에서는 그냥 서브클래스를 정의하고 다른 인스턴스와 새로 정의한 클래스의 인스턴스를 합성해서 기능을 재정의하는 방법을 도입한다.
- 전략 패턴에서 객체는 요청을 수행하는 추상화한 전략 객체에게 특정 요청을 위임한다.
- 이 두 패턴의 목적은 처리를 전달하는 객체를 변경하지 않고 객체의 행동을 변경할 수 있게 하자는 것이다.
- 알고리즘을 객체로 캡슐화하는 것, 이것이 전략 패턴의 의도이다. 이 전략 패턴의 주요 참여자는 Strategy 패턴을 구현한 객체(서로 다른 알고리즘들을 캡슐화한)와 이 객체가 동작할 전후 관계, 즉 동작 환경(context)이다.
- 전략 패턴을 적용하는 데 가장 중요한 것은 전략과 동작 환경에 대한 인터페이스를 충분히 일반화해야 한다는 것이다. 새로운 알고리즘을 지원하기 위해서 전략이나 배경 인터페이스를 변경할 필요는 없다.
- 서로 다른 서식 설정 알고리즘을 위한 전략 패턴

### Template Method Pattern<br>(템플릿 메소드 패턴)
- 상위 클래스에서 처리의 뼈대를 세우고,  
  구체적인 처리를 하위 클래스에서 실행하는 패턴
- 알고리즘 의존성. 변경이 가능한 알고리즘은 분리해낸다.

### Visitor Pattern<br>(방문자 패턴)
- 데이터 구조를 돌아다니면서 동일한 조작을  
  반복해서 적용하는 패턴
- 퍼사드 패턴은 서브시스템을 어떻게 객체로 표현할 수 있는지 설명하고, 플라이급 패턴은 규모는 작지만 개수는 많은 객체를 다루는 방법을 설명한다. 추상팩토리 패턴과 빌더 패턴은 다른 객체를 생성하는 책임만 있는 객체를 만들어 낸다. 방문자 패턴과 명령 패턴은 요청을 자신이 처리하는 것이 아니라, 다른 객체나 객체 집합이 요청을 처리하여 구현하도록 책임지는 객체를 만들어 낸다.
- 방문자 패턴에서 방문자 인터페이스는 방문자 객체가 방문하는 객체들의 클래스 인터페이스를 그 방문자 인터페이스에 모두 반영하도록 한다.
- 알고리즘 의존성. 변경이 가능한 알고리즘은 분리해낸다.
- 클래스 변경이 편하지 못한 점.
- 방문자 패턴에서, 객체 구조의 각 요소에 수행하는 연산은 언제나 방문자 객체에게 위임된 연산이다.
- 이 패턴의 주요 참여자가 바로 Visitor 클래스와 서브클래스이다. Visitor 패턴은 Glyph 클래스의 변경 없이도 추가 가능성을 내포한 글리프 구조 분석을 가능하게 하려고 사용한 기법을 잡아낸 것이다. 꼭 복합 객체에만 적용할 수 있는 것이 아니라 모든 구조에 다 적용할 수 있다. 방문자가 방문하는 클래스들이 꼭 동일한 부모 클래스를 가질 필요도 없다. 방문자 패턴을 사용하기 전에 반드시 확인해야 하는 부분 하나가 있다. 가장 자주 변경되는 클래스 계층이 무엇인가 하는 것이다. 구조 클래스 구조가 안정된 상태에서 객체에게 여러 가지 일을 많이 시키고 싶다면 방문자 패턴을 사용하는 것이 좋다. 기존 클래스 구조에 새로운 (서브)클래스가 추가되면 반드시 Visitor 클래스에 Visit...() 연산을 추가해야 한다는 것을 잊지 말아야 한다.
- 문서 구조의 구현을 복잡하게 하지 않고 다수의 분석 기능을 제공하기 위한 방문자 패턴



 

