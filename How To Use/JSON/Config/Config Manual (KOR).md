===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

이걸 찾으시나요? -> [config.json 예시](../../../How%20To%20Use/JSON/Config/example)

## 1. configVersion & usePlugin

```json
{
  "configVersion": "1.0.0",
  "usePlugin": true
}
```

### ▸ configVersion

* 현재 설정 파일의 버전
* 플러그인 업데이트 시 **설정 자동 마이그레이션** 또는 **호환성 검사**에 사용됨
* 값이 다를 경우 경고 로그 출력 가능

### ▸ usePlugin

* `true` : 플러그인 정상 동작
* `false` : 플러그인 전체 기능 비활성화 (안전 모드)
* 서버를 끄지 않고도 기능을 잠시 막고 싶을 때 사용

---

## 2. Debug (디버그 설정)

```json
"Debug": {
  "useDebug": true,
  "Debug-Default": true,
  "retryOnError": true,
  "retryCount": 3
}
```

### ▸ useDebug

* 디버그 모드 활성화 여부
* true 시 **파일 로드, 파싱, 등록, 오류 원인**을 상세 출력

### ▸ Debug-Default

* 기본 디버그 로그 출력 여부
* false일 경우 **치명적 오류만 출력**

### ▸ retryOnError

* 파일 로드/파싱 실패 시 자동 재시도 여부

### ▸ retryCount

* 재시도 횟수
* retryOnError가 true일 때만 사용됨

---

## 3. Logging (로그 설정)

```json
"Logging": {
  "logToConsole": true,
  "logToFile": true,
  "logFileName": "log.txt",
  "includeDebug": true,
  "includeStackTrace": true,
  "includeJsonError": true,
  "includePerformance": false
}
```

### ▸ logToConsole

* 콘솔에 로그 출력 여부

### ▸ logToFile

* 파일 로그 기록 여부

### ▸ logFileName

* 로그 파일 이름 (plugins/DRPG/logs/)

### ▸ includeDebug

* 디버그 로그 포함 여부

### ▸ includeStackTrace

* 예외 발생 시 StackTrace 포함

### ▸ includeJsonError

* JSON 파싱 오류 상세 출력

### ▸ includePerformance

* 처리 시간, 성능 관련 로그 출력

---

## 4. Performance (성능 관련 설정)

```json
"Performance": {
  "useAsync": true,
  "asyncThreads": 2,
  "centralAsyncExecutor": true,
  "useCache": true,
  "cacheExpireSeconds": 120,
  "preventDesync": true
}
```

### ▸ useAsync

* 무거운 작업을 비동기로 처리

### ▸ asyncThreads

* 비동기 스레드 수

### ▸ centralAsyncExecutor

* 중앙 집중형 스레드 풀 사용 여부

### ▸ useCache

* 스킬 / 보상 / 설정 캐시 사용

### ▸ cacheExpireSeconds

* 캐시 만료 시간 (초)

### ▸ preventDesync

* 비동기 처리 중 데이터 불일치 방지

---

## 5. PlayerData (플레이어 데이터 설정)

```json
"PlayerData": {
  "storageType": "JSON",
  "autoSave": true,
  "saveIntervalSeconds": 300,
  "autoBackup": true,
  "backupIntervalMinutes": 30,
  "backupMaxFiles": 10
}
```

### ▸ storageType

* 플레이어 데이터 저장 방식
* `JSON`, `SQLite`, `MySQL` 지원

### ▸ autoSave

* 자동 저장 활성화 여부

### ▸ saveIntervalSeconds

* 자동 저장 주기 (초)

### ▸ autoBackup

* 자동 백업 사용 여부

### ▸ backupIntervalMinutes

* 백업 생성 주기

### ▸ backupMaxFiles

* 최대 백업 파일 수 (초과 시 오래된 파일 삭제)

---

## 6. Permissions (권한 설정)

```json
"Permissions": {
  "opOnly": true,
  "useLuckPerms": true,
  "ignoreNoPermissionMessage": false
}
```

### ▸ opOnly

* OP만 사용 가능 여부

### ▸ useLuckPerms

* LuckPerms 연동 여부

### ▸ ignoreNoPermissionMessage

* 권한 없을 때 메시지 숨김

---

## 7. Skill (스킬 시스템 설정)

```json
"Skill": {
  "validateSkillFiles": true,
  "stopOnCriticalError": false,
  "autoFixSimpleError": true
}
```

### ▸ validateSkillFiles

* 스킬 JSON 파일 유효성 검사

### ▸ stopOnCriticalError

* 치명적 오류 발생 시 시스템 중단

### ▸ autoFixSimpleError

* 단순한 오류 자동 수정 시도

---

## 8. Reward (보상 시스템 설정)

```json
"Reward": {
  "validateRewardFiles": true,
  "preventDuplicateReward": true,
  "cooldownSeconds": 10,
  "Notify": {
    "chat": true,
    "actionBar": true,
    "title": false,
    "subtitle": false
  }
}
```

### ▸ validateRewardFiles

* 보상 JSON 유효성 검사

### ▸ preventDuplicateReward

* 중복 보상 지급 방지

### ▸ cooldownSeconds

* 보상 지급 쿨타임 (초)

### ▸ Notify

* 보상 알림 방식 설정

  * chat / actionBar / title / subtitle

---

## 9. Protection (보호 장치)

```json
"Protection": {
  "preventOverflow": true,
  "preventAsyncRace": true,
  "safeModeOnException": true
}
```

### ▸ preventOverflow

* 경험치/레벨 오버플로우 방지

### ▸ preventAsyncRace

* 비동기 경쟁 상태 방지

### ▸ safeModeOnException

* 예외 발생 시 안전 모드 진입

---

## 10. VersionControl (버전 관리)

```json
"VersionControl": {
  "checkPluginVersion": true,
  "executeOnlySupportedFeatures": true
}
```

### ▸ checkPluginVersion

* 플러그인 버전 체크

### ▸ executeOnlySupportedFeatures

* 지원되는 기능만 실행

---

## 11. PlaceholderAPI 연동

```json
"PlaceholderAPI": {
  "enable": true
}
```

### ▸ enable

* PlaceholderAPI 연동 활성화
* `%drpg_level%`, `%drpg_skill_xp%` 등 사용 가능

---
