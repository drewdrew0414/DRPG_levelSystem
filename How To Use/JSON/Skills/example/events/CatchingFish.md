===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# CatchingFish event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "CatchingFish": [ // 플레이어가 낚시로 아이템을 획득했을 때 발생
      {
        "CatchType": ["FISH", "TREASURE", "JUNK"],
        // 낚시 결과 타입
        // FISH / TREASURE / JUNK (Paper FishHook.Catch)

        "TypeItemName": ["String"],
        // 실제로 낚은 아이템(Material) 목록
        // 비워두면 모든 아이템 허용

        "EXP": {
          "min": int, // 최소 지급 EXP
          "max": int  // 최대 지급 EXP
        },

        "PlayerGetExp": int,
        // 플레이어에게 직접 지급되는 EXP

        "Chance": int,
        // EXP 지급 확률 (%)

        "RequiredLevel": int,
        // 해당 스킬(Name)의 최소 요구 레벨

        "RequiredRod": ["String"],
        // 사용한 낚싯대(Material)
        // 비어있으면 모든 낚싯대 허용

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
          // 최종 EXP 배율

          "bonusEXP": int
          // 고정 추가 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부

        "AdvancedSettings": {
          "PreventAFKFishing": {
            "Enable": boolean,
            // AFK 낚시 감지 사용 여부

            "MinMovementDistance": double,
            // 일정 시간 내 최소 이동 거리

            "MaxSamePositionCatches": int
            // 같은 위치에서 허용되는 최대 낚시 횟수
          },

          "RequireOpenWater": boolean,
          // 오픈 워터 낚시만 허용 여부

          "RequireBiome": ["String"],
          // 허용 바이옴 목록
          // "All" 입력 시 제한 없음

          "RequiredTime": {
            "Start": int,
            "End": int
          },
          // 월드 시간 제한 (0~24000)

          "CancelExpIfCancelled": boolean,
          // 이벤트가 취소되었을 경우 EXP 지급 취소

          "PlayerPermissionOverride": "String"
          // 해당 권한이 있으면 모든 제한 무시
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
    "CatchingFish": [ // Triggered when a player catches something while fishing
      {
        "CatchType": ["FISH", "TREASURE", "JUNK"],
        // Fishing result types

        "TypeItemName": ["String"],
        // List of caught item Materials

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

        "RequiredRod": ["String"],
        // Required fishing rod Material

        "ExtraEXP": {
          "Weather": {
            "rain": { "addMin": int, "addMax": int },
            "clear": { "addMin": int, "addMax": int }
          },

          "multiplier": double,
          "bonusEXP": int
        },

        "UseAdvancedSettings": boolean,

        "AdvancedSettings": {
          "PreventAFKFishing": {
            "Enable": boolean,
            "MinMovementDistance": double,
            "MaxSamePositionCatches": int
          },

          "RequireOpenWater": boolean,
          "RequireBiome": ["String"],

          "RequiredTime": {
            "Start": int,
            "End": int
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
