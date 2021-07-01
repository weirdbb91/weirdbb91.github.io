---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 도커 기본 2 # 제목
excerpt             : 도커 기본 # 썸네일 한줄 요약
last_modified_at    : 2021-05-10 # 마지막 수정일
categories          : etc
tags                : Docker Python
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---

출처 : 위키북스, 시작하세요! 도커/쿠버네티스

🚫 아래 내용은 책을 읽고 난 주관적인 해석이므로 사실과 다를 수 있습니다.

## 기존 가상화 방식과 도커 컨테이너 방식의 비교

기존 가상머신들의 경우 호스트 머신의 OS 위에 Hypervisor(가상머신을 만들거나 실행시키는 에뮬레이터)가 각각의 가상머신에 독립적인 자원을 할당하고 게스트 OS를 설치해 애플리케이션을 구동했다

그러나 도커 컨테이너의 경우 호스트OS 위에 Hypervisor를 대신해 도커 엔진이 자리하고 별도의 게스트 OS 없이 애플리케이션이 구동된다


애플리케이션 별로 각각의 게스트 OS가 생략되기 때문에 성능 저하가 

