---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 깃 토큰 인증  # 제목
excerpt             : 깃 비밀번호 deprecated의 대안 토큰 인증 # 썸네일 한줄 요약
last_modified_at    : 2021-06-30 # 마지막 수정일
categories          : etc
tags                : Git Auth Token
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---

현재 깃허브 인증 관련 이슈가 발생하고  
해결하게 된 정황 공유드립니다  

깃허브에서 비밀번호로 인증하는 방식을 비추천하게 되면서  
오늘부로 비밀번호로 인증이 어렵게 되었습니다  

제가 해결한 방법으로는  

1.  브라우저에서 깃허브에 로그인  
2.  Settings -> Developer settings -> Personal access tokens  
3.  필요한 권한을 설정해 토큰 생성  
4.  credential-osxkeychain 사용을 위해 homebrew로 git 설치(깃에 내장됨)
    ```
    $ brew install git
    ```
5.  깃 설정에서 credential-osxkeychain 사용등록
    ```
    $ git config --global credential.helper osxkeychain
    ```
6.  credential-osxkeychain에 깃허브 아이디와 3번에서 발행한 토큰을 비밀번호로 입력
    ```
    echo "\
    protocol=https
    host=github.com
    username=깃허브아이디
    password=엑세스토큰" | git credential-osxkeychain store
    ```
