---

# **DRPG Level System: Full Config Documentation / 전체 설정 문서**

---

## **Table of Contents / 목차**

1. [Introduction / 소개](#introduction--소개)
2. [configVersion / 설정 버전](#configversion--설정-버전)
3. [usePlugin / 플러그인 사용 여부](#useplugin--플러그인-사용-여부)
4. [Debug / 디버그 설정](#debug--디버그-설정)
5. [Logging / 로그 설정](#logging--로그-설정)
6. [Performance / 성능 최적화 설정](#performance--성능-최적화-설정)
7. [PlayerData / 플레이어 데이터 저장 설정](#playerdata--플레이어-데이터-저장-설정)
8. [Permissions / 권한 설정](#permissions--권한-설정)
9. [Skill / 스킬 관련 설정](#skill--스킬-관련-설정)
10. [Reward / 보상 관련 설정](#reward--보상-관련-설정)
11. [Protection / 보호 및 안정성 설정](#protection--보호-및-안정성-설정)
12. [VersionControl / 버전 관리](#versioncontrol--버전-관리)
13. [PlaceholderAPI / 플러그인 연동](#placeholderapi--플러그인-연동)

---

## **Introduction / 소개**

**EN:**
This documentation explains all configuration options in the DRPG Level System `config.json`.
Settings include plugin behavior, performance, player data management, permissions, skill and reward handling, logging, protection, and notifications.
Adjust these options according to your server performance and desired gameplay balance.

**KR:**
이 문서는 DRPG 레벨 시스템의 `config.json` 설정 옵션을 모두 설명합니다.
설정에는 플러그인 동작, 성능, 플레이어 데이터 관리, 권한, 스킬 및 보상 처리, 로그, 보호, 알림 등이 포함됩니다.
서버 성능과 게임플레이 밸런스에 맞게 옵션을 조정하세요.

---

## **configVersion / 설정 버전**

```json
"configVersion": "1.0.0"
```

**EN:** Specifies the configuration file version.

* Useful for plugin updates to detect outdated configs.

**KR:** 설정 파일 버전을 지정합니다.

* 플러그인 업데이트 시 구버전 설정 감지에 유용합니다.

---

## **usePlugin / 플러그인 사용 여부**

```json
"usePlugin": true
```

**EN:** Enable or disable the plugin entirely.

* `false` disables all plugin features without uninstalling.

**KR:** 플러그인을 전체적으로 활성화/비활성화합니다.

* `false`로 설정하면 기능은 모두 비활성화되지만 플러그인은 제거되지 않습니다.

---

## **Debug / 디버그 설정**

```json
"Debug": {
  "enable": true,
  "forceEnable": false,
  "retryOnError": true,
  "retryCount": 3
}
```

**EN:** Controls debug logging and automatic retries.

* `enable`: Enable debug logs.
* `forceEnable`: Always enable debug, ignoring other conditions.
* `retryOnError`: Retry failed operations automatically.
* `retryCount`: Number of retry attempts.

**Tip:** Use debug mode during testing to catch errors quickly.

**KR:** 디버그 설정은 로그와 재시도를 제어합니다.

* `enable`: 디버그 로그 활성화
* `forceEnable`: 조건 무시하고 항상 디버그 활성화
* `retryOnError`: 실패 작업 자동 재시도
* `retryCount`: 재시도 횟수

**팁:** 테스트 시 디버그를 켜 오류를 빨리 잡으세요.

---

## **Logging / 로그 설정**

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

**EN:** Configures log output.

* `logToConsole`: Output logs to console.
* `logToFile`: Save logs to a file.
* `logFileName`: Name of log file.
* `includeDebug`: Include debug logs.
* `includeStackTrace`: Include stack traces.
* `includeJsonError`: Include JSON parsing errors.
* `includePerformance`: Include performance logs.

**Tip:** Disable debug in live servers to reduce console spam.

**KR:** 로그 출력 방식을 설정합니다.

* `logToConsole`: 콘솔 출력
* `logToFile`: 파일 저장
* `logFileName`: 로그 파일 이름
* `includeDebug`: 디버그 로그 포함
* `includeStackTrace`: 스택 트레이스 포함
* `includeJsonError`: JSON 오류 포함
* `includePerformance`: 성능 로그 포함

**팁:** 운영 서버에서는 디버그를 끄세요.

---

## **Performance / 성능 최적화 설정**

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

**EN:** Optimizes server performance.

* `useAsync`: Use async tasks for better performance.
* `asyncThreads`: Number of async threads.
* `centralAsyncExecutor`: Use centralized async executor.
* `useCache`: Enable caching.
* `cacheExpireSeconds`: Cache expiry time in seconds.
* `preventDesync`: Prevent async data desync.

**Tip:** Adjust thread count based on CPU cores.

**KR:** 서버 성능 최적화 설정입니다.

* `useAsync`: 비동기 작업 사용
* `asyncThreads`: 비동기 쓰레드 수
* `centralAsyncExecutor`: 중앙 비동기 실행기 사용
* `useCache`: 데이터 캐싱 사용
* `cacheExpireSeconds`: 캐시 만료 시간(초)
* `preventDesync`: 비동기 데이터 불일치 방지

**팁:** 서버 CPU 코어에 맞춰 쓰레드 수를 조정하세요.

---

## **PlayerData / 플레이어 데이터 저장 설정**

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

**EN:** Controls how player data is stored and saved.

* `storageType`: "JSON" or "MySQL/SQLite"
* `autoSave`: Automatically save player data.
* `saveIntervalSeconds`: Auto-save interval.
* `autoBackup`: Enable automatic backups.
* `backupIntervalMinutes`: Backup interval.
* `backupMaxFiles`: Max number of backup files.

**KR:** 플레이어 데이터 저장 방식을 설정합니다.

* `storageType`: "JSON" 또는 "MySQL/SQLite"
* `autoSave`: 자동 저장 사용
* `saveIntervalSeconds`: 자동 저장 간격(초)
* `autoBackup`: 자동 백업 사용
* `backupIntervalMinutes`: 백업 간격(분)
* `backupMaxFiles`: 최대 백업 파일 수

---

## **Permissions / 권한 설정**

```json
"Permissions": {
  "opOnly": true,
  "useLuckPerms": true,
  "ignoreNoPermissionMessage": false
}
```

**EN:** Controls plugin permissions.

* `opOnly`: Only OPs can use plugin commands.
* `useLuckPerms`: Use LuckPerms integration.
* `ignoreNoPermissionMessage`: Suppress no-permission messages.

**KR:** 플러그인 권한 설정입니다.

* `opOnly`: OP만 사용 가능
* `useLuckPerms`: LuckPerms 연동 사용
* `ignoreNoPermissionMessage`: 권한 없음 메시지 숨김

---

## **Skill / 스킬 관련 설정**

```json
"Skill": {
  "validateSkillFiles": true,
  "stopOnCriticalError": false,
  "autoFixSimpleError": true
}
```

**EN:** Skill file validation.

* `validateSkillFiles`: Check for skill JSON errors.
* `stopOnCriticalError`: Stop plugin on critical skill error.
* `autoFixSimpleError`: Auto fix minor JSON errors.

**KR:** 스킬 파일 검증 설정입니다.

* `validateSkillFiles`: 스킬 JSON 검증
* `stopOnCriticalError`: 치명적 오류 시 플러그인 중지
* `autoFixSimpleError`: 간단한 오류 자동 수정

---

## **Reward / 보상 관련 설정**

```json
"Reward": {
  "validateRewardFiles": true,
  "preventDuplicateReward": true,
  "cooldownSeconds": 10,
  "Notify": { ... }
}
```

**EN:** Reward file validation and notifications.

* `validateRewardFiles`: Check reward JSON files.
* `preventDuplicateReward`: Avoid giving duplicate rewards.
* `cooldownSeconds`: Reward cooldown time.
* `Notify`: Options for broadcast, chat, actionbar, title, subtitle, bossbar, and log notifications.

**KR:** 보상 파일 검증 및 알림 설정.

* `validateRewardFiles`: 보상 JSON 검증
* `preventDuplicateReward`: 중복 보상 방지
* `cooldownSeconds`: 보상 쿨다운
* `Notify`: 브로드캐스트, 채팅, 액션바, 타이틀, 서브타이틀, 보스바, 로그 알림 옵션

---

## **Protection / 보호 및 안정성 설정**

```json
"Protection": {
  "preventOverflow": true,
  "preventAsyncRace": true,
  "safeModeOnException": true
}
```

**EN:** Ensures data safety and prevents crashes.

* `preventOverflow`: Avoid numeric overflows.
* `preventAsyncRace`: Prevent async race conditions.
* `safeModeOnException`: Enable safe mode on exceptions.

**KR:** 데이터 안전과 충돌 방지를 위한 설정입니다.

* `preventOverflow`: 숫자 오버플로 방지
* `preventAsyncRace`: 비동기 레이스 방지
* `safeModeOnException`: 예외 발생 시 안전 모드

---

## **VersionControl / 버전 관리**

```json
"VersionControl": {
  "checkPluginVersion": true,
  "executeOnlySupportedFeatures": true
}
```

**EN:** Manages plugin version checks and feature compatibility.

* `checkPluginVersion`: Verify if plugin is up-to-date.
* `executeOnlySupportedFeatures`: Skip unsupported features.

**KR:** 플러그인 버전 확인과 기능 호환성 관리.

* `checkPluginVersion`: 최신 버전 확인
* `executeOnlySupportedFeatures`: 지원되지 않는 기능 실행 생략

---

## **PlaceholderAPI / 플러그인 연동**

```json
"PlaceholderAPI": {
  "enable": true
}
```

**EN:** Enables PlaceholderAPI support for placeholders in messages.

**KR:** 메시지 내 플레이스홀더 사용을 위한 PlaceholderAPI 지원 활성화.

---
