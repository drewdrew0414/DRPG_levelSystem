===============

# Made By drewdrew0414 (혹은 drewdrew1_)

===============

---

## 0. 목차
* [1. 최상위 구조](#1-최상위-구조)
* [2. Events 구조](#2-events-구조)
  * [2-1. BlockBreak 이벤트](#2-1-blockbreak-이벤트)
  * [2-2. BlockPlace 이벤트](#2-2-blockplace-이벤트)
  * [2-3. EnchantItem 이벤트](#2-3-enchantitem-이벤트)
  * [2-4. CraftItem 이벤트](#2-4-craftitem-이벤트)
* [3. 동작 흐름 요약](#3-동작-흐름-요약)
* [4. 주의사항](#4-주의사항)

---

## 1. 최상위 구조
스킬 설정 파일의 루트(Root) 데이터 구조입니다.

```json
{
  "RewardJsonVersion": "String",
  "Name": "String",
  "DisplayName": "String",
  "LevelDrainage": int,
  "MaxLevel": int,
  "Events": {
    // 하위 이벤트 데이터
  }
}
````

### 필드 상세 설명

| 필드                | 타입     | 설명                   |
| ----------------- | ------ | -------------------- |
| RewardJsonVersion | String | JSON 포맷 버전 정보        |
| Name              | String | 스킬의 고유 식별 ID         |
| DisplayName       | String | 유저 인터페이스(UI)에 표시될 이름 |
| LevelDrainage     | int    | 레벨업 난이도 계수           |
| MaxLevel          | int    | 최대 레벨                |
| Events            | Object | 경험치 획득 로직 이벤트 객체     |

---

## 2. Events 구조

각 이벤트는 특정 행동에 대한 보상 및 검증 규칙을 정의합니다.

### 2-1. BlockBreak 이벤트

* 정의: 플레이어가 블록을 파괴했을 때

[바로가기](How To Use/JSON/Skills/example/events/BlockBreak.md)
---

### 2-2. BlockPlace 이벤트

* 정의: 플레이어가 블록을 설치했을 때

```json
"BlockPlace": [
  {
    "TypeItemName": ["String"],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
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
      }
    }
  }
]
```

---

### 2-3. EnchantItem 이벤트

* 정의: 플레이어가 아이템 인챈트 시도 시

```json
"EnchantItem": [
  {
    "TypeItemName": ["String"],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
    "Chance": int,
    "RequiredLevel": int,
    "RequiredTools": ["String"],
    "ExtraEXP": {
      "multiplier": double,
      "bonusEXP": int
    },
    "UseAdvancedSettings": boolean,
    "AdvancedSettings": {
      "RequireItemUnbreaking": boolean,
      "PreventXPGrinding": {
        "Radius": int,
        "CooldownSeconds": int,
        "MaxBlocksInChunk": int,
        "MinLightLevel": int,
        "MaxDailyXPPerBlock": int
      },
      "ActionControl": {
        "AllowCreativeMode": boolean,
        "CancelExpIfCancelled": boolean
      }
    }
  }
]
```

---

### 2-4. CraftItem 이벤트

* 정의: 플레이어가 아이템 제작(Crafting) 시

```json
"CraftItem": [
  {
    "TypeItemName": ["String"],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
    "Chance": int,
    "RequiredLevel": int,
    "RequiredTools": ["String"],
    "ExtraEXP": {
      "multiplier": double,
      "bonusEXP": int
    },
    "UseAdvancedSettings": boolean,
    "AdvancedSettings": {
      "PreventXPGrinding": {
        "Radius": int,
        "CooldownSeconds": int,
        "MaxBlocksInChunk": int,
        "MinLightLevel": int,
        "MaxDailyXPPerBlock": int
      },
      "ActionControl": {
        "AllowCreativeMode": boolean,
        "CancelExpIfCancelled": boolean
      }
    }
  }
]
```

---

## 3. 동작 흐름 요약

1. 이벤트 발생
2. 조건 체크 (레벨, 도구, 환경 등)
3. EXP 계산
4. AdvancedSettings 적용
5. 플레이어에게 EXP 지급 및 로그 기록

---

## 4. 주의사항

* JSON 키, 타입, 대소문자를 정확히 맞출 것
* AdvancedSettings 적용 시 보상/검증 로직이 달라짐
* PreventXPGrinding 옵션 설정에 따라 XP 획득이 제한될 수 있음
