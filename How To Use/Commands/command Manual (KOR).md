==========#####==========

# Made by drewdrew0414(or drewdrew1_)

==========#####==========

---

## Select Language / 언어 선택

* ## [English](#English)


* ## [한국어](#Korean)



---

## English

<a id="English"></a>

## 0. Table of Contents

* ### 1. [Command Overview](#eng1)


* ### 2. [Detailed Command Guide](#eng2)


* [User Commands](#eng2-1)
* [Admin: Data Modification](#eng2-2)
* [Admin: System Management](#eng2-3)


* ### 3. [Tab Completion Support](#eng3)


* ### 4. [Precautions](#eng4)



---

## 1. Command Overview

<a id="eng1"></a>

| Command Base | Target | Permission | Description |
| --- | --- | --- | --- |
| `/rpglevel` | Player | Default | Check own skill levels and EXP |
| `/drpg ls` | Admin | OP | Manage player data and plugin system |

---

## 2. Detailed Command Guide

<a id="eng2"></a>

### 2.1 User Commands

<a id="eng2-1"></a>

* **`/rpglevel`**
* Displays the player's current level and experience for all loaded skills in a formatted list.



### 2.2 Admin: Data Modification

<a id="eng2-2"></a>

> **Usage:** `/drpg ls <action> <player> <skill> <type> <value>`

| Parameter | Options | Description |
| --- | --- | --- |
| **action** | `add`, `remove`, `set` | Method of modification |
| **skill** | Skill Name | Target skill (e.g., Mining, Farming) |
| **type** | `level`, `exp` | Value type to modify |
| **value** | Integer | The amount to apply |

* **Reset Command:** `/drpg ls reset <player> <skill|all>`
* Resets specific skill or all skill data to 0 for the target player.



### 2.3 Admin: System Management (Reload)

<a id="eng2-3"></a>

> **Usage:** `/drpg ls reload <target>`

| Target | Description |
| --- | --- |
| **all** | Reloads Skills, Rewards, and Config.yml |
| **skill** | Reloads only files in the `/skills` folder |
| **reward** | Reloads only files in the `/rewards` folder |
| **config** | Reloads only the `config.yml` |

---

## 3. Tab Completion Support

<a id="eng3"></a>

The plugin provides smart tab completion for OP users:

1. Suggests `ls` after the base command.
2. Suggests sub-actions (`add`, `reload`, etc.).
3. Lists online player names.
4. Lists all currently loaded skill names.

---

## 한국어

<a id="Korean"></a>

## 0. 목차

* ### 1. [명령어 개요](#kor1)


* ### 2. [명령어 상세 가이드](#kor2)


* [일반 사용자 명령어](#kor2-1)
* [관리자: 데이터 수정](#kor2-2)
* [관리자: 시스템 관리](#kor2-3)


* ### 3. [탭 자동완성 지원](#kor3)


* ### 4. [주의사항](#kor4)



---

## 1. 명령어 개요

<a id="kor1"></a>

| 기본 명령어 | 대상 | 권한 | 설명 |
| --- | --- | --- | --- |
| `/rpglevel` | 플레이어 | 기본 | 자신의 기술 레벨 및 경험치 확인 |
| `/drpg ls` | 관리자 | OP | 플레이어 데이터 및 플러그인 시스템 관리 |

---

## 2. 명령어 상세 가이드

<a id="kor2"></a>

### 2.1 일반 사용자 명령어

<a id="kor2-1"></a>

* **`/rpglevel`**
* 플레이어가 보유한 모든 기술의 레벨과 현재 경험치 상태를 채팅창에 출력합니다.



### 2.2 관리자: 데이터 수정

<a id="kor2-2"></a>

> **사용법:** `/drpg ls <action> <player> <skill> <type> <value>`

| 파라미터 | 옵션 | 설명 |
| --- | --- | --- |
| **action** | `add`, `remove`, `set` | 수치 조작 방식 (추가, 제거, 설정) |
| **skill** | 기술 이름 | 대상 기술명 (예: Mining, Farming) |
| **type** | `level`, `exp` | 수정할 값의 종류 |
| **value** | 정수 | 적용할 수치 |

* **초기화 명령어:** `/drpg ls reset <player> <skill|all>`
* 대상 플레이어의 특정 기술 또는 모든 기술 데이터를 0으로 초기화합니다.



### 2.3 관리자: 시스템 관리 (리로드)

<a id="kor2-3"></a>

> **사용법:** `/drpg ls reload <target>`

| 대상(Target) | 설명 |
| --- | --- |
| **all** | 기술(Skills), 보상(Rewards), 설정을 모두 다시 불러옵니다. |
| **skill** | `/skills` 폴더 내의 파일만 다시 불러옵니다. |
| **reward** | `/rewards` 폴더 내의 파일만 다시 불러옵니다. |
| **config** | `config.yml` 설정만 다시 불러옵니다. |

---

## 3. 탭 자동완성 지원

<a id="kor3"></a>

운영자 편의를 위해 다음과 같은 자동완성을 지원합니다:

1. 기본 명령어 뒤에 `ls` 추천.
2. 서브 액션(`add`, `reload` 등) 추천.
3. 현재 접속 중인 플레이어 목록 표시.
4. 서버에 로드된 모든 기술 이름(`skillsInfo`) 목록 표시.

---

## 4. 주의사항

<a id="kor4"></a>

* ### 모든 관리자 명령어는 **OP 권한**이 있어야 실행 가능합니다.


* ### `remove` 액션 사용 시, 수치는 **0 미만**으로 내려가지 않습니다.


* ### `/rpglevel`은 플레이어 전용 명령어이며, 콘솔에서는 `/drpg ls <player>`를 사용해야 합니다.



---
