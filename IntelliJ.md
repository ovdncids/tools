# IntelliJ

## 터미널에서 ESC키 누르면 에디터로 돌아가는 현상
* https://intellij-support.jetbrains.com/hc/en-us/community/posts/360005050259-Disable-switching-from-embedded-terminal-to-editor-when-pressnig-ESC-button
```sh
Setting > Keymap > Plugins > Terminal > Switch Focus To Editor
```

## 주석 처리
* https://freedeveloper.tistory.com/222
```sh
# 주석 들여쓰기
Settings > Editor > Java > Wrapping and Braces > Keep when reformating > Comment at first column > 해제

# 주석 스페이스 하나 넣기
Settings > Editor > Java > Code  Generation > Comment Code > Add a space at comment start > 선택
```

## snake_case to camelCase
```sh
Setting > Plugins > CamelCase > Install

# 사용
Shift + Alt + U
```

## Commit 할때 문법 체크 안하기
```sh
Setting > Version Control > Commit > Analyze code > 해제
```

## MyBatis에서 xml 파일 쉽게 열기
```sh
Setting > Plugins > MyBatisX
재시작
```
* [Intellij에서 Service와 ServiceImpl 쉽게 이동
](https://github.com/ovdncids/java-curriculum/blob/master/SpringBootRestAPI.md#intellij%EC%97%90%EC%84%9C-service%EC%99%80-serviceimpl-%EC%89%BD%EA%B2%8C-%EC%9D%B4%EB%8F%99)

## Java file is located outside of the module source root, so it won't be complied
```sh
src > main > java > 오른쪽 클릭 > Mark Directory as > Sources Root
```

## Tomcat 프로젝트
* File > Settings > Build, Execution, Deployment > Application Servers > + Tomcat Server > Tomcat 경로 선택
* {Tomcat 경로}/webapps/ROOT 폴더명 변경
* Run > Edit Configurations... > + > Tomcat Server > Deployment > + > External Source... > 해당 프로젝트 선택 (해당 경로를 ROOT로 폴더명 변경해도 좋음)

### 라이브러리를 못 찾고 빨간색으로 표시 되는 경우
```sh
Project Structure > Project Settings > Modules > 해당 프로젝트 > Dependencies > + > 2. Library... > Project Libraries > lib와 Tomcat
```
