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
* ### 1. [
---

## 한국어

## 0. 목차
* ### 1. [Rewards Json 호환버전 확인](#kor1)
* ### 2. [Json 구조](#kor2)
* ### 3. [주의사항]()
* ### 4. [예제]()
  
---

## 1. 호환버전확인
<a id="kor1"></a>
| 플러그인 버전 | 호환되는 Rewards Json 버전 |
|---|---|
| 1.0.0 | 1.0.0 |

---

## 2. Json 구조
<a id="kor2"></a>

#### 2.1 최상위 구조
``` jsonc
"RewardJsonVersion": "<String>",
"Name": "<String>",
"DisplayName": "<String>"
"<int>": [ ... // 밑에 설명 됨
```

| 필드명 | 타입 | 설명 | 예시 |
| --- | --- | --- | --- |
| RewardJsonVersion | String | Reward Json의 버전 정의 (플러그인의 버전에 맞게 설정 할 것) | 1.0.0 |
| Name | String | 해당 스킬의 이름 | Farming |
| DisplayName | String | 플레이어가 보게 될 스킬의 이름 | Farming |
| "int" | int | int레벨 시 보상 출력 | 5, 10... |

### 2.2 내부구조1

```jsonc
"<int>": [
    
]
```
