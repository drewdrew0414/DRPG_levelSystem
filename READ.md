## This Plugin Isn't launched!

# 세상에서 가장 유연하고 안전한 마인크래프트 RPG 플러그인 "DRPG_LevelSystem".

---

**이 플러그인은 Minecraft 서버에 최고 수준의 안정성, 확장성, 디버깅 편의성을 제공하는 PRG 스킬 레벨링 시스템이다.**

* 모든 핵심 로직은 .json파일로 완벽히 커스텀마이징 가능하며, 서버 운영의 복잡성을 획기적으로 낮춘다.

---

## 1. 핵심 기능

**이 플러그인은 기존 RPG 레벨 시스템 플러그인들이 흔히 겪는 데이터 오류, 밸런싱 난이도, 유지보수 복잡성 등의 문제점을 근본적으로 해결하는데 중점을 두었다.**

### 1.1. 데이터 부결성 보장: 데이터 불일치 ( Desync ) 문제 해결

* 중앙 집중식 캐시 시스템을 이용해 모든 데이터는 메모리 캐시에 보관되며, 불러오기 및 저장 기능으로 데이터 유실을 최소화한다.

* 커맨드 - 캐시 동기화 강제: config.json의 설정을 통하여 명령어 사용 후 데이터 불일치 ( Desync )이 발생하지 않도록 모든 데이터는 중앙 캐시를 통해서만 이루어지며, 수정 직후 즉시 저장하는 로직으로, 서버 재부팅 시 발생 가능한 데이터 롤백 가능성은 완벽히 차단하였다.

* 비동기 I/O 및 성능 최적화:
config.json의 PlayerData 설정을 통해 데이터 로드와 저장을 **비동기(Async)**로 처리할 수 있어, I/O 작업량이 많을 때 서버 랙이 발생하는 것을 방지한다.

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

* ** PlaceHolderAPI 지원 (1.1.0 버전부터 지원 될 예정):
`config.json`에서 PlaceHolderAPI를 지원하게 할 수 있다.
(LuckPerms는 1.0.0에서 지원을 시작한다.)

* ** 프로그래머가 아닌 운영자를 위한 시스템:
첫 실행 시 예시 파일을 plugins/DRPG/levelSystem/에 만들어 별다른 코드 수정 없이 바로 사용 가능하게 할 수 있는 환경을 제공한다. (파일은 How To Use/JSON/ 안에 모든 예시 파일들이 들어간다.)

* ** 버전 괸리 시스템:
config.json, rewards/*.json 그리고 skills/*.json에는 버전들이 있으며 버전을 고정해서 쓸 수 있다. (최신기능은 사용 불가하며 만약 json을 최신버전으로 바꿀 시 jar도 지원하는 버전으로 바꾸어야함.)

### 2.4 관리자 명령어

** 모든 명령어는 /DRPG levelSystem ( 혹은 /drpg ls )으로 접근이 가능하며 config.json에서 권한 설정이 가능하다. (LuckPerms 연동 시) (예시) [How To Use/Commands/Commands Manual (KOR).md]
