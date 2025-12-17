# This Plugin Isn't Launched!

---

# The World's Most Flexible and Secure Minecraft RPG Plugin: "DRPG_LevelSystem"

## 세상에서 가장 유연하고 안전한 마인크래프트 RPG 플러그인 "DRPG_LevelSystem"

---

**This plugin is an RPG Skill Leveling System that provides the highest level of stability, scalability, and debugging convenience for Minecraft servers.**

**이 플러그인은 Minecraft 서버에 최고 수준의 안정성, 확장성, 디버깅 편의성을 제공하는 RPG 스킬 레벨링 시스템이다.**

* All core logic, including skill triggers, experience curves, and rewards, is fully customizable via `.json` files, allowing server operators to design deep, complex RPG content without touching a single line of Java code.
* 모든 핵심 로직(스킬 트리거, 경험치 곡선, 보상 포함)은 `.json` 파일로 완벽히 커스텀마이징 가능하며, 서버 운영자가 Java 코드를 수정하지 않고도 깊고 복잡한 RPG 콘텐츠를 설계할 수 있게 하여 운영의 복잡성을 획기적으로 낮춘다.

---

## 📚 Documentation & Guides / 문서 및 가이드

| 문서 유형 (Document Type) | 파일 이름 (File Name) | 주요 내용 (Key Content) |
| :--- | :--- | :--- |
| **Full Manual** | [`DRPG_levelSystem Full Manual.md`](DRPG_levelSystem%20Full%20Manual.md) | Plugin installation, detailed structure, and core design philosophy. / 플러그인 설치, 상세 구조, 핵심 설계 철학을 포함한 전체 가이드. |
| **Config Guide** | [`Config Manual (KOR).md`](Config%20Manual%20(KOR).md) | Comprehensive, detailed explanation of all options within `config.json`. / `config.json` 내 모든 옵션에 대한 포괄적이고 상세한 설명. |
| **Command Guide** | [`command Manual (KOR).md`](command%20Manual%20(KOR).md) | Usage instructions for both general user and administrator commands. / 일반 사용자 및 관리자 명령어 사용법 안내. |
| **Contributing/Bugs** | [`CONTRIBUTING.md`](CONTRIBUTING.md) | Official bug reporting procedure and code/localization contribution guidelines. / 공식 버그 보고 절차, 코드 및 현지화 기여 방법. |
| **Support/Suggestions** | [`SUPPORT.md`](SUPPORT.md) | Technical support channels and guidelines for feature requests and general inquiries. / 기술 지원 채널, 기능 요청 및 일반 문의 안내. |
| **Security Policy** | [`SECURITY.md`](SECURITY.md) | Policy on reporting and handling security vulnerabilities and exploits. / 보안 취약점 보고 및 처리 절차 정책. |
| **Next Update Plan** | [`aboutNextUpdate.md`](aboutNextUpdate.md) | Information and roadmap for the next major version (V 1.1.0) update. / 다음 주요 버전 (V 1.1.0) 업데이트 계획 및 로드맵. |

---

## 1. Core Features / 핵심 기능

**This plugin fundamentally focuses on solving common problems faced by existing RPG level system plugins, such as data corruption (Desync), balancing difficulty, and intensive maintenance complexity, by prioritizing stability and developer experience.**

**이 플러그인은 기존 RPG 레벨 시스템 플러그인들이 흔히 겪는 데이터 오류(Desync), 밸런싱 난이도, 과도한 유지보수 복잡성 등의 문제점을 안정성과 개발자 경험을 최우선으로 하여 근본적으로 해결하는데 중점을 두었다.**

### 1.1. Data Integrity Assurance: Solving Data Inconsistency Issues

### 1.1. 데이터 무결성 보장: 데이터 불일치 (`Desync`) 문제 해결

* Utilizing a centralized cache system, all player data is consistently stored in the memory cache, and robust loading/saving features minimize data loss, especially during unexpected server shutdowns.

* 중앙 집중식 캐시 시스템을 이용해 모든 플레이어 데이터는 메모리 캐시에 일관성 있게 보관되며, 강력한 불러오기 및 저장 기능으로 예상치 못한 서버 다운 시에도 데이터 유실을 최소화한다.

* The entire database connection (SQL/JSON) and saving logic is processed **asynchronously**, ensuring the server thread remains unblocked and preventing server lag when the Input/Output (I/O) workload is high.

* 전체 데이터베이스 연결(SQL/JSON) 및 저장 로직은 **비동기적**으로 처리되도록 설계되어, I/O 부하가 높을 때도 서버의 메인 스레드를 막지 않아 서버 지연(Lag)을 방지한다.

---

## 2. Dynamic Functionality & Scalability / 동적 기능 및 확장성

