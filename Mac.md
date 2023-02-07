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
* [Shell .zshrc, .bashrc 차이](https://github.com/ovdncids/python-curriculum/blob/master/PythonInstall.md#mac)

## mds 서비스 죽이기 (Spotlight 인덱싱)
* https://www.charlezz.com/?p=44913
```sh
sudo mdutil -a -i off
```

## .DS_Store 파일 삭제
* https://www.imymac.com/ko/mac-cleaner/how-to-delete-ds-store-file.html
```sh
find . -name '.DS_Store' -type f -delete
```

## Mac용 토렌트
https://transmissionbt.com/download

## macOS 버전별 .dmg 파일 설치
* https://blog.naver.com/hankboy/221203947247
* [Bic Sur](https://drive.google.com/file/d/19EyEYqurIQhrvyjlbgSU2IVl4mgd51kd/view?usp=share_link)
* [Monterey](https://drive.google.com/file/d/1HYDBsW3jvVDPwNy2ru6cD0qswBa7Q8N4/view?usp=share_link)

## Boot Camp
### 기본 설치
* https://support.apple.com/ko-kr/guide/bootcamp-assistant/bcmp173b3bf2/6.1/mac/11.0
```sh
하나의 파티션으로 `macOS` 설치 (재부팅 후 command + r)
응용 프로그램 > 유틸리티 > Boot Camp 지원 > 계속
Windows 10 ISO 파일 선택...
`macOS`와 `Wndows` 파티션의 크기 조절 (나중에 파티션 크기를 변경할 수 없음)
설치 진행
```

### Windows 지원 소프트웨어 다운로드 (Boot Camp 드라이버)
* https://support.apple.com/ko-kr/HT204923
```sh
응용 프로그램 > 유틸리티 > Boot Camp 지원
상단 메뉴 > 동작 > Windows 지원 소프트웨어 다운로드

# Mac에서 `FAT32`가 아니면 읽기만 가능
별도 저장: WindowsSupport (폴더명)
위치: `FAT32` 파일 시스템의 USB에 설치 (USB 포맷 되지 않음)
```

### Windows 재 설치
* [Boot Camp 드라이버_2013 Early 까지](https://support.apple.com/kb/DL1721?locale=ko_KR&viewlocale=ko_KR)
* [Boot Camp 드라이버_2013 Early 이후](https://support.apple.com/kb/DL1837?locale=ko_KR&viewlocale=ko_KR)
```sh
# Boot Camp 버전이 안 맞을 확률이 높다. `Windows 지원 소프트웨어 다운로드` 다운로드 받고 사용하자.
부팅 USB를 꼽고 재부팅 후 `option` 키를 누르면, USB 부팅 메뉴가 추가 된다.
```

### Mac이 USB-C 타입인 경우
```sh
Windows 설치시에 Mac의 키보드와 트릭패트를 쓸 수 없으므로 USB to USB-C 젠더 2개 필요.
```
