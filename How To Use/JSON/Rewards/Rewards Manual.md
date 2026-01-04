==========#####==========

# Made by drewdrew0414(or drewdrew1_)

==========#####==========

---

## Select Language / 언어 선택
* ## [English](#English)
* ## [한국어](#Korean)

---

## English
<a id="English"></a>

## 0. Table of Contents
* ### 1. [Rewards Json Compatibility Check](#eng1)
* ### 2. Versions
    * ### [1.0.0](#eng-1-0-0)
        * [Top-level Json Structure](#eng2-1-1)
        * [Basic Internal Structure](#eng2-1-2)
        * [Internal Structure (useRandom)](#eng2-1-3)
        * [Internal Structure (items)](#eng2-1-4)
        * [Internal Structure (effects)](#eng2-1-5)
* ### 3. [Precautions](#eng3)
* ### 4. [Error Conditions](#eng-error)
* ### 5. [Case Examples](#eng-case)

---

## 1. Compatibility Check
<a id="eng1"></a>

| Plugin Version | Compatible Rewards Json Version |
|---|---|
| 1.0.0 | 1.0.0 |

---

## 2. Json Structure by Version
<a id="eng2"></a>

## 1.0.0
<a id="eng-1-0-0"></a>

### 2.1 Top-level Json Structure
<a id="eng2-1-1"></a>

```json
{
  "RewardJsonVersion": "1.0.0",
  "Name": "Farming",
  "displayName": "Farming",

  "<level>": [
    { }
  ]
}
```

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| RewardJsonVersion | String | Defines the Reward Json version | 1.0.0 |
| Name | String | Internal ID of the skill | Farming |
| displayName | String | Name displayed to players | Farming |
| <level> | String | Level at which the reward is given (Must be string) | "5", "10" |

---

### 2.2 Basic Internal Structure
<a id="eng2-1-2"></a>

```json
"<level>": [
  {
    "useRandom": false,
    "randomValue": 0,
    "randomItems": [],
    "Permissions": null,
    "effects": [],
    "title": null,
    "items": []
  }
]
```

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| useRandom | boolean | Enable random reward logic | true / false |
| randomValue | int | Number of random groups to select | 1, 2 |
| randomItems | Array | Random reward pool groups | [ { "0": [...] } ] |
| Permissions | String | LuckPerms permission node | farming.reward |
| effects | Array | Potion or custom effects | See 2.5 |
| title | String | Title message displayed on screen | "Master" |
| items | Array | Guaranteed reward items | See 2.4 |

---

### 2.3 Internal Structure (useRandom)
<a id="eng2-1-3"></a>

```json
"randomItems": [
  {
    "0": [
      {
        "itemName": "BREAD",
        "amount": 8,
        "nbt": [],
        "enchant": [],
        "exp": 0
      }
    ]
  }
]
```

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| "int" | String | Index group (Must start from "0") | "0", "1" |
| itemName | String | Minecraft Material Name (UPPERCASE) | STONE |
| amount | int | Quantity of the item | 64 |
| nbt | Array | NBT tags (List format) | [] |
| enchant | Array | Enchantments [ ["NAME", Level] ] | [ ["FORTUNE", 3] ] |
| exp | int | Experience points given | 100 |

---

### 2.4 Internal Structure (items)
<a id="eng2-1-4"></a>

```json
"items": [
  {
    "itemName": "WHEAT",
    "amount": 64,
    "nbt": [],
    "enchant": [],
    "exp": 0
  }
]
```

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| itemName | String | Minecraft Material Name (UPPERCASE) | WHEAT |
| amount | int | Quantity of the item | 32 |
| nbt | Array | NBT tags | [] |
| enchant | Array | Enchantments | [ ["EFFICIENCY", 5] ] |
| exp | int | Experience points given | 50 |

---

### 2.5 Internal Structure (effects)
<a id="eng2-1-5"></a>

```json
"effects": [
  {
    "type": "SPEED",
    "level": 1,
    "time": 200,
    "cooltime": 0
  }
]
```

| Field | Type | Description | Example |
| :--- | :--- | :--- | :--- |
| type | String | Potion Effect Type | SPEED, HASTE |
| level | int | Potency level (Starting from 1) | 1, 2 |
| time | int | Duration in ticks (0 for infinite) | 200 |
| cooltime | int | Cooldown before next use | 0 |

---

## 3. Precautions
<a id="eng3"></a>
* `itemName` must match **Minecraft Material (UPPERCASE)**.
* `RewardJsonVersion` must match plugin version.
* `randomItems` index must start at `"0"` and be sequential.
* `<level>` key must be a **string**.

---

## 4. Error Conditions
<a id="eng-error"></a>
* `useRandom = true` but `randomItems` is empty.
* `randomValue` > number of groups in `randomItems`.
* Missing required fields or invalid Level key type.

---

## 5. Case Examples
<a id="eng-case"></a>

---

## 한국어
<a id="Korean"></a>

## 0. 목차
* ### 1. [Rewards Json 호환버전 확인](#kor1)
* ### 2. 버전
  * ### [1.0.0](#kor-1-0-0)
    * [Json 최상위 구조](#kor2-1-1)
    * [Json 기본 내부 구조](#kor2-1-2)
    * [Json 내부 구조 (useRandom)](#kor2-1-3)
    * [Json 내부 구조 (items)](#kor2-1-4)
    * [Json 내부 구조 (effects)](#kor2-1-5)
* ### 3. [주의사항](#kor3)
* ### 4. [에러 조건](#kor-error)
* ### 5. [케이스별 예제](#kor-case)

---

## 1. 호환버전확인
<a id="kor1"></a>

| 플러그인 버전 | Rewards Json 버전 |
| ------- | --------------- |
| 1.0.0   | 1.0.0           |

---

## 2. 버전 별 Json 구조
<a id="kor2"></a>

## 1.0.0
<a id="kor-1-0-0"></a>

### 2.1 Json 최상위 구조
<a id="kor2-1-1"></a>

```json
{
  "RewardJsonVersion": "1.0.0",
  "Name": "Farming",
  "displayName": "Farming",

  "<레벨>": [
    { }
  ]
}
```

| 필드명 | 타입 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| RewardJsonVersion | String | 보상 파일의 버전 정의 | 1.0.0 |
| Name | String | 스킬의 내부 고유 이름 | Farming |
| displayName | String | 플레이어에게 표시될 이름 | 농사 보상 |
| <레벨> | String | 보상이 지급될 레벨 (반드시 문자열) | "5", "10" |

---

### 2.2 Json 기본 내부 구조
<a id="kor2-1-2"></a>

```json
"<레벨>": [
  {
    "useRandom": false,
    "randomValue": 0,
    "randomItems": [],
    "Permissions": null,
    "effects": [],
    "title": null,
    "items": []
  }
]
```

| 필드명 | 타입 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| useRandom | boolean | 랜덤 보상 로직 사용 여부 | true / false |
| randomValue | int | 랜덤 그룹 중 선택할 개수 | 1, 2 |
| randomItems | Array | 랜덤 보상 아이템 그룹 리스트 | [ { "0": [...] } ] |
| Permissions | String | LuckPerms 권한 노드 | skill.farming.5 |
| effects | Array | 부여할 포션 및 특수 효과 리스트 | 하단 2.5 참조 |
| title | String | 화면 중앙에 뜰 타이틀 메시지 | "레벨 업!" |
| items | Array | 확정 지급 아이템 리스트 | 하단 2.4 참조 |

---

### 2.3 Json 내부 구조 (useRandom)
<a id="kor2-1-3"></a>

```json
"randomItems": [
  {
    "0": [
      {
        "itemName": "BREAD",
        "amount": 8,
        "nbt": [],
        "enchant": [],
        "exp": 0
      }
    ]
  }
]
```

| 필드명 | 타입 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| "인덱스" | String | 그룹 번호 (반드시 "0"부터 시작) | "0", "1" |
| itemName | String | 마인크래프트 아이템 명칭 (대문자) | STONE |
| amount | int | 지급할 아이템의 수량 | 64 |
| nbt | Array | NBT 태그 정보 (리스트 형식) | [] |
| enchant | Array | 인챈트 설정 [ ["이름", 레벨] ] | [ ["FORTUNE", 3] ] |
| exp | int | 지급할 경험치량 | 100 |

* ### 인덱스는 반드시 `"0"`부터 시작해야 함
* ### 순차적으로 증가해야 함 (0, 1, 2...)
* ### randomValue는 설정된 인덱스 그룹의 총 개수를 초과할 수 없음

---

### 2.4 Json 내부 구조 (items)
<a id="kor2-1-4"></a>

```json
"items": [
  {
    "itemName": "WHEAT",
    "amount": 64,
    "nbt": [],
    "enchant": [],
    "exp": 0
  }
]
```

| 필드명 | 타입 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| itemName | String | 마인크래프트 아이템 명칭 (대문자) | DIAMOND_HOE |
| amount | int | 지급 수량 | 1 |
| nbt | Array | NBT 태그 정보 | [] |
| enchant | Array | 인챈트 설정 [ ["이름", 레벨] ] | [ ["UNBREAKING", 3] ] |
| exp | int | 지급할 경험치량 | 100 |

---

### 2.5 Json 내부 구조 (effects)
<a id="kor2-1-5"></a>

```json
"effects": [
  {
    "type": "SPEED",
    "level": 1,
    "time": 200,
    "cooltime": 0,
    "operator": "AND",
    "when": [
      { "<String>": "<String>" }
    ]
  }
]
```

| 필드명 | 타입 | 설명 | 예시 |
| :--- | :--- | :--- | :--- |
| type | String | 포션 효과 종류 | HASTE, SPEED |
| level | int | 효과 강도 (1레벨부터 시작) | 2 |
| time | int | 지속 시간 (Tick 단위, 20틱=1초) | 600 |
| cooltime | int | 효과 재발동 대기 시간 | 0 |
| operator | String | 효과 발동 조건 연산자 | AND, OR |
| when | Array | 발동 트리거 리스트 | 하단 참조 |

### when 내부에서 사용가능한 이벤트들

| 조건 | 설명 | 내부구조 |
| --- | --- | --- |
| GET_DMG | 데미지를 입었을 때 | [참고](#ex1) |
| SNEAKING | 웅크릴 때 | [참고](#ex2) |
| L_CLICK | 좌클릭 했을 때 | [참고](#ex3) |
| R_CLICK | 우클릭 했을 때 | [참고](#ex4) |
| HOLDING_ITEM | 아이템을 손에 들고 있을 때 | [참고](#ex5) |
| INTERACT_ENTITY | 엔티티와 상호작용 했을 때 | [참고](#ex6) |
| INTERACT_BLOCK | 블록과 상호작용 했을 때 | [참고](#ex7) |
| KILL_ENTITY | 엔티티를 죽였을 때 | [참고](#ex8) |
| HP_REMAINING | 피가 <int>만큼 남았을 때 | [참고](#ex9) |

### GET_DMG
<a id="ex1"></a>

```json
"effect": [
    {
      // 기본 로직
      "when": [
      { "GET_DMG": [
          {
            "cause": [ "<String>" ],
            "by": [ "<String" ],
            "
          }
        ]
      }
    ]
  }
]

```

---

## 3. 주의사항
<a id="kor3"></a>
* ### 아이템 이름은 반드시 **대문자 Material** 명칭을 사용해야 합니다.
* ### 레벨 키는 반드시 **문자열** 형식이어야 합니다. (예: "5")
* ### randomValue가 그룹 수보다 많으면 로딩 에러가 발생합니다.

---

## 4. 에러 조건
<a id="kor-error"></a>
* ### 랜덤 설정(`useRandom = true`) 시 보상 풀(`randomItems`)이 비어있는 경우
* ### 필수 필드(RewardJsonVersion 등)가 누락된 경우
* ### 인챈트나 효과 이름이 올바르지 않은 경우

---

## 5. 케이스별 예제
<a id="kor-case"></a>

### 랜덤 지급 (Random Only)
```json
"5": [
  {
    "useRandom": true,
    "randomValue": 1,
    "randomItems": [
      {
        "0": [{ "itemName": "BREAD", "amount": 8, "nbt": [], "enchant": [], "exp": 0 }],
        "1": [{ "itemName": "COOKED_BEEF", "amount": 6, "nbt": [], "enchant": [], "exp": 0 }]
      }
    ],
    "Permissions": null,
    "effects": [],
    "title": "행운의 보상",
    "items": []
  }
]
```

### 고정 지급 (Items Only)
```json
"10": [
  {
    "useRandom": false,
    "randomValue": 0,
    "randomItems": [],
    "Permissions": null,
    "effects": [],
    "title": null,
    "items": [
      { "itemName": "WHEAT", "amount": 64, "nbt": [], "enchant": [], "exp": 0 }
    ]
  }
]
```
