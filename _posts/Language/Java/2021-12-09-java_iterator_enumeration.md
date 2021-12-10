---
title       : \[자바] Iterator와 Enumeration
excerpt     : \[자바] 이터레이더와 이뉴머레이션 # 썸네일 한줄 요약
categories  : Language Java
tags        : ETC Java Iterator Enumeration
---

출처 [구글 검색결과](https://www.geeksforgeeks.org/difference-between-iterator-and-enumeration-in-java-with-examples/), 개인적 의견 등

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

### 1. Enumeration

자바의 Collections 등장 이전의 집합 객체를 탐색하기 위한 목적의 인터페이스다  
커서(cursor)를 통해 집합 객체의 요소들을 순회하며 데이터를 꺼내올 수 있다  
다음 순서의 요소가 있는지 여부를 반환하는 hasMoreElements() 메소드와  
다음 요소를 반환하는 nextElement() 메소드를 포함한다  

---

### 2. Iterator

모든 Collection object에 사용(읽기/삭제) 가능  
구성 요소의 삭제 기능 remove()이 추가된 이뉴머레이션의 개선된 버전  
Set, List, Queue, Deque, Map 등의 인터페이스들을 구현하는  
모든 콜렉션 프레임워크들에서 이들을 열거하고 싶을때 사용한다  
모든 콜렉션 프레임워크에서 커서(cursor) 사용이 가능한 것은 이터레이터 뿐이다  

---

### 3. 차이점

|Iterator|Enumeration|
|--|--|
|모든 콜렉션 클래스들에서<br> 사용 가능한 범용 커서(cursor)다|오래된(legacy) 클래스들에서만<br> 사용 가능하다|
|요소를 삭제하는<br>remove() 메소드가 있다|삭제 메소드가 없다|
|순회중에 요소의<br>변경(삭제)가 가능하다|읽기 전용이므로<br>순회중 변경이 불가하다|
|HashMap,<br>LinkedList,<br>ArrayList,<br>HashSet,<br>TreeMap,<br>TreeSet<br>등에서 사용가능|Vector,<br>Hashtable에서<br>사용가능|

---

### 4. 부록 - Enum

이넘은 사용자 정의 타입이며, 주로 상수 집합을 정의하는데 사용된다  
정의에 사용되는 이름들은 프로그램의 유지보수와 가독성 향상에 도움이 된다  
자바(1.5 버전부터)의 이넘은 C/C++의 이넘보다 강력한 기능이 있다  
자바의 이넘에서는 변수나 메소드, 생성자를 추가할 수 있다  
이넘의 주목적은 자체 데이터 유형(Enumered Data Type)을 정의하는 것이다  
