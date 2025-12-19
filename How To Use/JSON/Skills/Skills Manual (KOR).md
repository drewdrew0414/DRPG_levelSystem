---
===============

# 제작자 drewdrew0414 (혹은 drewdrew1_)

===============

---

## 0. 목차

[1. 최상위 구조](#1-최상위-구조) 

[2. Events 구조](#2-Events-구조)
* [2-1. BlockBreak 이벤트](#2-1-BlockBreak-이벤트)
  * [2-1-1. 구조](#2-1-1-구조)
  * [2-1-2. 고급기능](#2-1-2-고급기능)
  * 
* [3. 동작 흐름 요약](#3-동작-흐름-요약)
* [4. 주의사항](#4-주의사항)
* [5. 예시 JSON (Farming)](#5-예시-JSON)

---

## 1. 최상위 구조
```
{
  "RewardJsonVersion": "<version>",
  "Name": "SkillName",
  "DisplayName": "Display Name",
  "LevelDrainage": <inteager>,
  "MaxLevel": <integer>,
  "Events": {

  }
}
```

필드                  | 타입     | 설명                 |
| ------------------- | ------ | ------------------ |
| `RewardJsonVersion` | String | JSON 포맷 버전         |
| `Name`              | String | 스킬 내부 ID           |
| `DisplayName`       | String | 화면에 표시될 이름         |
| `LevelDrainage`     | int    | 레벨업에 필요한 경험치 증가 계수 (공식 : (level + 1) * LevelDrainage) |
| `MaxLevel`          | int    | 스킬 최대 레벨           |
| `Events`            | Object | 이벤트 기반 경험치 규칙      |

---

## 2. Events 구조
**사용가능한 이벤트들** :
* blockBreak
* blockPlace
  
   ## 2-1. BlockBreak 이벤트
   **플레이어가 블록을 부쉈을 때 실행됨**

   ### 2-1-1. 구조
   
```
// "Events { } 내부
"BlockBreak": [
      {
        "TypeItemName": ["ItemName"],
        "EXP": { "min": <int>, "max": <int> },
        "PlayerGetExp": <int>,
        "Chance": <int>,
        "RequiredLevel": <int>,
        "RequiredTools": [<String>],

        "ExtraEXP": {
          "Weather": {
            "rain": { "addMin": <int>, "addMax": <int> },
            "clear": { "addMin": <int>, "addMax": <int> },
            "thunder": { "addMin: <int>, "addMax": <int> }
          },
          "multiplier": <double>,
          "bonusEXP": <int>
        },
        // if you set "UseAdvancedSettings" false, you don't need to write "AdvancedSettings"
        "UseAdvancedSettings": <boolean>,
        "AdvancedSettings": {
          "RequirePlayerPlaced": <boolean>,
          "PreventXPGrinding": {
            "Radius": <int>,
            "CooldownSeconds": <int>
          },
          "PlayerPermissionOverride": "Use LuckPerm at Here",
          "RequireBiome": [<biome>]
        }
      }

```

  ### 구조 설명

  | 필드                 | 타입   | 설명              |
| ------------------- | ----- | --------------- |
| `TypeItemName`  | String      | 대상 블록    |
| `EXP`        | int         | 기본 지급 경험치 범위    |
| `PlayerGetExp`   | int     | 플레이어 경험치 지급량 |
| `Chance`          | int    | 경험치 획득 확률 (%)   |
| `RequiredLevel`    | int   | 요구 스킬 레벨        |
| `RequiredTools`   | String    | 사용해야 하는 도구      |
| `ExtraEXP`       | int     | 추가 경험치 규칙       |
| `UseAdvancedSettings` | boolean | 고급 설정 사용 여부     |

### 2-1-2. 고급기능
  **고급기능설명**

  |       필드        |       타입      |        설명            |
  | --- | --- | --- |
  | UseAdvancedSettings | boolean | 고급모드 사용 설정 |
  | RequirePlayerPlaced | boolean | 플레이어가 설치한 블록일 때 |
  | PreventXPGrinding.Radius | int | |
  | PreventXPGrinding.CooldownSeconds | int | |
  | PlayerPermissionOverride | String | |
  | RequireBiome | String | |
  
