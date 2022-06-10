---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 자바의 String 타입 # 제목
excerpt             : 자바의 String 타입 # 썸네일 한줄 요약
categories          : Language Java
tags                : ETC Java String
---

출처: [More About Strings In Java](https://medium.com/omarelgabrys-blog/more-about-strings-in-java-fb2480af8a19)  

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.  

❗️ 한번에 이해가 안될 수도 있지만 일단 끝까지 읽어보자.  

## 자바의 String 타입

자바의 String 타입은 원시타입(Primitive type)에 속하지 않는다.  
자바의 String 타입은 객체 자체가 아닌 객체의 주소 값을 저장한다.  

String 변수를 또 다른 String 변수에 할당하면,  
객체의 주소 값을 할당하지 String 객체 자체를 할당하지 않는다.  

무슨 말이냐면,  
String 변수는 실제 String 객체 자체의 주소 값을 저장하므로  
넘겨주는 값은 실제 String 객체 자체가 아닌 그 주소 값이라는 뜻이다.  

> 주소 값이란, 데이터가 저장된 메모리의 위치 정보를 의미한다.

## 불변(Immutable)의 String

String 변수가 참조하는 객체(String 객체 자체)는 변경이 불가하다.  
String 변수의 length 값은 변수가 초기화되는대로 바로 정해진다.  

## 초기화 이후 String 변수를 변경하면?

String 객체는 불변이므로,  
String 변수는 메모리의 다른 장소(다른 주소 값)를 참조하게되고,  

이전의 String 객체는 만약 다른 곳에서 참조하고 있지 않다면,  
GC(Garbage Collection)에 의해 처리 가능한 상태가 된다.  

## 정리

String 변수의 재할당(변경)이 의미하는 바는  
변수가 참조하는 String 객체 자체(불변)가 변경되는게 아니라  
변수에 새로운 String 객체의 주소 값이 할당된다는 뜻이다.  

```java
// 일반 객체 변경
TestObject obj = new TestObject();
obj.setName("Object");
// Object.name: Object
// Object.hashCode(): 292938459
obj.setName("Object2");
// Object.name: Object2 - 주소 값에 해당하는 객체의 변경 O
// Object.hashCode(): 292938459 - 주소 값의 변경 X

// String 객체 변경
String testStr = "test";
// testStr: test
// testStr.hashCode(): 917142466

// "test2" 자체가 새로 메모리에 저장된 String 객체이고,
// 새 객체("test2")의 주소 값을 testStr 변수에 할당하는 구문이다.
testStr = "test2";
// testStr: test2 - 주소 값에 해당하는 객체의 변경 X
// testStr.hashCode(): 1993134103 - 주소 값의 변경 O
```
