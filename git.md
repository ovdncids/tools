# GIT

## commit명 바꾸기
```sh
git commit git commit --amend -m ""
```

# GitHub
* GitHub에서 새로운 프로젝트 생성
* `memberA` 디렉토리 생성 후 IntelliJ로 열기
```sh
# README.md 파일 생성
echo "# test" >> README.md

# 현재 디렉토리를 git이 관리하게 한다
git init

# 현재 디렉토리의 상태를 확인한다
git status

# 현재 디렉토리에서 변경된 모든 파일을 git에 적용 한다
git add .

# 변경된 내역을 commit 한다
git commit -m "first commit"

# GitHub와 현재 디렉토리 연결
git remote add origin https://github.com/...git

# GitHub에 master 브랜치 push
git push -u origin master
```

* `memberB` 디렉토리에 GitHub 클론 후 IntelliJ로 열기
```sh
cd ..
git clone https://github.com/...git memberB
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
