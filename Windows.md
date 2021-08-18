# Windows

## Microsoft .NET Framework 3.5
```cmd
DISM /Online /Enable-Feature /FeatureName:NetFx3 /All /LimitAccess /Source:d:\sources\sxs
# 시디롬 드라이버가 d:\ 드라이브인 경우
```

## 노트북 펜소음 줄이기
```cmd
제어판 -> 전원 옵션 -> 프로세서 전원 관리 -> 시스템 냉각 정책 -> 수동
                                        -> 최대 프로세서 상태 -> 80%
```

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
