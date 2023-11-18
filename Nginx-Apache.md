# Nginx

## Windows
* http://nginx.org/en/download.html
```sh
# Stable version > nginx/Windows-1.24.0 > 압축 해제 > C:\Program Files\nginx-1.24.0 이동

# Nginx 시작
cd "c:\Program Files\nginx-1.24.0"
nginx.exe

# Nginx 종료 (터미널을 하나더 띄우고 실행)
nginx.exe -s stop
## 이전 터미널의 nginx.exe 종료 됨
## nginx: [error] CreateFile() ".../logs/nginx.pid" 이미 Nginx가 종료된 상태

# Nginx 재실행 (설정 변경 후 실행)
nginx.exe -s reload
## 이전 터미널의 nginx.exe가 실행된 상태에서 실행
```

### 웹서버 디렉토리 변경
C:\Program Files\nginx-1.24.0\conf\nginx.conf
```diff
server {
  location / {
-     # root html;
+     root C:/Projects/react-study/build;
```

# Apache

## Windows
* https://www.apachelounge.com/download
```sh
httpd-2.4.58-win64-VS17.zip > 압축 해제 > C:\Program Files\Apache24 이동
```

### Apache 경로 수정
C:\Program Files\Apache24\conf\httpd.conf
```diff
- Define SRVROOT "c:/Apache24"
+ Define SRVROOT "C:\Program Files\Apache24"
```

### 실행
```sh
# 실행
cd "C:\Program Files\Apache24\bin"
httpd.exe

# 종료
Ctrl + c: 
```

### 웹서버 디렉토리 변경
C:\Program Files\Apache24\conf\httpd.conf
```diff
- # DocumentRoot "${SRVROOT}/htdocs"
- # <Directory "${SRVROOT}/htdocs">
+ DocumentRoot "C:/Projects/react-study/build"
+ <Directory "C:/Projects/react-study/build">
```
