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
* [2-2. BlockPlace 이벤트](#2-2-BlockPlace-이벤트)
  * [2-2-1. 구조](#2-2-1-구조)
  * [2-2-2. 고급기능](#2-2-2-고급기능)
* [2-3. EnchantItem 이벤트](#2-3-EnchantItem-이벤트)
  * [2-3-1. 구조](#2-3-1-구조)
  * [2-3-2. 고급기능](#2-3-2-고급기능)
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
* [BlockBreak](#2-1-BlockBreak-이벤트)
* [BlockPlace](#2-2-BlockPlace-이벤트)
* [EnchantItem](#2-3-EnxhantItem-이벤트)
  
  ---
  ## 2-1. BlockBreak 이벤트
**플레이어가 블록을 부쉈을 때 실행됨**
### 2-1-1. 구조
```
// "Events" { } 내부
"BlockBreak": [
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
        "RequiredWorldTimeEnd": int,
        "ProbabilitySuccessXP": int
      },
      "ToolSettings": {
        "DamageTool": boolean,
        "MinToolDurability": int,
        "AllowSilkTouch": boolean
      },
      "PlayerPermissionOverride": "String",
      "RequireBiome": ["String"]
    }
  }
]
```

### 2-1-1. 구조 설명
| 필드 | 타입 | 설명 |
|---|---|---|
| TypeItemName | List<String> | 대상 블록 아이템 코드 리스트 |
| EXP | Object | 기본 지급 경험치의 최소/최대 범위 |
| PlayerGetExp | int | 플레이어에게 직접 지급되는 경험치량 |
| Chance | int | 경험치 획득 성공 확률 (0~100) |
| RequiredLevel | int | 해당 블록으로 경험치를 얻기 위한 최소 스킬 레벨 |
| RequiredTools | List<String> | 경험치를 얻기 위해 반드시 사용해야 하는 도구 리스트 |
| ExtraEXP | Object | 날씨, 배수, 보너스 경험치 등 조건부 추가 보상 설정 |
| UseAdvancedSettings | boolean | 아래 AdvancedSettings 활성화 여부 |

### 2-1-2. 고급기능
**어뷰징 방지 및 세부 커스텀 설정**
[1] PreventXPGrinding (노가다 및 악용 방지)
| 필드 | 타입 | 설명 |
|---|---|---|
| Radius | int | 동일 좌표 기준 반경 내 재파괴 시 쿨타임 적용 범위 |
| CooldownSeconds | int | 동일 좌표 블록의 경험치 재발생 대기 시간 (초) |
| MaxBlocksInChunk | int | 한 청크 내에서 경험치를 줄 수 있는 최대 블록 수 |
| MinLightLevel | int | 블록 위치의 밝기가 설정값 이상일 때만 경험치 지급 |
| MaxDailyXPPerBlock | int | 해당 종류의 블록으로 하루에 획득 가능한 총 경험치 제한 |


[2] ActionControl (시스템 제어)
| 필드 | 타입 | 설명 |
|---|---|---|
| AllowCreativeMode | boolean | 크리에이티브 모드에서 경험치 지급 여부 |
| RequireNaturalBlock | boolean | 자연적으로 생성된 블록(청크 생성 시 블록)인지 검증 |
| CancelExpIfCancelled | boolean | 타 플러그인(지역 보호 등)에 의해 이벤트가 취소되면 경험치 미지급 |


[3] Requirements (환경 요구 조건)
| 필드 | 타입 | 설명 |
|---|---|---|
| RequiredWorldTimeStart | int | 경험치 획득이 가능해지는 게임 내 시간 (0~24000 틱) |
| RequiredWorldTimeEnd | int | 경험치 획득이 마감되는 게임 내 시간 (0~24000 틱) |
| ProbabilitySuccessXP | int | 파괴 성공과 별개로 경험치 지급 로직이 작동할 확률 |
| PlayerPermissionOverride | String | 특정 권한(LuckPerms 등) 보유자 전용 설정 |
| RequireBiome | List<String> | 특정 바이옴 내에서 파괴했을 때만 경험치 지급 |


[4] ToolSettings (도구 상세 설정)
| 필드 | 타입 | 설명 |
|---|---|---|
| DamageTool | boolean | 블록 파괴 시 도구의 내구도를 실제로 소모시킬지 여부 |
| MinToolDurability | int | 도구의 남은 내구도가 이 값보다 낮으면 경험치 미지급 |
| AllowSilkTouch | boolean | 실크 터치(섬세한 손길) 인챈트 도구 사용 시 경험치 지급 여부 |

---

## 2-2. BlockPlace 이벤트
**플레이어가 블록을 설치했을 때 실행됨**

### 2-2-1. 구조
```
// "Events" { } 내부
"BlockPlace": [
  {
    "TypeItemName": ["String"],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
    "Chance": int,
    "RequiredLevel": int,
    "RequiredTools": ["String"],
    "Cooldown": int,

    "ExtraEXP": {
      "multiplier": double,
      "bonusEXP": int
    },

    "UseAdvancedSettings": boolean,
    "AdvancedSettings": {
      "VerifyGravityBlock": boolean,
      "IgnoreLiquidPlacement": boolean,
      "BlockDataValidation": boolean,
      
      "BroadcastToAdmins": {
        "Enable": boolean,
        "AdminPermission": "String",
        "Message": "String"
      },

      "PreventMassPlace": {
        "MaxPerSecond": int,
        "MaxPerChunk": int
      },

      "Requirements": {
        "RequiredLightLevel": int,
        "SurfaceOnly": boolean,
        "MinDistanceBetweenSameBlock": int,
        "MinFoodLevel": int
      },

      "PlayerPermissionOverride": "String",
      "RequireBiome": ["String"]
    }
  ]
}
```

### 구조 설명
| 필드 | 타입 | 설명 |
|---|---|---|
| TypeItemName | List<String> | 대상 블록 아이템 코드 리스트 |
| EXP | Object | 기본 지급 경험치의 최소/최대 범위 |
| PlayerGetExp | int | 플레이어 레벨 경험치 외에 추가로 줄 경험치량 |
| Chance | int | 설치 시 경험치 획득 성공 확률 (0~100) |
| RequiredLevel | int | 해당 블록 설치로 경험치를 얻기 위한 최소 스킬 레벨 |
| RequiredTools | List<String> | 특정 도구를 들고 설치해야 할 경우 (예: 건설 망치 등) |
| Cooldown | int | 설치 경험치 획득 간의 대기 시간 (틱 단위) |

### 2-2-2. 고급 기능 (AdvancedSettings)
[1] 검증 및 보안 (Validation & Security)
| 필드 | 타입 | 설명 |
|---|---|---|
| VerifyGravityBlock | boolean | 모래, 자갈 등 중력 블록의 비정상 설치 어뷰징 방지 |
| IgnoreLiquidPlacement | boolean | 물/용암 등 액체 안에서의 설치 경험치 무시 여부 |
| BlockDataValidation | boolean | 블록의 방향이나 상태가 정상적인지 패킷 검증 |
| BroadcastToAdmins | Object | 특정 블록 설치 시 관리자에게 알림 전송 설정 |


[2] 대량 설치 제한 (Anti-Mass Place)
| 필드 | 타입 | 설명 |
|---|---|---|
| MaxPerSecond | int | 초당 최대 설치 허용 횟수 (매크로 방지) |
| MaxPerChunk | int | 한 청크 내에 설치 가능한 해당 블록의 최대 개수 제한 |


[3] 환경 요구 조건 (Requirements)
| 필드 | 타입 | 설명 |
|---|---|---|
| RequiredLightLevel | int | 설치 지점의 밝기가 이 값 이상이어야 경험치 지급 |
| SurfaceOnly | boolean | 하늘이 트인 지상에서 설치했을 때만 인정 여부 |
| MinDistanceBetweenSameBlock | int | 동일 종류 블록 간의 최소 거리 유지 (도배 방지) |
| MinFoodLevel | int | 플레이어의 배고픔 수치가 일정 수준 이상이어야 함 |

[4] 기타 설정
| 필드 | 타입 | 설명 |
|---|---|---|
| PlayerPermissionOverride | String | 특정 권한이 있는 유저만 이 로직을 적용하거나 우회함 |
| RequireBiome | List<String> | 특정 바이옴 내에서 설치했을 때만 경험치 지급 |

---

## 2-3. EnchantItem 이벤트
**플레이어가 인챈트 테이블에서 아이템에 마법을 부여했을 때 실행됨**
### 2-3-1. 구조
```
// "Events" { } 내부
"EnchantItem": [
  {
    "TypeItemName": ["String"],
    "CheckEnchant": [
      { "EnchantType": "String", "Level": int }
    ],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
    "Chance": int,

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
      "CheckEnchantingTableLevel": boolean
    }
  }
]
```

### 구조 설명

| 필드 | 타입 | 설명 |
|---|---|---|
| TypeItemName | List<String> | 대상 아이템 코드 리스트 |
| CheckEnchant | List<Object> | 부여된 마법의 종류와 레벨 확인 (경험치 지급 조건) |
| EXP | Object | 인챈트 성공 시 지급될 기본 경험치 범위 |
| PlayerGetExp | int | 플레이어 레벨 경험치 추가 지급량 |
| Chance | int | 경험치 획득 성공 확률 (0~100) |
| ExtraEXP | Object | 날씨에 따른 추가 경험치 및 배수 설정 |

### 2-3-2. 고급 기능 (AdvancedSettings)
**악용 방지 및 검증 설정**

| 필드 | 타입 | 설명 |
|---|---|---|
| CheckEnchantingTableLevel | boolean | [악용방지] 주변 책장 개수와 요청된 인챈트 레벨의 일치 여부를 서버에서 재검증 (핵 패킷 방지) |

---

## 2-4. CraftItem 이벤트
**플레이어가 조합창(작업대 등)에서 아이템을 제작했을 때 실행됨**

### 2-4-1. 구조
```
// "Events" { } 내부
"CraftItem": [
  {
    "TypeItemName": ["String"],
    "EXP": { "min": int, "max": int },
    "PlayerGetExp": int,
    "Chance": int,

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
      "PreventShiftClickCrafting": boolean,
      "ValidateNBTIngredients": boolean,
      "MaxCraftPerMinute": int,
      "CheckInventorySpace": boolean
    }
  }
]
```
### 구조 설명
| 필드 | 타입 | 설명 |
|---|---|---|
| TypeItemName | List<String> | 제작 결과물 아이템 코드 리스트 |
| EXP | Object | 제작 성공 시 지급될 기본 경험치 범위 |
| PlayerGetExp | int | 플레이어 레벨 경험치 추가 지급량 |
| Chance | int | 경험치 획득 성공 확률 (0~100) |
| ExtraEXP | Object | 날씨에 따른 추가 경험치 및 배수 설정 |

### 2-4-2. 고급 기능 (AdvancedSettings)
**제작 시스템 악용 및 버그 방지 설정**
| 필드 | 타입 | 설명 |
|---|---|---|
| PreventShiftClickCrafting | boolean | [악용방지] 시프트 클릭을 이용한 대량 제작 시 경험치가 비정상적으로 쌓이는 것을 방지 |
| ValidateNBTIngredients | boolean | [버그방지] 일반 아이템을 RPG 전용 재료로 속여 제작하는 것을 막기 위해 재료의 NBT 데이터까지 정밀 검증 |
| MaxCraftPerMinute | int | [악용방지] 1분당 최대 제작 횟수를 제한하여 매크로(Macro)를 이용한 초고속 레벨업 차단 |
| CheckInventorySpace | boolean | [버그방지] 인벤토리가 가득 찬 상태에서 제작 시 발생할 수 있는 아이템 복사 및 증발 버그 차단 |

---
