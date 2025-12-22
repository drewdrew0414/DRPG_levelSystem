===============

# Made By drewdrew0414(or drewdrew1_)

===============

---
# BlockBreak event example
## Version
### [1.0.0 (KOR)](#1-0-0-KOR)
### [1.0.0 (ENG)](#1-0-0-ENG)

---

### 1.0.0 KOR
``` json
  "Events": { // 모든 스킬/보상 이벤트의 최상위 컨테이너
    "BlockBreak": [ // 플레이어가 블록을 파괴했을 때 발생하는 이벤트
      {
        "TypeItemName": ["String"], 
        // 이 규칙이 적용될 블록(Material) 목록
        // Bukkit / Paper Material enum 이름 사용
        // 여기에 포함되지 않은 블록을 캐면 이 규칙은 무시됨

        "EXP": {
          // 기본 지급 EXP 설정
          // min ~ max 사이의 값이 랜덤으로 지급됨
          "min": int, // 최소 지급 EXP (0 가능)
          "max": int  // 최대 지급 EXP (min 이상이어야 함) (만약 min의 값과 max의 값이 같을 시 고정값이 됨)
        },

        "Chance": int,
        // EXP 지급 확률 (%)
        // 100 = 항상 지급, 50 = 50% 확률로 지급

        "RequiredLevel": int,
        // EXP를 받기 위해 필요한 최소 플레이어 레벨 (레벨은 마크에 플레이어 레벨이 아닌 해당 Name의 레벨로 봄)
        // 플레이어 레벨이 이 값보다 낮으면 EXP 지급 안 됨

        "RequiredTools": ["String"],
        // 블록을 캘 때 사용해야 하는 도구 목록
        // 들고 있는 아이템이 목록 중 하나와 일치해야 EXP 지급
        // 비어있거나 생략 시 도구 제한 없음

        "ExtraEXP": {
          // 기본 EXP 계산 이후 적용되는 추가 보정 설정

          "Weather": {
            // 현재 월드 날씨에 따른 EXP 추가 보정
            "rain": {
              "addMin": int, // 비가 올 때 추가되는 최소 EXP
              "addMax": int  // 비가 올 때 추가되는 최대 EXP
            },
            "clear": {
              "addMin": int, // 맑은 날씨일 때 추가되는 최소 EXP
              "addMax": int  // 맑은 날씨일 때 추가되는 최대 EXP
            },
            "thunder": {
              "addMin": int, // 천둥 번개 날씨일 때 추가되는 최소 EXP
              "addMax": int  // 천둥 번개 날씨일 때 추가되는 최대 EXP
            }
          },

          "multiplier": double,
          // 최종 EXP에 적용되는 배율
          // (기본 EXP + 추가 EXP) × multiplier
          // 1.0 = 변화 없음

          "bonusEXP": int
          // 모든 계산이 끝난 후 고정으로 추가되는 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정(AdvancedSettings) 사용 여부
        // false일 경우 AdvancedSettings 내부 설정 전부 무시됨

        "AdvancedSettings": {
          "RequirePlayerPlaced": boolean,
          // true  : 플레이어가 직접 설치한 블록만 EXP 지급
          // false : 자연 생성 블록도 EXP 지급 가능

          "PreventXPGrinding": {
            // EXP 노가다 / 자동 농장 방지용 설정

            "Radius": int,
            // 동일 위치 근처에서 반복 EXP 획득을 감지하는 반경(블록 단위)

            "CooldownSeconds": int,
            // 같은 블록 좌표에서 다시 EXP를 받을 수 있는 쿨타임(초)

            "MaxBlocksInChunk": int,
            // 하나의 청크(16x16) 내에서
            // EXP를 지급할 수 있는 최대 블록 수

            "MinLightLevel": int,
            // EXP 지급을 허용하는 최소 밝기 값
            // 암실 노가다 방지용

            "MaxDailyXPPerBlock": int
            // 블록 하나가 하루 동안 지급할 수 있는 EXP 최대치
          },

          "ActionControl": {
            // 플레이어 행동 및 상태에 따른 제어 설정

            "AllowCreativeMode": boolean,
            // 크리에이티브 모드 플레이어에게 EXP 지급 허용 여부

            "RequireNaturalBlock": boolean,
            // true일 경우 자연 생성 블록만 EXP 지급
            // 플레이어가 설치한 블록은 무시됨

            "CancelExpIfCancelled": boolean
            // 다른 플러그인에 의해 BlockBreakEvent가 취소되었을 경우
            // EXP 지급도 함께 취소할지 여부
          },

          "Requirements": {
            // 월드 시간 조건 (Minecraft tick 기준)

            "RequiredWorldTimeStart": int,
            // EXP 지급을 허용하는 월드 시간 시작값 (0~24000)

            "RequiredWorldTimeEnd": int
            // EXP 지급을 허용하는 월드 시간 종료값 (0~24000)
          },

          "PlayerPermissionOverride": "String",
          // 해당 권한을 가진 플레이어는
          // 모든 조건을 무시하고 EXP를 받을 수 있음 (관리자용)

          "RequireBiome": ["String"]
          // EXP 지급이 허용되는 바이옴 목록
          // 현재 플레이어 위치의 바이옴이 목록에 없으면 EXP 미지급 (만약 String에 "All" 입력 시 바이옴 상관없이 됨)
        }
      }
    ]
  }
}

```
