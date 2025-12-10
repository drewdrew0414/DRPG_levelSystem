# DrewRPGLevelSystem

본 플러그인은 Minecraft 서버에 최고 수준의 안정성, 확장성, 디버깅 편의성을 제공하도록 설계된 전문적인 RPG 스킬 레벨링 시스템입니다. 모든 핵심 로직은 JSON 파일을 통해 완벽하게 커스터마이징 가능하며, 서버 운영의 복잡성을 획기적으로 낮춥니다.
1. DrewRPG만의 차별화된 핵심 기능 (Competitive Advantages)
DrewRPG Level System은 기존 RPG 플러그인들이 흔히 겪는 데이터 오류, 밸런싱 난이도, 유지보수 복잡성 등의 문제점을 근본적으로 해결하는 데 중점을 두었습니다.
1.1. 데이터 무결성 보장: 비동기화 (Desync) 문제의 완벽한 해결
 * 중앙 집중식 캐시 시스템 (PlayerJsonManager):
   * 모든 플레이어 데이터는 중앙 집중식 메모리 캐시에 보관되며, PlayerManager를 통해 플레이어 접속 시 로드(loadPlayerJson)되고, 접속 종료 시 즉시 저장(savePlayerJson)되어 데이터 유실을 최소화합니다.
 * 커맨드-캐시 동기화 강제 (Critical Stability):
   * 가장 치명적인 문제인 관리자 명령어(예: /DRPG setLevel, /DRPG addExp) 사용 후 데이터 불일치(Desync)가 발생하지 않도록, 모든 데이터 수정 로직은 중앙 캐시를 통해서만 이루어지며, 수정 직후 디스크에 즉시 저장하는 로직을 강제하였습니다. 이는 서버 재부팅 시 발생할 수 있는 데이터 롤백 가능성을 완벽하게 차단합니다.
 * 비동기 I/O 및 성능 최적화:
   * config.json의 PlayerData 설정을 통해 데이터 로드와 저장을 비동기(Async)로 처리할 수 있어, 데이터 I/O 작업이 서버의 메인 틱(Main Tick)에 영향을 주지 않아 틱 멈춤(Lag) 현상을 미연에 방지합니다.
1.2. 타의 추종을 불허하는 설정 유연성 및 복합 EXP/보상 구조
 * 고급 환경 조건부 경험치 (BonusExpCalculator):
   * 단순한 EXP 지급을 넘어, 플레이어의 **환경 조건 (날씨: 비/맑음, 시간대: 주간/야간, 차원/Dimension: 오버월드/네더/엔드)**에 따라 추가 경험치(BonusEXP)를 지급하는 로직이 완벽하게 분리되어 구현되었습니다. 이는 특정 시간대에 활동을 장려하거나, 위험 지역(네더, 엔드)에서의 활동에 더 큰 보상을 주는 등 세밀한 밸런싱 툴로 활용됩니다.
 * 모듈식 복합 보상 처리 (RewardProcessor):
   * 레벨업 보상은 확률 기반 지급(enableChance), 다중 랜덤 아이템 그룹 선택(useRandom), 그리고 콘솔 명령어 실행이 하나의 보상 객체 내에서 유기적으로 결합됩니다.
   * 안전하지 않은 인챈트(Unsafe Enchantment) 지원: enchant 배열을 통해 바닐라 최대 레벨을 초과하는 인챈트 레벨까지 부여할 수 있어, RPG 서버 특유의 고성능 아이템을 손쉽게 정의할 수 있습니다.
1.3. 유지보수를 위한 통합 진단 시스템 및 개발자 모드
 * 글로벌 디버그 모드:
   * config.json의 Debug.useDebug 스위치 하나로 모든 핵심 로직(EXP 계산, 레벨업 체크, 보상 지급)의 상세 실행 정보를 콘솔에 출력합니다.
 * 세부 로깅 옵션 (Logging 섹션):
   * 파일 로깅: 콘솔 외에 별도 로그 파일(rpg-log.txt)에 기록하도록 설정할 수 있어, 서버 콘솔이 아닌 외부에서 심층 분석이 가능합니다.
   * 선택적 로깅: logSkillActions, logRewardGiving, logWarnings, logErrors 등 로깅 범위를 세분화하여, 필요한 정보만 필터링하여 추적할 수 있습니다.
 * 플러그인 무결성 검사 (Plugin_Integrity):
   * validateSkillFiles, validateRewardFiles 등의 옵션을 통해 JSON 파일 구조의 유효성을 자동으로 검사하고, autoFixCommonErrors를 통해 흔한 JSON 포맷 오류를 자동으로 수정하려는 시도를 하여 관리자 부담을 줄입니다.
