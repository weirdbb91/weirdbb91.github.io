---
title       : \[자바] 해시맵과 해시테이블의 차이
excerpt     : \[자바] 해시맵과 해시테이블의 차이 # 썸네일 한줄 요약
categories  : Language Java
tags        : ETC Java HashMap HashTable
---

출처 [구글 검색결과](https://javarevisited.blogspot.com/2010/10/difference-between-hashmap-and.html#axzz7EXZTwSXa)

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

---

HashMap과 Hashtable 모두 해싱과 Map 인터페이스 구현을 기반으로 하는 자료구조다  

## 차이점

### 1. Thread-safe

주요 차이점으로는 HashMap이 non-thread-safe한 것에 반해  
Hashtable은 thread-safe하다는 것이다  

그렇기 때문에 자바 멀티 스레드 어플리케이션에서 외부 동기화 처리 없이는 HashMap을 쓸 수 없다  
추가로 Hashtable의 thread-safety는 내부 동기화로 구현되었기 때문에 HashMap 보다 느리다

### 2. accept null as a key or value

또 다른 차이점으로는 HashMap이 key 또는 value 값으로 null을 허용하는데 반해  
Hashtable은 null을 key나 value 값으로 허용하지 않는다는 점  

### 3. Fail-fast/Fail-safe

HashMap에서는 Fail-fast한 Iterator를 사용하기 때문에  
Iterator 자신의 remove() 메소드가 아닌 다른 쓰레드에서 요소를 추가/삭제 하려하면  
ConcurrentModificationException이 발생한다  

그러나 Hashtable에서는 Fail-safe(non-fail-fast)한 Enumerator를 사용하므로  
순회 도중에 Hashtable이 구조적으로 수정(추가/삭제)되어도 예외를 발생시켜주지 않는다  

### 4. Performance

Hashtable의 thread-safety와 동기화 기능 때문에  
하나의 쓰레드 환경에서는 Hashtable이 HashMap 보다 느리다  

그러므로 동기화할 필요가 없고 하나의 쓰레드만 사용하는 환경이라면  
HashMap의 성능이 Hashtable 보다 훨씬 뛰어나다  
