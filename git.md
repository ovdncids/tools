# GIT

## commit명 바꾸기
```sh
git commit --amend -m ""
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
memberB: b2
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

## Reset
* 주로 되돌릴 때 많이 사용한다

### 마지막 commit 삭제
```sh
git reset HEAD~
# or
git reset --hard HEAD~1
```

### 마지막 reset 취소
```sh
git reset ORIG_HEAD
```

### 처음 commit 삭제
```sh
git update-ref -d HEAD
```

## Rebase
* commit 합치기, 이전 commit 내역 수정등, 주로 이전에 실수를 수정하기 위해서 쓰인다
* 하지만 실재로는 이전 내역이 수정 되는것이 아니고 새로 생성하기 때문에 push된 내역은 rebase에 포함하지 않아야 한다
* 따라서 push전 commit들에 대해서만 rebase를 사용하는게 바람직하다

### 이전 commit 이름 바꾸기
* 로컬 commit 2개 하기
```sh
git rebase -i HEAD~2
  # vi 에디터가 실행 됨
```
```vi
# i 키를 눌러서 INSERT 모드로 변경
# 첫째줄 pick을 edit로 수정
# esc 키를 눌러 INSERT 모드 종료
# :wq
  # 저장하고 종료하기
```
```sh
git commit --amend -m "커밋 메시지 수정"
git rebase --continue
```

### 마지막 commit과 이전 commit 합치기
```sh
git rebase -i HEAD~2
```
```vi
# 둘째줄 pick을 fixup으로 수정 후 저장 종료
```

### 이전 commit 내용 수정하기
* 로컬 commit 3개 하기
```sh
git rebase -i HEAD~3
```
```vi
# 첫째줄 pick을 edit으로 수정 후 저장 종료
```
```sh
# 파일 수정
git add .
git commit -m "중간에 끼워 넣을 commit명"
git rebase --continue
```
#### 충돌이 발생한 경우
```sh
# 파일 충돌 해결
git add .
git commit -m "충돌 해결 commit명"
git rebase --continue
```

## 로컬 commit을 최상단으로 올리기
memberA
```sh
git checkout master
# 파일 하나 새로 만들어서 commit
```

memberB/README.md
```sh
# 파일 수정 후 commit push
```

memberA
```sh
git pull
git rebase origin/master
```

## Stash
* 현재의 작업 내역을 commit 하지 않고 따로 보관 한다
* 현재 작업을 일시 중단하고, 새로운 작업이 우선 될경우, 작업 내역을 commit 하지 않고 따로 보관 할 때 쓰임
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
