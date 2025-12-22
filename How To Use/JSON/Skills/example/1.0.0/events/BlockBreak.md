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
          "min": 6,
          "max": 9
        },

        "Chance": 100,
        "RequiredLevel": 0,
        "RequiredTools": ["WOODEN_HOE", "STONE_HOE", "IRON_HOE"],

        "ExtraEXP": {
          "Weather": {
            "rain": { "addMin": 2, "addMax": 5 },
            "clear": { "addMin": 1, "addMax": 3 }
          },
          "multiplier": 1.2,
          "bonusEXP": 0
        },

        "UseAdvancedSettings": true,
        "AdvancedSettings": {
          "RequirePlayerPlaced": true,

          "PreventXPGrinding": {
            "Radius": 5,
            "CooldownSeconds": 10,
            "MaxBlocksInChunk": 20,
            "MinLightLevel": 9,
            "MaxDailyXPPerBlock": 100
          },

          "ActionControl": {
            "AllowCreativeMode": false,
            "RequireNaturalBlock": false,
            "CancelExpIfCancelled": true
          },

          "Requirements": {
            "RequiredWorldTimeStart": 0,
            "RequiredWorldTimeEnd": 24000
          },

          "PlayerPermissionOverride": "farming.bypass",
          "RequireBiome": ["PLAINS", "FOREST"]
        }
      }
    ]
  }
```
