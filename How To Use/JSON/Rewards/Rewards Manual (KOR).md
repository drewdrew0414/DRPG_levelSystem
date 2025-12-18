===============

# Made By drewdrew0414(or drewdrew1_)

===============

## 0. 목차

* [1. Rewards JSON 개요](#1-rewards-json-개요)
* [2. 최상위 구조](#2-최상위-구조)
* [3. 레벨 보상 구조](#3-레벨-보상-구조)
* [4. 보상 설정 객체](#4-보상-설정-객체)
* [5. 확정 보상 (items)](#5-확정-보상-items)
* [6. 인챈트 구조](#6-인챈트-구조)
* [7. 랜덤 보상 구조](#7-랜덤-보상-구조)
* [8. 랜덤 아이템 그룹 구조](#8-랜덤-아이템-그룹-구조)
* [9. 권한 (Permissions)](#9-권한-permissions)
* [10. 동작 흐름 요약](#10-동작-흐름-요약)
* [11. 주의사항](#11-주의사항)
* [12. 보상 JSON 예시 (Farming)](#12-보상-json-예시-farming)

---

## 1. Rewards JSON 개요

* 각 보상 JSON 파일은 **하나의 스킬**에 대응된다.
* 스킬의 레벨 도달 시점마다 **서로 다른 보상 규칙**을 설정할 수 있다.
* Java 코드 수정 없이 JSON 파일만으로 보상 구조를 변경할 수 있다.

---

## 2. 최상위 구조

```json
{
  "RewardJsonVersion": "1.0.0",
  "Name": "SkillName",
  "displayName": "Display Name",
  "레벨": [ 보상 정의 배열 ]
}
```

### 필드 설명

| 필드                  | 타입             | 설명                        |
| ------------------- | -------------- | ------------------------- |
| `RewardJsonVersion` | String         | 보상 JSON 포맷 버전             |
| `Name`              | String         | 내부 식별용 이름 (스킬 ID와 반드시 일치) |
| `displayName`       | String         | 화면 및 로그에 표시될 이름           |
| `"레벨"`              | String(Number) | 보상이 지급되는 스킬 레벨            |

⚠️ **레벨 키는 반드시 문자열 형태의 숫자여야 한다.**

---

## 3. 레벨 보상 구조

```json
"10": [
  {
    보상 설정 객체
  }
]
```

* 하나의 레벨에 **여러 개의 보상 조건**을 정의할 수 있음
* 배열 구조이므로 추후 확장에 유리

---

## 4. 보상 설정 객체

```json
{
  "useRandom": false,
  "Permissions": null,
  "items": []
}
```

### 필드 설명

| 필드            | 타입            | 설명            |
| ------------- | ------------- | ------------- |
| `useRandom`   | boolean       | 랜덤 보상 사용 여부   |
| `Permissions` | String / null | 보상 지급에 필요한 권한 |
| `items`       | Array         | 확정 지급 아이템 목록  |

---

## 5. 확정 보상 (items)

```json
"items": [
  {
    "itemName": "ITEM_ID",
    "amount": 1,
    "nbt": null,
    "enchant": [],
    "exp": 0
  }
]
```

| 필드         | 타입            | 설명                 |
| ---------- | ------------- | ------------------ |
| `itemName` | String        | Bukkit Material 이름 |
| `amount`   | int           | 지급 개수              |
| `nbt`      | Object / null | 커스텀 NBT 데이터        |
| `enchant`  | Array         | 아이템 인챈트 목록         |
| `exp`      | int           | 추가 지급 경험치          |

---

## 6. 인챈트 구조

```json
"enchant": [
  ["ENCHANT_NAME", 1]
]
```

* 첫 번째 값: 인챈트 이름
* 두 번째 값: 인챈트 레벨

---

## 7. 랜덤 보상 구조

```json
{
  "useRandom": true,
  "randomValue": 3,
  "randomItems": [],
  "Permissions": null,
  "items": []
}
```

| 필드            | 설명                  |
| ------------- | ------------------- |
| `randomValue` | 랜덤 선택 범위 (0 ~ N)    |
| `randomItems` | 랜덤 보상 그룹            |
| `items`       | 랜덤 사용 시 비워두는 것이 일반적 |

---

## 8. 랜덤 아이템 그룹 구조

```json
"randomItems": [
  {
    "0": [ 아이템 배열 ],
    "1": [ 아이템 배열 ]
  }
]
```

* 숫자 키는 랜덤 선택 인덱스
* 선택된 키에 포함된 **모든 아이템이 지급됨**

---

## 9. 권한 (Permissions)

```json
"Permissions": "plugin.reward.example"
```

* `null` → 누구나 지급
* 문자열 → 해당 권한 필요
* LuckPerms 등 권한 플러그인과 연동 가능

---

## 10. 동작 흐름 요약

1. 플레이어가 스킬 레벨 도달
2. 해당 레벨 보상 확인
3. 권한 검사
4. 랜덤 여부 판단
5. 보상 지급
6. 중복 보상 여부는 config 설정에 따름

---

## 11. 주의사항

* 레벨 키는 반드시 문자열 숫자
* `useRandom = true`일 때 `items`는 무시됨
* JSON 오류 발생 시 해당 보상만 스킵됨
* `Name`과 스킬 ID가 다르면 작동하지 않음

---

## 12. 보상 JSON 예시 (Farming)

> 아래는 **위 구조를 실제로 적용한 예시 파일**이다.

```json
{
  "RewardJsonVersion": "1.0.0",
  "Name": "Farming",
  "displayName": "Farming",
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
  ],
  "10": [
    {
      "useRandom": true,
      "randomValue": 3,
      "randomItems": [
        {
          "0": [ { "itemName": "WHEAT", "amount": 32, "nbt": null, "enchant": [], "exp": 0 } ],
          "1": [ { "itemName": "POTATO", "amount": 48, "nbt": null, "enchant": [], "exp": 0 } ]
        }
      ],
      "Permissions": null,
      "items": []
    }
  ]
}
```

---