2. 상세 기능 분석 (Detailed Feature Breakdown)
2.1. 스킬 정의 및 EXP 시스템
 * 커스텀 레벨업 공식: 각 스킬 JSON 파일의 LevelDrainage 상수를 기반으로 (현재 레벨 * LevelDrainage + 1) 공식에 따라 다음 레벨 필요 경험치가 결정됩니다. 스킬별로 성장 곡선을 달리하여 차별화된 난이도를 설계합니다.
 * 다중 이벤트 핸들링 (HandlerEvents):
   * BlockBreakEvent: (블록 캘 시)
   * EntityDeathEvent: (엔티티 죽일 시)
   * PlayerFishEvent: (낚시 할 시)
 * 연쇄 레벨업 로직 (checkLevelUp):
   * 획득한 경험치가 여러 레벨을 한 번에 올릴 수 있는 경우, while 루프를 통해 모든 레벨업을 정확하게 처리하고, 각 레벨업마다 정의된 보상을 빠짐없이 지급합니다.
2.2. 보상 시스템의 유연성 (RewardProcessor)
 * 보상 트리거 레벨 분리: 레벨업 시 지급되는 보상을 레벨(JSON의 키)별로 완벽하게 분리하여 관리하며, 보상 목록은 JSON 배열로 구성되어 원하는 만큼 보상을 추가할 수 있습니다.
 * 아이템 커스터마이징:
   * itemName (재료), amount (수량) 외에 nbt (NBT 데이터) 필드를 정의할 수 있어, 아이템에 이름, Lore, 기타 커스텀 데이터를 추가하여 아이템 가치를 높일 수 있도록 확장성을 확보하였습니다.
 * 보상 알림 시스템 (RewardNotify):
   * config.json을 통해 레벨업 보상 지급 시 일반 채팅, 액션바, 또는 타이틀 메시지 중 어떤 방식으로 알림을 보낼지 선택하고, 그 포맷까지 자유롭게 설정할 수 있습니다.
2.3. 서버 연동 및 운영 지원 (Integration & Operation)
 * PlaceholderAPI 지원:
   * config.json의 PlaceholderAPI 섹션을 통해 PlaceholderAPI 플러그인과 완벽하게 통합됩니다.
   * 외부 플러그인(스코어보드, 채팅 등)에 실시간 레벨 정보를 표시할 수 있습니다.
 * 권한 시스템 지원:
   * Permissions 섹션을 통해 플러그인 자체 권한 시스템 사용 여부를 제어하고, 기본적으로 플레이어에게 권한을 부여할지 여부를 설정할 수 있습니다.
 * 파일 자동 관리 (FileManager):
   * 플러그인 최초 실행 시 config.json에 정의된 모든 스킬 및 보상 JSON 파일(Mining, Farming, Hunting 등)을 JAR 파일에서 서버 폴더로 자동으로 복사하여, 즉시 사용 가능한 환경을 제공합니다.
 * 버전 관리 (JsonVersionLoader):
   * config.json의 version 키를 읽어 플러그인 로딩 로직을 버전별로 분기 처리하여, 향후 대규모 업데이트 시에도 사용자의 설정 파일이 자동으로 신규 버전 로직에 맞춰 로드되도록 유연성을 확보합니다.
2.4. 관리자 명령어 (Administrator Commands)
모든 명령어는 /DRPG levelSystem 또는 축약어 /drpg를 통해 접근하며, 관리자 권한이 필요합니다.

---------------------------------

This plugin is a professional RPG Skill Leveling System designed to provide the highest level of Stability, Scalability, and Debugging Convenience to Minecraft servers. All core logic is completely customizable via JSON files, dramatically reducing the complexity of server operation.
1. DrewRPG's Unique Core Features (Competitive Advantages)
The DrewRPG Level System focuses on fundamentally resolving common issues faced by existing RPG plugins, such as data errors, balancing difficulty, and maintenance complexity, enabling server administrators to implement almost any desired scenario without coding.
1.1. Guaranteed Data Integrity: Perfect Resolution of Desynchronization (Desync) Issues
 * Centralized Cache System (PlayerJsonManager):
   * All player data is stored in a centralized memory cache. Data is loaded upon player join (loadPlayerJson) via the PlayerManager and immediately saved (savePlayerJson) upon player quit, minimizing data loss.
 * Forced Command-Cache Synchronization (Critical Stability):
   * To prevent the most critical issue—data inconsistency (Desync) after using admin commands (e.g., /DRPG setLevel, /DRPG addExp)—all data modification logic must pass through the central cache, and saving to disk is immediately enforced after the modification. This completely eliminates the potential for data rollback upon server reboot.
 * Asynchronous I/O and Performance Optimization:
   * The PlayerData settings in config.json allow data loading and saving to be processed asynchronously (Async), preventing I/O operations from affecting the server's main tick and mitigating lag.
