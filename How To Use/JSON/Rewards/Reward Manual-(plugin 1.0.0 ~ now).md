---

# **DRPG Level System: Reward JSON Guide / 보상 JSON 사용 가이드**

---

## **1. Introduction / 소개**

**EN:**
This JSON defines rewards for players when they reach certain levels in a skill.
It supports both fixed and random rewards, item enchantments, experience points, and permission checks.

**KR:**
이 JSON은 플레이어가 특정 스킬 레벨에 도달했을 때 지급되는 보상을 정의합니다.
고정 보상, 랜덤 보상, 아이템 인챈트, 경험치, 권한 체크를 모두 지원합니다.

---

## **2. Overall Structure / 전체 구조**

```json
{
  "Name": "Farming",
  "displayName": "Farming",
  "5": [ ... ],
  "10": [ ... ],
  "15": [ ... ],
  ...
  "50": [ ... ]
}
```

**EN:**

* `"Name"`: Internal ID for the skill.
* `"displayName"`: Display name for players.
* Numbers like `"5"`, `"10"` … `"50"`: Skill level at which rewards are given.
* Each number key contains a list of reward objects.

**KR:**

* `"Name"`: 스킬 내부 ID
* `"displayName"`: 플레이어에게 보이는 이름
* 숫자 키 `"5"`, `"10"` … `"50"`: 해당 레벨에 지급되는 보상
* 각 레벨 키는 보상 객체 목록을 포함

---

## **3. Level Sections / 레벨별 보상 섹션**

**EN:** Each level can have multiple reward objects.
Each reward object may contain fixed items or random items.

* `"useRandom"`: `true` if the reward should randomly pick from `"randomItems"`.
* `"randomValue"`: Number of items to pick randomly if `"useRandom"` is true.
* `"randomItems"`: Object with numbered keys (`0`, `1`, …) containing lists of possible items.
* `"items"`: Items that are always given.
* `"Permissions"`: Optional permission required to receive the reward.

**KR:**

* 각 레벨은 여러 보상 객체를 가질 수 있습니다.
* `"useRandom"`: `true`이면 `"randomItems"` 중 랜덤 선택
* `"randomValue"`: 선택할 랜덤 아이템 개수
* `"randomItems"`: 인덱스(`0`, `1`, …)별 아이템 리스트
* `"items"`: 항상 지급되는 아이템
* `"Permissions"`: 권한 필요 시 지정

---

## **4. Item Object / 아이템 객체**

```json
{
  "itemName": "DIAMOND_HOE",
  "amount": 1,
  "nbt": null,
  "enchant": [
    ["UNBREAKING", 5],
    ["EFFICIENCY", 5],
    ["FORTUNE", 3]
  ],
  "exp": 0
}
```

**EN:**

* `"itemName"`: Minecraft item ID
* `"amount"`: Number of items to give
* `"nbt"`: Optional NBT data
* `"enchant"`: List of enchantments `[NAME, LEVEL]`
* `"exp"`: Experience points to give

**KR:**

* `"itemName"`: 마인크래프트 아이템 ID
* `"amount"`: 지급 수량
* `"nbt"`: 선택적 NBT 데이터
* `"enchant"`: 인챈트 리스트 `[이름, 레벨]`
* `"exp"`: 지급할 경험치

---

## **5. Example: Fixed Items / 예시: 고정 보상**

```json
"5": [
  {
    "useRandom": false,
    "Permissions": null,
    "items": [
      {
        "itemName": "BONE",
        "amount": 16,
        "nbt": null,
        "enchant": [],
        "exp": 0
      }
    ]
  }
]
```

**EN:**

* Level 5 reward gives 16 bones.
* `"useRandom"` is false, so all listed items are given.
* No permission required.

**KR:**

* 레벨 5 보상으로 뼈 16개 지급
* `"useRandom"`이 false이므로 리스트에 있는 모든 아이템 지급
* 권한 필요 없음

---

## **6. Example: Random Items / 예시: 랜덤 보상**

```json
"10": [
  {
    "useRandom": true,
    "randomValue": 3,
    "randomItems": [
      {
        "0": [
          { "itemName": "WHEAT", "amount": 32, "nbt": null, "enchant": [], "exp": 0 },
          { "itemName": "WHEAT_SEEDS", "amount": 16, "nbt": null, "enchant": [], "exp": 0 }
        ],
        "1": [
          { "itemName": "POTATO", "amount": 48, "nbt": null, "enchant": [], "exp": 0 }
        ],
        "2": [
          { "itemName": "CARROT", "amount": 48, "nbt": null, "enchant": [], "exp": 0 }
        ]
      }
    ],
    "Permissions": null,
    "items": []
  }
]
```

**EN:**

* Level 10 reward uses random selection.
* `"randomValue": 3` → picks 3 items from `"randomItems"`.
* Each index contains possible items to pick from.
* No fixed items in `"items"` array.

**KR:**

* 레벨 10 보상은 랜덤 선택
* `"randomValue": 3` → `"randomItems"`에서 3개 선택
* 각 인덱스(`0`, `1`, `2`)는 선택 가능한 아이템 목록
* `"items"` 배열에는 고정 보상 없음

---

## **7. Permissions / 권한 설정**

**EN:**

* `"Permissions"`: Optional field to restrict rewards.
* Null = everyone can receive.

**KR:**

* `"Permissions"`: 보상 수령 권한 제한
* null이면 모든 플레이어 가능

---

## **8. Notes / 주의 사항**

* Always use valid Minecraft item IDs in `"itemName"`.
* Enchantments must follow `[ENCHANT_NAME, LEVEL]` format.
* Random items only work if `"useRandom"` is true.
* Level keys (`5`, `10`, …) must match actual skill levels.

**KR:**

* `"itemName"`에는 항상 유효한 마인크래프트 아이템 ID 사용
* 인챈트는 `[인챈트 이름, 레벨]` 형식 사용
* 랜덤 아이템은 `"useRandom"`이 true일 때만 작동
* 레벨 키(`5`, `10`, …)는 실제 스킬 레벨과 일치해야 함

---
