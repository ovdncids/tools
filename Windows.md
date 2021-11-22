# Windows

## Microsoft .NET Framework 3.5
```cmd
DISM /Online /Enable-Feature /FeatureName:NetFx3 /All /LimitAccess /Source:d:\sources\sxs
  # 시디롬 드라이버가 d:\ 드라이브인 경우
```

## 노트북 펜소음 줄이기
```cmd
제어판 -> 전원 옵션 -> 프로세서 전원 관리 -> 최소 프로세서 상태 -> 1%
                                        -> 시스템 냉각 정책 -> 수동
                                        -> 최대 프로세서 상태 -> 99%
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
