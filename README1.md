## This Plugin Isn't launched!

# The world's most stable and flexible RPG Minecraft plugin "DRPG_LevelSystem".

---

** This plugin is a professional RPG skill leveling system designed to provide the highest level of stability, scalability, and ease of debugging for Minecraft servers. All core logic is completely customizable via JSON files, significantly reducing the complexity of server operation. **

---

## 1. Competitive Advantages

** The Plugin System focuses on fundamentally solving common problems in existing RPG plugins, such as data errors, balancing difficulty, and maintenance complexity. **

---

### 1.1. Data Integrity Guarantee: Complete Resolution of Data Inconsistency (Desync) Issues

* **Centralized Cache System (PlayerJsonManager):** All player data is stored in a centralized memory cache. It is loaded upon player login (`loadPlayerJson`) and saved immediately upon logout (`savePlayerJson`), minimizing data loss.

* **Forced Command-Cache Synchronization (Critical Stability):** To prevent data inconsistency (Desync) after using administrator commands (e.g., `/DRPG setLevel`, `/DRPG addExp`), all data modification logic is forced to go through the central cache and immediately saved to disk after modification. This completely eliminates the possibility of data rollback that can occur upon server reboot.
