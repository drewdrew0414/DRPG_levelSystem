===============
Made By drewdrew0414 (or drewdrew1_)
===============
PlayerRun event example
Version
 * 1.0.0 (KOR)
 * 1.0.0 (ENG)
<a id="1-0-0-kor"></a>
1.0.0 (KOR)
```
{
  "Events": {
    "PlayerRun": [
      {
        "When": "RUN",

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,

        "Chance": int,

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            "clear": {
              "addMin": int,
              "addMax": int
            }
          },

          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,

        "AdvancedSettings": {
          "CheckSneaking": boolean,
          "IgnoreVehicles": boolean,
          "MaxExpPerMinute": int
        }
      }
    ]
  }
}
```
<a id="1-0-0-eng"></a>
1.0.0 (ENG)
```
{
  "Events": {
    "PlayerRun": [
      {
        "When": "RUN",

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,

        "Chance": int,

        "ExtraEXP": {
          "Weather": {
            "rain": {
              "addMin": int,
              "addMax": int
            },
            "clear": {
              "addMin": int,
              "addMax": int
            }
          },

          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,

        "AdvancedSettings": {
          "CheckSneaking": boolean,
          "IgnoreVehicles": boolean,
          "MaxExpPerMinute": int
        }
      }
    ]
  }
}
```
