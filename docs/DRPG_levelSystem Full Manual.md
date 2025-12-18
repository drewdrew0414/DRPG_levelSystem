# Made By drewdrew0414 (or drewdrew1_)

---

# SELECT LANGUAGE
- [English](#english-version-manual)
- [한국어](#한국어-버전-설명서)

---

## ENGLISH VERSION MANUAL

## (Made By drewdrew0414(or drewdrew1_))

# SELECT LANGUAGE

* [English](#english-version-manual)
* [한국어](#한국어-버전-설명서)

---

## ENGLISH VERSION MANUAL

## 0. Table of Contents

* [1. About DRPG](#1-about-drpg)

  * [1-1. What is DRPG LevelSystem?](#1-1-what-is-drpg-levelsystem)
  * [1-2. System Design Philosophy](#1-2-system-design-philosophy)
  * [1-3. Data-Driven Architecture](#1-3-data-driven-architecture)

* [2. Installation Guide](#2-installation-guide)

* [3. File Structure](#3-file-structure)

* [4. How to Use `config.json`](#4-how-to-use-configjson)

* [5. How to Use `skills/*.json` & `rewards/*.json`](#5-how-to-use-skillsjson--rewardsjson)

* [6. Command Guide](#6-command-guide)

---

## 1. About DRPG

### 1-1. What is DRPG LevelSystem?

* DRPG LevelSystem is a **fully modular, JSON-based RPG level system** developed for Minecraft (Paper/Spigot) servers.
* It is designed so that **server operators, developers, and content creators can freely customize skills, experience rules, level-up mechanics, and reward structures without modifying Java code**.
* All system components are defined using text-based JSON files, which are loaded and merged into a unified runtime model when the server starts.
* This approach enables **high extensibility, easy maintenance, and rapid configuration changes**.
* Adding new skills or importing content packs from other servers is simple and efficient.

### 1-2. System Design Philosophy

The core design philosophy of DRPG LevelSystem is as follows:

* **Externalized Game Rules** – Game logic resides in JSON files, not Java code.
* **Modularity** – Skills and rewards are managed independently.
* **Fault Isolation** – A single corrupted file does not stop the entire system.
* **Data Integrity** – Player data is stored using UUIDs, safe from nickname changes.
* **Debug Visibility** – When debug mode is enabled, all loading events, parsing details, and registered content are logged.
* **Complete Customization** – Server owners can create unlimited skills, reward tiers, and finely tuned experience rules.

### 1-3. Data-Driven Architecture

* DRPG LevelSystem is built on a **Data-Driven Architecture**.
* Heavy or repetitive tasks are processed **asynchronously in the background**, ensuring stable operation without impacting server performance.

---

## 2. Installation Guide

### Installation

1. Install and run a [PaperMC](https://papermc.io/downloads) server.
2. Download the DRPG LevelSystem plugin `.jar` file.

   * Make sure the plugin version matches your server version.
3. Copy the `.jar` file into the server’s `plugins` folder.
4. Restart the server.
5. If the console outputs **"DRPG LevelSystem enabled"**, the installation was successful.

   * If errors occur, contact: **[drew0414drew@gmail.com](mailto:drew0414drew@gmail.com)**

### Usage

1. On server startup, the folder `plugins/DRPG/levelSystem/` will be created.
2. Place skill files into `plugins/DRPG/levelSystem/skills/`
   → [Example](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20%28ENG%29.md)
3. Place reward files into `plugins/DRPG/levelSystem/rewards/`
   → [Example](../How%20To%20Use/JSON/Skills/Skills%20Manual%20%28ENG%29.md)

---

## 3. File Structure

Base directory:

```
<ServerName>/plugins/DRPG/levelSystem/
```

1. **/config.json**

   * All global settings are configured here.
   * Detailed documentation:
     → [Config Manual](../How%20To%20Use/JSON/Config/Config%20Manual%20%28ENG%29.md)

2. **/skills/*.json**

   * All skill definition files must be placed here.
   * Documentation:
     → [Skills Manual](../How%20To%20Use/JSON/Skills/Skills%20Manual%20%28ENG%29.md)

3. **/rewards/*.json**

   * All reward definition files must be placed here.
   * Documentation:
     → [Rewards Manual](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20%28ENG%29.md)

---

## 4. How to Use `config.json`

* Full documentation is available here:
  → [Config Manual](../How%20To%20Use/JSON/Config/Config%20Manual%20%28ENG%29.md)

### 1. Base Configuration

| Option          | Type    | Description                                                                     |
| --------------- | ------- | ------------------------------------------------------------------------------- |
| `configVersion` | String  | Configuration file version. Used for automatic updates when the format changes. |
| `usePlugin`     | boolean | Enables or disables the plugin. If set to false, the plugin will not run.       |

### 2. Debug

| Option         | Type    | Description                                                  |
| -------------- | ------- | ------------------------------------------------------------ |
| `enable`       | boolean | Enables debug logging. Recommended to disable in production. |
| `forceEnable`  | boolean | Forces debug mode regardless of error state.                 |
| `retryOnError` | boolean | Retries failed tasks automatically.                          |
| `retryCount`   | integer | Maximum retry attempts on failure.                           |

### 3. Logging

| Option               | Type    | Description                                         |
| -------------------- | ------- | --------------------------------------------------- |
| `logToConsole`       | boolean | Outputs logs to the server console.                 |
| `logToFile`          | boolean | Saves logs to a file.                               |
| `logFileName`        | String  | Name of the log file.                               |
| `includeDebug`       | boolean | Includes debug logs in the log file.                |
| `includeStackTrace`  | boolean | Includes stack traces on errors.                    |
| `includeJsonError`   | boolean | Includes JSON parsing errors.                       |
| `includePerformance` | boolean | Logs performance metrics (enable only when needed). |

### 4. Performance

| Option               | Type    | Description                                    |
| -------------------- | ------- | ---------------------------------------------- |
| `useAsync`           | boolean | Runs heavy tasks asynchronously (recommended). |
| `asyncThreads`       | integer | Number of async worker threads.                |
| `useCache`           | boolean | Enables data caching for faster access.        |
| `cacheExpireSeconds` | integer | Cache expiration time in seconds.              |

### 5. Player Data

| Option                  | Type                         | Description                                             |
| ----------------------- | ---------------------------- | ------------------------------------------------------- |
| `storageType`           | String (JSON, MYSQL, SQLITE) | Data storage type. **Note:** v1.0.0 supports JSON only. |
| `autoSave`              | boolean                      | Automatically saves player data.                        |
| `saveIntervalSeconds`   | integer                      | Auto-save interval in seconds.                          |
| `autoBackup`            | boolean                      | Enables automatic backups (recommended).                |
| `backupIntervalMinutes` | integer                      | Backup interval in minutes.                             |
| `backupMaxFiles`        | integer                      | Maximum number of backup files to keep.                 |

### 6. Permissions

| Option                      | Type    | Description                              |
| --------------------------- | ------- | ---------------------------------------- |
| `opOnly`                    | boolean | Restricts commands/features to OPs only. |
| `useLuckPerms`              | boolean | Enables LuckPerms integration.           |
| `ignoreNoPermissionMessage` | boolean | Suppresses “no permission” messages.     |

### 7. Skills & Rewards

| Option                            | Type    | Description                                         |
| --------------------------------- | ------- | --------------------------------------------------- |
| Skill > `validateSkillFiles`      | boolean | Validates skill JSON format on load.                |
| Skill > `autoFixSimpleError`      | boolean | Attempts to auto-fix simple errors.                 |
| Reward > `preventDuplicateReward` | boolean | Prevents duplicate rewards.                         |
| Reward > `cooldownSeconds`        | integer | Minimum cooldown between rewards.                   |
| Reward > `Notify`                 | String  | Notification type: chat, actionBar, title, subtitle |

### 8. Protection & Version Control

| Option                                | Type    | Description                               |
| ------------------------------------- | ------- | ----------------------------------------- |
| Protection > `safeModeOnException`    | boolean | Enables safe mode on critical exceptions. |
| VersionControl > `checkPluginVersion` | boolean | Checks for plugin updates.                |

### 9. PlaceholderAPI Integration

| Option                    | Type    | Description                     |
| ------------------------- | ------- | ------------------------------- |
| PlaceholderAPI > `enable` | boolean | Enables PlaceholderAPI support. |

---

## 5. How to Use `skills/*.json` & `rewards/*.json`

Refer to the manuals below:

* [Skills JSON Manual](../How%20To%20Use/JSON/Skills/Skills%20Manual%20%28ENG%29.md)

  * [Examples](../How%20To%20Use/JSON/Skills/example/)
* [Rewards JSON Manual](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20%28ENG%29.md)

  * [Examples](../How%20To%20Use/JSON/Rewards/example/)

---

## 6. Command Guide

* [View Command Manual](../How%20To%20Use/Commands/command%20Manual%20%28ENG%29.md)

---

## 한국어 버전 설명서

## 0. 목차
* [1. DRPG에 대하여](#1-drpg에-대하여)
  * [1-1. DRPG levelSystem이란?](#1-1-drpg-levelsystem이란)
  * [1-2. 시스템 설계 철학](#1-2-시스템-설계-철학)
  * [1-3. 데이터 기반 아키텍처](#1-3-데이터-기반-아키텍처)
    
* [2. 설치 가이드](#2-설치-가이드)

* [3. 파일 구조](#3-파일-구조)

* [4. config.json 사용법](#4-configjson-사용법)

* [5. skills/\*.json 및 rewards/\*.json 사용법](#5-skillsjson--rewardsjson-사용법)

* [6. 명령어 가이드](#6-명령어-가이드)

---

## 1. DRPG에 대하여
### 1-1. DRPG levelSystem이란?
* DRPG levelSystem은 Minecraft(Paper/Spigot) 서버용으로 제작된 완전 모듈화된 JSON 기반 RPG 레벨 시스템이다.
* 서버 운영자, 개발자, 콘텐츠 제작자가 Java 코드를 수정하지 않고도 스킬, 경험치 규칙, 레벨 상승 방식, 보상 구조 등 RPG 관련 모든 동작을 자유롭게 변경할 수 있도록 설계되었다.
* 시스템의 모든 구성 요소는 텍스트(JSON) 기반 파일로 이루어져 있으며, 플러그인은 서버 시작 시 모든 설정 파일을 불러온 후 이를 통합하여 하나의 실행 모델로 만든다.
* 이는 높은 확장성, 유지보수 용이성, 빠른 설정 변경을 가능하게 한다.
* 또한 새로운 스킬을 추가하거나, 다른 서버에서 제작한 콘텐츠 팩을 가져오는 것도 매우 간단하다.

### 1-2. 시스템 설계 철학
* DRPG levelSystem의 핵심 설계 철학은 다음과 같다:
  * 외부화 게임 규칙은 Java 코드가 아니라 JSON 파일에 존재한다.
  * 모듈성 스킬과 보상은 독립적으로 관리된다.
  * 고장 격리 하나의 파일이 망가져도 전체 시스템이 중단되지 않는다.
  * 데이터 무결성 플레이어 데이터는 UUID 기반으로 저장되어 닉네임 변경에도 안전하다.
  * 디버그 가시성 디버그 기능을 켜면 모든 로드 이벤트, 파일 파싱 정보, 등록된 콘텐츠를 확인할 수 있다.
  * 완전한 커스터마이징 서버 운영자는 무제한 스킬, 무제한 보상 단계, 정밀 경험치 규칙을 만들 수 있다.

### 1-3. 데이터 기반 아키텍처
* DRPG LevelSystem은 **데이터 중심 아키텍처(Data-Driven Architecture)**를 기반으로 설계되었다.
* 이를 통해 무거운 작업이나 반복 작업을 **백그라운드에서 비동기 처리**하여, 서버 성능에 영향을 주지 않고 안정적으로 동작하도록 구현되었다.

---

## 2. 설치 및 사용 가이드

* **설치법**
  1. [PaperMC](https://papermc.io/downloads) 서버를 설치하고 실행합니다.
  2. DRPG LevelSystem 플러그인 `.jar` 파일을 다운로드합니다.
     * 서버 버전과 플러그인이 지원하는 버전 맞출 것
  3. 서버 디렉토리 내 `plugins` 폴더에 `.jar` 파일을 복사합니다.
  4. 서버를 재시작합니다.
  5. 서버 콘솔에 "DRPG LevelSystem enabled" 메시지가 출력되면 정상적으로 설치 완료입니다.
     * 오류가 날 시 (drew0414drew@gmail.com)에 문의할 것.

* **사용법**
 1. 서버 시작 시 `plugins/DRPG/levelSystem/ 폴더가 생성됩니다.
 2. `plugins/DRPG/levelSystem/skills/에 파일을 넣습니다. > [예시](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20(KOR).md)
 3. `plugins/DRPG/levelSystem/rewards/에 파일을 넣습니다. > [예시](../How%20To%20Use/JSON/Skills/Skills%20Manual%20(KOR).md)

---

## 3. 파일 구조
  * `<ServerName>/plugins/DRPG/levelSystem/` 위치에 기본 파일 생성됨.

    1. /config.json:
       * 모든 설정은 이 파일에서 진행된다.
       자세한 설명을 보려면 [여기](../How%20To%20Use/JSON/Config/Config%20Manual%20(KOR).md)를 클릭 하십시오.

    2. /skills/*.json
       * 모든 스킬은 이 위치에 있어야한다.
       자세한 설명을 보려면 [여기](../How%20To%20Use/JSON/Skills/Skills%20Manual%20(KOR).md)를 클릭 하십시오.
    3. /rewards/*.json
       * 모든 보상은 이 위치에 있어야한다.
       자세한 설명을 보려면 [여기](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20(KOR).md)를 클릭 하십시오.

---

## 4. `config.json` 사용법
* 자세한 사용법은 [여기](../How%20To%20Use/JSON/Config/Config%20Manual%20(KOR).md)에 있습니다.

* ### 1. 기본 설정 (Base Configuration)

| 설정 항목 | 값 | 설명 및 사용법 |
|---|---|---|
| "configVersion" | String | 설정 파일의 버전입니다. 이 버전이 변경되면 플러그인이 자동으로 설정 파일을 업데이트할 수 있습니다. |
| "usePlugin" | boolean | 플러그인 사용 여부를 결정합니다. false로 설정 시 플러그인이 비활성화 됨. |

* ### 2. 디버그 (Debug)

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| "enable" | boolean | 디버그 메시지를 출력할지 여부. 일반 운영 시에는 false로 설정하여 불필요한 로그 출력을 줄이는 것이 좋음. |
| "forceEnable" | boolean | 오류 발생 여부와 상관없이 디버그를 강제로 활성화합니다. |
| "retryOnError" | boolean | 오류 발생 시 작업을 재시도할지 여부. |
| "retryCount" | intager | 오류 발생 시 최대 재시도 횟수. |

* ### 3. 로깅 (Logging)

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| "logToConsole" | boolean | 로그를 콘솔(서버 화면)에 출력할지 여부. |
| "logToFile" | boolean | 로그를 파일로 저장할지 여부. |
| "logFileName" | <String>.txt | 로그 파일의 이름. |
| "includeDebug" | boolean | 로그 파일에 디버그 메시지를 포함할지 여부. |
| "includeStackTrace" | boolean | 오류 발생 시 호출 스택 정보를 포함할지 여부. (문제 해결에 유용) |
| "includeJsonError" | boolean | JSON 관련 오류 정보를 포함할지 여부. |
| "includePerformance" | boolean | 성능 측정 관련 로그를 포함할지 여부. 성능 분석이 필요할 때만 true로 설정할 것. |

* ### 4. 성능 (Performance)

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| "useAsync" | boolean | 시간이 오래 걸리는 작업을 비동기(Async)로 처리하여 서버 지연을 방지. 권장 설정입니다. |
| "asyncThreads" | intager | 비동기 작업을 처리할 스레드(Thread) 수. 서버 자원 및 플러그인 부하에 따라 조절 가능. |
| "useCache" | boolean | 데이터 캐싱을 사용하여 반복적인 데이터 조회 속도를 높힘. |
| "cacheExpireSeconds" | intager | 캐시된 데이터가 유지되는 시간(초). |

* ### 5. 플레이어 데이터 (PlayerData)

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| "storageType" | String(JSON, MYSQL, SQLITE) `WARN. 1.0.0버전은 MYSQL과 SQLITE 지원하지 않음.` | 데이터 저장 방식. 다른 옵션이 있다면 선택 가능하지만, 기본으로는 JSON으로 설정됨. |
| "autoSave" | boolean | 플레이어 데이터를 자동으로 저장할지 여부. |
| "saveIntervalSeconds" | intager | 자동 저장 간격(5분마다). 서버 부하를 고려하여 조절 가능. |
| "autoBackup" | boolean | 플레이어 데이터를 자동으로 백업할지 여부. 데이터 보호를 위해 true를 유지하는 것이 좋음. |
| "backupIntervalMinutes" | intager | 백업 간격(30분마다). |
| "backupMaxFiles" | intager | 보관할 최대 백업 파일 개수. |

* ### 6. 권한 (Permissions)

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| "opOnly" | boolean | 명령어/기능을 서버 운영자(OP)만 사용할 수 있도록 제한함. 권한 플러그인(예: LuckPerms)을 사용한다면 false로 설정하는 것이 일반적. |
| "useLuckPerms" | boolean | LuckPerms와 같은 권한 플러그인을 사용하여 권한을 관리할지 여부. |
| "ignoreNoPermissionMessage" | boolean | 권한이 없는 사용자에게 "권한이 없습니다" 메시지를 출력하지 않을지 여부. |

* ### 7. 스킬 및 보상 (Skill & Reward)
   
| 설정 항목 | 값 | 사용법 |
|---|---|---|
| Skill > "validateSkillFiles" | boolean | 스킬 정의 파일의 형식이 올바른지 검사. |
| Skill > "autoFixSimpleError" | boolean | 간단한 오류를 자동으로 수정하려고 시도합. |
| Reward > "preventDuplicateReward" | boolean | 동일한 보상이 중복 지급되는 것을 방지. |
| Reward > "cooldownSeconds" | intager | 보상 지급 후 다음 보상 지급까지의 최소 쿨다운 시간(초). |
| Reward > Notify | String (chat, actionBar, title, subtitle) | 보상 지급 시 플레이어에게 어떤 방식으로 알림을 보낼지 설정. |

* ### 8. 보호 및 버전 관리

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| Protection > "safeModeOnException" | boolean | 심각한 예외 발생 시 안전 모드를 활성화하여 추가적인 문제를 방지. |
| VersionControl > "checkPluginVersion" | boolean | 플러그인의 새 버전이 있는지 확인할지 여부. |

* ### 9. PlaceholderAPI 연동

| 설정 항목 | 값 | 사용법 |
|---|---|---|
| PlaceholderAPI > "enable" | boolean | PlaceholderAPI 플러그인과의 연동을 활성화. 다른 플러그인에서 이 플러그인의 변수(Placeholder)를 사용하려면 true여야 함. |

---

## 5. skills/\*.json, rewards/\*.json 사용법

* 이 json들은 아래를 참조하십시오.
* [skills/\*.json 참고하러가기](../How%20To%20Use/JSON/Skills/Skills%20Manual%20(KOR).md)
  * [예시 참고하기](../How%20To%20Use/JSON/Skills/example/)
 
 * [rewards/\*.json 참고하러가기](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20(KOR).md)
  * [예시 참고하기](../How%20To%20Use/JSON/Rewards/example/)

---

## 6. 명령어 가이드

** [명령어 확인하기](../How%20To%20Use/Commands/command%20Manual%20(KOR).md)

---
