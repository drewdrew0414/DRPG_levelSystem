===============

# Made By drewdrew0414(or drewdrew1_)

===============

---

## BlockBreak event example

### 1.0.0
``` json
"Events": {
    "BlockBreak": [
      {
        "TypeItemName": ["String"],

        "EXP": {
          "min": int,
          "max": int
        },

        "Chance": int,
        "RequiredLevel": int,
        "RequiredTools": ["String"],

        "ExtraEXP": {
          "Weather": {
            "rain": { "addMin": int, "addMax": int },
            "clear": { "addMin": int, "addMax": int },
            "thunder": { "addMin": int, "addMax": int }
          },
          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,
        "AdvancedSettings": {
          "RequirePlayerPlaced": boolean,

          "PreventXPGrinding": {
            "Radius": int,
            "CooldownSeconds": int,
            "MaxBlocksInChunk": int,
            "MinLightLevel": int,
            "MaxDailyXPPerBlock": int
          },

          "ActionControl": {
            "AllowCreativeMode": boolean,
            "RequireNaturalBlock": boolean,
            "CancelExpIfCancelled": boolean
          },

          "Requirements": {
            "RequiredWorldTimeStart": int,
            "RequiredWorldTimeEnd": int
          },

          "PlayerPermissionOverride": "String",
          "RequireBiome": ["String"]
        }
      }
    ]
  }
```
