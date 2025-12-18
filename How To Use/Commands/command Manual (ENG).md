===============
Made By drewdrew0414(or drewdrew1_).
===============
DRPG levelSystem Command Guide
/drpg ls or /drpg levelsystem
 * help : Displays all available commands for levelSystem
 * checkRewards < skillName > : Displays rewards for < skillName >
 * info : Displays plugin information, version, and the versions of all loaded json files
 * reloadAll : Reloads all json files
   * Files to reload : config.json , skills/*.json , rewards/*.json , database.json
   * WARN: database.json only exists in version 1.1.0 or higher.
 * skillInfo < skillName | all > : Displays the player's own level and exp for < skillName > or all skills
 * skillList : Displays the names of all currently existing skills
 * skillTop < skillName > : Displays currently online players ranked from highest to lowest level in that skill (Max 20 players, to be improved later)
 * admin : Admin-only commands
   * give
     * exp < player > < skillName > < integer > : Gives < integer > amount of exp to < player > for < skillName >
     * level < player > < skillName > < integer > : Gives < integer > amount of levels to < player > for < skillName >
   * set
     * exp < player > < skillName > < integer > : Sets the exp of < player >'s < skillName > to < integer >
     * level < player > < skillName > < integer > : Sets the level of < player >'s < skillName > to < integer >
   * reset
     * < player > all : Resets all levels and exp of < player > to 0
     * < player > < skillName > : Resets < skillName > of < player > to 0
   * list
     * < player > all : Displays all levels and exp
     * < player > < skillName > : Displays level and exp for < skillName >
   * data
     * saveAllData : Saves all data
     * backup : Backs up all data
     * loadData < json | mysql | sqlite > < zip File Name > : Loads auto-backed up files
       * WARN: MYSQL, SQLITE are supported from version 1.1.0
원하시는 대로 형식을 그대로 유지하며 내용만 영어로 번역해 드렸습니다. 추가로 수정하고 싶은 부분이 있으신가요?
