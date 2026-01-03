==========#####==========

# Made by drewdrew0414(or drewdrew1_)

==========#####==========

---

## Select Language / 언어 선택
* ## [English](#English)
* ## [한국어](#Korean)

---

## English
<a id="english"></a>

## 0. Table of Contents
* ### 1. [Rewards Json Compatibility Check](#eng1)
* ### 2. **Versions**
    * ### [1.0.0](#eng-1-0-0)
        * [Top-level Json Structure](#eng2-1-1)
        * [Basic Internal Structure](#eng2-1-2)
        * [Internal Structure (useRandom)](#eng2-1-3)
        * [Internal Structure (items)](#eng2-1-4)
* ### 3. [Precautions](#eng3)
* ### 4. [Example](#eng4)

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
"RewardJsonVersion": "<String>",
"Name": "<String>",
"DisplayName": "<String>",
"<int>": [ ... ] // Explained below
````

| Field             | Type   | Description                                                 | Example |
| ----------------- | ------ | ----------------------------------------------------------- | ------- |
| RewardJsonVersion | String | Defines the Reward Json version (must match plugin version) | 1.0.0   |
| Name              | String | Internal ID / name of the skill                             | Farming |
| DisplayName       | String | Name displayed to players                                   | Farming |
| "int"             | int    | Level at which the reward is given                          | 5, 10   |

---

### 2.2 Basic Internal Structure

<a id="eng2-1-2"></a>

```json
"<int>": [
  {
    "useRandom": <boolean>,
    "randomItems": [
      ... // Explained below
    ],
    "Permissions": <String>,
    "items": [
      {
        ... // Explained below
      }
    ]
  }
]
```

| Field       | Type    | Description                        | Example        |
| ----------- | ------- | ---------------------------------- | -------------- |
| useRandom   | boolean | Whether rewards are given randomly | false          |
| randomItems | Object  | Logic for random item selection    | See below      |
| Permissions | String  | Used for LuckPerms integration     | farming.reward |
| items       | Object  | Logic for guaranteed rewards       | See below      |

---

### 2.3 Internal Structure (useRandom)

<a id="eng2-1-3"></a>

```json
"randomItems": [
  {
    "0": [
      {
        "itemName": "<String>",
        "amount": <int>,
        "nbt": [ <String> ],
        "enchant": [ [ "<String>", <int> ], ... ],
        "exp": <int>
      }
    ],
    "1": [
      {
        "itemName": "<String>",
        "amount": <int>,
        "nbt": [ <String> ],
        "enchant": [ [ "<String>", <int> ] ],
        "exp": <int>
      }
    ]
    // ... more can be added
  }
]
```

| Field    | Type   | Description                      | Example         |
| -------- | ------ | -------------------------------- | --------------- |
| "int"    | int    | Must start from 0                | 0, 1, 2         |
| itemName | String | Item ID (UPPERCASE only)         | STONE           |
| amount   | int    | Item quantity                    | 8, 16, 32       |
| nbt      | String | NBT tags (supported from 1.2.0+) | WIP             |
| enchant  | List   | Enchantments to apply            | [UNBREAKING, 3] |
| exp      | int    | Experience given to player       | 100             |

---

### 2.4 Internal Structure (items)

<a id="eng2-1-4"></a>

```json
"items": [
  {
    "itemName": "<String>",
    "amount": <int>,
    "nbt": <String>,
    "enchant": [ [ "<String>", <int> ] ],
    "exp": <int>
  },
  {
    "itemName": "<String>",
    "amount": <int>,
    "nbt": <String>,
    "enchant": [ [ "<String>", <int> ] ],
    "exp": <int>
  }
]
```

| Field    | Type   | Description                      | Example         |
| -------- | ------ | -------------------------------- | --------------- |
| itemName | String | Item ID (UPPERCASE only)         | STONE           |
| amount   | int    | Item quantity                    | 8, 16, 32       |
| nbt      | String | NBT tags (supported from 1.2.0+) | WIP             |
| enchant  | List   | Enchantments to apply            | [UNBREAKING, 3] |
| exp      | int    | Experience given to player       | 100             |

---

## 3. Precautions

<a id="eng3"></a>

* Ensure `itemName` matches official Minecraft Material names (uppercase).
* `RewardJsonVersion` must be compatible with the plugin version.
* When using `randomItems`, indices must be sequential starting from `"0"`.

---

## 4. Example

<a id="eng4"></a>

[1.0.0 Farming.json Example](example/1.0.0/FarmingReward.json)

---

## 한국어
<a id="Korean"></a>

## 0. 목차
* ### 1. [Rewards Json 호환버전 확인](#kor1)
* ### 2. **버전**
    * ### [1.0.0](#1-0-0)
        * [Json 최상위 구조](#kor2-1-1)

        * [Json 기본 내부 구조](#kor2-1-2)

        * [Json 내부 구조 (useRandom)](#kor2-1-3)

        * [Json 내부 구조 (items)](#kor2-1-4)

* ### 3. [주의사항](#kor3)
* ### 4. [예제](#kor4)

---

## 1. 호환버전확인
<a id="kor1"></a>

| 플러그인 버전 | 호환되는 Rewards Json 버전 | 
|---|---|
| 1.0.0 | 1.0.0 |

---

## 2. 버전 별 Json 구조
<a id="kor2"></a>

## 1.0.0
<a id="1-0-0"></a>

* ### 2.1 최상위 구조
<a id="kor2-1-1"></a>

``` json
"RewardJsonVersion": "<String>",
"Name": "<String>",
"DisplayName": "<String>"
"<int>": [ ... ] // 밑에 설명 됨
```

| 필드명 | 타입 | 설명 | 예시 |
| --- | --- | --- | --- |
| RewardJsonVersion | String | Reward Json의 버전 정의 (플러그인의 버전에 맞게 설정 할 것) | 1.0.0 |
| Name | String | 해당 스킬의 이름 | Farming |
| DisplayName | String | 플레이어가 보게 될 스킬의 이름 | Farming |
| "int" | int | 보상을 주게 할 레벨 | 5, 10... |

* ### 2.2 기본 내부구조
<a id="kor2-1-2"></a>

```json
"<int>": [
    {
      "useRandom": <boolean>,
      "randomItems": [
        ... // 밑에 설명 됨
      ],
      "Permissions": <String>,
      "items": [
        {
            ... // 밑에 설명 됨
        }
      ]
    }
  ]
```

| 필드명 | 타입      | 설명                   | 예시             |
| --- |---------|----------------------|----------------|
|  useRandom   | boolean | 랜덤으로 보상을 줄 것인 지      | false          |
|  randomItems   |    아래에 설명     | 랜덤 아이템 선택 로직이 들어감    | 아래에 설명         |
|   Permissions  | String  | LuckPerms 연동 시 사용 가능 | farming.reward |
|   items  | 아래에 설명  | 지급 할 아이템의 로직이 들어감    | 아래에 설명         |

* ### 2.3 내부구조 (useRandom)
<a id="kor2-1-3"></a>

```json
"randomItems": [
        {
          "0": [ // 여러개 지급 할 시
            {
              "itemName": "<String>",
              "amount": <int>,
              "nbt": [ <String> ],
              "enchant": [ [<String>, <int> ], ... ],
              "exp": <int>
            },
            {
              "itemName": "<String>",
              "amount": <int>,
              "nbt": [ <String> ],
              "enchant": [ [<String>, <int> ], ... ],
              "exp": <int>
            }
          ],
          "1": [ // 한 개씩 지급 할 시 + 인첸트
            {
              "itemName": "<String>",
              "amount": <int>,
              "nbt": [ <String> ],
              "enchant": [ [<String>, <int> ] ],
              "exp": <int>
            }
          ],
          "2": [ // 인첸트가 여러개 일 시
            {
              "itemName": "<String>",
              "amount": <int>,
              "nbt": [ <String> ],
              "enchant": [ [<String>, <int> ], ... ],
              "exp": <int>
            }
          ]
          
          // ... 추가 가능
          
        }
      ]
```

| 필드명        | 타입       | 설명                                  | 예시               |
|------------|----------|-------------------------------------|------------------|
| "int"      | int      | 무조건 0에서 시작할 것                       | 0, 1, 2 ...      |
| itemName   | String   | 지급 할 아이템 이름 (대문자로 쓸 것)              |  STONE           |
| amount     | int      | 지급 할 아이템의 갯수                        | 8, 16, 32 ...    |
| nbt        | String   | 지급 할 아이템의 nbt 태그 부여 (1.2.0 이상부터 지원) | 미완성              |
| enchant    | String   | 지급 할 아이템에 넣을 인첸트                    | [UNBREAKING, 3 ] |
| exp        | int      | 플레이어에게 지급 할 경험치 (exp기준)             | 100              |

* ### 2.4 내부구조 (items)
<a id="kor2-1-4"></a>

```json
"items": [
        {
          "itemName": "<String>",
          "amount": <int>,
          "nbt": <String>,
          "enchant": [ [ <String>, <int>] ],
          "exp": <int>
        }, // 여러 개 일 시 중첩법
        {
          "itemName": "<String>",
          "amount": <int>,
          "nbt": <String>,
          "enchant": [ [ <String>, <int>] ],
          "exp": <int>
          }
      ]
```

| 필드명        | 타입       | 설명                                  | 예시               |
|------------|----------|-------------------------------------|------------------|
| itemName   | String   | 지급 할 아이템 이름 (대문자로 쓸 것)              |  STONE           |
| amount     | int      | 지급 할 아이템의 갯수                        | 8, 16, 32 ...    |
| nbt        | String   | 지급 할 아이템의 nbt 태그 부여 (1.2.0 이상부터 지원) | 미완성              |
| enchant    | String   | 지급 할 아이템에 넣을 인첸트                    | [UNBREAKING, 3 ] |
| exp        | int      | 플레이어에게 지급 할 경험치 (exp기준)             | 100              |

---

## 3. 주의사항
<a id="kor3"></a>
* ​itemName은 공식 마인크래프트 아이템 명칭(Material Name)과 일치해야 하며, 반드시 대문자로 작성해야 합니다.
* ​RewardJsonVersion은 현재 사용 중인 플러그인 버전과 호환되어야 로딩 오류를 방지할 수 있습니다.
* ​randomItems를 사용할 때, 인덱스(번호)는 반드시 **"0"**부터 시작하여 순차적으로 작성해야 합니다.
---

## 4. 예제
<a id="kor4"></a>
[1.0.0 Farming.json 예제](example/1.0.0/FarmingReward.json)
