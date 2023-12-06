# Docker (24.0.7)
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

## 호스트(내 컴퓨터)와 연결 하며 컨테이너 생성 (run = create, start, attach 한번에 실행)
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

## Mac M1 - Docker 초기화
* https://github.com/docker/for-mac/issues/6145
```sh
Docker 종료
# brew uninstall docker

rm -rf ~/.docker
rm -rf ~/Library/Caches/com.docker.docker
rm -rf ~/Library/Group Containers/group.com.docker
rm -rf ~/Library/Containers/com.docker.docker
rm -rf ~/Library/Application\ Support/Docker\ Desktop

open --background -a Docker
# brew install --cask docker
## --cask는 GUI 기반 프로그램 설치
```

## Ubuntu
* https://sleepyeyes.tistory.com/67
```sh
# Ubuntu 이미지 설치
docker pull ubuntu:latest

# 컨테이너 생성
docker create -it --name con_ubuntu -p 38080:8080 -p 33000:3000 -p 33306:3306 ubuntu
## -it = 컨테이너 내부로 진입 (attach 가능)
## -d = 데몬 서비스 (detached 모드)
## -p = 포트 바인딩

# 컨테이너 실행
docker start con_ubuntu

# 컨테이너 Shell 접속 (root로 접속됨)
docker attach con_ubuntu
```

### Shell 접속
```sh
# 버전 보기
cat /etc/os-release

# apt update를 하지 않으면 sudo, net-tools 등을 설치 할 수 없다.
apt update

# sudo 설치
api install sudo
sudo adduser [사용자]
sudo passwd root
su - [사용자]

# 네트워크 설치
sudo apt install net-tools
sudo apt install iputils-ping
```

### 컨테이너 생성시 포트를 설정하지 않은 경우
* https://stackoverflow.com/questions/19335444/how-do-i-assign-a-port-mapping-to-an-existing-docker-container
* [컨테이너 파일의 위치](https://yooloo.tistory.com/188)
