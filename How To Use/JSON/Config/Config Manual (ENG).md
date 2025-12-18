===============
Made By drewdrew0414 (or drewdrew1_)
===============
Looking for this? -> [example config.json](../../../How%20To%20Use/JSON/Config/example)
1. configVersion & usePlugin (ENG)
{
  "configVersion": "1.0.0",
  "usePlugin": true
}

▸ configVersion
 * Current version of the configuration file
 * Used for automatic migration or compatibility checks during plugin updates
 * May output warning logs if the value does not match
▸ usePlugin
 * true : Plugin operates normally
 * false : Disables all plugin functions (Safe Mode)
 * Use this to temporarily block features without stopping the server
2. Debug (ENG)
"Debug": {
  "useDebug": true,
  "Debug-Default": true,
  "retryOnError": true,
  "retryCount": 3
}

▸ useDebug
 * Whether to enable debug mode
 * If true, outputs detailed information on file loading, parsing, registration, and error causes
▸ Debug-Default
 * Whether to output basic debug logs
 * If false, only critical errors are displayed
▸ retryOnError
 * Whether to automatically retry when file loading/parsing fails
▸ retryCount
 * Number of retry attempts
 * Only used when retryOnError is set to true
3. Logging (ENG)
"Logging": {
  "logToConsole": true,
  "logToFile": true,
  "logFileName": "log.txt",
  "includeDebug": true,
  "includeStackTrace": true,
  "includeJsonError": true,
  "includePerformance": false
}

▸ logToConsole
 * Whether to output logs to the console
▸ logToFile
 * Whether to record logs to a file
▸ logFileName
 * Name of the log file (located in plugins/DRPG/logs/)
▸ includeDebug
 * Whether to include debug logs
▸ includeStackTrace
 * Includes StackTrace when an exception occurs
▸ includeJsonError
 * Outputs detailed JSON parsing errors
▸ includePerformance
 * Outputs logs related to processing time and performance
4. Performance (ENG)
"Performance": {
  "useAsync": true,
  "asyncThreads": 2,
  "centralAsyncExecutor": true,
  "useCache": true,
  "cacheExpireSeconds": 120,
  "preventDesync": true
}

▸ useAsync
 * Process heavy tasks asynchronously
▸ asyncThreads
 * Number of asynchronous threads
▸ centralAsyncExecutor
 * Whether to use a centralized thread pool
▸ useCache
 * Use cache for skills / rewards / settings
▸ cacheExpireSeconds
 * Cache expiration time (seconds)
▸ preventDesync
 * Prevents data inconsistency during asynchronous processing
5. PlayerData (ENG)
"PlayerData": {
  "storageType": "JSON",
  "autoSave": true,
  "saveIntervalSeconds": 300,
  "autoBackup": true,
  "backupIntervalMinutes": 30,
  "backupMaxFiles": 10
}

▸ storageType
 * Method for storing player data
 * Supports JSON, SQLite, MySQL
▸ autoSave
 * Whether to enable automatic saving
▸ saveIntervalSeconds
 * Interval for automatic saving (seconds)
▸ autoBackup
 * Whether to use automatic backups
▸ backupIntervalMinutes
 * Interval for creating backups
▸ backupMaxFiles
 * Maximum number of backup files (old files are deleted when exceeded)
6. Permissions (ENG)
"Permissions": {
  "opOnly": true,
  "useLuckPerms": true,
  "ignoreNoPermissionMessage": false
}

▸ opOnly
 * Whether features are restricted to OPs only
▸ useLuckPerms
 * Whether to integrate with LuckPerms
▸ ignoreNoPermissionMessage
 * Hides the message when a player lacks permission
7. Skill (ENG)
"Skill": {
  "validateSkillFiles": true,
  "stopOnCriticalError": false,
  "autoFixSimpleError": true
}

▸ validateSkillFiles
 * Validates the integrity of skill JSON files
▸ stopOnCriticalError
 * Stops the system if a critical error occurs
▸ autoFixSimpleError
 * Attempts to automatically fix simple errors
8. Reward (ENG)
"Reward": {
  "validateRewardFiles": true,
  "preventDuplicateReward": true,
  "cooldownSeconds": 10,
  "Notify": {
    "chat": true,
    "actionBar": true,
    "title": false,
    "subtitle": false
  }
}

▸ validateRewardFiles
 * Validates the integrity of reward JSON files
▸ preventDuplicateReward
 * Prevents duplicate reward distribution
▸ cooldownSeconds
 * Cooldown for reward distribution (seconds)
▸ Notify
 * Settings for reward notification methods
   * chat / actionBar / title / subtitle
9. Protection (ENG)
"Protection": {
  "preventOverflow": true,
  "preventAsyncRace": true,
  "safeModeOnException": true
}

▸ preventOverflow
 * Prevents EXP/Level overflow
▸ preventAsyncRace
 * Prevents asynchronous race conditions
▸ safeModeOnException
 * Enters Safe Mode when an exception occurs
10. VersionControl (ENG)
"VersionControl": {
  "checkPluginVersion": true,
  "executeOnlySupportedFeatures": true
}

▸ checkPluginVersion
 * Checks the plugin version
▸ executeOnlySupportedFeatures
 * Executes only the features supported by the current version
11. PlaceholderAPI Integration (ENG)
"PlaceholderAPI": {
  "enable": true
}

▸ enable
 * Enables PlaceholderAPI integration
 * Allows usage of placeholders like %drpg_level%, %drpg_skill_xp%, etc.
Would you like me to translate any other files or documentation for this plugin?
