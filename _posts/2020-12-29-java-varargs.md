---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 가변인자 # 제목
excerpt             : Java VarArgs # 썸네일 한줄 요약
last_modified_at    : 2020-12-29 # 마지막 수정일
categories          : etc
tags                : ETC Java VarArgs
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---

## 출처 [oracle](https://docs.oracle.com/javase/8/docs/technotes/guides/language/varargs.html)

## 출처 [baeldung](https://www.baeldung.com/java-varargs)

사용 언어 자바

## 가변인자 VarArgs

임의의 갯수의 매개변수를 받을 때,  
변수의 갯수마다 전부 오버로딩을 해야만 하는줄 알았다  

그러나 VarArgs 가변인자를 사용하면 그럴 필요가 없어진다  


## 사용방법

가변인자는 자료형 뒤에 `...`을 붙여 명시한다  

```java
public String formatWithVarArgs(String... values){ ..내용 생략.. }

formatWithVarArgs();
formatWithVarArgs("a", "b", "c", "d");
```

가변인자는 항상 마지막 매개변수 자리에 위치해야하며  
각 메소드당 단 하나의 가변인자만 사용이 가능하다  


## 유의사항

- 전달받은 VarArgs 가변인자는 일반 배열로 취급된다
- Heap Pollution(힙 오염) 발생에 유의
  - 다른 타입의 변수를 가리키려하면 발생(ClassCastException)
  - 타입을 명확히하는 확인절차를 거치는게 좋다

## 안전한 사용방법

가변인자를 사용하게되면 Java 컴파일러가 암묵적으로 배열을 생성하고  
그 배열에 전달할 인자들을 담아 보내게 된다  

- 이 배열에는 아무것도 저장하지 말 것
- 이 배열의 참조(주소값)가 메소드 밖으로 나가지 않도록 유의

## 경고

제네릭과 함께 가변인자를 사용할 경우,  
Java 컴파일러가 치명적인 런타입 예외 발생의 가능성을 경고한다  

만약 정말 확실히 진짜로 안전하다면 `@SafeVarargs`으로 경고를 끌 수 있다

VarArgs는 임의의 수의 매개변수를 전달받기 위함이지  
다른 목적으로 사용해선 안된다

---
---

왜 이런 개꿀 기술을 아무도 안가르쳐줬는지 이해가 된다  
이것은 최대한 쓰지 않는 것이 좋을것 같다  