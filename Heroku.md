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

# 로그 보기
heroku logs -t
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

## Django
```sh
# heroku create (프로젝트를 생성하지 말고, 위에서 프로젝트를 선택 하자)

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
Account settings -> Billing -> Credit card -> 카드등록
이제 다시 위의 Submit Order Form 선택
```

### 생성된 ClearDB MySQL 정보보기
```
Resources -> ClearDB MySQL -> NAVISITE 이동후 Name 선택 -> System Information
-> Username, Password 확인

Settings -> Reveal Config Vars -> mysql://... (이렇게 MySQL 접속 정보를 볼 수 있다.)
```
