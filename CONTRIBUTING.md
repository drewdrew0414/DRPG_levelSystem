# CONTRIBUTING GUIDE / 기여 및 피드백 가이드

Thank you for contributing to the DrewRPG Level System project! Your feedback and reports are invaluable in advancing this plugin.
DrewRPG Level System 프로젝트에 기여해 주셔서 감사합니다! 여러분의 피드백과 보고는 이 플러그인을 더욱 발전시키는 데 큰 힘이 됩니다.

## 1. Bug Reports and Issue Reports / 버그 보고 및 문제점 보고

If you discover an issue or encounter an unexpected error during server operation, please follow the detailed steps below to report it.
서버 운영 중 문제점이나 예상치 못한 오류를 발견하신 경우, 다음 상세 절차를 따라 보고해 주시면 됩니다.

* **상세 보고는 필수:** 정확한 정보는 문제의 신속한 파악 및 해결에 결정적인 도움이 됩니다.
    * **Detailed Reporting is Critical:** Accurate information allows for quick identification and resolution of the problem.

### A. 자가 진단 체크리스트 (Self-Diagnosis Checklist)

보고 전에 다음 단계를 확인하여 문제의 원인을 좁힐 수 있습니다.

1.  **무결성 검사:** 관리자 명령어 `/drpg validate`를 실행하여 JSON 설정 파일(`skills`, `rewards`, `playerdata`)에 문법적 오류나 데이터 누락이 없는지 확인합니다.
2.  **디버그 로그 확보:** `config.json`에서 `Debug.useDebug`를 `true`로 설정하고 서버를 재로드하여 콘솔이나 로그 파일(`rpg-log.txt`)에 기록된 오류 메시지(Stack Trace)를 확보합니다.
3.  **재현 단계 기록:** 문제가 어떻게 발생했는지 (예: "A라는 아이템으로 B 블록을 부쉈을 때 발생함") 상세한 단계를 기록합니다.

### B. 공식 보고 채널 (Official Reporting Channels)

자가 진단 후 확보한 정보를 포함하여 아래 채널 중 하나를 통해 보고해 주십시오.

* **권장 채널:** **GitHub Issues**
    * 가장 선호되는 보고 방식입니다. 문제 재현 단계, 확보한 디버그 로그, 사용 중인 서버 환경(Paper/Spigot 버전, 플러그인 버전 등)을 상세히 기재해 주십시오.
* **이메일:** **drew0414drew@gmail.com**
    * GitHub 사용이 어렵거나 비공개적으로 보고하고 싶을 경우, 상세한 오류 내용과 관련 로그 파일을 첨부하여 보내주십시오.

---

## 2. Feature Requests and Suggestions / 기능 요청 및 제안

새로운 기능 아이디어, 기존 기능 변경 요청 또는 성능 개선에 대한 제안이 있다면 언제든지 환영합니다.

* **공식 채널:** GitHub Issues 또는 이메일(`drew0414drew@gmail.com`)
* **포함 정보:** 제안의 목적, 구현 시 예상되는 이점, 현재 플러그인 버전

---

## 3. Code & Localization Contributions / 코드 및 현지화 기여 (개발 기여)

Pull Requests (PRs) for code improvements, bug fixes, or localization files (e.g., `messages.yml`) are welcome. Please ensure your contributions adhere to the following guidelines:
코드 개선, 버그 수정, 또는 현지화 파일(예: `messages.yml`)에 대한 Pull Request(PR)를 환영합니다. 기여 시 다음 가이드라인을 준수해 주십시오.

* **Code Style:** Java Code should follow standard Minecraft/Spigot API practices.
* **Localization:** If submitting a new language file, please ensure all keys are included and properly translated.
* **PR Description:** Clearly describe the purpose and scope of your changes in the Pull Request title and body.
2.  **디버그 로그 확보:** `config.json`에서 `Debug.useDebug`를 `true`로 설정하고 서버를 재로드하여 콘솔이나 로그 파일(`rpg-log.txt`)에 기록된 오류 메시지(Stack Trace)를 확보합니다.
3.  **재현 단계 기록:** 문제가 어떻게 발생했는지 (예: "A라는 아이템으로 B 블록을 부쉈을 때 발생함") 상세한 단계를 기록합니다.

### B. 공식 보고 채널 (Official Reporting Channels)

자가 진단 후 확보한 정보를 포함하여 아래 채널 중 하나를 통해 보고해 주십시오.

* **권장 채널:** **GitHub Issues**
    * 가장 선호되는 보고 방식입니다. 문제 재현 단계, 확보한 디버그 로그, 사용 중인 서버 환경(Paper/Spigot 버전, 플러그인 버전 등)을 상세히 기재해 주십시오.
* **이메일:** **drew0414drew@gmail.com**
    * GitHub 사용이 어렵거나 비공개적으로 보고하고 싶을 경우, 상세한 오류 내용과 관련 로그 파일을 첨부하여 보내주십시오.

## 2. Feature Requests and Suggestions / 기능 요청 및 제안

If you have an idea for a new feature, a change to existing functionality, or a performance improvement, we welcome your suggestions.
새로운 기능 아이디어, 기존 기능의 변경 제안, 또는 성능 개선 아이디어가 있다면 언제든지 환영합니다.

* **Feature Proposal:** Please clearly explain the necessity of the feature, the use case for server operation, and the expected benefits for end-users.
    * **기능 제안:** 해당 기능의 필요성, 서버 운영에서의 사용 시나리오, 그리고 최종 사용자에게 미치는 기대 이점을 명확하게 설명해 주십시오.

## 3. Documentation Improvement / 문서 개선 제안

If you find any ambiguities, missing explanations, or errors in the provided documentation (`README.md`, `commands.md`, etc.), please report them.
제공된 문서(`README.md`, `commands.md` 등)에서 모호한 부분, 설명이 부족한 부분, 또는 오류가 있다면 알려주십시오.