**DRPG_levelSystem is explicitly designed for high flexibility and ease of expansion, built upon a modular, data-driven architecture.**

**DRPG_levelSystem은 모듈식 데이터 기반 아키텍처를 기반으로 하여, 높은 유연성과 확장 용이성을 명시적으로 목표하고 설계 되었다.**

### 2.1. Skill Logic Customization via JSON

### 2.1. JSON을 통한 스킬 로직 커스터마이징

* **JSON Defined Events:** All skill experience triggers and growth logic are defined entirely within easily readable JSON files located in `plugins/DRPG/levelSystem/skills/`.

* JSON 정의 이벤트: 모든 스킬 경험치 트리거와 성장 로직은 `plugins/DRPG/levelSystem/skills/`에 위치한 읽기 쉬운 JSON 파일 내에서 완전히 정의된다.

* **Precise Event Mapping:** The system ensures that experience gained from specific in-game events is calculated precisely, level-ups are processed accurately, and predefined rewards are immediately granted upon reaching the required level.

* 정밀한 이벤트 매핑: 인게임 특정 이벤트에서 얻는 경험치가 정확하게 계산되고, 레벨업이 정확하게 처리되며, 도달한 레벨마다 미리 정의된 보상이 즉시 지급되도록 보장한다.

### 2.2. Flexible Reward System

### 2.2. 유연한 보상 시스템

* **Separated Reward Levels:** Rewards granted upon level-up are managed entirely separately by level using a structured JSON array (`rewards/*.json`). This simplifies balancing and maintenance.

* 분리된 보상 발동 레벨: 레벨 업 시 지급되는 보상은 구조화된 JSON 배열(`rewards/*.json`)을 이용해 레벨별로 완전히 분리되어 관리된다. 이는 밸런싱과 유지보수를 간소화한다.

* **Advanced Item Customization (NBT Data):** Extensibility is secured by utilizing the `nbt` field, allowing operators to add custom data, names, lore, and powerful attributes to items defined as rewards.

* 고급 아이템 커스터마이징 기능 (NBT 데이터): `nbt` 필드를 활용하여 보상으로 정의된 아이템에 커스텀 데이터, 이름, 설명(Lore), 강력한 속성을 추가할 수 있는 확장성을 확보하였다.

### 2.3. Server Integration

### 2.3. 서버 통합 및 연동

* **PlaceholderAPI Support:** Supports perfect integration with PlaceholderAPI, allowing levels, experience, and other dynamic data to be displayed in scoreboards, chat, and various UI elements.

* PlaceholderAPI 지원: PlaceholderAPI와의 완벽한 연동을 지원하여, 레벨, 경험치 및 기타 동적 데이터를 스코어보드, 채팅, 다양한 UI 요소에 표시할 수 있다.

* **Permission System Support:** Integrates with leading permission plugins (like LuckPerms) to provide granular control over skill usage and command execution, ensuring only authorized players can access specific features.

* 권한 시스템 지원: 주요 권한 플러그인(예: LuckPerms)과 연동되어 스킬 사용 및 명령어 실행에 대한 세밀한 권한 제어를 제공하며, 권한이 부여된 플레이어만 특정 기능에 접근하도록 보장한다.

---

## 3. Debugging & Management Convenience / 디버깅 및 관리 편의성

* **JSON File Validation & Auto-Correction:** The plugin proactively validates the syntax and structure of `config.json` and all skill/reward definition files. It attempts **automatic correction** for simple errors and reports the source of critical errors in detail.

* JSON 파일 유효성 검사 및 자동 수정: 플러그인은 `config.json` 및 모든 스킬/보상 정의 파일의 구문 및 구조를 사전에 검사한다. 단순한 오류에 대해서는 **자동 수정**을 시도하며, 치명적인 오류 발생 시 그 원인을 상세하게 보고한다.

* **Precise Debugging Logs:** By enabling the `Debug` setting in `config.json`, detailed logs of file loading, parsing, registration, and specific error causes are output, drastically reducing the time required for troubleshooting.

* 정밀한 디버깅 로그: `config.json`의 `Debug` 설정을 활성화하면 파일 로드, 파싱, 등록, 그리고 구체적인 오류 원인에 대한 상세 로그가 출력되어 문제 해결에 필요한 시간을 획기적으로 단축시킨다.

* **Fail-Safe Mode:** Includes a **Safe Mode** feature that, upon encountering an unexpected critical exception, prevents the server from crashing and instead only provides comprehensive warnings and reports to the administrators.

* 페일-세이프 모드: 예상치 못한 치명적인 예외가 발생했을 때 서버 다운을 방지하고, 대신 관리자에게만 포괄적인 경고와 보고서를 제공하는 **안전 모드** 기능을 포함하고 있다.

