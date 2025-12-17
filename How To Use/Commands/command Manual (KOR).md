===============

# Made By drewdrew0414(or drewdrew1_).

===============

---

# DRPG levelSystem 명령어 사용법

## /drpg ls 혹은 /drpg levelsystem
 * help : levelSystem에서 사용가능한 명령어들 출력
   
 * info : 현재 플러그인의 정보 및 버전 그리고 로드 된 모든 json파일의 버전을 출력

 * reloadAll : 모든 json파일을 다시 읽어옴
   * 읽어오는 파일들 : `config.json` , `skills/*.json` , `rewards/*.json` , `database.json`
  
   * WARN: `database.json`은 `1.1.0` 이상의 버전에만 있습니다.
  
 * skillInfo <skillName | all> : 플레이어 자신의 <skillName>의 레벨과 경험치 혹은 모든 스킬의 레벨과 경험치를 출력

 * skillList : 현재 존재하는 스킬들의 이름 출력

 * skillTop <skillName> : 현재 온라인인 플레이어 중 가장 해당 스킬의 레벨이 높은 순에서 낮은 순으로 출력 (최대 20명이며, 추후 개선될 예정)
 
 * ㅅ
