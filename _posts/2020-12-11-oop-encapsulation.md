---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 캡슐화 # 제목
excerpt             : Encapsulation # 썸네일 한줄 요약
last_modified_at    : 2020-12-11 # 마지막 수정일
categories          : oop
tags                : OOP Encapsulation
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

캡슐화는 객체의 `의존성을 낮추기` 위해 필요한 아주 중요한 개념이다  

캡슐화를 통해 `객체의 데이터와 연산을 하나로` 묶고,  
객체의 구성요소들을 `외부에서 직접 접근하지 못하게 은닉`하거나  
`변경할 수 없도록` 한다


```java
public class PersonalInformation {
  public static final String name = "홍길동";
  private String phoneNumber = "010-1234-1234";

  public void setPhoneNumber(String phoneNumber) {
    this.phoneNumber = phoneNumber; 
  }

  public String getPhoneNumber() { return phoneNumber; }
}
```