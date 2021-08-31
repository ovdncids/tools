# Docker
* 가상 컨테이너를 활용하여 원하는 서비스(웹서버, DB등)를 최소화 하여 설치 할 수 있다.
* https://www.youtube.com/watch?v=Ps8HDIAyPD0&list=PLuHgQVnccGMDeMJsGq2O-55Ymtx0IdKWf

# Docker hub
* Docker Image들의 모음
* https://hub.docker.com

## 설치
https://docs.docker.com/get-docker

## 아파치 Image 설치
```sh
# 설치된 image 보기
docker images

# 아파치 image 설치
docker pull httpd

# 아파치 image 삭제
docker rmi httpd
```

## 설치된 아파치 Image를 바탕으로 컨테이너 생성
```sh
# 모든 컨테이너 보기
docker ps -a
# 실행중인 컨테이너만 보기
docker ps

# 아파치 컨테이너를 httpd1 이름으로 생성
docker run --name httpd1 httpd
  # 컨테이너 생성과 동시에 현재 터미널에서 컨테이너 실행
docker run --name httpd1 -d httpd
  # 컨테이너 생성 후 데몬으로 실행

# 컨테이너 log 보기
docker logs -f httpd1

# 컨테이너 httpd1 중지
docker stop httpd1

# 컨테이너 httpd1 실행
docker start httpd1

# 컨테이너 httpd1 삭제
docker rm httpd1
```

## 호스트(내 컴퓨터)와 연결 하며 컨테이너 생성
```sh
# 호스트와 컨테이너 사이에 포트 포워딩 하는 httpd2 컨테이너 생성
docker run --name httpd2 -p 8880:80 httpd

# 호스트와 컨테이너 사아에 포트 포워딩과 파일 연결 하는 httpd2 컨테이너 생성
docker run --name httpd3 -p 8880:80 -v {호스트 경로}:/usr/local/apache2/htdocs httpd
```

## 컨테이너에 터미널 연결
```sh
docker exec -it httpd3 /bin/sh
docker exec -it httpd3 /bin/bash
```
