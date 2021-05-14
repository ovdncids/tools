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

* ❔ 실습: `memberA/README.md`에서 `memberA: a2` 입력 후 push 하기 (충돌 해결 하기)
* ❔ 실습: `memberB`에서 `B.txt` 파일을 만들고 push 하기
* ❕ 여러 사람과 프로젝트를 같이 한다면, 항상 `push`전에 `pull` 먼저 해야 한다

## 브랜치 생성과 머지
```sh
git branch f/memberA
git checkout f/memberA
```

memberA/README.md
```md
f/memberA: a2
```

```sh
git status
git add .
git commit -m "a2"
git pull
git push
```

memberB/README.md
```md
memberB: b1
```

```sh
git status
git add .
git commit -m "b2"
git pull
git push
```

### 브랜치 머지
```sh
git merge origin/f/memberA
```
```md
<<<<<<< HEAD
memberB: b1
=======
f/memberA: a2
>>>>>>> origin/f/memberA
```

* ❔ 실습: 충돌 해결 후 push
* ❔ 실습: `memberA`에서 `origin/master` merge 하기
* ❔ 실습: `f/memberA: a3` 다시 해보기

## Pull Request
* 주로 master 브랜치에 작업 브랜치를 머지할때 쓰인다
* GitHub(https://github.com/{유저}/{리포지토리}/pulls)페이지에서 요청 할 수 있다
* 담당자 또는 콜라보레이터들에게 코드 리뷰를 받을 수 있다
* 담당자가 머지 승인 또는 거절을 할 수 있다
```github
# 새로운 Pull request를 생성하는 페이지로 이동
New pull request

# base: 작업물을 받을 브렌치, compare: 작업한 브랜치
base: master <- compare: 작업 브랜치
  # 선택 후 'There isn’t anything to compare.'가 나오면 f/memberA 브랜치에서 작업 후 push

# 작업한 내역이 있을 경우 Open a pull request 페이지로 이동
Create pull request

Pull request 이름과 comment 쓰기
Reviewers 리뷰어(옵션)
Assignees 담당자(옵션)
# 작업한 내용을 확인 후
Create pull request

# 이제 담당자 또는 콜라보레이터들이 확인 후 댓글을 남길 수 있다
이상이 없다면 Merge pull request 실행
```

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
