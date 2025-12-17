# Made By drewdrew0414 (or drewdrew1_)

---

# SELECT LANGUAGE
- [English](#english-version-manual)
- [한국어](#한국어-버전-설명서)

---

## ENGLISH VERSION MANUAL
여기에 영어 설명을 작성하면 됩니다.

---

## 한국어 버전 설명서

## 0. 목차
* [1. DRPG에 대하여](#1-drpg에-대하여)
  * [1-1. DRPG levelSystem이란?](#1-1-drpg-levelsystem이란)
  * [1-2. 시스템 설계 철학](#1-2-시스템-설계-철학)
  * [1-3. 데이터 기반 아키텍처](#1-3-데이터-기반-아키텍처)
    
* [2. 설치 가이드](#2-설치-가이드)

---

## 1. DRPG에 대하여
### 1-1. DRPG levelSystem이란?
* DRPG levelSystem은 Minecraft(Paper/Spigot) 서버용으로 제작된 완전 모듈화된 JSON 기반 RPG 레벨 시스템이다.
* 서버 운영자, 개발자, 콘텐츠 제작자가 Java 코드를 수정하지 않고도 스킬, 경험치 규칙, 레벨 상승 방식, 보상 구조 등 RPG 관련 모든 동작을 자유롭게 변경할 수 있도록 설계되었다.
* 시스템의 모든 구성 요소는 텍스트(JSON) 기반 파일로 이루어져 있으며, 플러그인은 서버 시작 시 모든 설정 파일을 불러온 후 이를 통합하여 하나의 실행 모델로 만든다.
* 이는 높은 확장성, 유지보수 용이성, 빠른 설정 변경을 가능하게 한다.
* 또한 새로운 스킬을 추가하거나, 다른 서버에서 제작한 콘텐츠 팩을 가져오는 것도 매우 간단하다.

### 1-2. 시스템 설계 철학
* DRPG levelSystem의 핵심 설계 철학은 다음과 같다:
  * 외부화 게임 규칙은 Java 코드가 아니라 JSON 파일에 존재한다.
  * 모듈성 스킬과 보상은 독립적으로 관리된다.
  * 고장 격리 하나의 파일이 망가져도 전체 시스템이 중단되지 않는다.
  * 데이터 무결성 플레이어 데이터는 UUID 기반으로 저장되어 닉네임 변경에도 안전하다.
  * 디버그 가시성 디버그 기능을 켜면 모든 로드 이벤트, 파일 파싱 정보, 등록된 콘텐츠를 확인할 수 있다.
  * 완전한 커스터마이징 서버 운영자는 무제한 스킬, 무제한 보상 단계, 정밀 경험치 규칙을 만들 수 있다.

### 1-3. 데이터 기반 아키텍처
* DRPG LevelSystem은 **데이터 중심 아키텍처(Data-Driven Architecture)**를 기반으로 설계되었다.
* 이를 통해 무거운 작업이나 반복 작업을 **백그라운드에서 비동기 처리**하여, 서버 성능에 영향을 주지 않고 안정적으로 동작하도록 구현되었다.

---

## 2. 설치 및 사용 가이드

* **설치법**
  1. [PaperMC](https://papermc.io/downloads) 서버를 설치하고 실행합니다.
  2. DRPG LevelSystem 플러그인 `.jar` 파일을 다운로드합니다.
     * 서버 버전과 플러그인이 지원하는 버전 맞출 것
  3. 서버 디렉토리 내 `plugins` 폴더에 `.jar` 파일을 복사합니다.
  4. 서버를 재시작합니다.
  5. 서버 콘솔에 "DRPG LevelSystem enabled" 메시지가 출력되면 정상적으로 설치 완료입니다.
     * 오류가 날 시 (drew0414drew@gmail.com)에 문의할 것.

* **사용법**
 1. 서버 시작 시 `plugins/DRPG/levelSystem/ 폴더가 생성됩니다.
 2. `plugins/DRPG/levelSystem/skills/에 파일을 넣습니다. > [예시](../How%20To%20Use/JSON/Rewards/Rewards%20Manual%20(KOR).md)
 3. `plugins/DRPG/levelSystem/rewards/에 파일을 넣습니다.

