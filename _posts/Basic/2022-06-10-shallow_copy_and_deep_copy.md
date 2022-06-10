---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 얕은 복사와 깊은 복사 # 제목
excerpt             : Shallow copy and Deep copy # 썸네일 한줄 요약
categories          : Basic
tags                : Basic Shallow_copy Deep_copy
---

출처 모름: 그냥 알던거 정리  

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

## 변수와 할당의 개념

```java
// 예시에 사용할 객체
class A {
    int data;
    
    A(int data) { this.data = data; }

    int getData() { return data; }
}

A a = new A(1);
// new A(1) 구문으로 새로운 객체를 메모리에 할당하고,
// A a = {객체}; 구문으로 위 객체의 주소 값을 변수 a에 할당했다.
// a.data = 1
// a.hashCode() = 292938459

```

## 얕은 복사(Shallow copy)란?

복사할 대상의 주소 값만을 복사하는 것을 말한다.

```java
A b = a; // 얕은 복사(Shallow copy)
// 변수 a에 할당된 값은 객체의 주소 값이므로,
// 변수 b에 할당된 값 또한 같은 주소 값이다.
// a.data = 1
// b.data = 1

// a.hashCode() = 292938459
// b.hashCode() = 292938459

// a와 b가 가리키는 주소 값이 같기 때문에 b.data는 a.data다.
b.data = 2;
// 두 변수가 가리키는 객체가 같아, 영향을 받은 객체도 하나다.
// a.data = 2
// b.data = 2
```

## 깊은 복사(Deep copy)란?

복사할 대상의 데이터 값 자체를 복사하는 것을 말한다.

```java
A b = new A(a.getData()); // 깊은 복사(Deep copy)
// 얕은 복사와는 다르게 a의 데이터와 동일한 데이터를 가지는,
// 새로운 객체를 선언하고, 새 객체의 주소를 변수 b에 할당한다.
// a.data = 1
// b.data = 1

// a.hashCode() = 292938459
// b.hashCode() = 1993134103

// a와 b가 가리키는 주소 값이 달라, b.data는 a.data가 아니다.
b.data = 2;
// 두 변수가 서로 다른 객체를 가리키고 있어서 결과도 다르다.
// a.data = 1
// b.data = 2
```

## 자바의 String

[자바의 String](../../Language/Java/string_in_java) 클래스는 문자열을 저장하는 클래스이다.  
[자바의 String](../../Language/Java/string_in_java) 클래스는 불변(Immutable)의 성질을 가지고 있어  
변경이 불가하므로,  
얕은 복사를 하더라도 주소 값 자체가 변경되기 때문에  
같은 객체를 참조하던 다른 변수가 영향을 받을 일은 없다.  
