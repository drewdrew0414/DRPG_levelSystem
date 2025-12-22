===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# BlockBreak event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
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
          "max": int  // 최대 지급 EXP (min 이상이어야 함)
          // min과 max가 같을 경우 고정 EXP 지급
        },

        "Chance": int,
        // EXP 지급 확률 (%)
        // 100 = 항상 지급, 50 = 50% 확률

        "RequiredLevel": int,
        // EXP를 받기 위한 최소 요구 레벨
        // (마인크래프트 기본 레벨이 아닌, 해당 Name 스킬 레벨 기준)

        "RequiredTools": ["String"],
        // 블록을 캘 때 사용해야 하는 도구 목록
        // 들고 있는 아이템이 목록 중 하나와 일치해야 EXP 지급
        // 비어있거나 생략 시 도구 제한 없음

        "ExtraEXP": {
          // 기본 EXP 계산 이후 적용되는 추가 보정 설정

          "Weather": {
            // 현재 월드 날씨에 따른 EXP 추가
            "rain": { "addMin": int, "addMax": int },
            "clear": { "addMin": int, "addMax": int },
            "thunder": { "addMin": int, "addMax": int }
          },

          "multiplier": double,
          // 최종 EXP 배율
          // (기본 EXP + 추가 EXP) × multiplier

          "bonusEXP": int
          // 모든 계산 이후 고정으로 추가되는 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부
        // false일 경우 AdvancedSettings 전부 무시됨

        "AdvancedSettings": {
          "RequirePlayerPlaced": boolean,
          // true  : 플레이어가 직접 설치한 블록만 허용
          // false : 자연 생성 블록도 허용

          "PreventXPGrinding": {
            "Radius": int,
            // 반복 EXP 획득 감지 반경 (블록 단위)

            "CooldownSeconds": int,
            // 같은 블록에서 EXP를 다시 받을 수 있는 쿨타임 (초)

            "MaxBlocksInChunk": int,
            // 청크(16x16)당 EXP 지급 가능 블록 수 제한

            "MinLightLevel": int,
            // 최소 밝기 조건 (암실 노가다 방지)

            "MaxDailyXPPerBlock": int
            // 블록 하나가 하루 동안 줄 수 있는 최대 EXP
          },

          "ActionControl": {
            "AllowCreativeMode": boolean,
            // 크리에이티브 모드 EXP 지급 허용 여부

            "RequireNaturalBlock": boolean,
            // 자연 생성 블록만 EXP 지급 여부

            "CancelExpIfCancelled": boolean
            // 다른 플러그인에 의해 이벤트가 취소되었을 경우
            // EXP 지급도 함께 취소
          },

          "Requirements": {
            "RequiredWorldTimeStart": int,
            // EXP 지급 시작 월드 시간 (0~24000)

            "RequiredWorldTimeEnd": int
            // EXP 지급 종료 월드 시간 (0~24000)
          },

          "PlayerPermissionOverride": "String",
          // 해당 권한이 있으면 모든 조건 무시

          "RequireBiome": ["String"]
          // EXP 지급 허용 바이옴 목록
          // "All" 입력 시 모든 바이옴 허용
        }
      }
    ]
  }
}
```

---

<a id="1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": { // Root container for all skill/reward events
    "BlockBreak": [ // Event triggered when a player breaks a block
      {
        "TypeItemName": ["String"],
        // List of block Materials that trigger this rule
        // Uses Bukkit / Paper Material enum names

        "EXP": {
          // Base EXP reward range
          // A random value between min and max is selected
          "min": int, // Minimum EXP (can be 0)
          "max": int  // Maximum EXP (must be >= min)
          // If min == max, EXP becomes a fixed value
        },

        "Chance": int,
        // Chance to receive EXP (percentage)
        // 100 = always, 50 = 50% chance

        "RequiredLevel": int,
        // Minimum required skill level
        // (Not Minecraft XP level, but the level of this skill Name)

        "RequiredTools": ["String"],
        // Tools required to receive EXP
        // If the held item does not match, EXP is not granted

        "ExtraEXP": {
          // Additional EXP modifiers applied after base EXP calculation

          "Weather": {
            // Weather-based EXP bonuses
            "rain": { "addMin": int, "addMax": int },
            "clear": { "addMin": int, "addMax": int },
            "thunder": { "addMin": int, "addMax": int }
          },

          "multiplier": double,
          // Final EXP multiplier
          // (Base EXP + Extra EXP) × multiplier

          "bonusEXP": int
          // Flat EXP added after all calculations
        },

        "UseAdvancedSettings": boolean,
        // Enables or disables AdvancedSettings entirely

        "AdvancedSettings": {
          "RequirePlayerPlaced": boolean,
          // true  : Only player-placed blocks give EXP
          // false : Natural blocks are also allowed

          "PreventXPGrinding": {
            "Radius": int,
            // Radius used to detect repetitive EXP farming

            "CooldownSeconds": int,
            // Cooldown before the same block can give EXP again

            "MaxBlocksInChunk": int,
            // Maximum number of EXP-yielding blocks per chunk

            "MinLightLevel": int,
            // Minimum light level required to gain EXP

            "MaxDailyXPPerBlock": int
            // Maximum EXP a single block can give per day
          },

          "ActionControl": {
            "AllowCreativeMode": boolean,
            // Allow EXP in Creative mode

            "RequireNaturalBlock": boolean,
            // Only naturally generated blocks give EXP

            "CancelExpIfCancelled": boolean
            // Cancel EXP if the BlockBreakEvent was cancelled
          },

          "Requirements": {
            "RequiredWorldTimeStart": int,
            // World time start (0–24000 ticks)

            "RequiredWorldTimeEnd": int
            // World time end (0–24000 ticks)
          },

          "PlayerPermissionOverride": "String",
          // Players with this permission bypass all restrictions

          "RequireBiome": ["String"]
          // Allowed biomes for EXP rewards
          // Use "All" to allow every biome
        }
      }
    ]
  }
}
```

---
