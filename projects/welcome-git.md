# Welcome-git · Git desktop client

[← 포트폴리오](../README.md) · [내 포크](https://github.com/Ontheway-01/Welcome-git) · [팀 원본 저장소](https://github.com/so0-biin/Welcome-git)

**Git 명령의 결과를 파일 상태, 브랜치 목록, 커밋 그래프와 상세 정보로 보여주는 C# 데스크톱 프로젝트에 참여했습니다.**

2023년 오픈소스SW 팀 프로젝트 · `C#` `Windows Forms` `Git CLI` `Process I/O`

## 프로젝트와 본인 역할

Welcome-git은 기존 [FileManager](https://github.com/arsabyaneh/FileManager)를 확장한 Windows용 Git GUI입니다. 팀 전체 기능에는 파일 탐색, 저장소 생성, 버전 관리, 브랜치 관리·병합, 이력 조회와 clone이 포함됩니다.

본인은 **브랜치 생성·삭제·이름 변경·checkout, 커밋 이력의 표시·상세 정보 파싱, 파일 상태 표시와 관련 오류 처리**에 기여했습니다. 원본 파일 탐색기와 팀원의 작업을 포함한 전체 기능을 개인 구현으로 제시하지 않습니다.

## 1. Git 프로세스와 GUI 연결

Windows의 `ProcessStartInfo`로 명령 프로세스를 실행하고, 표준 입력으로 Git 명령을 전달하며 표준 출력·오류를 읽는 구조를 사용했습니다. 현재 탐색 중인 디렉터리를 이력 화면과 브랜치 제어에 전달해 사용자가 보고 있는 저장소에 명령을 적용합니다.

브랜치 목록에서 우클릭 메뉴로 삭제·이름 변경·checkout을 수행하고, 실행 후 브랜치 목록과 커밋 그래프를 다시 불러오도록 연결했습니다. 명령의 결과가 화면에 남은 이전 상태와 어긋나지 않게 갱신 시점을 다뤘습니다.

## 2. 커밋 그래프와 상세 정보

`git log --pretty=oneline --graph`의 결과를 그래프·축약 hash·메시지로 나누어 목록에 표시하는 흐름에 기여했습니다. 커밋을 선택하면 전체 hash로 `git cat-file -p`를 실행해 parent·author·committer·메시지를 보여줍니다.

그래프 연결선만 있는 행에는 커밋 hash가 없으므로 상세 조회를 수행하지 않도록 처리했습니다. 서명 정보가 포함된 커밋 메시지의 파싱과 checkout·merge 후 그래프 새로고침도 수정했습니다.

## 3. 파일·저장소 상태에 따른 동작

추적되지 않은 파일, staged 변경, 수정된 파일, 변경이 없는 파일을 상태·색상·아이콘으로 구분하는 작업에 기여했습니다. 파일명 뒷부분이 같은 서로 다른 경로의 상태가 함께 바뀌는 문제, rename·index 삭제에 따른 상태 표시도 수정했습니다.

저장소가 아닌 경로에서 이력 버튼을 누르거나, 충돌이 남아 commit이 실패하는 경우에는 성공으로 안내하지 않도록 오류 표시를 보완했습니다. Git의 상태를 GUI의 버튼·목록·메시지로 표현한 경험입니다.

## 구현 범위

Git CLI를 GUI와 연결한 학부 팀 프로젝트입니다. 브랜치·커밋 구조를 새로 구현한 Git 엔진이 아니며, 기존 파일 탐색기 위에 작업 흐름을 확장했습니다. 당시 명령 문자열과 출력 형식에 의존하는 파싱은 공백·특수문자 경로와 실행 실패에 대한 추가 검증이 필요한 부분입니다.

<details>
<summary>본인 기여와 구현 근거</summary>

- [브랜치 삭제·이름 변경·checkout · 2fa51a4](https://github.com/so0-biin/Welcome-git/commit/2fa51a4c2ab3a1f884a2637bf9e3ed9ec6059331)
- [커밋 상세 표시 · 89fdc47](https://github.com/so0-biin/Welcome-git/commit/89fdc479cda46fe4641a15b091f88a57e7ba4f07)
- [파일 경로별 상태 수정 · 9c7817b](https://github.com/so0-biin/Welcome-git/commit/9c7817b63ed69ebb1f966a5ff0756a10e72f82bf)
- [충돌 중 commit 오류 표시 · 0f39ced](https://github.com/so0-biin/Welcome-git/commit/0f39ced1bb256dc58fd7da886bb2163ddc3e0885)
- [BranchList.cs](https://github.com/so0-biin/Welcome-git/blob/main/Controls/BranchList.cs) · [CommitHistory.cs](https://github.com/so0-biin/Welcome-git/blob/main/Controls/CommitHistory.cs) · [HistoryMenu.cs](https://github.com/so0-biin/Welcome-git/blob/main/HistoryMenu.cs)
- [전체 기여 기록](https://github.com/so0-biin/Welcome-git/commits?author=Ontheway-01)

</details>
