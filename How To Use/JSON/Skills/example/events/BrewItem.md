===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# BrewItem event example

## Version

* ### [1.0.0 (KOR)](#brewitem-1-0-0-kor)
* ### [1.0.0 (ENG)](#brewitem-1-0-0-eng)

---

<a id="brewitem-1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "BrewItem": [ // 플레이어가 포션을 제조했을 때 발생
      {
        "PotionType": ["String"], 
        // 제조 대상 포션 목록

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
          "PreventAFKBrew": boolean,
          // 자동 포션 제조 방지

          "CheckIngredients": boolean,
          // 재료 정확성 확인

          "MaxBrewPerMinute": int,
          // 분당 최대 제조 가능 포션 수

          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---

<a id="brewitem-1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": {
    "BrewItem": [ // Triggered when a player brews a potion
      {
        "PotionType": ["String"],
        // Target potion types

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
          "PreventAFKBrew": boolean,
          // Prevent AFK/automatic brewing

          "CheckIngredients": boolean,
          // Validate ingredients

          "MaxBrewPerMinute": int,
          // Maximum brews per minute

          "PlayerPermissionOverride": "String"
        }
      }
    ]
  }
}
```

---
