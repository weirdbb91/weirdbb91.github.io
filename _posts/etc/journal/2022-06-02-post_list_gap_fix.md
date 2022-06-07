---
title       : 포스트 목록 오류 해결
excerpt     : 언어별 폰트 높이 차이 # 썸네일 한줄 요약
categories  : ETC
tags        : 일기
---

# 문제점

포스트의 목록은 한줄당 3개의 포스트로 4줄, 즉 최대 12개의 포스트를 출력한다.  
그러나 그 중 중 좌측을 기준으로 한칸 또는 두 칸의 공백이 생기는 경우가 있었다.

자료화면 1
<img src="/assets/images/posts/2022-06-02-post_list_gap_fix/row_error_image_1.png" alt="자료화면1">

자료화면 2
<img src="/assets/images/posts/2022-06-02-post_list_gap_fix/row_error_image_2.png" alt="자료화면2">

---

# 문제점 분석

- 좌측을 기준으로 공백 발생
- 공백이 생긴 경우 4줄 초과 출력

---

# 문제점 확인

개발자 도구로 살펴보니 각 포스트의 높이가 달랐다.  
포스트 중에서도 타이틀의 높이만 달랐으며,  
정확히는 타이틀로 출력되는 언어에 따라 높이가 달라졌다.

한글이 포함된 타이틀이 그렇지 않은 타이틀의 높이보다 미묘하게 높아서  
다음 라인이 출력될 때 윗줄에서 튀어나온 그 미묘한 턱에 밀려난것이었다.

포스트의 목록을 수식하는 CSS 파일을 찾아  
포스트 타이틀의 높이에 관여하는 부분 점검.

```css
/_sass/minimal-mistakes/_archive.scss

.archive__item-title {
  margin-top: 0;
  margin-bottom: 0.25em;
  font-family: $sans-serif-narrow;
  line-height: initial; // <- 요놈이 문제임
  ...
}
```

위 수식 중 line-height 항목이  
최상위에서 모든 타이틀 태그들을 수식하는  

```css
/_sass/minimal-mistakes/_base.scss

h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 2em 0 0.5em;
  line-height: 1.2;
  font-family: $header-font-family;
  font-weight: bold;
}
```

위 수식을 오버라이딩 해 모든 폰트에 적용되었던 높이가  
각 폰트별 기본값으로 높이가 설정되었다.  
[참고자료 - w3schools CSS line-height Property](https://www.w3schools.com/cssref/pr_dim_line-height.asp)

---

# 해결

해당 수식 삭제  

---

# 느낀점

확실히 직접 작성하지 않은 외부의 템플릿이나 패키지를 사용하려면  
그 구조나 작동방식에 대한 어느정도의 이해가 반드시 필요하다고 느꼈다.  

웹개발자는 백엔드나 프론트엔드로 구분할 수 없다.  
다 알아야된다.

따흑.......

---
