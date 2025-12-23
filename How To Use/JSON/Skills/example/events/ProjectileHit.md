===============

# Made By drewdrew0414 (or drewdrew1_)

===============

---

# ProjectileHit event example

## Version

* ### [1.0.0 (KOR)](#archery-1-0-0-kor)
* ### [1.0.0 (ENG)](#archery-1-0-0-eng)

---

<a id="archery-1-0-0-kor"></a>

## 1.0.0 (KOR)

```jsonc
{
  "Events": {
    "ProjectileHit": [ // 투사체(화살 등)가 엔티티에 명중했을 때 발생
      {
        "WeaponType": ["BOW", "CROSSBOW"],
        // BOW : 활
        // CROSSBOW : 석궁
        // 적용 대상 무기 타입

        "TargetEntity": ["String"],
        // EXP를 지급할 대상 엔티티
        // 비워두면 모든 엔티티 적용

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,
        // 플레이어에게 직접 지급되는 EXP

        "Chance": int,
        // EXP 지급 확률 (%)

        "RequiredLevel": int,
        // 해당 이벤트를 통해 EXP를 받을 수 있는 최소 스킬 레벨

        "ExtraEXP": {
          "Distance": {
            "min": double,
            // 최소 거리 조건 (블록 단위)

            "addMin": int,
            "addMax": int
            // 거리 조건 충족 시 추가 EXP
          },

          "multiplier": double,
          // 최종 EXP 배율

          "bonusEXP": int
          // 모든 계산 이후 고정 추가 EXP
        },

        "UseAdvancedSettings": boolean,
        // 고급 설정 사용 여부

        "AdvancedSettings": {
          "RequireFullyCharged": boolean,
          // 활 풀차지 상태일 때만 EXP 지급

          "PreventSameTargetSpam": boolean,
          // 동일 대상 연속 공격 EXP 방지

          "SameTargetCooldownTick": int,
          // 같은 대상 EXP 지급 쿨타임 (틱)

          "IgnoreArmorStand": boolean,
          // 아머 스탠드 무시

          "IgnoreFriendly": boolean,
          // 파티 / 아군 무시

          "MaxExpPerSecond": int,
          // 초당 획득 가능한 최대 EXP

          "PlayerPermissionOverride": "String"
          // 해당 조건을 무시할 수 있는 권한
        }
      }
    ]
  }
}
```

---

<a id="archery-1-0-0-eng"></a>

## 1.0.0 (ENG)

```jsonc
{
  "Events": {
    "ProjectileHit": [ // Triggered when a projectile hits an entity
      {
        "WeaponType": ["BOW", "CROSSBOW"],
        // Target weapon types

        "TargetEntity": ["String"],
        // Target entities for EXP rewards
        // Empty = all entities

        "EXP": {
          "min": int,
          "max": int
        },

        "PlayerGetExp": int,
        // EXP directly given to the player

        "Chance": int,
        // EXP reward chance (%)

        "RequiredLevel": int,
        // Minimum skill level required

        "ExtraEXP": {
          "Distance": {
            "min": double,
            // Minimum distance requirement

            "addMin": int,
            "addMax": int
            // Additional EXP if distance condition is met
          },

          "multiplier": double,
          // Final EXP multiplier

          "bonusEXP": int
          // Fixed EXP added after all calculations
        },

        "UseAdvancedSettings": boolean,
        // Enable advanced settings

        "AdvancedSettings": {
          "RequireFullyCharged": boolean,
          // Only give EXP if bow is fully charged

          "PreventSameTargetSpam": boolean,
          // Prevent EXP farming on the same target

          "SameTargetCooldownTick": int,
          // EXP cooldown per same target (ticks)

          "IgnoreArmorStand": boolean,
          // Ignore armor stands

          "IgnoreFriendly": boolean,
          // Ignore friendly / party members

          "MaxExpPerSecond": int,
          // Maximum EXP per second

          "PlayerPermissionOverride": "String"
          // Permission to bypass restrictions
        }
      }
    ]
  }
}
```

---
