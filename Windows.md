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

## Services
```cmd
rem cmd 관라자 권한으로 실행

rem 서비스 등록
sc create "서비스 이름" start= demand displayname= "서비스 이름" binpath= "C:\서비스.bat"
rem = 뒤에 스페이스 한칸 띄어야 한다.

rem 서비스 상태
sc query "서비스 이름"

rem 서비스 시작
sc start "서비스 이름"
rem StartService FAILED 1053: The service did not respond to the start or control request in a timely fashion.
rem regedit > HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control > DWORD32 > ServicesPipeTimeout: 180000
rem 재시작 후에 또 "StartService FAILED 1053" 발생하면 NSSM를 설치한다.

rem 서비스 종료
sc stop "서비스 이름"

rem 삭제
sc create "서비스 이름"
```
* [StartService FAILED 1053](https://www.partitionwizard.com/clone-disk/windows-could-not-start-the-service-on-local-computer-error-1053.html)

### NSSM
* https://nssm.cc
* https://stackoverflow.com/questions/415409/run-batch-file-as-a-windows-service
* https://github.com/ovdncids/tools/blob/master/download/nssm-2.24.zip
```cmd
nssm-2.24\wind64\nssm.exe install "서비스 이름"
nssm start "서비스 이름"
rem nssm 시작하면 윈도우 Service 또한 시작된다.
rem regedit > HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services > "서비스 이름"이 추가 된다.
```

# WSL (Windows Subsystem for Linux)
* https://learn.microsoft.com/ko-kr/windows/wsl/install
* https://www.yalco.kr/_01_install_wsl
```sh
# PowerShell 관리자 권한으로 실행

# wsl2 버전 기본 설치
wsl --install
# 설치 가능한 Linux 버전 보기
wsl -l -o
# Ubuntu 설치
wsl --install -d Ubuntu
# Ubuntu 실행
Ubuntu
# 설치된 WSL 목록
wsl -l -v
# 실행중인 모든 WSL 종료
wsl --shutdown
# Ubuntu 등록 삭제
wsl --unregister Ubuntu
```
* [0x80370102 오류](https://velog.io/@jaylnne/WSL-Error-0x80370102-%ED%95%B4%EA%B2%B0)

## Ubuntu
* [Docker - Ubuntu](https://github.com/ovdncids/tools/blob/master/Docker.md#shell-%EC%A0%91%EC%86%8D)
* [Raspberry Pi - MariaDB](https://github.com/ovdncids/raspberrypi-curriculum#mariadb)
