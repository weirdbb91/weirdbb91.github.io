---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 캡슐화 # 제목
excerpt             : 캡슐화의 정의 # 썸네일 한줄 요약
last_modified_at    : 2020-12-06 # 마지막 수정일
categories          : oop
tags                : OOP
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---
이 글은 아래의 출처에서 내용을 참고하여 작성하였습니다.  
출처 : [https://yrok.tistory.com/](https://yrok.tistory.com/)

---
---

객체지향 프로그램은 객체(Object)로 만듭니다.  
객체는 데이터와 이 데이터에 연산을 가하는 프로시저(Procedure)를 함께 묶은 단위입니다.  
프로시저를 일반적으로 메서드(Method) 또는 연산(Operation)이라고 합니다.  
객체는 요청(Request) 또는 메시지(Message)를 사용자에게 받으면 연산을 수행합니다.  

요청은 객체에 연산을 실행하게 하는 유일한 방법이고,  
연산은 객체의 내부 데이터의 상태를 변경하는 유일한 방법입니다.  
이러한 접근의 제약 사항으로 객체의 내부 상태는 캡슐화(Encapsulate)된다고 말합니다.  
객체 외부에서는 객체의 내부 데이터에 직접 접근할 수 없고,  
객체의 내부 데이터 표현 방법(데이터 타입 등)을 알 수 없습니다.

