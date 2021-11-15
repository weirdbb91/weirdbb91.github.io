---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 도커 기본 # 제목
excerpt             : 도커 파이썬 환경 # 썸네일 한줄 요약
last_modified_at    : 2021-04-07 # 마지막 수정일
categories          : Cloud Docker
tags                : Basic Cloud Docker Python
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---

🚫 아래 내용은 주관적인 생각이므로 사실과 다를 수 있습니다.

사용 언어 파이썬

## 파이썬 가상환경 설치 & 활성화
```
python3 -m venv venv
 . venv/bin/activate
```

이후 개발하며 가상환경에 의존성 추가
``` 
...
pip install fastapi
pip install uvicorn
...
```

---

## 현재 가상환경의 의존성을 파일로 출력
```
pip freeze > requirements.txt
```

---

## Dockerfile 작성
```
# 메인 도커 이미지
FROM python:3.9.2

# 내부 작업 디렉토리 경로 설정
WORKDIR /프로젝트 이름

# pip freeze로 출력해뒀던 의존성 목록을
# 도커 이미지의 작업 디렉토리로 복사
COPY requirements.txt .

# 도커 이미지 내부에서 명령 실행
# 복사 해둔 의존성 목록을 읽어 전체 설치
RUN pip install -r requirements.txt

# 개발해온 앱 디렉토리를 도커 이미지 내부로 복사
COPY ./app ./app

# main.py 실행
CMD ["python", "./app/main.py"]
```

---

## 도커 이미지 빌드 & 컨테이너 실행

```
# 도커 이미지 빌드 ( -t: 태그 )
docker build -t 이미지태그이름 .

# 도커 컨테이너 실행 ( --name: 컨테이너이름, -p: 포트 )
docker run --name 컨테이너이름 -p 호스트포트:이미지포트 이미지태그이름
```

