===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# SmeltItem event example

## Version

* ### [1.0.0 (KOR)](#smeltitem-1-0-0-kor)
* ### [1.0.0 (ENG)](#smeltitem-1-0-0-eng)

---

<a id="smeltitem-1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "SmeltItem": [ // 플레이어가 아이템을 제련했을 때 발생
      {
        "ItemType": ["String"], 
        // 제련 대상 아이템(Material) 목록

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,
        "Chance": int,
        "RequiredLevel": int,

        "ExtraEXP": {
          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,

        "AdvancedSettings": {
          "PreventAutoSmelt": boolean,
          // 자동 제련기, 노가다 방지

          "MaxSmeltPerMinute": int,
          // 분당 최대 제련 가능 개수

          "RequireFuel": boolean,
          // 반드시 연료 사용 여부 확인

          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---

<a id="smeltitem-1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": {
    "SmeltItem": [ // Triggered when a player smelts an item
      {
        "ItemType": ["String"],
        // Target items for smelting

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,
        "Chance": int,
        "RequiredLevel": int,

        "ExtraEXP": {
          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,

        "AdvancedSettings": {
          "PreventAutoSmelt": boolean,
          // Prevent AFK/automatic smelting

          "MaxSmeltPerMinute": int,
          // Maximum smelts per minute

          "RequireFuel": boolean,
          // Check that fuel is used

          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---
