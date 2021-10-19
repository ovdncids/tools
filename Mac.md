# Mac

## VSCode
### code . 사용하게 만들기
```vscode
command + shift + p(명령 팔레트)
>shell
셸 명령: PATH에 'code' 명령 설치
```

### Terminal 현재 경로를 Finder로 열기
```sh
open .
```

### Finder에서 VSCode 단축키로 열기
https://gist.github.com/tonysneed/f9f09bfa28bcf98e8d8306f9b21f99e2
```
Automator 실행 > 빠른 동작(서비스)
동작 > 보관함 > 유틸리티 > 셸 스크립트 실행
현재 수신하는 작업흐름: 파일 또는 폴더
선택 항목 위치: Finder
셸: /bin/bash
통과 입력: 변수
open -n -b "com.microsoft.VSCode" --args "$*"
  # 실행 버튼을 눌러서 VSCode가 실행 되는지 확인
저장: Open in Visual Studio Code

시스템 환경 설정
키보드 > 단축키 > 서비스 > 파일 및 폴더 > Open in Visual Studio Code > 단축키 설정
  # Finder가 이미 실행 되었다면 command + w 종료 후 재실행
```

## Shell 변경하기
```sh
# bash -> zsh
chsh -s /bin/zsh
# zsh -> bash
chsh -s /bin/bash
```
* [Shell .zshrc, .bashrc 차이](https://github.com/ovdncids/python-curriculum/blob/master/PythonInstall.md)

## Mac용 토렌트
https://transmissionbt.com/download
