# Heroku
* GitHub의 소스를 바탕으로 Node.js의 Express 서버를 배포(호스팅) 할 수 있다.

## Heroku 프로젝트 생성
https://www.heroku.com

```sh
# 회원가입
홈페이지 > Sign up > 이메일 패스워트 생성

# 프로젝트 생성
홈페이지 > 로그인 > New
```

## Heroku CLI
https://devcenter.heroku.com/articles/heroku-cli

```sh
# 설치
npm install -g heroku
## 설치 안되면 위에 링크에서 다운로드

# 로그인
heroku login

# 프로젝트 리스트 보기
heroku apps

# 프로젝트 선택
heroku git:remote -a {프로젝트 리스트 안에 있는 프로젝트 선택}
## .git/config (아래 부분을 지우면 default 프로젝트가 삭제 된다)
[remote "heroku"]
	url = https://git.heroku.com/{프로젝트}.git
	fetch = +refs/heads/*:refs/remotes/heroku/*

# 프로젝트 클론
heroku git:clone -a {프로젝트 리스트 안에 있는 프로젝트 선택}

# 로그 보기
heroku logs --tail

# 서버 재시작
heroku restart --app {프로젝트 이름}

# push (동시에 배포 시작)
git push heroku master
```

## Backend Server
* [Download](https://github.com/ovdncids/vue-curriculum/raw/master/download/express-server.zip)

### public 경로 설정
index.js
```js
// Set public
app.use('/', express.static('build'));
```

### Backend Server와 Heroku 연동을 위한 소스 수정
```diff
- global.location = new URL('http://localhost:3100');
- app.listen(global.location.port, function() {
```
```js
global.location = new URL('http://localhost:3100');
if (process.env.PORT) {
  global.location = new URL('https://프로젝트명.herokuapp.com');
} else {
  process.env.PORT = global.location.port;
}
app.listen(process.env.PORT, function() {
  console.log('Express server listening on ' + global.location.protocol + '//' + global.location.host);
});
```

## React 환경 설정
.env.development
```env
REACT_APP_BASE_URL=http://localhost:3100
```

.env.production
```env
REACT_APP_BASE_URL=https://프로젝트명.herokuapp.com
```

src/stores/MembersStore.js
```js
axios.defaults.baseURL = process.env.REACT_APP_BASE_URL;
```

## Githu와 연결
```sh
# 연결
홈페이지 > 로그인 > 해당 프로젝트 > Deploy > GitHub > Connect

# 배포
홈페이지 > 로그인 > 해당 프로젝트 > Deploy > GitHub > Deploy Branch
```

## Django
```sh
# heroku create (프로젝트를 생성하지 말고, 위에서 프로젝트를 선택 하자.)

# Django shell 실행
heroku run python manage.py shell

# Shell 실행
heroku run bash
```
* https://devcenter.heroku.com/articles/getting-started-with-python
* https://egg-money.tistory.com/115

## MySQL
* https://m.blog.naver.com/gofkdvjvl/222041889095

### Add-ons 선택
```
Overview -> Configue Add-ons -> Find more Add-ons -> ClearDB MySQL -> Install ClearDB My SQL
-> Ignite - Free 선택
-> App to provision to: 사용할 프로젝트 선택
-> Submit Order Form 누를때 경고 토스트 뜨면 카드 등록 해야함
```

### 카드 등록
```
헤로쿠 상단 아바타 -> Account settings -> Billing -> Credit card -> 카드등록
이제 다시 위의 Submit Order Form 선택
```

### 생성된 ClearDB MySQL 정보보기
```
Resources -> ClearDB MySQL -> NAVISITE 이동후 Name 선택 -> System Information
-> Username, Password 확인

Settings -> Reveal Config Vars -> mysql://... (이렇게 MySQL 접속 정보를 볼 수 있다.)
```

## Spring Boot for Java 1.8
* 특별한 설정 필요 없음

### 환경 변수
#### Spring boot 환경 변수
```sh
서버 -> Edit Configurations... -> Environment Variables -> db.url=localhost;db.username=root;db.password=root
```
* ❕ 변수와 변수 사이에 공백이 있으면 안 됨

#### Heroku 환경 설정
```sh
Settings -> Config Vars ->

db.url: localhost
db.username: root
db.password: root
```

#### application.properties 설정
```properties
spring.datasource.url=jdbc:mysql://${db.url}
spring.datasource.username=${db.username}
spring.datasource.password=${db.password}
```

## Spring Boot for Java 11
* `Spring boot 2.7.5`, `Java 11`, `MyBatis 2.2.2`에서 정상 동작 확인
* ❕ Java 11버전을 사용하면 지금까지 만나보지 못한 에러를 만날 수 있다.

#### Fatal error compiling: invalid target release: 11 발생시
* https://stackoverflow.com/questions/71763260/heroku-fatal-error-compiling-invalid-target-release-11

system.properties
```properties
java.runtime.version=11
```

## Spring Boot 수동 설정 (Git에 소스 파일 없이 jar 파일만 올리고 싶을때)
#### EntelliJ에서 jar 파일 만들기
* 설정
```sh
File -> Project Structure... -> Artifacts -> + -> JAR -> From Modules with dependencies -> Main Class 선택
```
* jar 파일 생성
```sh
Build -> Build Artifacts... -> Build
```

#### Procfile 파일 생성 (Heroku에서 읽을 설정 파일)
Procfile
```
web: java -Dserver.port=$PORT $JAVA_OPTS -jar {생성한 jar 경로 (out/artifacts/...)}
```
