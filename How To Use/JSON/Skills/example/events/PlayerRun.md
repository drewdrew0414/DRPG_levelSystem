===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# PlayerRun event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>
### 1.0.0 (KOR)
```
{
  "Events": {
    "PlayerRun": [ // 플레이어가 달릴 때 발생하는 이벤트
      {
        "When": "RUN", // 이벤트 발생 시점 (기본값: RUN)

        "EXP": {
          "min": int, // 최소 지급 스킬 EXP
          "max": int  // 최대 지급 스킬 EXP (min과 같으면 고정값)
        },

        "PlayerGetExp": int, // 플레이어에게 직접 지급되는 추가 경험치

        "Chance": int, // EXP 지급 확률 (0~100)

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int, // 비 올 때 추가되는 최소 EXP
              "addMax": int  // 비 올 때 추가되는 최대 EXP
            },
            "clear": {
              "addMin": int, // 맑을 때 추가되는 최소 EXP
              "addMax": int  // 맑을 때 추가되는 최대 EXP
            }
          },

          "multiplier": double, // 최종 EXP 배율 (예: 1.5)
          "bonusEXP": int // 모든 계산 후 더해지는 고정 보너스 EXP
        },

        "UseAdvancedSettings": boolean, // 고급 설정 활성화 여부

        "AdvancedSettings": {
          "CheckSneaking": boolean, // 앉기(Shift) 상태에서 달릴 때 EXP 지급 여부
          "IgnoreVehicles": boolean, // 탈것(말, 마인카트 등) 탑승 중 이동 제외 여부
          "MaxExpPerMinute": int // 1분당 획득 가능한 최대 EXP 제한
        }
      }
    ]
  }
}
```

<a id="1-0-0-eng"></a>
### 1.0.0 (ENG)
```
{
  "Events": {
    "PlayerRun": [ // Event triggered when a player runs
      {
        "When": "RUN", // Trigger condition (Default: RUN)

        "EXP": {
          "min": int, // Minimum skill EXP to grant
          "max": int  // Maximum skill EXP to grant (fixed if equal to min)
        },

        "PlayerGetExp": int, // Additional EXP given directly to the player

        "Chance": int, // Chance to receive EXP (0-100%)

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int, // Additional min EXP during rain
              "addMax": int  // Additional max EXP during rain
            },
            "clear": {
              "addMin": int, // Additional min EXP during clear weather
              "addMax": int  // Additional max EXP during clear weather
            }
          },

          "multiplier": double, // Final EXP multiplier (e.g., 1.5)
          "bonusEXP": int // Flat bonus EXP added after all calculations
        },

        "UseAdvancedSettings": boolean, // Whether to use AdvancedSettings

        "AdvancedSettings": {
          "CheckSneaking": boolean, // Grant EXP even while sneaking (Shift)
          "IgnoreVehicles": boolean, // Exclude movement while riding vehicles (Horse, Minecart, etc.)
          "MaxExpPerMinute": int // Maximum limit for EXP gain per minute
        }
      }
    ]
  }
}
```
