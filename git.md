# GIT

## commit명 바꾸기
```sh
git commit git commit --amend -m ""
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
