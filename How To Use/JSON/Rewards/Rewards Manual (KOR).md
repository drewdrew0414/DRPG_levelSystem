==========#####==========

# Made by drewdrew0414(or drewdrew1_)

==========#####==========

---

## Select Language / 언어 선택
* ## [English](#English)
* ## [한국어](#한국어)

---

## English

## 0. Table of Contents
* ### 1.
---

## 한국어

## 0. 목차
* ### 1. [Rewards Json 호환버전 확인](#kor1)
* ### 2. **버전**
    * ### [1.0.0](#1-0-0)
        * [Json 최상위 구조](#kor2-1-1)

        * [Json 기본 내부 구조](#kor2-1-2)

        * [Json 내부 구조 (useRandom)](#kor2-1-3)

        * [Json 내부 구조 (items)](#kor2-1-4)

* ### 3. [주의사항](#)
* ### 4. [예제](#)

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

---

## 4. 예제
<a id="kor4"></a>
[1.0.0 Farming.json 예제](example/1.0.0/FarmingReward.json)