# This Plugin Isn't Launched! This is Alpha Test Version!
### Use Modrinth! https://modrinth.com/project/drewrpgproject#download
# DrewRPG Level System

**Minecraft Server's Ultimate RPG Leveling System**
**Minecraft 서버의 궁극적인 RPG 레벨링 시스템**

This plugin is a professional RPG skill leveling system designed to provide the highest level of stability, scalability, and ease of debugging for Minecraft servers. All core logic is completely customizable via JSON files, significantly reducing the complexity of server operation.

본 플러그인은 Minecraft 서버에 최고 수준의 안정성, 확장성, 디버깅 편의성을 제공하도록 설계된 전문적인 RPG 스킬 레벨링 시스템입니다. 모든 핵심 로직은 JSON 파일을 통해 완벽하게 커스터마이징 가능하며, 서버 운영의 복잡성을 획기적으로 낮춥니다.

---

## 1. DrewRPG's Competitive Advantages / DrewRPG만의 차별화된 핵심 기능

The DrewRPG Level System focuses on fundamentally solving common problems in existing RPG plugins, such as data errors, balancing difficulty, and maintenance complexity.

DrewRPG Level System은 기존 RPG 플러그인들이 흔히 겪는 데이터 오류, 밸런싱 난이도, 유지보수 복잡성 등의 문제점을 근본적으로 해결하는 데 중점을 두었습니다.

### 1.1. Data Integrity Guarantee: Complete Resolution of Data Inconsistency (Desync) Issues / 데이터 무결성 보장: 데이터 불일치 (Desync) 문제의 완벽한 해결

* **Centralized Cache System (PlayerJsonManager):** All player data is stored in a centralized memory cache. It is loaded upon player login (`loadPlayerJson`) and saved immediately upon logout (`savePlayerJson`), minimizing data loss.
  
    * 중앙 집중식 캐시 시스템 (PlayerJsonManager): 모든 플레이어 데이터는 중앙 집중식 메모리 캐시에 보관되며, 플레이어 접속 시 로드(loadPlayerJson)되고, 접속 종료 시 즉시 저장(savePlayerJson)되어 데이터 유실을 최소화합니다.
      
* **Forced Command-Cache Synchronization (Critical Stability):** To prevent data inconsistency (Desync) after using administrator commands (e.g., `/DRPG setLevel`, `/DRPG addExp`), all data modification logic is forced to go through the central cache and immediately saved to disk after modification. This completely eliminates the possibility of data rollback that can occur upon server reboot.
  
    * 커맨드-캐시 동기화 강제 (Critical Stability): 관리자 명령어(예: `/DRPG setLevel`, `/DRPG addExp`) 사용 후 데이터 불일치(Desync)가 발생하지 않도록, 모든 데이터 수정 로직은 중앙 캐시를 통해서만 이루어지며, 수정 직후 디스크에 즉시 저장하는 로직을 강제하였습니다. 이는 서버 재부팅 시 발생할 수 있는 데이터 롤백 가능성을 완벽하게 차단합니다.
      
* **Asynchronous I/O and Performance Optimization:** Data loading and saving can be processed **asynchronously (Async)** via the `PlayerData` settings in `config.json`, preventing server lag during heavy I/O operations.
  
    * 비동기 I/O 및 성능 최적화: `config.json`의 PlayerData 설정을 통해 데이터 로드와 저장을 **비동기(Async)**로 처리할 수 있어, I/O 작업량이 많을 때 서버 랙이 발생하는 것을 방지합니다.

---

## 2. Dynamic Features and Extensibility / 동적 기능 및 확장성

DrewRPG is designed to be highly flexible and easy to extend through its modular architecture.

DrewRPG는 모듈식 아키텍처를 통해 높은 유연성과 확장 용이성을 갖도록 설계되었습니다.

### 2.1. Skill Logic Customization (EventProcessor) / 스킬 로직 커스터마이징 (EventProcessor)

* **JSON-Defined Events:** Skill EXP gain triggers are defined in `skills/*.json`. For example, EXP can be granted for `BlockBreakEvent`, `EntityDeathEvent`, or `PlayerInteractEvent` and customized with various conditions (e.g., specific block IDs, specific entity types).
  
    * JSON 정의 이벤트: 스킬 경험치 획득 트리거는 `skills/*.json`에 정의됩니다. 예를 들어, `BlockBreakEvent`, `EntityDeathEvent`, `PlayerInteractEvent` 등에 경험치를 부여할 수 있으며, 다양한 조건(예: 특정 블록 ID, 특정 엔티티 종류)으로 커스터마이징됩니다.
      
* **Accurate Event-to-EXP Mapping:** The system ensures that experience gained from in-game events is calculated precisely, level-ups are processed accurately, and defined rewards are dispensed for every level reached.
  
    * 정확한 이벤트-EXP 매핑: 인게임 이벤트에서 얻는 경험치가 정확하게 계산되고, 레벨업이 정확하게 처리되며, 도달한 레벨마다 정의된 보상이 지급되도록 보장합니다.

### 2.2. Reward System Flexibility (RewardProcessor) / 보상 시스템 유연성 (RewardProcessor)

