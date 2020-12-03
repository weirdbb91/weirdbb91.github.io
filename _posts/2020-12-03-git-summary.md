---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : Git - sumup # 제목
excerpt             : Git - Summary # 썸네일 한줄 요약
last_modified_at    : 2020-12-03 # 마지막 수정일
categories          : git
tags                : git, summary
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---
---
이 글은 아래의 출처에서 내용을 참고하여 작성하였습니다.  
출처 : [https://git-scm.com/](https://git-scm.com/)

---

## Git keywords
  - commit
 
  - branch 
    - \<BRANCH\> : 새 브랜치 생성
    - -f \<이동할 BRANCH\> \<목적지 COMMIT\> : 브랜치 강제 이동
    - -u \<REMOTE_BRANCH\> : 현재 브랜치가 해당 원격 브랜치를 대신 추적하게 설정
    - -u \<REMOTE_BRANCH\> \<BRANCH\>: [상동] + 특정 브랜치를 지정
 
  - checkout 
    - \<COMMIT\> : 현재 포인터를 해당 커밋으로 이동
    - -b \<BRANCH\> : 현재 포인터에 해당 이름으로 브랜치를 생성합니다
    - -b \<BRANCH\> \<REMOTE_BRANCH\> : [상동] + 원격 브랜치를 대신 추적하게 설정
  
  - cherry-pick 
    - \<COMMIT1\> \<COMMIT2\> \<...\> : 현재 포인터 밑으로 해당 커밋들을 복사
 
  - reset 
    - \<COMMIT\> : 현재 포인터에서 해당 커밋 전까지 전체 취소
 
  - revert
    - \<COMMIT\> : 현재 포인터 밑에 해당 커밋의 반대 내용으로 커밋
 
  - rebase 
    - \<COMMIT\> : 현재 브랜치를 복사해 해당 커밋에서부터 추가 커밋함<br>(소속이 같다면 포인터만 해당 브랜치로 이동)
  
    - -i \<COMMIT\> : [상동] + 커밋 순서를 원하는대로 재배치
  
  - merge 
    - \<COMMIT\> : 현재 포인터에서 해당 브랜치의 내용을 흡수한 커밋 실행
  
  - tag
    - \<TAG\> : \<HEAD\>에 태그 생성
    - \<TAG\> \<COMMIT\> : 해당 커밋에 태그 생성

  - describe : \<가장 가까운 부모 태그\>_\<거리\>_g<현재 커밋의 해시> 출력 
    - : 미지정시 \<HEAD\> 기준 
    - \<COMMIT\> : 해당 커밋 기준
  
  - 포인터 참조 \<COMMIT\>^, \<COMMIT\>~n, 중첩 가능 (ex. dp~2^2~6)
    - ^ : 한번에 한 커밋 위로 포인터 이동 (^^는 2커밋 위로)
    - ^\<n\> : n번째 부모로 참조
    - ~\<n\> : 한번에 n만큼 커밋 위로 포인터 이동


---

## Remote
  - fetch
    - : 원격 저장소의 커밋들을 로컬 저장소로 로드
  - pull
    - : fetch와 merge를 한번에 수행함
    - --rebase : fetch와 rebase를 한번에 수행함
  - push
    - : 로컬 저장소의 커밋들을 원격 저장소에 반영함
  - fakeTeamwork
    - : 원격 저장소에 새 커밋 생성
    - \<n\> : [상동] + n개 생성
    - \<BRANCH\> \<n\> : 해당 브랜치에서부터 n개 생성

---
