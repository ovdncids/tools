# Windows

## Microsoft .NET Framework 3.5
* https://learn.microsoft.com/ko-kr/windows-hardware/manufacture/desktop/deploy-net-framework-35-by-using-deployment-image-servicing-and-management--dism?view=windows-11
```cmd
DISM /Online /Enable-Feature /FeatureName:NetFx3 /All /LimitAccess /Source:d:\sources\sxs
  # 시디롬 드라이버가 d:\ 드라이브인 경우 (추천)

DISM /Online /Enable-Feature /FeatureName:NetFx3 /All
  # 온라인 설치
```

## 노트북 펜소음 줄이기
```cmd
제어판 -> 전원 옵션 -> 균형 조정(권장) -> 설정 변경 -> 고급 전원 관리 옵션 설정 변경 ->
  프로세서 전원 관리 -> 최소 프로세서 상태 -> 1%
                    -> 시스템 냉각 정책 -> 수동
                    -> 최대 프로세서 상태 -> 99%
```

### 프로세서 성능 강화 모드
```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Power\PowerSettings\54533251-82be-4824-96c1-47b60b740d00\be337238-0d82-4146-a960-4f3749d470c7
Attributes -> 2

  프로세서 전원 관리 -> 프로세서 성능 강화 모드 -> 효율적으로 활성화됨
```

### 노트북 펜 컨트롤
https://github.com/hirschmann/nbfc
```cmd
Asus F5SR <- 선택
Target fan spped: 25%
```
* 노트북 쿨러는 쉽게 휠러를 분리 할 수 있다. 청소를 쉽게 할 수 있다.

## 크롬 인증서 오류
```regedit
HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\SystemCertificates\AuthRoot
1 -> 0
```
* https://wuimer.tistory.com/entry/%ED%81%AC%EB%A1%AC-%EC%9D%B8%EC%A6%9D%EC%84%9C-%EC%98%A4%EB%A5%98-%EC%97%B0%EA%B2%B0%EC%9D%B4-%EB%B9%84%EA%B3%B5%EA%B0%9C%EB%A1%9C-%EC%84%A4%EC%A0%95%EB%90%98%EC%96%B4-%EC%9E%88%EC%A7%80-%EC%95%8A%EC%8A%B5%EB%8B%88%EB%8B%A4-%ED%95%B4%EA%B2%B0%EB%B2%95

<!--
## 최고의 성능
```cmd
powercfg -duplicatescheme e9a42b02-d5df-448d-aa00-03f14749eb61
```

## 백그라운드 앱 끄기
```
개인 정보 설정 -> 백그라운드 앱
```
-->

## .cmd 파일
```cmd
@echo off
rem 'rem은 주석'
rem sc query wiredService
rem sc query "CCDN Service"
sc query NATService
set /p confirmStr=Do you want to delete "NATService" service?(y/n)
if /i "%confirmStr%" == "y" goto YES
if /i not "%confirmStr%" == "y" goto NO

:YES
echo "NATService" is deleting
sc stop NATService
sc delete NATService

:NO
echo.

pause

rem "윈도우 업데이트 서비스 확인"
sc query wuauserv
```

<!--
## DirectX (최종)
* https://www.microsoft.com/ko-kr/download/confirmation.aspx?id=35
-->

# WSL (Windows Subsystem for Linux)
* https://www.yalco.kr/_01_install_wsl
```sh
# PowerShell 관리자 권한으로 실행
wsl --install
## wsl2 버전 기본 설치
wsl --install -d Ubuntu
## Ubuntu 설치
```
* [0x80370102 오류](https://velog.io/@jaylnne/WSL-Error-0x80370102-%ED%95%B4%EA%B2%B0)
