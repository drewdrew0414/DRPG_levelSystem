# **DRPG Level System: Complete Event JSON Manual / 완전 이벤트 JSON 매뉴얼**

---

## **Table of Contents / 목차**

1. [Introduction / 소개](#introduction--소개)
2. [JSON Structure / JSON 구조](#json-structure--json-구조)
3. [Event Examples / 이벤트 예시](#event-examples--이벤트-예시)

   1. [BlockBreakEvent / 블록 파괴 이벤트](#1-blockbreakevent--블록-파괴-이벤트)
   2. [BlockPlaceEvent / 블록 설치 이벤트](#2-blockplaceevent--블록-설치-이벤트)
   3. [PlayerFishEvent / 낚시 이벤트](#3-playerfishevent--낚시-이벤트)
   4. [EntityDeathEvent / 엔티티 사망 이벤트](#4-entitydeathevent--엔티티-사망-이벤트)
   5. [PlayerRunEvent / 달리기 이벤트 (주기적)](#5-playerrunevent--달리기-이벤트-주기적)
   6. [PlayerToggleSneakEvent / 스니크 전환 이벤트](#6-playertogglesneakevent--스니크-전환-이벤트)
   7. [EntityDamageByEntityEvent / 엔티티 공격 이벤트](#7-entitydamagebyentityevent--엔티티-공격-이벤트)
   8. [EntityRegainHealthEvent / 체력 회복 이벤트](#8-entityregainhealthevent--체력-회복-이벤트)
   9. [PlayerInteractEvent / 블록/아이템 상호작용 이벤트](#9-playerinteractevent--블록아이템-상호작용-이벤트)
   10. [EntityBreedEvent / 엔티티 번식 이벤트](#10-entitybreedevent--엔티티-번식-이벤트)
   11. [PlayerToggleFlightEvent / 비행 전환 이벤트](#11-playertoggleflightevent--비행-전환-이벤트)
   12. [PlayerSwimEvent / 수영 이벤트](#12-playerswimevent--수영-이벤트)
   13. [ProjectileHitEvent / 투사체 적중 이벤트](#13-projectilehitevent--투사체-적중-이벤트)

---

## **Introduction / 소개**

**EN:**
The DRPG Level System plugin allows detailed configuration of player skills using JSON files. Each event type can trigger EXP rewards based on player actions.
This manual explains the structure, fields, and usage for each event type to help server admins customize skills efficiently.

**KR:**
DRPG 레벨 시스템 플러그인은 JSON 파일을 통해 플레이어 스킬을 세부적으로 설정할 수 있습니다.
각 이벤트 유형은 플레이어 행동에 따라 EXP를 지급하며, 서버 관리자가 스킬을 효율적으로 커스터마이징할 수 있도록 구조, 필드, 사용법을 설명합니다.

---

## **JSON Structure / JSON 구조**

| Field             | Type         | EN Description                                     | KR 설명                   |
| ----------------- | ------------ | -------------------------------------------------- | ----------------------- |
| Event             | String       | Event type (e.g., BlockBreakEvent, PlayerRunEvent) | 이벤트 타입                  |
| Name              | Array/String | Target block/entity/item/action names              | 이벤트 대상 블록/엔티티/아이템/행동 이름 |
| EXP               | Object       | Minimum and maximum EXP granted                    | 지급되는 최소/최대 EXP          |
| PlayerExp         | Int          | Internal tracking of player EXP                    | 플레이어 EXP 내부 추적용         |
| Chance            | Int          | Probability to grant EXP (0-100%)                  | EXP 지급 확률               |
| LevelRequired     | Int          | Minimum skill level required                       | 이벤트 발생 최소 스킬 레벨         |
| Tools             | Array        | Required items/tools                               | 이벤트 발생 필요 아이템/도구        |
| BonusMultiplier   | Double       | Additional EXP multiplier                          | EXP 보너스 배율              |
| PenaltyMultiplier | Double       | Penalty multiplier                                 | EXP 패널티 배율              |
| StartDelayMs      | Int          | Delay before first EXP (periodic events)           | 반복 이벤트 최초 지급 지연 시간      |
| RepeatIntervalMs  | Int          | Interval between repeated EXP (periodic)           | 반복 이벤트 EXP 간격           |

> **EN:** `StartDelayMs` and `RepeatIntervalMs` are used for periodic actions like running, swimming, or flying.
> **KR:** `StartDelayMs`와 `RepeatIntervalMs`는 달리기, 수영, 비행 등 반복 행동 이벤트에 사용됩니다.

---

## **Event Examples / 이벤트 예시**

---

### **1. BlockBreakEvent / 블록 파괴 이벤트**

```json
{
  "Event": "BlockBreakEvent",
  "Name": ["WHEAT", "POTATO", "CARROT", "BEETROOT"],
  "EXP": {"min": 5, "max": 15},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when the player breaks specific blocks. Can configure level requirement, probability, and tools.
**Tip:** Use `Tools` to restrict EXP to specific tools like hoes.

**KR:** 플레이어가 특정 블록(밀, 감자, 당근, 비트루트)을 부술 때 EXP를 지급합니다.
**팁:** `Tools` 필드를 활용하면 특정 도구(예: 괭이)로만 EXP 지급 가능.

---

### **2. BlockPlaceEvent / 블록 설치 이벤트**

```json
{
  "Event": "BlockPlaceEvent",
  "Name": ["WHEAT_SEEDS", "POTATO", "CARROT", "BEETROOT"],
  "EXP": {"min": 2, "max": 10},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when placing specific blocks or seeds. Useful for farming skills.
**Tip:** Combine with `BlockBreakEvent` to track full farming activity.

**KR:** 플레이어가 특정 블록이나 씨앗을 설치할 때 EXP를 지급합니다.
**팁:** `BlockBreakEvent`와 함께 사용하면 전체 농사 활동 추적 가능.

---

### **3. PlayerFishEvent / 낚시 이벤트**

```json
{
  "Event": "PlayerFishEvent",
  "Name": ["RAW_FISH", "SALMON", "PUFFERFISH"],
  "EXP": {"min": 5, "max": 15},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": ["FISHING_ROD"],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when catching fish. Can limit EXP to certain fish types.
**Tip:** Useful for fishing or survival skills.

**KR:** 플레이어가 낚시로 물고기를 잡을 때 EXP를 지급합니다.
**팁:** 낚시 또는 생존 스킬용으로 활용 가능.

---

### **4. EntityDeathEvent / 엔티티 사망 이벤트**

```json
{
  "Event": "EntityDeathEvent",
  "Name": ["ZOMBIE", "SKELETON", "CREEPER"],
  "EXP": {"min": 10, "max": 30},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when specific entities die. Great for combat or hunting skills.
**Tip:** Use `Name` to differentiate between monsters and bosses.

**KR:** 특정 엔티티가 사망할 때 EXP를 지급합니다. 전투/사냥 스킬에 적합합니다.
**팁:** 일반 몬스터와 보스를 구분할 때 `Name` 필드 활용.

---

### **5. PlayerRunEvent / 달리기 이벤트 (주기적)**

```json
{
  "Event": "PlayerRunEvent",
  "Name": ["RUN"],
  "EXP": {"min": 3, "max": 5},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "StartDelayMs": 2000,
  "RepeatIntervalMs": 2500,
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP periodically when the player runs.
`StartDelayMs` sets the delay before the first gain, `RepeatIntervalMs` sets repetition.

**KR:** 플레이어가 달릴 때 주기적으로 EXP를 지급합니다.
`StartDelayMs`는 최초 지급 지연, `RepeatIntervalMs`는 반복 간격을 설정합니다.

---

### **6. PlayerToggleSneakEvent / 스니크 전환 이벤트**

```json
{
  "Event": "PlayerToggleSneakEvent",
  "Name": ["SNEAK"],
  "EXP": {"min": 2, "max": 5},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when the player toggles sneak mode. Useful for stealth or agility skills.
**KR:** 플레이어가 스니크 상태를 전환할 때 EXP를 지급합니다. 은신/민첩 스킬에 적합합니다.

---

### **7. EntityDamageByEntityEvent / 엔티티 공격 이벤트**

```json
{
  "Event": "EntityDamageByEntityEvent",
  "Name": ["PLAYER", "ZOMBIE", "SKELETON"],
  "EXP": {"min": 5, "max": 20},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": ["SWORD", "BOW"],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when the player attacks an entity. Can differentiate melee/ranged.
**KR:** 플레이어가 엔티티를 공격할 때 EXP를 지급합니다. 근접/원거리 구분 가능.

---

### **8. EntityRegainHealthEvent / 체력 회복 이벤트**

```json
{
  "Event": "EntityRegainHealthEvent",
  "Name": ["PLAYER"],
  "EXP": {"min": 1, "max": 5},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when the player regains health. Useful for healing skills.
**KR:** 플레이어가 체력을 회복할 때 EXP를 지급합니다. 치유 스킬에 적합합니다.

---

### **9. PlayerInteractEvent / 블록/아이템 상호작용 이벤트**

```json
{
  "Event": "PlayerInteractEvent",
  "Name": ["CHEST", "LEVER", "BUTTON"],
  "EXP": {"min": 2, "max": 6},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when interacting with blocks/items. Useful for utility or crafting skills.
**KR:** 플레이어가 블록/아이템과 상호작용할 때 EXP를 지급합니다. 유틸리티/제작 스킬에 적합합니다.

---

### **10. EntityBreedEvent / 엔티티 번식 이벤트**

```json
{
  "Event": "EntityBreedEvent",
  "Name": ["COW", "SHEEP", "PIG"],
  "EXP": {"min": 5, "max": 15},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": ["WHEAT", "CARROT"],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when breeding animals. Useful for farming or animal husbandry skills.
**KR:** 플레이어가 동물을 번식시킬 때 EXP를 지급합니다. 농사/사육 스킬에 적합합니다.

---

### **11. PlayerToggleFlightEvent / 비행 전환 이벤트**

```json
{
  "Event": "PlayerToggleFlightEvent",
  "Name": ["FLIGHT"],
  "EXP": {"min": 2, "max": 5},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "StartDelayMs": 2000,
  "RepeatIntervalMs": 2500,
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP periodically while flying.
**KR:** 플레이어가 비행 중일 때 주기적으로 EXP를 지급합니다.

---

### **12. PlayerSwimEvent / 수영 이벤트**

```json
{
  "Event": "PlayerSwimEvent",
  "Name": ["SWIM"],
  "EXP": {"min": 1, "max": 3},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": [],
  "StartDelayMs": 2000,
  "RepeatIntervalMs": 2500,
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP periodically while swimming. Useful for survival or water skills.
**KR:** 플레이어가 수영할 때 주기적으로 EXP를 지급합니다. 생존/수중 스킬에 적합합니다.

---

### **13. ProjectileHitEvent / 투사체 적중 이벤트**

```json
{
  "Event": "ProjectileHitEvent",
  "Name": ["ARROW", "SNOWBALL", "EGG"],
  "EXP": {"min": 3, "max": 10},
  "PlayerExp": 0,
  "Chance": 100,
  "LevelRequired": 0,
  "Tools": ["BOW", "CROSSBOW"],
  "BonusMultiplier": 1.0,
  "PenaltyMultiplier": 1.0
}
```

**EN:** Grants EXP when a projectile hits a target. Useful for archery or ranged skills.
**KR:** 플레이어의 투사체가 대상에 적중할 때 EXP를 지급합니다. 활/원거리 스킬에 적합합니다.

---
