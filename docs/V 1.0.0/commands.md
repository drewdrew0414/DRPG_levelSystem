DrewRPG Level System Commands Guide
All administrative and diagnostic functions of the DrewRPG Level System plugin are accessible via the main command: /DRPG levelSystem. The alias /drpg can also be used.
These commands are primarily intended for administrators and require the appropriate permissions. Any command that modifies player data is designed to immediately save the changes to ensure data stability.

1. System Management and Diagnostic Commands

1.1. Plugin Configuration and Data Loading
 * /drpg reload: This command reloads all configuration files (Config, Skill JSONs, and Reward JSONs) without requiring a server restart. This is used to quickly apply changes made to your settings.

 * /drpg validate: This command checks the integrity and validity of all currently loaded player data JSON structures. It helps maintain data stability by automatically adding default fields (level: 1, exp: 0) if they are found missing in a player's data.

1.2. Player Data Inquiry and Deletion
 * /drpg info <Player>: Displays the current status of all skills for the specified player, including their Level and Experience (Exp) values.

   * Example: /drpg info Notch

 * /drpg delete <Player>: Permanently deletes the skill data JSON for the specified player from the server's memory cache. This command is used to completely reset a player's RPG progression.

2. Skill Data Editing Commands (/drpg edit)
These commands are used for manual modification or reset of a player's skill data. All editing commands follow the structure /drpg edit <action> <player> <skill> [value].

2.1. Experience (Exp) and Level Management
 * /drpg edit add <Player> <Skill> <Exp>: Adds the specified amount of <Exp> to the designated <Skill> for the <Player>. After adding experience, the plugin automatically checks for level-ups and processes reward granting.

 * /drpg edit remove <Player> <Skill> <Exp>: Removes the specified amount of <Exp> from the designated <Skill> for the <Player>. The experience value will not drop below zero.

 * /drpg edit set <Player> <Skill> <Level>: Forcefully sets the level of the designated <Skill> for the <Player> to the specified <Level>. After setting the level, the plugin attempts to process reward granting.

2.2. Skill Data Reset and Inquiry
 * /drpg edit reset <Player> <Skill>: Completely removes the data for the designated <Skill> from the player's profile, effectively resetting their progress for that specific skill.

 * /drpg edit info <Player> <Skill>: Displays the current Level and Experience information for a single specified skill for the player. This is useful for focused troubleshooting.

💡 Important Notes
 * <Player>: Input the target player's in-game name.
 * <Skill>: Input the exact internal key of the skill as defined in your configuration (e.g., Mining, Combat_Axe).
 * [value]: Input the required numerical value for <Exp> or <Level>.

----------

DrewRPG 레벨 시스템 명령어 가이드 (Commands Guide) - 한국어
DrewRPG 레벨 시스템 플러그인의 모든 관리 및 진단 기능은 주 명령어인 **/DRPG levelSystem**을 통해 접근할 수 있습니다. 축약어 /drpg 사용도 가능합니다.
모든 명령어는 주로 관리자를 대상으로 하며 적절한 권한이 필요합니다. 플레이어 데이터를 수정하는 명령어는 실행 즉시 변경 사항이 저장되어 데이터 안정성을 보장하도록 설계되었습니다.

1. 시스템 관리 및 진단 명령어

1.1. 플러그인 설정 및 데이터 로드 관리
 * /drpg reload: 이 명령어는 서버를 재시작하지 않고 모든 설정 파일(Config, 스킬 JSON, 보상 JSON 등)을 다시 불러와 플러그인에 적용합니다. 설정 파일을 수정한 후 서버에 빠르게 반영할 때 사용됩니다.

 * /drpg validate: 현재 로드된 모든 플레이어 데이터 JSON 구조의 무결성을 검사하고 유효성을 확인합니다. 데이터 안정성을 유지하는 데 도움이 되며, 만약 'level'이나 'exp'와 같은 필수 필드가 누락된 경우 기본값(level: 1, exp: 0)을 자동으로 추가하여 보정합니다.

1.2. 플레이어 데이터 조회 및 삭제

 * /drpg info <Player>: 지정된 플레이어의 모든 스킬 현황을 조회하여 해당 스킬의 현재 레벨 및 경험치(Exp) 값을 출력합니다.

   * 예시: /drpg info Notch

 * /drpg delete <Player>: 지정된 플레이어의 스킬 데이터 JSON을 서버 메모리 캐시에서 영구적으로 삭제합니다. 이 명령어는 플레이어의 RPG 진행 기록을 완전히 초기화할 때 사용됩니다.

2. 스킬 데이터 편집 명령어 (/drpg edit)
플레이어의 스킬 데이터를 수동으로 수정하거나 초기화할 때 사용됩니다. 모든 편집 명령어는 /drpg edit <action> <player> <skill> [value] 구문을 따릅니다.

2.1. 경험치(Exp) 및 레벨 관리
 * /drpg edit add <Player> <Skill> <Exp>: 특정 플레이어의 지정된 <Skill>에 원하는 양의 <Exp>를 추가합니다. 경험치 추가 후에는 자동으로 레벨업 여부를 확인하고 보상 지급 로직을 실행합니다.

 * /drpg edit remove <Player> <Skill> <Exp>: 특정 플레이어의 지정된 <Skill>에서 원하는 양의 <Exp>를 차감합니다. 경험치 값은 0 미만으로 떨어지지 않습니다.

 * /drpg edit set <Player> <Skill> <Level>: 특정 플레이어의 지정된 <Skill> 레벨을 원하는 <Level>로 강제로 설정합니다. 레벨 설정 후에는 보상 지급 로직을 실행합니다.

2.2. 스킬 데이터 초기화 및 조회
 * /drpg edit reset <Player> <Skill>: 지정된 플레이어의 특정 <Skill> 데이터를 완전히 제거하여 해당 스킬의 진행 상황을 초기화합니다.

 * /drpg edit info <Player> <Skill>: 특정 플레이어의 지정된 <Skill>에 대한 현재 레벨 및 경험치 정보만 상세히 확인합니다.

💡 중요 참고 사항
 * <Player>: 대상 플레이어의 닉네임을 입력합니다.
 * <Skill>: 설정 파일에 정의된 스킬의 정확한 내부 키(예: Mining, Combat_Axe)를 입력해야 합니다.
 * [value]: <Exp> 또는 <Level>과 같이 필요한 숫자 값을 입력합니다.

-------------------