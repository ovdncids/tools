# Heroku
* GitHub의 소스를 바탕으로 Node.js의 Express 서버를 배포(호스팅) 할 수 있다.

## Heroku 프로젝트 생성
https://www.heroku.com/

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

# 로그인
heroku login

# 로그 보기
heroku logs
```

## Backend Server
* [Download](https://github.com/ovdncids/vue-curriculum/raw/master/download/express-server.zip)

### Backend Server와 Heroku 연동을 위한 소스 수정
```diff
- app.listen(process.env.PORT, function() {
```
```js
if (process.env.PORT) {
  global.location = new URL('https://프로젝트명.herokuapp.com');
} else {
  process.env.PORT = global.location.port;
}
app.listen(process.env.PORT, function() {
```

## Githu와 연결
```sh
# 연결
홈페이지 > 로그인 > 해당 프로젝트 > Deploy > GitHub > Connect

# 배포
홈페이지 > 로그인 > 해당 프로젝트 > Deploy > GitHub > Deploy Branch
```