*  Asynchronous I/O and Performance Optimization:
The `PlayerData` settings in `config.json` allow data loading and saving to be processed **Asynchronously**, preventing server lag when the I/O workload is high.
1.1. 데이터 무결성 보장: 데이터 불일치 (Desync) 문제 해결
1.1. Data Integrity Assurance: Solving Data Inconsistency (Desync) Issues
 * 중앙 집중식 캐시 시스템을 이용해 모든 데이터는 메모리 캐시에 보관되며, 불러오기 및 저장 기능으로 데이터 유실을 최소화한다.
 * Utilizing a centralized cache system, all data is stored in the memory cache, minimizing data loss through dedicated load and save functionalities.
 * 커맨드 - 캐시 동기화 강제: config.json의 설정을 통하여 명령어 사용 후 데이터 불일치 (Desync)가 발생하지 않도록 모든 데이터는 중앙 캐시를 통해서만 이루어지며, 수정 직후 즉시 저장하는 로직으로, 서버 재부팅 시 발생 가능한 데이터 롤백 가능성은 완벽히 차단하였다.
 * Command-Cache Synchronization Enforcement: By setting configurations in config.json, all data operations are strictly routed through the central cache to prevent data inconsistency (Desync) after command usage. The logic ensures immediate saving right after modification, completely blocking the possibility of data rollback during server reboot.
 * 비동기 I/O 및 성능 최적화:
   config.json의 PlayerData 설정을 통해 데이터 로드와 저장을 **비동기 (Async )**로 처리할 수 있어, I/O 작업량이 많을 때 서버 랙이 발생하는 것을 방지한다.
 * Asynchronous I/O and Performance Optimization:
   The PlayerData settings in config.json allow data loading and saving to be processed Asynchronously, preventing server lag when the I/O workload is high.

---

## 2. 동적 기능 및 확장성

**DRPG_levelSystem은 모듈식 아키텍쳐를 이용해 높은 유연성과 확장 용이성을 갖도록 설계 되었다.**

### 2.1 스킬 로직 커스터마이징

* Json 정의 이벤트: 스킬 경험치 트리거는 plugins/DRPG/levelSystem/skills/ 안에 정의한다. (예시)[How To Use/JSON/Skills/Skills Manual (KOR).md]

* ** 정확한 이벤트와 EXP 매핑:
 인게임 이벤트에서 얻는 경험치가 정확하게 계산되고, 레벨업이 정확하게 처리되며, 도달한 레벨마다 정의된 보상이 지급되도록 보장한다.

### 2.2 보상 시스템 유연성

* ** 분리된 보상 발동 레벨:
 레벨 업 시 지급되는 보상은 레벨별 (JSON)으로 완전하게 분리되어 관리되며 JSON배열로 구성된다. (예시) [How To Use/JSON/rewards/Rewards Manual (KOR).md]

* ** 아이템 커스터마이징 기능 (NBT데이터): 
nbt 필드를 이용해 아이템에 커스텀 데이터, 이름, 설명 등을 추가할 수 있는 확장성을 확보하였다. (예시) [How To Use/JSON/rewards/Rewards Manual(KOR).md]

* ** 보상 알림 시스템:
config.json을 이용해 레벨업 보상 알림 표시 형식을 선택하고 커스터마이징 할 수 있다. (예시) [How To Use/JSON/Config/Config Manual (KOR).md]

### 2.3 서버 통합 및 운영 지원

* **PlaceHolderAPI 지원 (1.1.0 버전부터 지원 될 예정)** :
 `config.json`에서 PlaceHolderAPI를 지원하게 할 수 있다.

* **LuckPerms 지원 (1.0.0버전부터 지원 될 예정)** :
 `config.json`에서 LuckPerms 지원하게 할 수 있다.

* **프로그래머가 아닌 운영자를 위한 시스템**:
첫 실행 시 예시 파일을 plugins/DRPG/levelSystem/에 만들어 별다른 코드 수정 없이 바로 사용 가능하게 할 수 있는 환경을 제공한다. (파일은 How To Use/JSON/ 안에 모든 예시 파일들이 들어간다.)

* **버전 괸리 시스템**:
config.json, rewards/\*.json 그리고 skills/\*.json에는 버전들이 있으며 버전을 고정해서 쓸 수 있다. (최신기능은 사용 불가하며 만약 json을 최신버전으로 바꿀 시 jar도 지원하는 버전으로 바꾸어야함.)

### 2.4 관리자 명령어

**모든 명령어는 /DRPG levelSystem ( 혹은 /drpg ls )으로 접근이 가능하며 config.json에서 권한 설정이 가능하다.**(LuckPerms 연동 시) (예시) [How To Use/Commands/Commands Manual (KOR).md]
