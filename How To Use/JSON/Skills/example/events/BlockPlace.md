===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# BlockPlace event example

## Version

* ### [1.0.0 (KOR)](#1-0-0-kor)
* ### [1.0.0 (ENG)](#1-0-0-eng)

---

<a id="1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "BlockPlace": [ // 플레이어가 블록을 설치했을 때 발생하는 이벤트
      {
        "TypeItemName": ["String"],
        // 설치 대상 블록(Material) 목록
        // Bukkit / Paper Material enum 이름 사용

        "EXP": {
          "min": int, // 최소 지급 EXP
          "max": int  // 최대 지급 EXP (min과 같으면 고정 EXP)
        },

        "PlayerGetExp": int,
        // 플레이어에게 직접 지급되는 EXP
        // (스킬 EXP와 별도로 사용 가능)

        "Chance": int,
        // EXP 지급 확률 (%)
        // 100 = 항상 지급

        "RequiredLevel": int,
        // 해당 스킬(Name)의 최소 요구 레벨
        // 마인크래프트 기본 레벨 아님

        "RequiredTools": ["String"],
        // 블록 설치 시 손에 들고 있어야 하는 아이템
        // 비어있거나 생략 시 제한 없음

        "Cooldown": int,
        // 동일 블록 설치 후 EXP 재지급 쿨타임 (초)

        "ExtraEXP": {
          "multiplier": double,
          // 최종 EXP 배율
          // (기본 EXP × multiplier)

          "bonusEXP": int
          // 모든 계산 이후 고정으로 추가되는 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부
        // false면 AdvancedSettings 전체 무시

        "AdvancedSettings": {
          "VerifyGravityBlock": boolean,
          // 중력 블록(SAND, GRAVEL 등) 검증 여부
          // 낙하 중 설치 악용 방지

          "IgnoreLiquidPlacement": boolean,
          // 물/용암 같은 액체 설치 시 EXP 지급 여부

          "BlockDataValidation": boolean,
          // BlockData까지 완전히 일치해야 EXP 지급
          // (방향, 상태 등)

          "BroadcastToAdmins": {
            "Enable": boolean,
            // 관리자 알림 기능 사용 여부

            "AdminPermission": "String",
            // 알림을 받을 관리자 권한

            "Message": "String"
            // 관리자에게 전송할 메시지
          },

          "PreventMassPlace": {
            "MaxPerSecond": int,
            // 초당 설치 가능한 최대 블록 수

            "MaxPerChunk": int
            // 청크(16x16)당 설치 가능한 최대 블록 수
          },

          "Requirements": {
            "RequiredLightLevel": int,
            // 최소 밝기 조건

            "SurfaceOnly": boolean,
            // true일 경우 지표면에서만 설치 허용

            "MinDistanceBetweenSameBlock": int,
            // 동일 블록 간 최소 거리 (블록 단위)

            "MinFoodLevel": int
            // 최소 허기 게이지 조건
          },

          "PlayerPermissionOverride": "String",
          // 해당 권한이 있으면 모든 제한 무시

          "RequireBiome": ["String"]
          // EXP 지급 허용 바이옴 목록
          // "All" 입력 시 바이옴 제한 없음
        }
      }
    ]
  }
}


```

---

<a id="1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": {
    "BlockPlace": [ // Event triggered when a player places a block
      {
        "TypeItemName": ["String"],
        // List of block Materials that trigger this rule

        "EXP": {
          "min": int, // Minimum EXP
          "max": int  // Maximum EXP (fixed if equal to min)
        },

        "PlayerGetExp": int,
        // EXP given directly to the player
        // Separate from skill EXP if needed

        "Chance": int,
        // Chance to receive EXP (percentage)

        "RequiredLevel": int,
        // Minimum required skill level (not Minecraft XP level)

        "RequiredTools": ["String"],
        // Required item in hand to receive EXP

        "Cooldown": int,
        // Cooldown before EXP can be granted again (seconds)

        "ExtraEXP": {
          "multiplier": double,
          // Final EXP multiplier

          "bonusEXP": int
          // Flat EXP added after all calculations
        },

        "UseAdvancedSettings": boolean,
        // Enables or disables AdvancedSettings entirely

        "AdvancedSettings": {
          "VerifyGravityBlock": boolean,
          // Validates gravity blocks (sand, gravel, etc.)

          "IgnoreLiquidPlacement": boolean,
          // Ignore liquid placements (water/lava)

          "BlockDataValidation": boolean,
          // Requires exact BlockData match

          "BroadcastToAdmins": {
            "Enable": boolean,
            // Enable admin notifications

            "AdminPermission": "String",
            // Permission required to receive alerts

            "Message": "String"
            // Message sent to admins
          },

          "PreventMassPlace": {
            "MaxPerSecond": int,
            // Maximum blocks placed per second

            "MaxPerChunk": int
            // Maximum blocks placed per chunk
          },

          "Requirements": {
            "RequiredLightLevel": int,
            // Minimum light level

            "SurfaceOnly": boolean,
            // Only allow surface placements

            "MinDistanceBetweenSameBlock": int,
            // Minimum distance between identical blocks

            "MinFoodLevel": int
            // Minimum food level required
          },

          "PlayerPermissionOverride": "String",
          // Players with this permission bypass all restrictions

          "RequireBiome": ["String"]
          // Allowed biomes
          // Use "All" to allow all biomes
        }
      }
    ]
  }
}

```

---
