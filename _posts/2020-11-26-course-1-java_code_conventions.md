---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 자바 코드 컨벤션 # 제목
excerpt             : Java Code Conventions # 썸네일 한줄 요약
last_modified_at    : 2020-11-26 # 2020-11-22 # 작성일 또는 마지막 수정일
categories          : course # java dataStructure algorithm git liquid math course / workout journal
tags                : conventions
toc                 : # 목차 사용 default: true
toc_label           : # 목차 제목 default: "목차"
# 알림박스 = {: .notice--info}
---
---

[자바 코드 컨벤션](https://google.github.io/styleguide/javaguide.html#s2.1-file-name)을 읽고 그 일부를 정리해봤다.

출처 : [https://google.github.io/styleguide/javaguide.html#s2.1-file-name](https://google.github.io/styleguide/javaguide.html#s2.1-file-name)

---
---
# 1 소개
---
---

## 1.1 용어 참고

 * `클래스(class)`는 일반 클래스, 열거형 클래스, 인터페이스 또는 주석유형(@interface)을 의미합니다.  
 * 클래스의 `멤버(member)`는 내부의 클래스, 필드, 메서드 또는 생성자를 의미합니다.  
      즉, 이니셜 라이저와 주석을 제외한 클래스의 모든 최상위 콘텐츠입니다.  
 * `주석(comment)` 이라는 용어 는 항상 구현 주석을 의미합니다.  
      "문서 주석(documentation comments)"이라는 문구는 사용하지 않습니다.  
      대신 "Javadoc"이라는 일반적인 용어를 사용합니다.  

---
---
# 2 소스 파일 기본
---
---

## 2.1 파일 이름

소스 파일의 이름은 최상위 클래스의 이름(정확히 하나만 있음, 대소문자 구분)과 .java확장자로 구성됩니다.

---

## 2.3.1 공백 문자

소스파일에서 사용하는 공백 문자는 오직 ASCII 가로 공백 문자(0x20) 하나 입니다.  
(줄 마침 시퀀스 제외)  

 * 

---