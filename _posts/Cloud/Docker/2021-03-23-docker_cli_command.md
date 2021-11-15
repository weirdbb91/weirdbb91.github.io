---
header:
  teaser            : # 썸네일 이미지 /assets/images/face_army.jpg
title               : 도커 명령어 메모 # 제목
excerpt             : 메모 # 썸네일 한줄 요약
last_modified_at    : 2021-03-23 # 마지막 수정일
categories          : Cloud Docker
tags                : Basic Cloud Docker Command CLI
toc                 : # 목차 사용여부
toc_label           : # 목차 제목
# {: .notice--info}
---

---
## 출처 : [얄팍한 코딩사전](https://www.youtube.com/watch?v=hWPv9LMlme8)

메모용 포스트

설치
```
sudo yum install docker-io

sudo systemctl start docker

sudo setfacl -m user:{유저이름}:ec2-user:rw /var/run/docker.sock
```



컨테이너 실행 (이미지 없으면 다운로드) & cli
```
sudo docker run -it {이미지 이름}
```

```
docker run
    --name {컨테이너 이름}
    // ex) frontend-container
    -v {내부 공유 경로}:{외부 공유 경로}
    // ex) ${pwd}:/home/node/app
    -p {컨테이너 포트}:{연결할 포트}
    // ex) 8080:8081
    {이미지 이름}
    // ex) node-image

    // 그 외
    // -d detached mode, 백그라운드 모드
    // -rm 프로세스 종료시 컨테이너 자동제거
    ...
```

배쉬 쉘
```
docker exec -it {컨테이너 태그} bash
```

로그 확인
```
docker logs -f {컨테이너 태그}
```

모두 종료
```
docker stop $(docker ps -aq)
docker system prune -a
```

Dockerfile
ex) frontend
```
FROM {부모 이미지}:{버전}
// ex) node:12.18.4
      --- 베이스 이미지 ---
RUN {이미지 명령어}
// ex) npm install -g http-server
WORKDIR {실행 위치}
// ex) /home/node/app
      --- 컨테이너 생성 완료 ---
CMD {컨테이너 명령어}
// ex) ["http-server", "-p", "8080", "./public"]
```

ex) db
```
FROM {부모 이미지}:{버전}
// ex) mysql:5.7
      --- 베이스 이미지 ---
ENV {이미지 환경변수}
// ex) MYSQL_USER weirdbb91
      --- 컨테이너 생성 완료 ---
COPY {대상} {목적지}
// ex) ./scripts/ /docker-entrypoint-initdb.d/
// 시작과 동시에 실행될 .sql 파일들이 저장되는 폴더
```

도커 컴포즈 실행
```
docker-compose up
```

Docker-compose.yml
```
version: {도커 컴포즈 파일 버전} // ex) '3'
service:
    database:
        // Dockerfile 위치
        build: ./database
        // 내부 개방 포트 : 외부 접근 포트
        ports:
            -"3306:3306"
    backend:
        build: ./backend
        // 연결할 외부 폴더 : 컨테이너 내부 폴더
        volumes:
            - ./backend:/usr/src/app
        ports:
            - "5000:5000"
        // 환경변수 설정
        environment:
            - DBHOST=database
    frontend:
        build: ./frontend
        volumes:
            - ./frontend:/home/node/app
        ports:
            - "8080:8081"
```