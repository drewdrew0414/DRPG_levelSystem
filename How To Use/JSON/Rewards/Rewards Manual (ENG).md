===============

# Made By drewdrew0414(or drewdrew1_)

===============

## 0. Table of Contents

* [1. Rewards JSON Overview](#1-rewards-json-overview)
* [2. Top-Level Structure](#2-top-level-structure)
* [3. Level Reward Structure](#3-level-reward-structure)
* [4. Reward Configuration Object](#4-reward-configuration-object)
* [5. Fixed Rewards (items)](#5-fixed-rewards-items)
* [6. Enchantment Structure](#6-enchantment-structure)
* [7. Random Reward Structure](#7-random-reward-structure)
* [8. Random Item Group Structure](#8-random-item-group-structure)
* [9. Permissions](#9-permissions)
* [10. Execution Flow Summary](#10-execution-flow-summary)
* [11. Notes & Warnings](#11-notes--warnings)
* [12. Reward JSON Example (Farming)](#12-reward-json-example-farming)

---

## 1. Rewards JSON Overview

* Each reward JSON file corresponds to **one skill**.
* Different rewards can be configured for **each skill level milestone**.
* All reward logic can be customized **without modifying Java code**, using JSON only.

---

## 2. Top-Level Structure

```json
{
  "RewardJsonVersion": "1.0.0",
  "Name": "SkillName",
  "displayName": "Display Name",
  "level": [ reward definitions ]
}
```

### Field Description

| Field               | Type           | Description                                   |
| ------------------- | -------------- | --------------------------------------------- |
| `RewardJsonVersion` | String         | Reward JSON format version                    |
| `Name`              | String         | Internal identifier (must match the skill ID) |
| `displayName`       | String         | Name displayed in UI and logs                 |
| `"level"`           | String(Number) | Skill level at which rewards are granted      |

⚠️ **Level keys must be numeric values written as strings.**

---

## 3. Level Reward Structure

```json
"10": [
  {
    reward configuration object
  }
]
```

* Multiple reward conditions can be defined for a single level
* Uses an array structure for future extensibility

---

## 4. Reward Configuration Object

```json
{
  "useRandom": false,
  "Permissions": null,
  "items": []
}
```

### Field Description

| Field         | Type          | Description                               |
| ------------- | ------------- | ----------------------------------------- |
| `useRandom`   | boolean       | Whether this reward uses random selection |
| `Permissions` | String / null | Required permission to receive the reward |
| `items`       | Array         | Fixed reward item list                    |

---

## 5. Fixed Rewards (`items`)

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

| Field      | Type          | Description                      |
| ---------- | ------------- | -------------------------------- |
| `itemName` | String        | Bukkit Material name             |
| `amount`   | int           | Amount to give                   |
| `nbt`      | Object / null | Custom NBT data                  |
| `enchant`  | Array         | Enchantments applied to the item |
| `exp`      | int           | Extra experience granted         |

---

## 6. Enchantment Structure

```json
"enchant": [
  ["ENCHANT_NAME", 1]
]
```

* First value: Enchantment name
* Second value: Enchantment level

---

## 7. Random Reward Structure

```json
{
  "useRandom": true,
  "randomValue": 3,
  "randomItems": [],
  "Permissions": null,
  "items": []
}
```

| Field         | Description                               |
| ------------- | ----------------------------------------- |
| `randomValue` | Random selection range (0 ~ N)            |
| `randomItems` | Random reward groups                      |
| `items`       | Usually left empty when random is enabled |

---

## 8. Random Item Group Structure

```json
"randomItems": [
  {
    "0": [ item array ],
    "1": [ item array ]
  }
]
```

* Numeric keys represent **random selection indices**
* One index is selected based on `randomValue`
* **All items under the selected index are granted**

---

## 9. Permissions

```json
"Permissions": "plugin.reward.example"
```

* `null` → Reward is granted to everyone
* String → Player must have the specified permission
* Compatible with permission plugins such as LuckPerms

---

## 10. Execution Flow Summary

1. Player reaches a skill level
2. Reward configuration for that level is found
3. Permission check is performed
4. Random or fixed reward logic is determined
5. Rewards are granted
6. Duplicate rewards are handled based on `config.json`

---

## 11. Notes & Warnings

* Level keys **must** be numeric strings
* When `useRandom = true`, `items` is ignored
* JSON syntax errors skip only the affected reward
* If `Name` does not match the skill ID, rewards will not be granted

---

## 12. Reward JSON Example (Farming)

> This is a **practical example** using the structure described above.

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
          "0": [
            {
              "itemName": "WHEAT",
              "amount": 32,
              "nbt": null,
              "enchant": [],
              "exp": 0
            }
          ],
          "1": [
            {
              "itemName": "POTATO",
              "amount": 48,
              "nbt": null,
              "enchant": [],
              "exp": 0
            }
          ]
        }
      ],
      "Permissions": null,
      "items": []
    }
  ]
}
```

---
