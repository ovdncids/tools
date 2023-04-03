# Visual Studio Code (VSCode)

## 단축키
```sh
대문자: Ctrl + u
  # 설정 해야함
소문자: Ctrl + Shift + u
  # 설정 해야함
아래에 줄 복사: Shift + Alt + DownArrow
닫힌 편집기 다시 열기: Ctrl + Shift + t
탐색기 열고 닫기: Ctrl + b
문서 서식, 코드 자동 정렬(Auto indent): Alt + Shift + f
```

## 설정
```sh
에디터에서 파일 선택시, 탐색기 이동하지 않기
  파일 -> 기본설정 -> 설정 -> "explorer.autoReveal": false
에디터 파일에서 단축키로 해당 파일 탐색기 위치로 이동하기
  파일 -> 기본설정 -> 바로 가기키 ->
    workbench.files.action.showActiveFileInexplorer: 원하는 단축키로 설정
    세로 막대에서 활성 파일 표시: 키 바인딩 Ctrl + Alt + e
자동 Tab 사이즈 결정
  파일 -> 기본설정 -> 설정 > 검색 > editor.detectIndent
  "editor.tabSize": 2
    # 기본 텝 사이즈를 2칸으로 변경 한다.
  "editor.detectIndentation": false
    # 해당 파일의 텝 사이즈를 무시하고 기본 텝 사이즈로 설정한다.
열린 파일 목록 가로 스크롤 안 되기
  파일 -> 기본설정 -> 설정 -> Wrap Tabs 체크
```

## Code Spell Checker
* 오타 체크 프로그램

## HTML Mifify, Maxify
* https://codepen.io/depthdev/pen/HKuLs
* 변경 후 문서 서식으로 줄 마춤

## Vue.js
* Format Document(Alt + Shift + f)에서 Semicolon 빼기
* https://stackoverflow.com/questions/47122915/stop-visual-studio-code-from-automatically-adding-semicolons-in-vue-files
* 파일 -> 기본설정 -> 설정 -> 설정 열기(JSON): (오른쪽 상단 아이콘) -> settings.json
```json
"vetur.format.defaultFormatterOptions": {
    "prettier": {
    "semi": false
    }
}
```

## Prettier - Code formatter
* `Prettier - Code formatter` 확장 프로그램 설치
* Ctrl + , -> format -> 사용자 -> 텍스트 편집기 -> Editor: Default Formatter -> Prettier - Code formatter
* `test.json` 파일을 만들어서 정상적으로 json 모양으로 변하는지 테스트
