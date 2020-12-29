---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 어댑터 패턴 # 제목
excerpt             : Structural Adapter Pattern # 썸네일 한줄 요약
last_modified_at    : 2020-12-12 # 마지막 수정일
categories          : gof
tags                : DesignPattern GoF Structural Adapter
toc                 : false # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
### Adapter Pattern<br>(적응자 패턴)
구조 패턴 (Structural)

서로 `인터페이스가 달라` 연결될 수 없는 객체나 메소드들을  
`중간`에서 `변환을 통해 연결`해주는 패턴  

```java
// int를 받아 int로 반환하는 객체
public class Math {
    public static int halfOf(int num) {
        return num/2;
    }
}

...

// String - int 어댑터
public class StrToIntNumAdapter implements NumAdapter {
    @Override
    public int convert(String num) {
        System.out.print("log도 가능 ");
        return Integer.parseInt(num);
    }
}

...

// String형태의 숫자를 반으로 나눠야 하는 객체
public class Print {
    public void printNum {
        NumAdapter numAdapter = new StrToIntNumAdapter();
        String num = "44";
        System.out.println(Math.halfOf(num));  
        // 에러
        System.out.println(Math.halfOf(numAdapter.convert(num)));  
        // log도 가능 22
    }
}
```