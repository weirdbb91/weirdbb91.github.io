---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 소스트리 깃 토큰 인증  # 제목
excerpt             : 깃 토큰을 이용한 소스트리 인증 # 썸네일 한줄 요약
last_modified_at    : 2021-06-30 # 마지막 수정일
categories          : ETC
tags                : Sourcetree Git Auth Token
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---

현재 깃허브 인증 관련 이슈가 발생하고  
해결하게 된 정황 공유드립니다  

깃허브에서 비밀번호로 인증하는 방식을 비추천하게 되면서  
오늘부로 비밀번호로 인증이 어렵게 되었습니다  

그로인해 소스트리 이용자분들 중  
깃 비밀번호로 인증을 해오신분들도 어렵게 되었습니다

제가 해결한 방법으로는  

1.  브라우저에서 깃허브에 로그인  
2.  Settings -> Developer settings -> Personal access tokens  
3.  필요한 권한을 설정해 토큰 생성  
4.  Sourcetree 설정 -> 계정 -> 추가 또는 편집
    -  호스트: github
    -  인증방식: 베이직 
    -  프로토콜: HTTPS
    -  사용자 이름: 깃허브 계정 아이디
    -  암호: 3.에서 생성한 토큰 입력

이상입니다  