# GIT

## commit명 바꾸기
```sh
git commit git commit --amend -m ""
```

# GitHub
* GitHub에서 새로운 프로젝트 생성
* `memberA` 디렉토리 생성 후 VSCode로 열기
```sh
# README.md 파일 생성
echo "# test" >> README.md

# 현재 디렉토리를 git이 관리하게 한다
git init

# 현재 디렉토리의 상태를 확인한다
git status

# 현재 디렉토리에서 변경된 모든 파일을 git에 적용 한다
git add .

# 변경된 내역을 commit 한다 (로컬 컴퓨터에만 저장됨)
git commit -m "first commit"

# GitHub와 현재 디렉토리 연결
git remote add origin https://github.com/...git

# GitHub에 master 브랜치 push (GitHub에 저장됨)
git push -u origin master
```

* `memberB` 디렉토리에 GitHub 클론 후 VSCode로 열기
```sh
cd ..
git clone https://github.com/...git memberB
```

## 동일한 브랜치에서 충돌 테스트
memberA/README.md
```md
memberA: a1
```
* commit 후 push
```sh
git status
git add .
git commit -m "a1"
git push
```

memberB/README.md
```md
memberB: b1
```
* commit 후 push
```sh
git status
git add .
git commit -m "b1"
git push
```
* ❕ reject(거부) 발생 설명

```sh
# GitHub에서 수정된 내역을 받아 온다
git pull
```
* ❕ 충돌 발생

### 충돌 해결하기
memberB/README.md
```md
# test
<<<<<<< HEAD
memberB: b1
=======
memberA: a1
>>>>>>> 해쉬값
```
* `Accept Current Change`, `Accept Incomming`, `Accept Both Changes`, `Compare Changes` 하나씩 눌러 보기

memberB/README.md
```md
# test
memberA: a1
memberB: b1
```
* commit 후 push
```sh
git status
git add .
git commit -m "b1 resolved"
git push
```

* ❕ 여러 사람과 프로젝트를 같이 한다면, 항상 `push`전에 `pull` 먼저 해야 한다

## stash
```sh
# 현재 변경 내역 stash 생성
git stash
# 현재 변경 내역 stash 생성 이름 주기
git stash save ""

# stash 리스트 보기
git stash list

# stash 꺼기
git stash apply ${0}

# stash 꺼내고 지우기
git stash pop ${0}

# stash 하나 지우기
git stash drop ${1}

# stash 모두 지우기
git stash clear
```