* **Separated Reward Trigger Levels:** Rewards granted upon level-up are managed entirely separately by level (JSON key) and are configured as JSON arrays.
  
    * 분리된 보상 발동 레벨: 레벨업 시 지급되는 보상은 레벨별(JSON 키)로 완전히 분리되어 관리되며 JSON 배열로 구성됩니다.
      
* **Item Customization (NBT Data):** In addition to `itemName` and `amount`, the `nbt` (NBT data) field can be defined, securing the scalability to add custom data, names, and Lore to items.
  
    * 아이템 커스터마이징 (NBT 데이터): `itemName`과 `amount` 외에 `nbt` (NBT 데이터) 필드를 정의할 수 있어, 아이템에 커스텀 데이터, 이름, Lore 등을 추가할 수 있는 확장성을 확보합니다.
      
* **Reward Notification System (RewardNotify):** The `config.json` allows administrators to select and customize the display format (Chat, Actionbar, or Title message) for level-up reward notifications.
  
    * 보상 알림 시스템 (RewardNotify): `config.json`을 통해 관리자는 레벨업 보상 알림의 표시 형식(채팅, 액션바, 또는 타이틀 메시지)을 선택하고 커스터마이징할 수 있습니다.

### 2.3. Server Integration and Operation Support (Integration & Operation) / 서버 통합 및 운영 지원 (Integration & Operation)

* **PlaceholderAPI Support:** The PlaceholderAPI section in `config.json` provides seamless integration with the PlaceholderAPI plugin.
  
    * PlaceholderAPI 지원: `config.json`의 PlaceholderAPI 섹션은 PlaceholderAPI 플러그인과 완벽한 통합을 제공합니다.
      
* **Automatic File Management (FileManager):** Upon first launch, all Skill and Reward JSON files defined in `config.json` are automatically copied from the JAR file to the server folder, providing a ready-to-use environment.
  
    * 자동 파일 관리 (FileManager): 첫 실행 시 `config.json`에 정의된 모든 스킬 및 보상 JSON 파일이 JAR 파일에서 서버 폴더로 자동 복사되어 바로 사용할 수 있는 환경을 제공합니다.
      
* **Version Management (JsonVersionLoader):** The version key in `config.json` is used to execute plugin loading logic based on the version number, ensuring flexibility for future major updates.
  
    * 버전 관리 (JsonVersionLoader): `config.json`의 버전 키는 버전 번호에 따라 플러그인 로딩 로직을 실행하는 데 사용되어, 향후 주요 업데이트에 대한 유연성을 보장합니다.

### 2.4. Administrator Commands (Administrator Commands) / 관리자 명령어 (Administrator Commands)

All commands are accessed via `/DRPG levelSystem` or the alias `/drpg`, and administrator permission is required. Detailed usage is provided in `commands.md`.

모든 명령어는 `/DRPG levelSystem` 또는 별칭인 `/drpg`를 통해 접근할 수 있으며, 관리자 권한이 필요합니다. 상세한 사용법은 `commands.md`에 제공됩니다.

---

Made by drewdrew1_

 * 다중 이벤트 핸들링 (HandlerEvents):
   * BlockBreakEvent (블록 캘 시), EntityDeathEvent (엔티티 죽일 시), PlayerFishEvent (낚시 할 시)
 * 연쇄 레벨업 로직 (checkLevelUp):
   * 획득한 경험치가 여러 레벨을 한 번에 올릴 수 있는 경우, while 루프를 통해 모든 레벨업을 정확하게 처리하고, 각 레벨업마다 정의된 보상을 빠짐없이 지급합니다.

2.2. 보상 시스템의 유연성 (RewardProcessor)
 * 보상 트리거 레벨 분리: 레벨업 시 지급되는 보상을 레벨(JSON의 키)별로 완벽하게 분리하여 관리하며, 보상 목록은 JSON 배열로 구성됩니다.
 * 아이템 커스터마이징:
   * itemName, amount 외에 nbt (NBT 데이터) 필드를 정의할 수 있어, 아이템에 이름, Lore, 기타 커스텀 데이터를 추가할 수 있습니다.
 * 보상 알림 시스템 (RewardNotify):
   * config.json을 통해 레벨업 보상 지급 시 일반 채팅, 액션바, 또는 타이틀 메시지 중 어떤 방식으로 알림을 보낼지 선택하고 그 포맷까지 자유롭게 설정할 수 있습니다.

2.3. 서버 연동 및 운영 지원 (Integration & Operation)
 * PlaceholderAPI 지원:
   * config.json의 PlaceholderAPI 섹션을 통해 PlaceholderAPI 플러그인과 완벽하게 통합됩니다.
 * 파일 자동 관리 (FileManager):
   * 플러그인 최초 실행 시 config.json에 정의된 모든 스킬 및 보상 JSON 파일을 JAR 파일에서 서버 폴더로 자동으로 복사하여, 즉시 사용 가능한 환경을 제공합니다.
 * 버전 관리 (JsonVersionLoader):
   * config.json의 version 키를 읽어 로딩 로직을 버전별로 분기 처리하여, 향후 대규모 업데이트 시에도 설정 파일의 유연성을 확보합니다.

2.4. 관리자 명령어 (Administrator Commands)
모든 명령어는 /DRPG levelSystem 또는 축약어 /drpg를 통해 접근하며, 관리자 권한이 필요합니다.

---------------------------------

Made By drewdrew1_
