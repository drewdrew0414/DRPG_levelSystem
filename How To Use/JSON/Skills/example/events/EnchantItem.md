===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# EnchantItem event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "EnchantItem": [ // 플레이어가 아이템을 인챈트할 때 발생하는 이벤트
      {
        "TypeItemName": ["String"],
        // 인챈트 대상 아이템(Material) 목록
        // Bukkit / Paper Material enum 이름 사용
        // 예: DIAMOND_SWORD, BOOK

        "CheckEnchant": [
          {
            "EnchantType": "String",
            // 확인할 인챈트 종류
            // Bukkit Enchantment 키 이름 사용
            // 예: SHARPNESS, EFFICIENCY

            "Level": int
            // 요구되는 최소 인챈트 레벨
            // 실제 부여된 레벨이 이 값 이상이어야 조건 충족
          }
        ],
        // 여러 개 지정 시 모든 조건을 만족해야 EXP 지급

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

        "RequiredLevel": int,
        // 해당 스킬(Name)의 최소 요구 레벨
        // 마인크래프트 기본 레벨 아님

        "Cooldown": int,
        // 동일 인챈트 반복 시 EXP 재지급 쿨타임 (초)

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            // 비 오는 날 추가 EXP 범위

            "clear": {
              "addMin": int,
              "addMax": int
            },
            // 맑은 날 추가 EXP 범위

            "thunder": {
              "addMin": int,
              "addMax": int
            }
            // 번개(폭풍) 날씨 추가 EXP 범위
          },

          "multiplier": double,
          // 최종 EXP 배율
          // (기본 EXP + 날씨 EXP) × multiplier

          "bonusEXP": int
          // 모든 계산 이후 고정으로 추가되는 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부
        // false면 AdvancedSettings 전체 무시

        "AdvancedSettings": {
          "CheckEnchantingTableLevel": boolean
          // 인챈트 테이블 레벨(책장 수) 검증 여부
          // true일 경우 충분한 테이블 레벨이 아니면 EXP 지급 안 함
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
    "EnchantItem": [ // Event triggered when a player enchants an item
      {
        "TypeItemName": ["String"],
        // List of target item Materials
        // Bukkit / Paper Material enum names

        "CheckEnchant": [
          {
            "EnchantType": "String",
            // Enchantment type to check
            // Bukkit Enchantment key name

            "Level": int
            // Minimum required enchantment level
          }
        ],
        // All listed enchant conditions must be satisfied

        "EXP": {
          "min": int, // Minimum EXP
          "max": int  // Maximum EXP (fixed if equal to min)
        },

        "PlayerGetExp": int,
        // EXP given directly to the player
        // Separate from skill EXP

        "Chance": int,
        // Chance to receive EXP (percentage)

        "RequiredLevel": int,
        // Minimum required skill level (not Minecraft XP level)

        "Cooldown": int,
        // Cooldown before EXP can be granted again (seconds)

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            // Extra EXP during rain

            "clear": {
              "addMin": int,
              "addMax": int
            },
            // Extra EXP during clear weather

            "thunder": {
              "addMin": int,
              "addMax": int
            }
            // Extra EXP during thunderstorm
          },

          "multiplier": double,
          // Final EXP multiplier

          "bonusEXP": int
          // Flat EXP added after all calculations
        },

        "UseAdvancedSettings": boolean,
        // Enables or disables AdvancedSettings entirely

        "AdvancedSettings": {
          "CheckEnchantingTableLevel": boolean
          // Validates enchanting table level (bookshelves)
        }
      }
    ]
  }
}
```

---
