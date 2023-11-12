# Nginx
* http://nginx.org/en/download.html

## Windows
```sh
# Stable version > nginx/Windows-1.24.0 > 압축 해제 > C:\Program Files\nginx-1.24.0 이동

# Nginx 시작
nginx.exe

# Nginx 끄기
nginx.exe -s stop

# Nginx 재실행 (설정 변경 후 실행)
nginx.exe -s reload
```

### 설정
C:\Program Files\nginx-1.24.0\conf\nginx.conf
```diff
server {
  location / {
-     root html;
+     root C:/Projects/react-study/build;
```