1.2. Unrivaled Configuration Flexibility and Complex EXP/Reward Structure
 * Advanced Environmental Conditional Experience (BonusExpCalculator):
   * Beyond simple EXP grants, the logic for providing additional experience (BonusEXP) based on a player's environmental conditions (Weather: rain/clear, Time of Day: day/night, Dimension: Overworld/Nether/End) is completely separated and implemented. This acts as a critical balancing tool to encourage activity during specific times or reward higher risk (Nether/End) activities.
 * Modular Complex Reward Processing (RewardProcessor):
   * Level-up rewards are structured to seamlessly combine chance-based grants (enableChance), selection from multiple random item groups (useRandom), and console command execution within a single reward object.
   * Unsafe Enchantment Support: The enchant array allows defining enchantment levels beyond the standard vanilla maximum, enabling the easy creation of powerful, unique items characteristic of RPG servers.
1.3. Integrated Diagnostics System and Developer Mode for Maintenance
 * Global Debug Mode:
   * A single switch (Debug.useDebug: true) in config.json enables the detailed output of all core logic execution paths and data flows (EXP calculation results, level-up loop entry, reward chance checks) to the console.
 * Detailed Logging Options (Logging Section):
   * File Logging: Data can be recorded to a separate log file (rpg-log.txt) in addition to the console, allowing for in-depth analysis outside the live server environment.
   * Selective Logging: Options like logSkillActions, logRewardGiving, logWarnings, and logErrors allow administrators to filter and track only the necessary information.
 * Plugin Integrity Check (Plugin_Integrity):
   * Options like validateSkillFiles and validateRewardFiles automatically check the validity of the JSON file structure. Furthermore, autoFixCommonErrors attempts to automatically correct common JSON formatting errors, reducing the administrator's burden.
2. Detailed Feature Breakdown
2.1. Skill Definition and EXP Acquisition System
 * Custom Leveling Formula: Based on the LevelDrainage constant in each skill's JSON file, the next level's required experience is determined by a custom difficulty formula, typically (CurrentLevel * LevelDrainage + 1). This allows for differentiated growth curves for each skill.
 * Multiple Event Handling (HandlerEvents):
   * BlockBreakEvent (Mining, WoodCutting, Farming)
   * EntityDeathEvent (Hunting)
   * PlayerFishEvent (Fishing)
 * Chained Level-up Logic (checkLevelUp):
   * If the acquired EXP is sufficient to pass multiple levels at once, a while loop ensures all level-ups are processed accurately, and defined rewards are dispensed for every level reached.
2.2. Reward System Flexibility (RewardProcessor)
 * Separated Reward Trigger Levels: Rewards granted upon level-up are managed entirely separately by level (JSON key) and are configured as JSON arrays, allowing for the addition of any number of rewards per level.
 * Item Customization (NBT Data):
   * In addition to itemName (material) and amount (quantity), the nbt (NBT data) field can be defined. This secures the scalability to add custom data, names, and Lore to items, increasing their value.
 * Reward Notification System (RewardNotify):
   * The config.json allows administrators to select and customize the display format (Chat, Actionbar, or Title message) for level-up reward notifications.
2.3. Server Integration and Operation Support (Integration & Operation)
 * PlaceholderAPI Support:
   * The PlaceholderAPI section in config.json provides seamless integration with the PlaceholderAPI plugin.
   * can be used to display real-time level information in external plugins (Scoreboards, Chat, etc.).
 * Permission System Support:
   * The Permissions section controls the use of the plugin's internal permission system, allowing the administrator to set whether players should have default access.
 * Automatic File Management (FileManager):
   * Upon first launch, all Skill and Reward JSON files defined in config.json (e.g., Mining, Farming, Hunting) are automatically copied from the JAR file to the server folder, providing a ready-to-use environment.
 * Version Management (JsonVersionLoader):
   * The version key in config.json is used to execute plugin loading logic based on the version number. This ensures flexibility, allowing user configuration files to be automatically loaded according to the new version's logic during future major updates.
2.4. Administrator Commands (Administrator Commands)
All commands are accessed via /DRPG levelSystem or the alias /drpg, and administrator permission need


---------------------------------

Made by drewdrew1_