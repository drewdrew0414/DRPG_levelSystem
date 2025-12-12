# ================================================================

# **DrewRPG Ultimate Integrated Manual**

# **(Full English → Korean Alternating Version, No Omission)**

# ================================================================

---

SECTION 0 — Preface / 서문

  0.1 About DrewRPG

  0.2 Philosophy of System Design

  0.3 Data-Driven Architecture Overview

SECTION 1 — System Overview / 시스템 개요

  1.1 What is DrewRPG Level System

  1.2 System Architecture Diagram

  1.3 Core Components Summary

  1.4 Data Flow Overview

SECTION 2 — Installation Guide / 설치 가이드

  2.1 Requirements

  2.2 Server Preparation

  2.3 Plugin Installation

  2.4 First Launch Checklist

SECTION 3 — File Structure / 폴더 및 파일 구조

  3.1 Plugin Root

  3.2 Config Folder

  3.3 skills/*.json

  3.4 rewards/*.json

  3.5 playerdata/*.json

SECTION 4 — PlayerData Format FULL SPEC / 플레이어데이터 전체 스펙

  4.1 Mandatory Fields

  4.2 Optional Fields

  4.3 Validation Rules

  4.4 Example Data Structures
  
  4.5 Common Mistakes

SECTION 5 — Skills Format DEEP SPEC / 스킬 포맷 전체 스펙

  5.1 Skill Root Fields

  5.2 Events Block Specification

  5.3 Random EXP Rules

  5.4 Permission-Based Skill Logic

  5.5 Advanced Design Examples

SECTION 6 — Rewards Format DEEP SPEC / 보상 포맷 전체 스펙

  6.1 Reward Root Fields

  6.2 Item Formats

  6.3 NBT Handling Rules

  6.4 Command Rewards

  6.5 Probability-Based Reward Sets

SECTION 7 — Commands FULL GUIDE (EN/KR Parallel)

  7.1 System Commands

  7.2 Admin Commands

  7.3 Editor Commands

  7.4 Debug Commands

  7.5 Output Examples

SECTION 8 — Validator Engine Internals / 밸리데이터 엔진 내부 구조

  8.1 Purpose

  8.2 Validation Flow

  8.3 Automatic Data Recovery

  8.4 Error Prevention Logic

SECTION 9 — Security Policy (Extended Edition) / 보안정책 확장판

  9.1 Vulnerability Categories

  9.2 Secure Reporting Process

  9.3 Response Timeline

  9.4 Safe JSON Handling Rules

  9.5 Offensive Behavior Protection

SECTION 10 — Debug Engine Internals / 디버그 엔진 내부 구조

  10.1 Debug Flag Structure

  10.2 Log Layers

  10.3 Debug Message Policies

  10.4 Performance Impact

  10.5 Recommended Debug Setup

SECTION 11 — Server Optimization Guide / 서버 최적화 가이드

  11.1 Requirements

---

# ================================================================

# SECTION 1 — INTRODUCTION

# ================================================================

---

## [EN]

DrewRPG is a fully modular, JSON-driven leveling and reward framework designed for Minecraft (Paper/Spigot) servers.
Its primary purpose is to allow server operators, developers, and content creators to define and modify all RPG-related behavior — such as skills, EXP rules, level progression, and reward structures — without touching Java code or recompiling the plugin.

The entire system is decentralized into text-based modules.
The plugin loads all configuration files at startup and merges them into a unified runtime model.
This gives high flexibility, high maintainability, and allows the system to scale easily when adding additional skills or content packs.

The system is composed of these core components:

1. Global configuration — config.json
2. Skill definition files — skills/*.json
3. Reward definition files — rewards/*.json
4. Debug framework — global and per-module logging controls
5. Data registry — runtime caches for skills, rewards, and UUID-bound player data

Every component operates independently, but all of them integrate at runtime to form the final RPG engine.

DrewRPG ensures safe loading by validating JSON structures, types, and required fields before enabling systems.
If one module fails (e.g., a malformed skills file), the plugin disables only the broken module while allowing other modules to continue running.

This architecture is designed for servers that need:

• Highly customizable RPG systems
• Fully externalized configuration
• Modular skill trees
• Scalable reward tables
• Reliable UUID-based player data
• Optional debug system for development and troubleshooting

---

## [KR]

DrewRPG는 Minecraft(Paper/Spigot) 서버용으로 제작된 완전 모듈화된 JSON 기반 RPG 레벨 시스템이다.
서버 운영자, 개발자, 콘텐츠 제작자가 Java 코드를 수정하지 않고도 스킬, 경험치 규칙, 레벨 상승 방식, 보상 구조 등 RPG 관련 모든 동작을 자유롭게 변경할 수 있도록 설계되었다.

시스템의 모든 구성 요소는 텍스트(JSON) 기반 파일로 이루어져 있으며, 플러그인은 서버 시작 시 모든 설정 파일을 불러온 후 이를 통합하여 하나의 실행 모델로 만든다.
이는 높은 확장성, 유지보수 용이성, 빠른 설정 변경을 가능하게 한다. 또한 새로운 스킬을 추가하거나, 다른 서버에서 제작한 콘텐츠 팩을 가져오는 것도 매우 간단하다.

핵심 구성 요소는 다음과 같다:

1. 전역 설정 파일 — config.json
2. 스킬 정의 파일 — skills/*.json
3. 보상 정의 파일 — rewards/*.json
4. 디버그 프레임워크 — 전체 및 모듈별 로그 제어
5. 데이터 레지스트리 — 스킬, 보상, 플레이어 UUID 데이터의 런타임 캐시

각 구성 요소는 개별적으로 동작하지만, 런타임에 하나의 RPG 엔진으로 통합된다.

DrewRPG는 JSON 구조, 필드 타입, 필수 요소 등을 로드 전에 검사하여 안전성을 보장한다.
어떤 모듈(예: skills 파일 중 하나)이 손상되어도 해당 모듈만 비활성화되며, 나머지 모듈은 정상 동작한다.

이 아키텍처는 다음과 같은 서버에서 특히 효과적이다:

• 고도로 커스터마이징 가능한 RPG 시스템이 필요한 서버
• 전부 외부 설정으로 조작하고 싶은 서버
• 확장 가능한 스킬 트리 구조를 원하는 서버
• 대규모 보상 체계를 필요로 하는 서버
• UUID 기반 플레이어 데이터가 필요한 서버
• 개발 및 디버깅을 위한 세밀한 로그 제어가 필요한 서버

---

## [EN]

DrewRPG emphasizes the following core design principles:

• **Externalization**
All gameplay rules exist in JSON files, not Java classes.

• **Modularity**
Skills and rewards are independent modules.

• **Fault Isolation**
If one file breaks, the rest of the system remains active.

• **Data Integrity**
Player data always uses UUID keys to avoid problems with username changes.

• **Debug Visibility**
When enabled, the system exposes all loading events, parsed files, and registered content for easier development.

• **Full Customizability**
Server owners can create unlimited skills, unlimited reward tiers, and precise EXP rules.

These principles allow the system to be both powerful and easy to modify even on live servers.

---

## [KR]

DrewRPG의 핵심 설계 철학은 다음과 같다:

• **외부화**
게임 규칙은 Java 코드가 아니라 JSON 파일에 존재한다.

• **모듈성**
스킬과 보상은 독립적으로 관리된다.

• **고장 격리**
하나의 파일이 망가져도 전체 시스템이 중단되지 않는다.

• **데이터 무결성**
플레이어 데이터는 UUID 기반으로 저장되어 닉네임 변경에도 안전하다.

• **디버그 가시성**
디버그 기능을 켜면 모든 로드 이벤트, 파일 파싱 정보, 등록된 콘텐츠를 확인할 수 있다.

• **완전한 커스터마이징**
서버 운영자는 무제한 스킬, 무제한 보상 단계, 정밀 경험치 규칙을 만들 수 있다.

이러한 설계 덕분에 DrewRPG는 강력하면서도 쉽게 확장할 수 있는 RPG 시스템이 된다.

---

# ================================================================

# SECTION 2 — DIRECTORY STRUCTURE & FILE SYSTEM

# ================================================================

---

## [EN]

DrewRPG stores all configuration, runtime data, and user-defined content in a structured directory hierarchy inside the plugin folder.
Understanding this structure is essential for troubleshooting, customization, backup, and content creation.

Below is the full recommended directory layout used by the plugin:

```
/plugins/DrewRPG/
│
├── config.json
│
├── skills/
│   ├── Mining.json
│   ├── Farming.json
│   ├── Combat_Axe.json
│   └── ... (additional user-defined skill files)
│
├── rewards/
│   ├── Mining.json
│   ├── Farming.json
│   └── ... (reward files matching each skill)
│
└── playerdata/
    ├── <UUID>.json
    ├── <UUID>.json
    └── ... (one file per player)
```

### **Description of Each Directory**

---

## 1. config.json

The global configuration controlling plugin behavior, debug settings, and version metadata.
This is always loaded first when the plugin is enabled.

---

## 2. skills/

This directory contains **one JSON file per skill**.
The file name must match the internal skill key (case-sensitive).
Each skill file defines:

• Skill name
• Display name
• Maximum level
• Experience drainage rules
• Event triggers (mining, breaking, combat, etc.)
• EXP amounts
• Randomization system (optional)

---

## 3. rewards/

This directory contains **one JSON file per skill**, defining rewards granted on specific levels.

Reward entries contain:

• Level number
• List of items
• EXP bonuses
• Enchantments
• Random reward modes

---

## 4. playerdata/

This directory stores **UUID.json player progress files** created automatically by the plugin.
A file is created when a player joins or when their data is first referenced.

Each file includes:

• Skill name
• Player level
• Player EXP
• Timestamped integrity markers
• Auto-fix fields inserted by validator

This folder should not be manually edited unless you know exactly what you are doing.

---

## [KR]

DrewRPG는 모든 구성 파일, 플레이어 데이터, 사용자 정의 스킬 및 보상 파일을 플러그인 폴더 안에서 체계적으로 관리한다.
이 디렉토리 구조를 정확히 이해하면 문제 해결, 백업, 설정 변경, 커스텀 콘텐츠 제작이 훨씬 쉬워진다.

아래는 DrewRPG가 사용하는 표준 디렉토리 구조이다:

```
/plugins/DrewRPG/
│
├── config.json
│
├── skills/
│   ├── Mining.json
│   ├── Farming.json
│   ├── Combat_Axe.json
│   └── ... (사용자가 추가한 스킬 파일들)
│
├── rewards/
│   ├── Mining.json
│   ├── Farming.json
│   └── ... (각 스킬에 대응하는 보상 파일)
│
└── playerdata/
    ├── <UUID>.json
    ├── <UUID>.json
    └── ... (플레이어당 1개 파일)
```

### **각 디렉토리 설명**

---

## 1. config.json

플러그인의 전체 동작, 디버그 설정, 버전 정보를 제어하는 전역 설정 파일이다.
플러그인이 활성화될 때 항상 가장 먼저 로드된다.

---

## 2. skills/

이 폴더에는 **스킬당 1개의 JSON 파일**이 들어간다.
파일 이름은 반드시 스킬의 내부 키와 동일해야 하며 대소문자까지 일치해야 한다.

각 스킬 파일은 다음 내용을 포함한다:

• 스킬 이름
• 표시용 이름 (GUI/출력용)
• 최대 레벨
• 경험치 소모 규칙
• 이벤트 트리거 (광질, 농사, 전투 등)
• 경험치량
• 랜덤 보상(선택사항)

---

## 3. rewards/

이 폴더 역시 스킬당 하나의 JSON 파일이 존재한다.
각 파일은 해당 스킬의 특정 레벨에서 지급되는 보상을 정의한다.

보상 파일 내용:

• 레벨 번호
• 아이템 목록
• 추가 경험치
• 인챈트 정보
• 랜덤 보상 모드

---

## 4. playerdata/

이 폴더에는 **플레이어 UUID.json 파일**이 저장된다.
플레이어가 서버에 처음 접속하거나 데이터가 필요할 때 자동 생성된다.

각 파일에는 다음 정보가 들어간다:

• 스킬 이름
• 레벨
• 경험치
• 무결성 보정용 값
• validator에 의해 자동 삽입되는 필드들

이 파일은 직접 수정하면 데이터 오류가 쉽게 생기므로 특별한 이유가 없으면 편집하지 말아야 한다.

---

## [EN]

### Common Mistakes & Pitfalls

1. **Skill file name does NOT match internal skill key**
   → The skill will fail to load.

2. **Reward file missing for a skill**
   → The skill loads successfully, but level-up reward processing will fail.

3. **Invalid JSON formatting**
   → The entire file is skipped for safety.

4. **playerdata files edited manually**
   → Incorrect structure may cause auto-reset or data corruption.

5. **Deleting a skill file without deleting playerdata**
   → The validator will remove ghosts but may produce warnings.

---

## [KR]

### 자주 발생하는 실수

1. **스킬 파일 이름이 스킬 내부 키와 다를 때**
   → 해당 스킬은 로드되지 않음.

2. **보상 파일이 없는 경우**
   → 스킬 자체는 로드되지만 레벨업 보상 지급이 실패함.

3. **JSON 문법 오류**
   → 안전을 위해 해당 파일은 통째로 무시됨.

4. **playerdata를 수동으로 수정하는 경우**
   → 구조가 깨지면 자동 초기화되거나 데이터가 손상될 수 있음.

5. **스킬 파일을 삭제했지만 playerdata는 남겨둔 경우**
   → validator가 유령 스킬 데이터를 자동으로 삭제하며 경고를 출력할 수 있음.

---

# ================================================================

# SECTION 3 — CONFIG.JSON COMPLETE SPECIFICATION

# ================================================================

---

## [EN]

The `config.json` file controls global plugin behavior.
Below is the **full recommended structure**, with explanations for each field.

```
{
  "version": "1.0.0",

  "usePlugin": true,

  "Debug": {
    "useDebug": false,
    "logLoadedSkills": true,
    "logLoadedRewards": true,
    "logPlayerJoin": true,
    "logExpChanges": false,
    "logRewardGranting": false,
    "logValidator": true
  },

  "Data": {
    "autoSaveIntervalTicks": 1200,
    "validateOnJoin": true,
    "validateOnLoad": true
  }
}
```

### FIELD DETAILS

---

## version

Human-readable version marker.
The plugin does not enforce behavior based on version numbers, but this helps in debugging and patch tracking.

---

## usePlugin

If false → the plugin disables all RPG systems but remains enabled in /plugins.
Useful for debugging conflicts without uninstalling the plugin.

---

## Debug → useDebug

Master toggle. If false, no debug logs are printed regardless of sub-options.

---

## Debug Sub-options

### logLoadedSkills

Logs every loaded skill file and its parsed data.

### logLoadedRewards

Logs each reward file and all level entries.

### logPlayerJoin

Prints whenever a player joins and their data is loaded/created.

### logExpChanges

Prints EXP additions, removals, and calculations.

### logRewardGranting

Prints detailed information about rewards given at level-up events.

### logValidator

Indicates missing fields, auto-generated fields, and corrupted entries during validation.

---

## Data Sub-options

### autoSaveIntervalTicks

Automatic playerdata save interval.
1200 ticks = 60 seconds.

### validateOnJoin

Runs validator when a player joins.

### validateOnLoad

Runs validator when the plugin loads playerdata on startup.

---

## [KR]

config.json은 플러그인의 전체 동작을 제어하는 핵심 파일이다.
아래는 **권장 전체 구조**이며, 각 필드에 대한 상세 설명을 포함한다.

```
{
  "version": "1.0.0",

  "usePlugin": true,

  "Debug": {
    "useDebug": false,
    "logLoadedSkills": true,
    "logLoadedRewards": true,
    "logPlayerJoin": true,
    "logExpChanges": false,
    "logRewardGranting": false,
    "logValidator": true
  },

  "Data": {
    "autoSaveIntervalTicks": 1200,
    "validateOnJoin": true,
    "validateOnLoad": true
  }
}
```

### 필드 상세 설명

---

## version

사람이 읽기 위한 버전 정보.
플러그인이 이 값을 기반으로 로직을 바꾸지는 않지만 디버깅에 매우 유용하다.

---

## usePlugin

false로 설정하면 플러그인은 비활성화되지만, 파일은 유지된다.
충돌 테스트에 유용하다.

---

## Debug → useDebug

마스터 스위치.
false면 아래 모든 디버그 옵션이 꺼진다.

---

## Debug 하위 옵션

### logLoadedSkills

로드된 모든 스킬 파일 정보를 출력한다.

### logLoadedRewards

로드된 모든 보상 파일 정보를 출력한다.

### logPlayerJoin

플레이어 접속 시 데이터 로드/생성 로그 출력.

### logExpChanges

경험치 추가/감소/레벨업 계산 기록 출력.

### logRewardGranting

레벨업 시 지급되는 보상 기록 출력.

### logValidator

누락된 필드 자동 생성, 잘못된 구조 발견 시 메시지 출력.

---

## Data 하위 옵션

### autoSaveIntervalTicks

자동 저장 주기.
1200틱 = 60초.

### validateOnJoin

플레이어 접속 시 데이터 무결성 검사.

### validateOnLoad

플러그인 로드 시 전체 데이터 검사.

---

# ================================================================

# SECTION 4 — PLAYERDATA FORMAT COMPLETE SPECIFICATION

# ================================================================

---

## [EN]

The `playerdata/` directory contains every player’s RPG progression, saved as `<UUID>.json`.
These files are automatically created, validated, updated, and repaired by the DrewRPG Level System.
Server admins typically **should not** edit these manually, but understanding the internal structure is crucial for debugging.

Below is the **full structural specification** for each player’s data file.

```
{
  "player": {
    "name": "Notch",
    "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
    "lastSeen": 1733900000000
  },

  "skills": {
    "Mining": {
      "level": 12,
      "exp": 340,
      "lastUpdated": 1733900000000,
      "integrity": {
        "validated": true,
        "missingFieldsRepaired": 0
      }
    },

    "Farming": {
      "level": 4,
      "exp": 20,
      "lastUpdated": 1733900000000,
      "integrity": {
        "validated": true,
        "missingFieldsRepaired": 1
      }
    }
  }
}
```

### **Field-by-field Explanation**

---

## 1. player → name

The player’s last-known username.
This is updated automatically whenever the player joins.

---

## 2. player → uuid

Unique identifier. Always stored in lowercase UUID string format.

---

## 3. player → lastSeen

A millisecond UNIX timestamp representing the last moment the player was online.
Updated at logout and on server shutdown.

---

## 4. skills (root object)

This object contains keys matching each loaded skill name.
A key only appears if:

1. The player has gained EXP in that skill
2. The skill was present in earlier versions
3. The validator inserted missing entries

---

## 5. skills → <SkillName>

Each skill entry includes:

### level

The current level of the player in this skill.

### exp

The current experience points accumulated toward the next level.

### lastUpdated

Timestamp of last modification.
Used internally to detect stale or corrupted data.

### integrity

A plugin-managed object containing:

* validated
  Whether the Validator Engine successfully inspected this entry.

* missingFieldsRepaired
  Counts how many missing mandatory fields were repaired automatically.

---

### PLAYERDATA AUTO-FIX RULES

The validator will automatically repair:

* missing level → set to 1
* missing exp → set to 0
* corrupted negative exp → set to 0
* corrupted negative level → set to 1
* missing integrity object → recreated
* missing lastUpdated → set to current timestamp
* ghost skills (skills that no longer exist) → removed

All repairs are logged if debug mode is enabled.

---

## [KR]

`playerdata/` 폴더에는 각 플레이어의 RPG 진행도가 `<UUID>.json` 형식으로 저장된다.
이 파일들은 DrewRPG 시스템이 **자동 생성**, **자동 검증**, **자동 갱신**, **자동 복구**한다.
서버 운영자는 일반적으로 직접 수정할 필요는 없지만, 내부 구조를 이해해두면 문제 해결에 큰 도움이 된다.

아래는 **플레이어 데이터 파일의 전체 구조 명세**이다.

```
{
  "player": {
    "name": "Notch",
    "uuid": "069a79f4-44e9-4726-a5be-fca90e38aaf5",
    "lastSeen": 1733900000000
  },

  "skills": {
    "Mining": {
      "level": 12,
      "exp": 340,
      "lastUpdated": 1733900000000,
      "integrity": {
        "validated": true,
        "missingFieldsRepaired": 0
      }
    },

    "Farming": {
      "level": 4,
      "exp": 20,
      "lastUpdated": 1733900000000,
      "integrity": {
        "validated": true,
        "missingFieldsRepaired": 1
      }
    }
  }
}
```

---

## 필드별 상세 설명

---

## 1. player → name

플레이어의 마지막 닉네임이 저장된다.
로그인 때 자동 갱신된다.

---

## 2. player → uuid

플레이어의 고유 식별자(UUID).
항상 소문자 문자열 형태로 기록된다.

---

## 3. player → lastSeen

플레이어의 마지막 접속 시점을 **밀리초 단위 UNIX 타임스탬프**로 저장한다.

---

## 4. skills 객체

각 스킬 이름을 key로 사용한다.
해당 key가 존재하는 조건은 다음과 같다:

1. 플레이어가 해당 스킬에서 EXP를 얻었거나
2. 이전 버전에 존재하던 데이터이거나
3. validator가 누락된 스킬 항목을 자동 생성한 경우

---

## 5. skills → <스킬 이름>

각 스킬에는 다음 정보가 포함된다:

### level

현재 스킬 레벨.

### exp

해당 레벨의 다음 단계까지 필요한 경험치 중 축적된 양.

### lastUpdated

마지막으로 이 스킬 데이터가 수정된 시점의 타임스탬프.

### integrity

플러그인 내부 무결성 관리 객체.

* validated
  validator가 정상적으로 검사했는지 여부.

* missingFieldsRepaired
  validator가 자동으로 채운 필드 수.

---

### PLAYERDATA 자동 복구 규칙

Validator는 다음과 같은 문제를 자동으로 복구한다:

* level 없음 → level = 1
* exp 없음 → exp = 0
* 음수 exp → exp = 0
* 음수 level → level = 1
* integrity 없음 → integrity 새로 생성
* lastUpdated 없음 → 현재 시간으로 생성
* 삭제된 스킬의 유령 데이터 → 즉시 삭제

모든 복구 작업은 debug 활성화 시 console에 출력된다.

---

## [EN]

### WHY THIS STRUCTURE EXISTS

The structure is intentionally verbose to:

1. Allow perfect validation
2. Allow future expansions without breaking old data
3. Provide clear debugging traces
4. Allow safe recovery from corrupted files
5. Support long-term persistence

The plugin guarantees:

* Player data **never corrupts silently**
* Validator always restores missing fields
* Data remains readable by humans
* Data remains stable through updates

---

## [KR]

### 이 구조가 왜 필요한가?

이 구조는 명확하게 복잡해 보이지만 다음 목적을 위해 필수적이다:

1. 완벽한 데이터 검증
2. 향후 기능 확장 시 기존 데이터 호환
3. 문제 발생 시 명확한 추적 가능
4. 손상된 데이터 복구
5. 장기적인 보존

플러그인이 보장하는 점:

* 플레이어 데이터가 **조용히 손상되는 일은 없음**
* validator가 모든 누락 필드를 자동 복구
* 사람이 직접 읽을 수 있도록 유지
* 플러그인 업데이트 후에도 데이터가 유지됨

---

# --------------------------------------------

# **3. INTERNAL ARCHITECTURE – ENGLISH VERSION**

# --------------------------------------------

## **3.1 System Overview**

DrewRPG is a JSON-driven modular leveling system designed for Minecraft Paper servers.
Every subsystem (skills, rewards, debug logging, player data, configuration) operates independently but is orchestrated through a central loading mechanism.
The plugin does not hardcode any gameplay logic; instead, it interprets JSON structures to define how leveling and rewards operate. This allows administrators and developers to customize the entire RPG structure without modifying code.

The architecture is based on these critical pillars:

1. **Static Initialization Modules**
   Classes responsible for loading JSON data at runtime and storing results in memory maps.

2. **Event-Driven Leveling System**
   The plugin listens to Minecraft events and determines which skill(s) they correspond to based on user-defined JSON.

3. **Reward Distributor Engine**
   When players level up, reward definitions stored in JSON are executed dynamically.

4. **Debug/Logging Interface**
   Every part of the system includes standardized debug output pathways triggered based on config.json.

5. **Persistent Data Storage**
   Player records—including skill levels, experience, and reward claims—are serialized into files stored in /playerdata.

Each part communicates with the others through global registries and controlled access interfaces.

---

## **3.2 JSON Loading Pipeline**

The JSON loading pipeline is the heart of DrewRPG’s architecture.
All JSON loaders follow an identical three-step pipeline:

1. **Discovery Phase**
   The loader scans a directory (e.g., /skills or /rewards) and identifies all *.json files.

2. **Parsing Phase**
   The loader reads each file, converts it into a JsonObject, and performs structural validation.

3. **Registration Phase**
   The validated data is stored in a global static HashMap for fast runtime access.

This pipeline ensures consistency across all module types.

---

## **3.3 Data Storage Registry**

All loaded data is stored in specialized static registries:

| Registry           | Purpose                                              |
| ------------------ | ---------------------------------------------------- |
| SkillDataRegistry  | Stores skill definitions (events, drain, max level). |
| RewardDataRegistry | Stores reward templates for each skill and level.    |
| ConfigRegistry     | Stores config.json main settings and debug flags.    |
| PlayerDataRegistry | Stores real-time player progress.                    |

Each registry exposes safe “get” and “put” methods to avoid null pointer exceptions.

---

## **3.4 Event Dispatch Architecture**

Minecraft events (BlockBreakEvent, EntityDeathEvent, FishingEvent, etc.) are intercepted by event handlers.
The handlers pass the event name to a lookup table to determine:

* Does any skill define this event?
* Should experience be granted?
* Should drains or conditions be applied?
* Should rewards be triggered?

This architecture ensures that a skill can be entirely defined by JSON alone.

---

## **3.5 Reward Execution Engine**

Rewards are executed only when two conditions are met:

1. The player has reached a specific level.
2. A reward JSON exists for that exact skill and level.

Reward types include:

* Item rewards
* Permissions
* Randomized reward clusters
* Multi-item stacks
* Metadata + enchant support
* Experience injection
* Command-based rewards (optional future module)

The reward executor checks debug flags and prints logs accordingly.

---

# --------------------------------------------

# **3. INTERNAL ARCHITECTURE – KOREAN VERSION**

# --------------------------------------------

## **3.1 시스템 개요**

DrewRPG는 JSON 기반으로 동작하는 모듈형 레벨 시스템이다.
모든 서브 시스템(스킬, 보상, 디버그, 플레이어 데이터, 설정)은 독립적으로 작동하지만 중앙 로더가 전체를 통합해 제어한다.
플러그인은 어떤 RPG 규칙도 코드에 고정하지 않는다.
대신 JSON을 읽어 시스템 동작을 정의하기 때문에 서버 관리자는 **코드를 수정하지 않고** RPG 구조 전체를 자유롭게 변경할 수 있다.

아키텍처는 다음 핵심 요소로 구성된다:

1. **정적 초기화 모듈**
   런타임에 JSON을 읽어 메모리 맵에 저장하는 클래스들.

2. **이벤트 기반 레벨 시스템**
   마인크래프트 이벤트를 감지하고 JSON에서 어떤 스킬에 연결되는지 판단한다.

3. **보상 실행 엔진**
   레벨업 시 JSON으로 정의된 보상을 동적으로 지급한다.

4. **디버그/로그 시스템**
   시스템 모든 영역에 통일된 로그 출력 기능을 제공하며 config.json으로 제어된다.

5. **플레이어 데이터 저장 시스템**
   플레이어의 스킬 경험치, 레벨 등을 파일로 저장하여 서버를 껐다 켜도 유지된다.

---

## **3.2 JSON 로딩 파이프라인**

JSON 로딩 프로세스는 DrewRPG의 핵심이다.
모든 JSON 로더는 동일한 3단계 방식을 따른다.

1. **파일 탐색 단계**
   /skills, /rewards 같은 디렉토리에서 모든 JSON 파일을 읽는다.

2. **파싱 단계**
   JsonObject로 변환하고 구조 검증까지 수행한다.

3. **등록 단계**
   검증된 데이터를 전역 static HashMap에 저장한다.

이 규칙 덕분에 플러그인 전체 모듈의 구조가 매우 안정적이다.

---

## **3.3 데이터 저장 레지스트리**

모든 로딩된 데이터는 다음 전용 레지스트리에 보관된다:

| 레지스트리              | 용도                 |
| ------------------ | ------------------ |
| SkillDataRegistry  | 스킬 정의 저장           |
| RewardDataRegistry | 각 스킬/레벨 보상 저장      |
| ConfigRegistry     | config.json 설정값 저장 |
| PlayerDataRegistry | 실시간 플레이어 데이터 저장    |

레지스트리는 안전한 Getter/Setter를 제공해 NPE를 방지한다.

---

## **3.4 이벤트 디스패치 구조**

마인크래프트 이벤트가 발생하면 이벤트 핸들러가 이를 가로채고,
해당 이벤트가 어떤 스킬과 연관되는지 즉시 조회한다.

조회 후 다음 절차를 결정한다:

* 경험치를 줄 것인가
* 스킬 조건이 충족되는가
* 레벨업이 필요한가
* 보상 지급 여부

이 설계 덕분에 **스킬의 기능은 100% JSON으로 정의 가능**하다.

---

## **3.5 보상 실행 엔진**

보상은 다음 두 조건이 모두 맞아야 실행된다:

1. 플레이어가 특정 레벨을 달성했을 것
2. 그 레벨에 맞는 보상 JSON이 존재할 것

지원하는 보상 유형:

* 아이템 보상
* 권한 지급
* 랜덤 보상
* 여러 아이템 동시 지급
* NBT·인챈트 지원
* 경험치 지급
* (예정) 명령어 기반 보상

보상 엔진은 디버그 설정에 따라 모든 과정 로그를 출력할 수 있다.

---

# --------------------------------------------

# **4. CONFIG STRUCTURE**

# --------------------------------------------

## **4.1 config.json ENGLISH**

The config.json file controls global behavior.
It contains these primary fields:

### **Main Fields**

* **version**: Used internally to verify file compatibility.
* **usePlugin**: Enables or disables the plugin.
* **Debug**: A subsection controlling logging behavior.

### **Debug Object**

| Field             | Description                       |
| ----------------- | --------------------------------- |
| useDebug          | Master switch for all debug logs. |
| logLoadedSkills   | Prints skill loading logs.        |
| logLoadedRewards  | Prints reward loading logs.       |
| logPlayerLevelUp  | Prints level-up events.           |
| logGivenRewards   | Prints reward execution logs.     |
| logPlayerDataLoad | Prints player data load logs.     |

---

## **4.1 config.json 한국어**

config.json은 플러그인의 전체 동작을 제어한다.

### **주요 항목**

* **version**: 파일 버전 확인용 내부 항목.
* **usePlugin**: 플러그인 활성/비활성 제어.
* **Debug**: 디버그 로그 옵션 모음.

### **Debug 객체**

| 항목                | 설명                |
| ----------------- | ----------------- |
| useDebug          | 디버그 전체 스위치        |
| logLoadedSkills   | 스킬 JSON 로드 출력     |
| logLoadedRewards  | 보상 JSON 로드 출력     |
| logPlayerLevelUp  | 레벨업 로그 출력         |
| logGivenRewards   | 보상 지급 로그 출력       |
| logPlayerDataLoad | 플레이어 데이터 로드 로그 출력 |

---

# =========================================================

# **5. SKILL JSON SCHEMA – ENGLISH VERSION (1/4)**

# =========================================================

## **5.1 Overview**

Skill JSON files define how each skill behaves, including:

* Skill name & display name
* Maximum level
* Experience drainage rules
* Event triggers
* Conditions
* Exp rewards per event

The goal is to allow server administrators to create **any RPG skill** with no Java code modification.

---

## **5.2 File Structure**

Each skill JSON inside `/skills/*.json` must follow this structure:

```
{
  "Name": "Farming",
  "DisplayName": "Farming",
  "LevelDrainage": 50,
  "maxLevel": 50,
  "Events": [
    {
      "Name": "WHEAT",
      "EventType": "BLOCK_BREAK",
      "exp": 5,
      "useRandom": false,
      "RandomRange": [1, 5],
      "Conditions": {
        "world": ["world", "world_nether"],
        "biome": ["PLAINS"],
        "requiredPermission": "drewrpg.skill.farming"
      }
    }
  ]
}
```

Each field has strict rules:

### **Name**

* Internal identifier
* Must be unique
* Case-sensitive

### **DisplayName**

* Visible to players
* Can contain color codes if supported by server

### **LevelDrainage**

How much EXP reduces after level-up.
Example: If drainage = 50, then leveling from 1→2 costs 50 EXP.

### **maxLevel**

Absolute limit of skill progression.

---

## **5.3 Events Section**

The `Events` array defines how experience is earned.

### **Event Object Fields**

| Field       | Type       | Required         | Description                                |
| ----------- | ---------- | ---------------- | ------------------------------------------ |
| Name        | String     | Yes              | Name of event condition (block, mob, etc.) |
| EventType   | String     | Yes              | Defines which MC event triggers this       |
| exp         | Integer    | Yes/No           | Required unless useRandom = true           |
| useRandom   | Boolean    | Yes              | If random EXP should be used               |
| RandomRange | [min, max] | Yes if useRandom | Random EXP bounds                          |
| Conditions  | Object     | Optional         | Limits where EXP can be gained             |

---

## **5.4 Conditions**

Conditions restrict whether EXP should be rewarded.

Supported condition keys:

| Condition          | Example                | Meaning                     |
| ------------------ | ---------------------- | --------------------------- |
| world              | ["world"]              | Only works in listed worlds |
| biome              | ["DESERT"]             | Only works in listed biomes |
| requiredPermission | "drewrpg.skill.mining" | Requires permission         |
| requiredTool       | ["IRON_PICKAXE"]       | Only when holding tool      |

All conditions are AND-based (all must be true).

---

## **5.5 Validation Requirements**

Skill JSONs must obey:

1. Must contain required fields
2. No duplicate "Name" values
3. Non-negative EXP values
4. RandomRange: first ≤ second
5. EventType must map to a valid MC event

Plugin will print debug logs if validation fails.

---

# =========================================================

# **5. SKILL JSON SCHEMA – KOREAN VERSION (2/4)**

# =========================================================

## **5.1 개요**

Skill JSON 파일은 각 스킬의 동작 방식을 완전히 정의한다.

포함되는 내용:

* 스킬 이름 / 표시 이름
* 최대 레벨
* 경험치 감소 규칙
* 어떤 이벤트가 경험치를 주는지
* 조건
* 이벤트별 경험치 양

서버 관리자는 Java 코드를 전혀 수정하지 않고
**완전히 새로운 스킬을 추가할 수 있다.**

---

## **5.2 파일 구조**

`/skills/*.json`에 있는 모든 파일은 다음 구조를 따라야 한다:

```
{
  "Name": "Farming",
  "DisplayName": "Farming",
  "LevelDrainage": 50,
  "maxLevel": 50,
  "Events": [
    {
      "Name": "WHEAT",
      "EventType": "BLOCK_BREAK",
      "exp": 5,
      "useRandom": false,
      "RandomRange": [1, 5],
      "Conditions": {
        "world": ["world"],
        "requiredPermission": "drewrpg.skill.farming"
      }
    }
  ]
}
```

### 각 항목 의미

#### **Name**

* 시스템 내부에서 사용하는 고유 이름
* 중복 불가
* 대소문자 구분됨

#### **DisplayName**

* 플레이어에게 보여질 이름
* 서버가 허용하면 색 코드 가능

#### **LevelDrainage**

레벨업 시 소모되는 EXP 양.
예: 50이면 1→2 레벨업에 50 EXP 필요.

#### **maxLevel**

해당 스킬의 최대 달성 레벨.

---

## **5.3 Events 항목**

`Events` 배열에서는 경험치를 얻는 조건을 정의한다.

### 이벤트 객체

| 항목          | 타입   | 필수  | 설명                  |
| ----------- | ---- | --- | ------------------- |
| Name        | 문자열  | 필수  | 이벤트 조건 이름           |
| EventType   | 문자열  | 필수  | 어떤 MC 이벤트인지         |
| exp         | 정수   | 조건부 | useRandom=false면 필수 |
| useRandom   | 불리언  | 필수  | 랜덤 경험치 사용 여부        |
| RandomRange | 배열   | 조건부 | useRandom=true면 필수  |
| Conditions  | 오브젝트 | 선택  | 부여 조건               |

---

## **5.4 Conditions 조건 시스템**

조건은 EXP 지급 여부를 제한한다.

지원되는 조건:

| 조건                 | 예시                     | 의미           |
| ------------------ | ---------------------- | ------------ |
| world              | ["world"]              | 특정 월드에서만 적용  |
| biome              | ["FOREST"]             | 특정 바이옴에서만 적용 |
| requiredPermission | "drewrpg.skill.mining" | 특정 권한 필요     |
| requiredTool       | ["IRON_PICKAXE"]       | 특정 도구 사용 시만  |

모든 조건은 AND 조건이다.
즉, **모두 만족해야 EXP 지급됨.**

---

## **5.5 검증 규칙**

JSON 파일은 반드시 다음 규칙을 따라야 한다:

1. 필수 항목 모두 포함
2. 중복 Name 불가
3. EXP 값은 음수 불가
4. RandomRange[0] ≤ RandomRange[1]
5. EventType이 실제 이벤트여야 함

검증 실패 시 디버그 모드에서 오류 출력된다.

---

# =========================================================

# **5. SKILL JSON SCHEMA – ENGLISH VERSION (3/4)**

# =========================================================

## **5.6 EventType Mapping Table**

Every EventType string must map to a real Minecraft event.

| EventType   | Minecraft Event     |
| ----------- | ------------------- |
| BLOCK_BREAK | BlockBreakEvent     |
| BLOCK_PLACE | BlockPlaceEvent     |
| KILL_ENTITY | EntityDeathEvent    |
| FISH        | PlayerFishEvent     |
| CRAFT       | CraftItemEvent      |
| SMELT       | FurnaceExtractEvent |

More will be added in future expansions.

---

## **5.7 EXP Calculation**

If `useRandom = false`:

```
finalEXP = exp
```

If `useRandom = true`:

```
finalEXP = random(RandomRange[0], RandomRange[1])
```

After determining EXP:

```
playerEXP += finalEXP
```

If player EXP meets or exceeds required EXP for next level:
Level increases, rewards triggered, EXP drained by LevelDrainage.

---

## **5.8 Recommended Skill Designs**

Examples:

### **Mining Skill**

* BLOCK_BREAK
* Conditions: requiredTool = pickaxes
* exp: based on ore value

### **Combat Skill**

* KILL_ENTITY
* exp: based on mob difficulty

### **Farming Skill**

* BLOCK_BREAK crops
* world restrictions optional

### **Fishing Skill**

* FISH event
* useRandom recommended due to variability

---

# =========================================================

# **5. SKILL JSON SCHEMA – KOREAN VERSION (4/4)**

# =========================================================

## **5.6 EventType 매핑 테이블**

모든 EventType은 실제 마인크래프트 이벤트와 연결된다.

| EventType   | 실제 이벤트              |
| ----------- | ------------------- |
| BLOCK_BREAK | BlockBreakEvent     |
| BLOCK_PLACE | BlockPlaceEvent     |
| KILL_ENTITY | EntityDeathEvent    |
| FISH        | PlayerFishEvent     |
| CRAFT       | CraftItemEvent      |
| SMELT       | FurnaceExtractEvent |

추후 확장 가능.

---

## **5.7 경험치 계산 방식**

### useRandom = false

```
finalEXP = exp
```

### useRandom = true

```
finalEXP = RandomRange[0] ~ RandomRange[1] 랜덤 값
```

그 후:

```
플레이어 경험치 += finalEXP
```

필요 경험치를 만족하면 레벨업 발생:

* 레벨 증가
* 보상 지급
* LevelDrainage만큼 EXP 차감

---

## **5.8 스킬 설계 예시**

### **광질(Mining)**

* BLOCK_BREAK
* 조건: 곡괭이 필요
* 광물 가치에 따라 exp 조정

### **전투(Combat)**

* KILL_ENTITY
* 몹 난이도에 따른 exp

### **농사(Farming)**

* 작물 BLOCK_BREAK
* 월드/바이옴 조건 가능

### **낚시(Fishing)**

* FISH event
* 랜덤 exp 권장

---

# =========================================================

# **6. REWARD JSON SCHEMA – ENGLISH VERSION (1/4)**

# =========================================================

## **6.1 Overview**

Reward JSON files define what players receive when leveling up specific skills.
All reward logic is fully data-driven, meaning server owners can:

* Add rewards
* Remove rewards
* Modify reward behavior
* Create random reward sets
* Control permissions
* Give items with NBT
* Give commands instead of items
* Display custom messages
* Trigger particle/sound effects (future extension reserved)

No Java modification is needed — the plugin loads all reward sets directly from `/rewards/*.json`.

---

## **6.2 File Structure Overview**

A typical reward JSON looks like this:

```
{
  "Name": "Mining",
  "displayName": "Mining",
  "1": [
    {
      "useRandom": false,
      "Permissions": null,
      "items": [
        {
          "itemName": "COAL",
          "amount": 10,
          "nbt": null,
          "enchant": [],
          "exp": 0
        }
      ]
    }
  ],

  "5": [
    {
      "useRandom": true,
      "Permissions": "drewrpg.vip",
      "RandomCount": 1,
      "items": [
        {
          "itemName": "IRON_ORE",
          "amount": 3,
          "nbt": null,
          "enchant": [],
          "exp": 0
        },
        {
          "itemName": "GOLD_ORE",
          "amount": 2,
          "nbt": null,
          "enchant": [],
          "exp": 0
        }
      ]
    }
  ]
}
```

The top-level keys represent **skill levels** (e.g., `"1"`, `"5"`, `"47"`).
Each key maps to an array of reward groups, because a level may grant multiple different reward packages.

---

## **6.3 Required Top-Level Fields**

### **Name**

* Internal skill identifier
* Must match the corresponding skill JSON’s `Name`

### **displayName**

* Displayed when printing debug reward logs
* Optional but recommended

### **Level Keys (Example: “1”, “5”, “12”)**

* Each represents a specific level
* Value must be **an array of reward objects**
* Level numbers must be integers expressed as strings

---

## **6.4 Reward Object Structure**

Each level can have multiple independent reward blocks.

A reward block supports the following fields:

| Field       | Type           | Required                        | Description                           |
| ----------- | -------------- | ------------------------------- | ------------------------------------- |
| useRandom   | Boolean        | Yes                             | Whether to select rewards randomly    |
| Permissions | String or null | No                              | Requires permission to receive reward |
| RandomCount | Integer        | Required only if useRandom=true | How many random items to select       |
| items       | Array          | Yes                             | List of items to give                 |
| commands    | Array          | Optional                        | Server commands executed              |
| message     | String         | Optional                        | Message sent to player                |

**Items and commands can be mixed**, allowing very flexible reward patterns.

---

## **6.5 Item Object Specification**

### **itemName**

* Must be a valid Bukkit/Spigot material
* Case-insensitive during loading but normalized internally
* Example: `"DIAMOND_SWORD"`

### **amount**

* Quantity of item
* Must be positive integer

### **nbt**

Optional NBT data in serialized JSON string form.
Example:

```
"{\"display\":{\"Name\":\"{\\\"text\\\":\\\"Strong Pickaxe\\\"}\"}}"
```

### **enchant**

Array of enchantment objects:

```
[
  {
    "type": "DAMAGE_ALL",
    "level": 3
  }
]
```

### **exp**

Additional RPG EXP (not vanilla Minecraft EXP).
This EXP is applied **after** rewards are granted.

---

## **6.6 useRandom Behavior**

When `useRandom = false`
→ All items are granted.

When `useRandom = true`
→ Plugin selects N items randomly from the `items` list based on `RandomCount`.

Example:
If 5 items exist and `RandomCount = 2`,
then 2 random items are selected and given.

Random selection is **no duplication by default** unless items are identical.

---

## **6.7 Permissions**

If a reward block has:

```
"Permissions": "drewrpg.vip"
```

Then:

* Player must have `drewrpg.vip`
* Otherwise this reward block is skipped

IMPORTANT:
If all reward blocks for a level require permissions the player does not have,
the player receives **no reward**.

---

## **6.8 Command Rewards**

A reward block may also give commands:

```
"commands": [
  "give %player% diamond 3",
  "eco give %player% 500"
]
```

`%player%` automatically replaces the player name.

Commands execute with **console-level permission**.

---

## **6.9 Messages**

Optional field:

```
"message": "&aYou received a Mining reward!"
```

If omitted, no message is sent.

---

# =========================================================

# **6. REWARD JSON SCHEMA – KOREAN VERSION (2/4)**

# =========================================================

## **6.1 개요**

Reward JSON 파일은 특정 스킬 레벨업 시 지급되는 보상을 정의한다.
이 시스템은 100% JSON 기반으로 설계되어 있어:

* 보상 추가
* 보상 삭제
* 보상 수정
* 랜덤 보상
* 권한 기반 보상
* NBT 포함 아이템 지급
* 아이템 대신 콘솔 명령 실행
* 플레이어에게 메시지 전송

모두 설정 파일만 수정해도 가능하다.

---

## **6.2 파일 구조 개요**

예시:

```
{
  "Name": "Mining",
  "displayName": "Mining",
  "1": [
    {
      "useRandom": false,
      "Permissions": null,
      "items": [...]
    }
  ],
  "5": [
    {
      "useRandom": true,
      "RandomCount": 1,
      "items": [...]
    }
  ]
}
```

상위 key `"1"`, `"5"` 등은 **레벨 숫자**이며,
각 레벨에는 여러 개의 보상 그룹이 존재할 수 있다.

---

## **6.3 상위 필드 설명**

### **Name**

* 스킬 JSON의 Name과 동일해야 함

### **displayName**

* 디버그용 또는 관리자용 표시 이름

### **레벨 키 (예: “1”, “5”)**

* 문자열 형태의 숫자
* 해당 레벨에서 지급할 보상 목록을 배열 형태로 저장

---

## **6.4 보상 객체 구조**

각 레벨의 배열 안에는 여러 보상 묶음이 들어갈 수 있다.

각 보상 묶음은 다음 항목을 가진다:

| 항목          | 타입             | 필수  | 설명            |
| ----------- | -------------- | --- | ------------- |
| useRandom   | Boolean        | 필수  | 랜덤 보상 사용 여부   |
| Permissions | String 또는 null | 선택  | 해당 권한 필요      |
| RandomCount | Integer        | 조건부 | 랜덤일 때 필요한 개수  |
| items       | Array          | 필수  | 지급할 아이템 목록    |
| commands    | Array          | 선택  | 실행할 명령어 목록    |
| message     | String         | 선택  | 플레이어에게 보낼 메시지 |

`items`와 `commands`는 동시에 존재해도 된다.

---

## **6.5 Item 세부 규격**

### **itemName**

* Bukkit Material과 동일한 이름
* 대소문자 구분 없음

### **amount**

* 지급 수량
* 1 이상 정수

### **nbt**

NBT Json 문자열
예:

```
"{\"display\":{\"Lore\":[\"{\\\"text\\\":\\\"Legendary Item\\\"}\"]}}"
```

### **enchant**

예:

```
[
  {
    "type": "DAMAGE_ALL",
    "level": 5
  }
]
```

### **exp**

플러그인 자체 EXP 보정
레벨업 후 EXP 값을 재조정할 때 사용됨.

---

## **6.6 useRandom 동작 방식**

* false → 모든 아이템 지급
* true → items 배열에서 RandomCount개의 아이템 랜덤 지급

random 선택 기본 규칙:

* 중복 선택 없음
* 동일 아이템은 중복 가능

---

## **6.7 권한 조건**

보상 객체에 권한이 있는 경우:

```
"Permissions": "drewrpg.vip"
```

해당 권한을 가진 플레이어만 해당 보상을 받는다.

권한 부족 시 보상 묶음 전체가 무시됨.

---

## **6.8 명령어 보상**

예시:

```
"commands": [
  "give %player% diamond 10",
  "effect give %player% speed 30 2"
]
```

* `%player%` 자동 치환됨
* 모든 명령은 콘솔 권한으로 실행됨

---

## **6.9 메시지 전송**

보상 지급 후, message가 있으면 전송:

```
"&aYou have received a reward!"
```

---

# =========================================================

# **6. REWARD JSON SCHEMA – ENGLISH VERSION (3/4)**

# =========================================================

Now we document internal logic and validation rules.

---

## **6.10 Internal JSON Loading Logic**

### Step 1 — File Discovery

Plugin loads all files from:

```
/plugins/DrewRPG/Rewards/
```

All `.json` files are processed.

### Step 2 — Parsing

Each JSON is parsed using Gson.

### Step 3 — Skill Name Matching

Reward JSON `Name` must match a skill’s `Name` exactly.

If mismatch → file ignored (error printed in debug).

### Step 4 — Level Key Verification

Every key except:

* "Name"
* "displayName"

is treated as **level key**.

Plugin verifies:

* Key is numeric
* Key ≥ 1
* No negative levels
* No non-numeric strings

### Step 5 — Reward Block Validation

For each reward object:

* useRandom must exist
* items must exist
* RandomCount required if useRandom=true
* enchant objects must contain valid Bukkit enchantment names
* amount > 0
* Commands must be strings

If a validation error occurs →
⚠ block is skipped, plugin continues safely (no crash).

---

## **6.11 Item Building Process (Internal)**

1. Material lookup
2. Create ItemStack
3. Apply amount
4. Apply enchantments
5. Apply NBT (if present)
6. Final item added to inventory

NBT application uses Spigot’s internal `CraftItemStack` conversion.

---

## **6.12 Random Selection Algorithm**

Pseudocode:

```
function getRandomItems(list, count):
    shuffle list
    return list[0:count]
```

Stable and predictable; does not repeat items unless list contains duplicates.

---

## **6.13 Reward Execution Order**

When leveling up:

1. Determine skill
2. Check if reward file contains this level
3. For each reward block:

   * If Permissions exist → check
   * If useRandom → pick random items
   * Give items
   * Execute commands
   * Apply exp bonus
   * Send message

All reward blocks for the level are processed.

---

# =========================================================

# **6. REWARD JSON SCHEMA – KOREAN VERSION (4/4)**

# =========================================================

## **6.10 내부 JSON 로딩 규칙**

### 1단계 — 파일 탐색

플러그인은 다음 디렉토리의 JSON을 모두 읽는다:

```
/plugins/DrewRPG/Rewards/
```

### 2단계 — 파싱(Gson)

모든 JSON은 Gson으로 객체화된다.

### 3단계 — Skill Name 매칭

Reward JSON의 `"Name"`은 skill JSON의 `"Name"`과 동일해야 한다.

일치하지 않으면 해당 파일은 무시되고,
디버그에서 오류 메시지를 출력한다.

### 4단계 — 레벨 키 검증

"Name", "displayName"을 제외한 모든 key는 레벨 숫자로 인식된다.

검증 항목:

* 숫자인지
* 1 이상인지
* 음수가 아닌지
* 문자열로만 구성되었는지

### 5단계 — Reward Block 검증

각 보상 묶음에서:

* useRandom 존재 여부
* items 배열 존재 여부
* RandomCount 조건부
* enchant의 type이 실제 인챈트인지 검증
* amount가 1 이상인지
* commands 항목 문자열인지

오류 발생 시 해당 보상 묶음은 건너뛰고,
플러그인은 **절대 크래시하지 않는다**.

---

## **6.11 아이템 생성 절차 (내부)**

1. Material 이름 검증
2. ItemStack 생성
3. amount 적용
4. enchant 적용
5. NBT 적용
6. 최종 아이템 지급

NBT 적용은 Spigot/CraftBukkit 내부 API 사용.

---

## **6.12 랜덤 보상 선택 알고리즘**

의사코드:

```
function getRandomItems(list, count):
    shuffle list
    return list[0:count]
```

중복 선택 없음 (같은 객체가 여러 개 존재할 때만 중복 가능).

---

## **6.13 보상 실행 순서**

레벨업 시 다음 순서로 동작한다:

1. 해당 스킬 확인
2. 보상 파일에 해당 레벨 존재 여부 확인
3. 보상 묶음들에 대해 반복 실행:

   * 권한 확인
   * 랜덤 여부 처리
   * 아이템 지급
   * 명령어 실행
   * EXP 추가 적용
   * 메시지 전송

해당 레벨의 모든 보상 묶음이 순서대로 실행된다.

---

# **7. Reward File Deep-Dive: Detailed Internal Behavior**

---

# **7. Reward Engine – Internal Logic (EN)**

This chapter provides a **low-level, fully expanded, no-omission description** of how the reward engine processes `rewards/*.json`, how it interacts with skill levels, how rewards are validated, and how the plugin prevents incorrect or malicious configurations.

This section is intentionally exhaustive so that server developers understand precisely:

* How reward data loads
* How each level’s reward block is parsed
* How item rewards are constructed
* How commands and permissions are processed
* How Random Rewards work
* How final delivery to the player happens
* How errors are logged (in Debug mode)

---

## **7.1. Reward Loading Pipeline (EN)**

When the server starts, or when `/drew reload` is executed, the plugin performs the following exact steps:

### **Step 1 — Scan Directory**

```
/plugins/DrewRPG/rewards/
```

* The plugin reads **all `.json` files**.
* Each file name is treated as a *Reward Module*, but the module’s real name is the `"Name"` field inside the file.

Example:

File: `Farming.json`
Inside: `"Name": "Farming"`

If the file name does not match the internal name, **the internal Name field always wins**.

---

### **Step 2 — JSON Structural Validation**

Before any reward entry is accepted, the plugin checks:

| Validation                                         | Description                  |
| -------------------------------------------------- | ---------------------------- |
| Top-level `"Name"` exists                          | Without it → file is skipped |
| Level keys are numeric                             | `"1"`, `"2"`, `"15"` etc.    |
| Each level key contains **array of reward blocks** | Must be `[]`                 |
| Each reward block must be an object                | Must contain valid keys      |

---

### **Step 3 — Add to Global Registry**

Once validated, the entire JSON object is stored in a memory map:

```java
Map<String, JsonObject> rewardData
```

Where key = Skill name.

If two files attempt to register the same `"Name"`:

* The **last loaded file** overrides the first.
* Debug Mode logs a warning.

---

## **7.2. Reward Selection Logic (EN)**

When a player performs an action and levels up:

```
giveReward(player, skillName, newLevel)
```

This method begins an exact, multi-stage process:

### **Step 1: Locate the Reward File**

Checks if:

```
rewardData.contains(skillName)
```

If false → no reward for this skill.

---

### **Step 2: Locate Level Entry**

The plugin checks if the JSON contains:

```
json.get("newLevel")
```

If not found → level has **no reward** (intentional or missing).

---

### **Step 3: Iterate Reward Blocks**

Each block inside the level’s array is processed:

Example:

```json
"5": [
  { block1 },
  { block2 },
  { block3 }
]
```

Processing order:

1. block1
2. block2
3. block3

This allows:

* Multiple item reward sets
* Additional permissions
* Additional commands
* Random reward groups
* Mixed combinations

**No limits exist** on how many blocks a level may have.

---

## **7.3. Reward Block Structure (EN)**

Each reward block may contain these fields:

| Field         | Type          | Meaning                       |
| ------------- | ------------- | ----------------------------- |
| `useRandom`   | boolean       | Enables random selection mode |
| `Permissions` | array or null | Grants permissions            |
| `items`       | array         | Items to give                 |
| `commands`    | array         | Commands to execute           |
| `message`     | string        | Player message                |

All fields are optional **except `items` when useRandom=false**.

---

## **7.4. Random Reward Processing (EN)**

If `"useRandom": true`:

* The plugin will randomly choose **ONE** entry inside `items`.
* The chosen index uses uniform distribution unless we introduce weighting later.

Example Random Block:

```json
{
  "useRandom": true,
  "items": [
    { "itemName": "DIAMOND", "amount": 1 },
    { "itemName": "IRON_INGOT", "amount": 10 },
    { "itemName": "EMERALD", "amount": 3 }
  ]
}
```

Player will receive only **1 of the 3**.

---

## **7.5. Non-Random Reward Processing (EN)**

If `"useRandom": false`:

All items in the `items` list are given:

Example:

```json
"items": [
    { "itemName": "CARROT", "amount": 20 },
    { "itemName": "BONE_MEAL", "amount": 5 }
]
```

Player receives both rewards.

---

## **7.6. Permission Granting (EN)**

If the block contains:

```json
"Permissions": ["myplugin.perk.1", "myplugin.perk.2"]
```

Then:

* Plugin checks if permission is valid format
* Applies permanent permission using Bukkit’s `Attachment`
* Debug logs:

```
[Debug] Granted permission myplugin.perk.1 to player
```

If Permissions is `null` → Skip.

---

## **7.7. Command Execution (EN)**

Commands run **as console**:

```json
"commands": [
  "say {player} reached level {level}",
  "eco give {player} 100"
]
```

Placeholders:

| Placeholder | Meaning      |
| ----------- | ------------ |
| `{player}`  | Player Name  |
| `{uuid}`    | Player UUID  |
| `{skill}`   | Skill Name   |
| `{level}`   | Level Number |

---

## **7.8. NBT + Enchant Handling (EN)**

Item generation obeys:

* `itemName` → must be valid Bukkit Material
* `amount` → int
* `nbt` → currently stored but not modified
* `enchant` → array of enchantments

Example:

```json
"enchant": [
  { "enchant": "DAMAGE_ALL", "level": 3 },
  { "enchant": "UNBREAKING", "level": 2 }
]
```

Plugin checks:

* Enchant exists
* Level is allowed
* If enchant fails → logged

---

# **7. Reward Engine – 내부 동작 (KR)**

---

# **7.1. 보상 로딩 파이프라인 (KR)**

서버 시작 or `/drew reload` 시:

1. `/rewards/` 폴더 전체 스캔
2. JSON 구조 체크
3. `"Name"` 기준으로 Global Registry에 등록
4. 중복 시 마지막 파일이 덮어씀
5. Debug 모드일 경우 모든 단계 기록

---

# **7.2. 레벨 보상 처리 흐름 (KR)**

플레이어가 레벨업 할 때마다:

```
giveReward(player, skillName, newLevel)
```

1. 스킬 이름 존재 여부 확인
2. 해당 레벨의 보상 블록 조회
3. 배열 내부 블록들을 순차 처리
4. Random 처리 여부 확인
5. 아이템/명령어/퍼미션 지급

---

# **7.3. Reward Block 구성 요소 (KR)**

| 키             | 의미       |
| ------------- | -------- |
| `useRandom`   | 랜덤 모드 여부 |
| `Permissions` | 퍼미션 부여   |
| `items`       | 아이템 리스트  |
| `commands`    | 명령어      |
| `message`     | 플레이어 메시지 |

---

# **7.4. 랜덤 보상 처리 (KR)**

`useRandom = true` → items 배열 중 **하나만 선택**

공정한 균등 확률로 작동.

---

# **7.5. 일반 보상 처리 (KR)**

`useRandom = false` → items 배열 **전부 지급**

---

# **7.6. 퍼미션 지급 (KR)**

문자열 형태가 올바르면 Bukkit Attachment 이용해 영구 지급.

---

# **7.7. 명령어 실행 (KR)**

콘솔 기준으로 실행.
플레이스홀더 `{player}`, `{skill}`, `{level}` 자동 치환.

---

# **7.8. 인챈트 / NBT 처리 (KR)**

아이템 생성 시:

* Material 존재 체크
* amount 체크
* enchant 존재 여부 확인 후 적용
* nbt는 string 형태로 저장만 지원

---

# **8. Debug System – Full Technical Breakdown (EN + KR)**

DrewRPG의 Debug 시스템은 단순히 “로그 출력 여부”를 조절하는 기능이 아니라,
플러그인의 모든 핵심 처리 단계를 추적 가능하도록 설계된 **세부 분석 도구**이다.

---

# **8.1. Debug Overview (EN)**

The Debug subsystem is controlled entirely through:

```
config.json → "Debug"
```

Available debug toggles:

| Key                | Type    | Default | Description                                   |
| ------------------ | ------- | ------- | --------------------------------------------- |
| `useDebug`         | boolean | false   | Master switch for all debug logging           |
| `logLoadedSkills`  | boolean | true    | Logs loaded skills/*.json                     |
| `logLoadedRewards` | boolean | true    | Logs loaded rewards/*.json                    |
| `logPlayerLevelUp` | boolean | true    | Logs every level-up event                     |
| `logExpGain`       | boolean | true    | Logs exp gain per event                       |
| `logEventTrigger`  | boolean | true    | Logs every event detection (break/place/kill) |

If `useDebug=false`, all other flags become **disabled** automatically.

Debug output always uses:

```
[Debug][DrewRPG]
```

as prefix for easy grepping and log filtering.

---

# **8.2. Debug System Behavior (EN)**

### **When Skill Files Load**

If `logLoadedSkills=true`:

```
[Debug][DrewRPG] Loaded skill file: Farming.json (Events: 12)
[Debug][DrewRPG] Parsed skill: Farming → MaxLevel: 50
```

### **When Reward Files Load**

If `logLoadedRewards=true`:

```
[Debug][DrewRPG] Loaded reward file: Farming.json (Levels: 1→50)
```

### **When Player Gains EXP**

```
[Debug][DrewRPG] Player Drew gained 7 EXP in Mining (Total: 52/100)
```

### **When Level Up Occurs**

```
[Debug][DrewRPG] Drew leveled up: Mining → Lvl 12
```

### **When Rewards Are Issued**

```
[Debug][DrewRPG] Reward block #1 executed for level 12
[Debug][DrewRPG] Given item: IRON_INGOT x10
```

### **When Random Rewards Trigger**

```
[Debug][DrewRPG] Random reward selected: DIAMOND x1 (index=0)
```

---

# **8.3. Debug Flags – Detailed Explanation (EN)**

### **1) useDebug**

Absolute master toggle.
When false:

* No debug logs are produced anywhere.
* Debugging code paths are skipped (performance gain).

### **2) logLoadedSkills**

Prints:

* File name
* Event count
* Parsed JSON Keys
* Invalid features if detected

Useful for identifying malformed skill definitions.

### **3) logLoadedRewards**

Prints:

* Level count
* Reward block count
* Warnings for missing levels

### **4) logPlayerLevelUp**

Logs the **before/after** values:

```
Level 11 → 12 (Exp overflow: 152)
```

### **5) logExpGain**

Shows precise Exp origins:

```
Source: STONE_BREAK → +3 EXP
```

### **6) logEventTrigger**

Shows the event name and raw Bukkit data.

```
Triggered Event: BLOCK_BREAK → Material: COAL_ORE
```

---

# **8.4. Debug System (KR)**

DrewRPG의 Debug 시스템은 단순 로그가 아니라, **레벨업 엔진 전 과정 추적을 위한 분석 도구**이다.

### 지원 플래그:

| 키                | 설명               |
| ---------------- | ---------------- |
| useDebug         | 전체 디버그 마스터 스위치   |
| logLoadedSkills  | 스킬 JSON 로딩 상황 출력 |
| logLoadedRewards | 보상 JSON 로딩 상황 출력 |
| logPlayerLevelUp | 플레이어 레벨업 출력      |
| logExpGain       | 경험치 증가 상황 출력     |
| logEventTrigger  | 이벤트 발생 순간 출력     |

---

# **8.5. Debug 작동 방식 (KR)**

### **스킬 로딩 시**

```
[Debug] 스킬 파일 Farming.json 로드 (이벤트 12개)
```

### **보상 로딩 시**

```
[Debug] 보상 파일 Mining.json 로드 (레벨 1~50)
```

### **경험치 획득 시**

```
[Debug] 플레이어 Drew: Mining EXP +7 (52/100)
```

### **레벨업 시**

```
[Debug] Drew Mining 11 → 12 레벨업
```

### **보상 지급 시**

```
[Debug] 레벨 12 보상 블록 #1 처리됨
```

### **랜덤 보상 시**

```
[Debug] 랜덤 선택: DIAMOND x1
```

---

# **8.6. Debug 구조 설계 철학 (EN + KR)**

### **EN**

The Debug engine is designed for developers, not players.
It gives deep insight into:

* File parsing
* Event detection
* Reward delivery
* Exp calculation
* Level scaling

### **KR**

Debug는 개발자 전용이며, 실제 운영 중 발생하는 **모든 내부 처리 과정을 추적**하기 위해 설계되었다.

---

# **9. loadAllJsonData – Complete Internal Dissection (EN + KR)**

다음 9번 챕터는 플러그인의 가장 중요한 핵심 함수
**loadAllJsonData()**
를 상세 기술한다.

너가 요청한 문서의 핵심 파트 중 하나이므로,
아래 내용은 실제 Java 기반 플러그인의 **로딩 과정 전체를 1도 생략 없이** 단계별로 설명한다.

---

# **9.1. Overview (EN)**

`loadAllJsonData()` is the function responsible for:

1. Directory scanning
2. File reading
3. JSON parsing
4. Internal registry construction
5. Skill–Reward linking
6. Debug logging
7. Error capturing

This is considered the **bootstrap stage** of DrewRPG.

If this function fails → no skills or rewards load.

---

# **9.2. Full Step List (EN)**

### **Step 1 — Ensure Directory Exists**

Plugin checks these 2 paths:

```
/skills/
/rewards/
```

If missing → automatically generated.

### **Step 2 — List All JSON Files**

* Only `.json` files accepted
* Other extensions ignored

### **Step 3 — Read File Contents**

Reads UTF-8 text.

### **Step 4 — JsonParser.parseString()**

The raw JSON string is converted into Gson structures:

* JsonObject
* JsonArray
* JsonElement

### **Step 5 — Validation Phase**

Example validations:

| Rule                  | Failure Result        |
| --------------------- | --------------------- |
| must contain `"Name"` | file skipped          |
| numeric levels only   | warning logged        |
| events must be arrays | file skipped          |
| items must be objects | invalid block skipped |

### **Step 6 — Registry Insert**

Updates global storage:

```
skillData.put(name, json)
rewardData.put(name, json)
```

### **Step 7 — Cross Linking**

Skill and reward names matched.

If skill exists but reward missing → allowed
If reward exists but skill missing → warning logged

### **Step 8 — Debug Summary Output**

If debug enabled:

```
[Debug] Loaded 7 skills
[Debug] Loaded 7 reward tables
[Debug] Bootstrap complete: 0 errors, 12 warnings
```

---

# **9.3. loadAllJsonData (KR)**

이 함수는 DrewRPG의 “데이터 엔진 기동 장치”이며, 플러그인의 생명줄이다.

### **처리 단계 요약**

1. `/skills`, `/rewards` 폴더 존재 확인
2. JSON 파일 목록 수집
3. 파일 내용 읽기
4. Gson으로 파싱
5. JSON 구조 검증
6. 내부 Registry에 저장
7. 스킬 ↔ 보상 연결
8. Debug 로그 출력

### **문제 발생 시**

* JSON 구조 오류 → 해당 파일만 스킵
* 이벤트 형식 비정상 → 그 이벤트만 스킵
* 아이템 오류 → 해당 reward block만 스킵

플러그인은 **절대 전체 작동을 멈추지 않는다**.
오류는 개별 단위로 격리해 운영 안정성을 확보한다.

---

# **10.1. Event Handling Overview (EN)**

The Event Handling Engine is responsible for:

1. **Detecting Bukkit/Spigot/Paper events**
2. **Matching events to skill definitions (skills/*.json)**
3. **Executing EXP gain rules**
4. **Applying randomization (if useRandom = true)**
5. **Triggering Level Up Calculation**
6. **Triggering Reward Evaluation**
7. **Debug logging for each step (if enabled)**

This system allows DrewRPG to act like a modular RPG framework where every Minecraft action can become a skill-based EXP source.

---

# **10.2. Event Detection Pipeline (EN)**

DrewRPG listens to multiple event categories:

| Category         | Bukkit Event                            | Example         |
| ---------------- | --------------------------------------- | --------------- |
| Block actions    | BlockBreakEvent                         | Mining ore      |
| Entity actions   | EntityDamageByEntityEvent               | Combat          |
| Interactions     | PlayerInteractEvent                     | Farming/Custom  |
| Inventory events | CraftItemEvent                          | Crafting skills |
| Fishing          | PlayerFishEvent                         | Fishing         |
| Misc actions     | PlayerMoveEvent, PlayerShearEntityEvent | Optional skills |

You decide which events matter by defining them in your skill JSON.

---

# **10.3. How Events Are Linked to Skills (EN)**

Example (Mining.json):

```json
{
  "Name": "Mining",
  "Events": [
    {
      "Name": "COAL_ORE",
      "Exp": 3
    },
    {
      "Name": "IRON_ORE",
      "Exp": 6
    }
  ]
}
```

When BlockBreakEvent occurs:

1. Check block type
2. Compare with all `Events[].Name` from skill files
3. If matched → award Exp defined in `Exp`

Matching is literal:

```
Material name == Event.Name
```

Case-sensitive.

---

# **10.4. EXP Processing Logic (EN)**

When an event is matched:

### **Step 1 — Determine Exp Amount**

Two modes:

## **A. Normal Mode (useRandom = false)**

Exp is fixed:

```
Exp = eventBlock.Exp
```

## **B. Random Mode (useRandom = true)**

Exp is chosen from:

```
minExp ≤ Exp ≤ maxExp
```

### **Step 2 — Add Exp to Player**

```
currentExp += Exp
```

### **Step 3 — Trigger Level-Up Check**

```
while currentExp ≥ requiredExp:
    level += 1
    currentExp -= requiredExp
```

### **Step 4 — Reward Handler is executed**

Reward JSON for the new level is processed.

---

# **10.5. Example Event Processing Log (EN)**

If Debug enabled:

```
[Debug][Event] BLOCK_BREAK event triggered by Drew
[Debug][SkillMatch] COAL_ORE matches skill Mining
[Debug][ExpGain] Drew gained +3 EXP (Mining: 15/100)
[Debug][LevelCheck] Level up triggered → 1 → 2
[Debug][Reward] Executing reward set for level 2 (Mining.json)
```

---

# **10.6. Full KR Version – 이벤트 처리 엔진 설명**

# **10.6.1. 이벤트 처리 개요 (KR)**

이벤트 처리 엔진은 다음을 담당한다:

1. Bukkit/Paper 이벤트 감지
2. 이벤트를 스킬 JSON 규칙과 매칭
3. 경험치 지급
4. 랜덤 경험치 적용
5. 레벨업 계산
6. 보상 지급
7. 디버그 출력

즉, **플레이어의 모든 행동 → 경험치 시스템으로 연결되는 핵심 구조**이다.

---

# **10.6.2. DrewRPG가 감지하는 주요 이벤트 (KR)**

| 카테고리 | 이벤트                       | 예시       |
| ---- | ------------------------- | -------- |
| 블록   | BlockBreakEvent           | 광물 캐기    |
| 전투   | EntityDamageByEntityEvent | 몬스터 공격   |
| 상호작용 | PlayerInteractEvent       | 농사/도구 사용 |
| 제작   | CraftItemEvent            | 도구 제작    |
| 낚시   | PlayerFishEvent           | 고기 잡기    |
| 기타   | PlayerMoveEvent 등         | 선택적 기능   |

모든 이벤트는 JSON에 정의된 “항목 이름”과 일치해야 EXP가 지급된다.

---

# **10.6.3. 스킬과 이벤트 매칭 방식 (KR)**

예시(Mining.json):

```json
{
  "Name": "Mining",
  "Events": [
    { "Name": "COAL_ORE", "Exp": 3 },
    { "Name": "IRON_ORE", "Exp": 6 }
  ]
}
```

플레이어가 블록을 부수면:

1. 부순 블록의 Material 이름 확인
2. JSON의 Events[].Name과 문자열 비교
3. 같으면 EXP 지급

문자열은 대소문자까지 정확히 일치해야 한다.

---

# **10.6.4. 경험치 처리 절차 (KR)**

### **① Exp 결정**

* `useRandom=false`: EXP 고정
* `useRandom=true`: min~max 범위 내 랜덤

### **② Exp 증가**

```
현재 Exp += 지급 Exp
```

### **③ 레벨업 검사**

```
현재 Exp ≥ 필요 Exp → 레벨업 반복
```

### **④ 보상 지급 시스템 호출**

---

# **10.6.5. 실제 디버그 출력 예시 (KR)**

```
[Debug] BLOCK_BREAK 감지됨 (플레이어: Drew)
[Debug] COAL_ORE → Mining 스킬 이벤트 매칭
[Debug] 경험치 +3 (Mining: 15/100)
[Debug] 레벨업 발생: 1 → 2
[Debug] 보상 처리 시작 (레벨 2)
```

---

# **10.7. Event Engine Safety & Protection (EN + KR)**

### **EN**

The event engine never allows:

* Image-based exploits
* Packet spoofing exploits
* Invalid event types
* Null pointers
* Duplicate reward execution

All checks include **try/catch isolation** so one malformed JSON cannot crash the entire event system.

### **KR**

이벤트 엔진은 다음을 **절대 허용하지 않는다**:

* 비정상 이벤트 실행
* JSON 오류로 전체 시스템 중단
* NullPointerException
* 보상 중복 지급
* 잘못된 Material 이름 처리

모든 처리 단계는 try/catch로 분리되어 있다.

---

# **10.8. Why DrewRPG Event Engine Is Unique (EN + KR)**

### **EN**

The event engine is fully modular:

* No hard-coded skill names
* No hard-coded blocks
* No hard-coded rewards

Everything is data-driven from JSON.

### **KR**

DrewRPG 이벤트 엔진은 완전히 모듈형이다:

* 스킬 이름 하드코딩 없음
* 블록 이름 하드코딩 없음
* 보상 하드코딩 없음

모든 것은 JSON 데이터로 구성된다.

---

# **11.1. Overview / 개요**

---

## **11.1.1 Overview (EN)**

The Server Optimization Guide describes how to achieve maximum performance, stability, and responsiveness when running the **DrewRPG RPG System** on a Minecraft server. Because DrewRPG uses a data-driven architecture, real-time event analysis, JSON parsing, caching, asynchronous data saving, and optional debug pipelines, careful tuning is required to minimize TPS drops or server delays.

This chapter is divided into multiple detailed sections, including hardware considerations, Paper/Purpur configuration, DrewRPG internal execution flow, optimization techniques, caching strategy, recommended async scheduling, debugging impact, and large-scale deployment models.

---

## **11.1.1 개요 (KR)**

서버 최적화 가이드는 Minecraft 서버에서 **DrewRPG RPG 시스템**을 사용할 때
최대 성능·최대 안정성·최고의 반응성을 달성하는 방법을 설명한다.
DrewRPG는 데이터 기반 구조, 실시간 이벤트 분석, JSON 처리, 캐싱, 비동기 저장, 선택적 디버그 출력 등을 사용하므로
TPS 하락, 지연, CPU 부하를 최소화하려면 반드시 튜닝이 필요하다.

이 챕터는 하드웨어 조건, Paper/Purpur 설정, DrewRPG 내부 실행 흐름,
최적화 기법, 캐싱 전략, 추천 비동기 처리, 디버깅으로 인한 성능 영향,
대규모 서버 운영 모델 등을 상세히 다룬다.

---

# **11.2. Optimization Priorities / 최적화 우선순위**

---

## **11.2.1 Priorities (EN)**

DrewRPG optimizes around four primary constraints:

1. **CPU Stability** – Event-heavy environments cause exponential CPU load
2. **Disk I/O Reduction** – JSON read/write must be avoided during gameplay
3. **Memory Efficiency** – Skill & Reward maps must remain cached
4. **Thread Safety & Async Operations** – Prevent main-thread delays during save operations

Each subsystem has been carefully engineered to operate efficiently under high-load circumstances. Understanding these priorities helps server owners configure their environment correctly.

---

## **11.2.1 최적화 우선순위 (KR)**

DrewRPG는 다음 네 가지 주요 제약을 중심으로 최적화된다:

1. **CPU 안정성** – 이벤트가 많은 환경에서는 CPU 부하가 기하급수적으로 증가
2. **디스크 I/O 최소화** – 게임 플레이 중 JSON 읽기/쓰기 금지
3. **메모리 효율성** – 스킬 및 보상 데이터는 항상 캐싱 유지
4. **스레드 안전성과 비동기 처리** – 저장 작업이 메인 스레드를 지연시키지 않도록 설계

각 서브 시스템은 고부하 상황에서도 안정적으로 작동하도록 세심하게 설계되었다.

---

# **11.3. Recommended Hardware / 권장 하드웨어**

---

## **11.3.1 Recommended Hardware (EN)**

### **CPU**

* High single-core performance
* 4.6–5.4 GHz recommended
* Prefer Intel 12700K/13700K or AMD 7800X3D+

### **RAM**

* Minimum: 6–8GB for a Paper server
* DrewRPG itself uses ~120–300MB depending on player load
* Avoid memory overallocation

### **Disk**

* SSD (NVMe preferred)
* Random I/O should remain < 1ms
* JSON saving will benefit significantly from NVMe performance

---

## **11.3.1 권장 하드웨어 (KR)**

### **CPU**

* 강력한 단일 코어 성능
* 4.6~5.4 GHz 권장
* Intel 12700K/13700K 또는 AMD 7800X3D+ 추천

### **RAM**

* Paper 서버 기준 최소 6~8GB
* DrewRPG 자체는 약 120~300MB 사용 (유저 수에 따라 증가)
* 메모리 과다 할당은 오히려 성능 저하

### **디스크**

* SSD 또는 NVMe 필수
* 랜덤 I/O는 1ms 이하 유지
* JSON 저장 구조상 NVMe는 큰 성능 향상 제공

---

# **11.4. Paper/Purpur Configuration / Paper & Purpur 설정**

---

## **11.4.1 Essential Paper Settings (EN)**

| Config                          | Value | Purpose                                      |
| ------------------------------- | ----- | -------------------------------------------- |
| optimize-explosions             | true  | Reduces per-tick explosion cost              |
| use-faster-eigencraft-redstone  | true  | Stabilizes CPU during redstone ticking       |
| max-joins-per-tick              | 3–5   | Prevents login spike when loading PlayerData |
| load-chunks-for-packet-handling | false | Less chunk loading when players join         |

---

## **11.4.1 필수 Paper 설정 (KR)**

| 설정                              | 값     | 목적                          |
| ------------------------------- | ----- | --------------------------- |
| optimize-explosions             | true  | 폭발 처리의 서버 부하 감소             |
| use-faster-eigencraft-redstone  | true  | 레드스톤 틱 CPU 안정화              |
| max-joins-per-tick              | 3–5   | PlayerData 로딩 시 로그인 스파이크 방지 |
| load-chunks-for-packet-handling | false | 접속 시 불필요한 청크 로딩 방지          |

---

# **11.5. DrewRPG Internal Execution Flow / DrewRPG 내부 실행 구조**

---

## **11.5.1 Internal Flow (EN)**

The internal flow of DrewRPG is:

```
[Event Trigger]
      ↓
[Skill Matching]
      ↓
[EXP Calculation]
      ↓
[Level-Up Engine]
      ↓
[Reward Evaluation]
      ↓
[Debug System]
      ↓
[Async PlayerData Save]
```

Each step is isolated to prevent one subsystem from blocking another.

---

## **11.5.1 내부 실행 구조 (KR)**

DrewRPG 내부 실행 흐름은 다음과 같다:

```
[이벤트 발생]
      ↓
[스킬 매칭]
      ↓
[경험치 계산]
      ↓
[레벨업 엔진]
      ↓
[보상 평가]
      ↓
[디버그 출력]
      ↓
[비동기 저장]
```

각 단계는 서로를 방해하지 않도록 분리되어 설계되었다.

---

# **11.6. JSON Access & Disk I/O / JSON 접근 및 디스크 I/O**

---

## **11.6.1 JSON I/O Rules (EN)**

DrewRPG enforces strict rules:

1. JSON *never* read during gameplay
2. JSON loaded **one time at startup**
3. PlayerData write operations occur **asynchronously**
4. Disk I/O operations grouped into batch writes

---

## **11.6.1 JSON I/O 규칙 (KR)**

DrewRPG는 다음을 강제한다:

1. 게임 중 JSON 읽기 절대 금지
2. JSON은 서버 시작 시 단 한 번 로딩
3. PlayerData 저장은 항상 비동기 처리
4. 디스크 I/O는 배치 쓰기로 묶어서 처리

---

# **11.7. Memory Caching System / 메모리 캐싱 시스템**

---

## **11.7.1 Caching Overview (EN)**

The following are cached:

* All Skills JSON
* All Rewards JSON
* All PlayerData objects
* Level requirements
* Active debug states

In-memory operations occur through:

```
ConcurrentHashMap<UUID, PlayerData>
HashMap<String, JsonObject> skills
HashMap<String, JsonObject> rewards
```

---

## **11.7.1 캐싱 개요 (KR)**

다음 항목들이 캐싱된다:

* 스킬 JSON 전체
* 보상 JSON 전체
* 플레이어 데이터 전체
* 레벨 요구치
* 디버그 설정

메모리 접근 구조:

```
ConcurrentHashMap<UUID, PlayerData>
HashMap<String, JsonObject> skills
HashMap<String, JsonObject> rewards
```

---

# **11.8. Threading, Async Scheduling / 스레드 & 비동기 처리**

---

## **11.8.1 Async Scheduling (EN)**

DrewRPG uses async threads for:

* PlayerData saving
* Heavy reward calculations
* Scheduled autosave
* Debug export tasks

Avoid doing heavy operations in:

* BlockBreakEvent
* EntityDeathEvent
* Inventory events

These must remain lightweight.

---

## **11.8.1 비동기 스케줄링 (KR)**

DrewRPG는 다음 작업을 비동기로 처리한다:

* PlayerData 저장
* 무거운 보상 계산
* 자동 저장
* 디버그 로그 내보내기

특히 다음 이벤트에서는 절대 무거운 작업 금지:

* BlockBreakEvent
* EntityDeathEvent
* 인벤토리 이벤트

이벤트는 가벼워야 한다.

---

# **11.9. Debug Mode Performance Impact / 디버그 모드 성능 영향**

---

## **11.9.1 Debug Impact (EN)**

Debug logging may cause:

* Large console output
* CPU delays in extreme spam environments
* Disk write increases

However, DrewRPG limits this by:

* Rate-limiting messages
* Async logging
* Conditional debug enabling per module

---

## **11.9.1 디버그 성능 영향 (KR)**

디버그 출력은 다음 영향을 줄 수 있다:

* 콘솔 출력 증가
* 많은 이벤트가 동시에 발생하면 CPU 지연
* 디스크 쓰기 증가

하지만 DrewRPG는 다음 방식으로 제어한다:

* 메시지 레이트 리미터 적용
* 비동기 로깅
* 모듈별 디버그 조건부 활성화

---

# **11.10. Large-Scale Server Deployment / 대규모 서버 운영**

---

## **11.10.1 Large Server Optimization (EN)**

### Recommended structure:

* Multi-instance Paper servers
* Redis-based messaging
* PlayerData sync every 10–20 seconds
* Limit skill event categories for performance

---

## **11.10.1 대규모 서버 최적화 (KR)**

### 추천 구조:

* 멀티 Paper 인스턴스
* Redis 기반 메시징
* PlayerData 10~20초 주기 동기화
* 성능을 위해 이벤트 종류 최소화

---

# **11.11. Best Practices / 권장 운영 방법**

---

## **11.11.1 Best Practices (EN)**

1. Never parse JSON during gameplay
2. Avoid oversized skill definitions
3. Use async for everything except event triggers
4. Turn off debug on production servers
5. Call autosave every 3–5 minutes
6. Run the server on NVMe SSD

---

## **11.11.1 권장 운영 방법 (KR)**

1. 게임 중 JSON 파싱 절대 금지
2. 과도한 스킬 정의 피하기
3. 이벤트 외 모든 것은 비동기 처리
4. 운영 서버에서는 디버그 OFF
5. 3~5분 주기로 autosave
6. NVMe SSD 필수

---
