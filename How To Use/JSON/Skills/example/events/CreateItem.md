===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# CraftItem event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "CraftItem": [ // 플레이어가 아이템을 제작했을 때 발생하는 이벤트
      {
        "TypeItemName": ["String"],
        // 제작 대상 아이템(Material) 목록
        // Bukkit / Paper Material enum 이름 사용
        // 예: IRON_PICKAXE, BREAD

        "EXP": {
          "min": int, // 최소 지급 EXP
          "max": int  // 최대 지급 EXP (min과 같으면 고정 EXP)
        },

        "PlayerGetExp": int,
        // 플레이어에게 직접 지급되는 EXP
        // (스킬 EXP와 별도로 사용 가능)

        "Chance": int,
        // EXP 지급 확률 (%)
        // 100 = 항상 지급

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            // 비 오는 날 추가 EXP

            "clear": {
              "addMin": int,
              "addMax": int
            }
            // 맑은 날 추가 EXP
          },

          "multiplier": double,
          // 최종 EXP 배율
          // (기본 EXP + 추가 EXP) × multiplier

          "bonusEXP": int
          // 모든 계산 이후 고정으로 추가되는 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부
        // false일 경우 AdvancedSettings 전체 무시

        "AdvancedSettings": {
          "PreventShiftClickCrafting": boolean,
          // 쉬프트 클릭 대량 제작 시 EXP 지급 여부
          // true = 쉬프트 제작 차단

          "ValidateNBTIngredients": boolean,
          // 재료 아이템의 NBT까지 검증
          // 커스텀 아이템 악용 방지

          "MaxCraftPerMinute": int,
          // 분당 최대 EXP 인정 제작 횟수

          "CheckInventorySpace": boolean
          // 인벤토리 공간 부족 시 EXP 지급 여부
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
  "Events": {
    "CraftItem": [ // Event triggered when a player crafts an item
      {
        "TypeItemName": ["String"],
        // List of crafted item Materials
        // Uses Bukkit / Paper Material enum names

        "EXP": {
          "min": int, // Minimum EXP
          "max": int  // Maximum EXP (fixed if equal to min)
        },

        "PlayerGetExp": int,
        // EXP given directly to the player
        // Separate from skill EXP if needed

        "Chance": int,
        // Chance to receive EXP (percentage)

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            // Bonus EXP during rain

            "clear": {
              "addMin": int,
              "addMax": int
            }
            // Bonus EXP during clear weather
          },

          "multiplier": double,
          // Final EXP multiplier

          "bonusEXP": int
          // Flat EXP added after all calculations
        },

        "UseAdvancedSettings": boolean,
        // Enables or disables AdvancedSettings

        "AdvancedSettings": {
          "PreventShiftClickCrafting": boolean,
          // Prevent EXP from shift-click crafting

          "ValidateNBTIngredients": boolean,
          // Validate ingredient NBT data

          "MaxCraftPerMinute": int,
          // Maximum crafts counted per minute

          "CheckInventorySpace": boolean
          // Require free inventory space to grant EXP
        }
      }
    ]
  }
}
```

---
