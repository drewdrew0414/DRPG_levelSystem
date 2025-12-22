===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# KillEntity event example

## Version

* ### [1.0.0 (KOR)](#killentity-1-0-0-kor)
* ### [1.0.0 (ENG)](#killentity-1-0-0-eng)

---

<a id="killentity-1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "KillEntity": [ // 플레이어가 엔티티를 처치했을 때 발생
      {
        "EntityType": ["String"], 
        // 처치 대상 엔티티 목록 (예: ZOMBIE, SKELETON)

        "EXP": {
          "min": int, // 최소 지급 EXP
          "max": int  // 최대 지급 EXP (min과 같으면 고정)
        },

        "PlayerGetExp": int,
        // 플레이어에게 직접 지급되는 EXP

        "Chance": int,
        // EXP 지급 확률 (%)

        "RequiredLevel": int,
        // 해당 스킬(Name)의 최소 요구 레벨

        "RequiredWeapon": ["String"],
        // 처치 시 사용해야 하는 무기
        // 비어있으면 제한 없음

        "ExtraEXP": {
          "CriticalKillBonus": int,
          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부

        "AdvancedSettings": {
          "MaxDistance": int,
          // 플레이어와 몹 사이 최대 거리

          "BiomeEXPMultiplier": {
            "PLAINS": double,
            "DESERT": double,
            "NETHER_WASTES": double,
            "DEEP_DARK": double
          },

          "BabyMultiplier": double,
          // 아기 엔티티 배율

          "RequireLastHit": boolean,
          "IgnoreSpawnerMobs": boolean,

          "DailyLimit": int,
          // 하루 최대 EXP

          "AssistEXPPercent": int,
          // 기여자 EXP 비율 (%)

          "PreventAFKFarm": {
            "Enable": boolean,
            "MaxKillsPerMinute": int,
            "SameLocationRadius": int
          },

          "CancelExpIfCancelled": boolean,
          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---

<a id="killentity-1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": {
    "KillEntity": [ // Triggered when a player kills an entity
      {
        "EntityType": ["String"], 
        // Target EntityTypes (e.g., ZOMBIE, SKELETON)

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,
        // EXP given directly to the player

        "Chance": int,
        // Chance to receive EXP (%)

        "RequiredLevel": int,
        // Minimum required skill level

        "RequiredWeapon": ["String"],
        // Required weapon (empty = no restriction)

        "ExtraEXP": {
          "CriticalKillBonus": int,
          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,
        // Enables or disables AdvancedSettings

        "AdvancedSettings": {
          "MaxDistance": int,
          // Maximum distance between player and mob

          "BiomeEXPMultiplier": {
            "PLAINS": double,
            "DESERT": double,
            "NETHER_WASTES": double,
            "DEEP_DARK": double
          },

          "BabyMultiplier": double,
          // Multiplier for baby mobs

          "RequireLastHit": boolean,
          "IgnoreSpawnerMobs": boolean,

          "DailyLimit": int,
          // Max EXP per day

          "AssistEXPPercent": int,
          // EXP % for contributors

          "PreventAFKFarm": {
            "Enable": boolean,
            "MaxKillsPerMinute": int,
            "SameLocationRadius": int
          },

          "CancelExpIfCancelled": boolean,
          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---
