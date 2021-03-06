---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 템플릿 # 제목
excerpt             : 템플릿 입니다. # 썸네일 한줄 요약
last_modified_at    : # 2020-11-22 # 작성일 또는 마지막 수정일
categories          : # java dataStructure algorithm git math course etc/ workout journal
tags                : 
toc                 : # 목차 사용 default: true
toc_label           : # 목차 제목 default: "목차"
# 알림박스 = {: .notice--info}
---


## 코드 언급
```java
import java.util.*;
```
## 코드 삽입
{% highlight java linenos %}
public static class Main {
  public static void main(String[] args) {
    System.out.println("hello world");
  }
}
{% endhighlight %}

## 텍스트 박스
`/assets/images/background.jpg`

## 알림
**강조하기** 기본 알림 박스.
{: .notice--info}

## 부연설명 첨삭
You can just type sout[^sout] [^or-not].

[^sout]: it'll turn to `System.out.println();` automatically.
[^or-not]: or not.

## [링크](https://google.com)
이메일 링크: <address@example.com>

## [버튼](https://github.com/weirdbb91){: .btn .btn--info .btn--large}

## 줄 삽입
---

## 그대로 출력
{% raw %}{% highlight %}{% endraw %}

## Gist 삽입
<script src="https://gist.github.com/mmistakes/77c68fbb07731a456805a7b473f47841.js"></script>


# 1. 마크다운에 관하여

## 순서 있는 목록
숫자를 쓰면 된다.
1. 한개와
1. 두 개는
1. 차이가 있다.

## 순서 없는 목록
글머리 기호: `*`, `+`, `-` 지원.
* 빨강
  * 녹색
    * 파랑
* 1단계
  - 2단계
    + 3단계
      + 4단계

## 블럭인용문자
좌측 선은 ```>```를 이용한다.
> 블럭 인용문자
> * List
>	```
>	code
>	```

## 들여쓰기

This is a normal paragraph:

    This is a code block.

end code block.

> 한줄 띄어쓰지 않으면 인식이 제대로 안되는 문제가 발생합니다.

## 강조

*single asterisks*

**double asterisks**

~~cancelline~~


## 이미지 첨부
![석촌호수 러버덕](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0)
![석촌호수 러버덕](http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0 "RubberDuck")

사이즈 조절 기능은 없기 때문에 ```<img width="" height=""></img>```를 이용한다.

<img src="http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="RubberDuck"></img><br/>
<img src="http://cfile6.uf.tistory.com/image/2426E646543C9B4532C7B0" width="40%" height="30%" title="%(비율) 크기 설정" alt="RubberDuck"></img>
