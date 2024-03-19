# Mac

## 설정
* `배터리 퍼센트 보기`: 시스템 설정 > 제어 센터 > 배터리 > 퍼센트 보기

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
동작 > 보관함 > 유틸리티 > 셸 스크립트 실행을 오른쪽으로 드래그 (동작 또는 파일을 여기로 드래그하여 작업흐름을 구착하십시오.)
현재 수신하는 작업흐름: 파일 또는 폴더
선택 항목 위치: Finder
셸: /bin/zsh
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

## 소프트웨어 자동 업데이트 막기 (필수)
```sh
시스템 환경설정 > 소프트웹어 업데이트 > 고급... > 업데이트 확인만 체크
```

## Chrome 업데이트 막기
```sh
defaults write com.google.keystone.agent checkinterval 0
```

## VSCode 업데이트 막기
```sh
설정 > update mode > manual
```

## .DS_Store 파일 삭제
* https://www.imymac.com/ko/mac-cleaner/how-to-delete-ds-store-file.html
```sh
find . -name '.DS_Store' -type f -delete
```

## 삼바
```sh
Finder > 이동 > 서버에 연결...
smb://{ip}
```

## Mac용 토렌트
https://transmissionbt.com/download

## Mac 복원에서 macOS 설치에서 하드가 안 보이는 경우
* [부팅 시 키조합](https://support.apple.com/ko-kr/guide/mac-help/mchl338cf9a8/mac)
* ❕ 파티션 문제일 수 있다. 파티션 삭제 하고 다시 macOS 설치 실행 해본다.

## 복구 모드
* https://kimsungjin.tistory.com/582
* [SMC 설정 초기화](https://kimsungjin.tistory.com/51): shift + control + option + 전원 (BIOS 초기화라고 생각하면 쉽다. 조합키 순서 중요)
* [NVRAM 설정 초기화](https://kimsungjin.tistory.com/33): command + option + p + r (설정을 비활성 메모리에 저장 해논 부분을 초기화)

## macOS 버전별 .dmg 파일 설치
* https://blog.naver.com/hankboy/221203947247
* [Bic Sur](https://drive.google.com/file/d/19EyEYqurIQhrvyjlbgSU2IVl4mgd51kd/view?usp=share_link)
* [Monterey](https://drive.google.com/file/d/1HYDBsW3jvVDPwNy2ru6cD0qswBa7Q8N4/view?usp=share_link)

## Boot Camp
### 기본 설치
* https://support.apple.com/ko-kr/guide/bootcamp-assistant/bcmp173b3bf2/6.1/mac/11.0
* [공식 Windows 10 ISO 파일](https://www.microsoft.com/ko-kr/software-download/windows10ISO)
```sh
재부팅 후 command + r > 하나의 파티션으로 `macOS` 설치
응용 프로그램 > 유틸리티 > Boot Camp 지원 > 계속
Windows 10 ISO 파일 선택... (ISO 파일은 AirDrop으로 옮기자 빠름, USB와 다운로드는 비슷한 속도)
`macOS`와 `Wndows` 파티션의 크기 조절 (나중에 파티션 크기를 변경할 수 없음)
윈도우 자동 설치 > 설치 완료 (설치 중에 키보드, 트릭패드 사용 가능)
D:\bootcamp 폴더에서 setup.exe 실행 (실행 전 복사, setup.exe 완료 후 D:\ 사라짐)
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

#### Mac이 USB-C 타입인 경우
```sh
`option` 키를 누고 Windows 설치시에 Mac의 키보드와 트릭패트를 쓸 수 없으므로 `USB to USB-C 젠더` 2개 필요. (CD-ROM, 마우스)
```

# Launch (서비스)
* https://phillip5094.tistory.com/142
```sh
cd ~/Library/LaunchAgents
vi com.nextjs.server.plist
```
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>com.nextjs.server</string>
    <key>ProgramArguments</key>
    <array>
        <string>sh</string>
        <string>next.sh</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
    <key>WorkingDirectory</key>
    <string>{프로젝트 경로}/</string>
    <key>StandardOutPath</key>
    <string>{프로젝트 경로}/log.out</string>
    <key>StandardErrorPath</key>
    <string>{프로젝트 경로}/error.out</string>
  </dict>
</plist>
```
* 시스템 설정 > 일반 > 로그인 항목(백그라운드)에 추가 된다. (여기서 재부팅 후 실행 유무 선택 가능)

{프로젝트 경로}/next.sh
```sh
vi {프로젝트 경로}/next.sh

source ~/.zshrc
nvm use 16
npm run dev

chmod 755 {프로젝트 경로}/next.sh
```

```sh
# 서비스에 등록, 해제
launchctl load ~/Library/LaunchAgents/com.nextjs.server.plist
launchctl unload ~/Library/LaunchAgents/com.nextjs.server.plist

# 서비스가 등록 되었는지 확인 ("Label" = "com.nextjs.server")
launchctl list | grep nextjs
launchctl list com.nextjs.server

# 서비스 시작, 종료
launchctl start com.nextjs.server
launchctl stop com.nextjs.server
```
* ❕ `com.nextjs.server.plist` 파일에서 사용되는 `{프로젝트 경로}/next.sh` 파일 안에서는 `cd 명령`을 사용해도 경로가 변하지 않는다.

# M1 - UTM (Virtual machines for Mac)
* https://mac.getutm.app

## Windows 10
* [다운로드 - Windows 10 Client Arm64 Insider Preview](https://drive.google.com/file/d/1i8z6Q7l7P7NgftLmEUSnoHGfqQzKhmHj/view)
```sh
+ 버튼 > Virtualize
아키텍처: ARM64 (aarch64)
시스템: QEMU 7.2 ARM Virtual Machine (virt-7.2)
```

## Windows 11
* https://velog.io/@junsugi/M1-Apple-UTM-%EC%9D%B4%EC%9A%A9%ED%95%B4%EC%84%9C-Window-11-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0
* [다운로드 - Windows 11 Client Arm64 Insider Preview (Beta) - Build 22598](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewARM64)
```sh
+ 버튼 > Virtualize
아키텍처: ARM64 (aarch64)
시스템: QEMU 7.2 ARM Virtual Machine (alias of virt-7.2) (virt)
Let’s connect you to a network <- 여기서 진행 못함
재부팅 > Shift + F10 > taskmgr > Windows Explorer > Open file location > D:\spice-guest-tools...exe 설치
```
* [임시 인증](https://pcwindows.tistory.com/362)

## AltTab
* https://alt-tab-macos.netlify.app
* 현재 모니터에서 실행되어 있는 프로그램만 이동 가능한 단축키(option + tab) 프로그램
```sh
brew install --cask alt-tab
```

## Keyboard Maestro (마우스 1px 이동 가능 매크로)
* https://www.keyboardmaestro.com/main
* https://brunch.co.kr/@second-space/10
```sh
Macros > + New Macro > Triggered by any of the following > + New Trigger > Hot Key Trigger > 단축키 > is down
Will execute the following actions > + New Action > Interface Control > Move or Click Mouse > at: 1, relative to the current mouse location
```
