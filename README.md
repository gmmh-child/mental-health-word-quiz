# 정신건강 가로세로 낱말퀴즈 — GitHub Pages + Google 스프레드시트

## 파일 구성
- `index.html`: GitHub Pages에 배포할 퀴즈 페이지 (배경 선명도 수정본, 참여자 CSV 다운로드 버튼 없음)
- `Code.gs`: Google Apps Script 응답 수신 코드

## A. Google 스프레드시트 연결
1. Google 스프레드시트를 새로 만들거나 기존 응답용 시트를 엽니다.
2. 주소 `https://docs.google.com/spreadsheets/d/문서ID/edit` 중 `문서ID` 부분을 복사합니다.
3. `Code.gs` 상단의 `SPREADSHEET_ID` 값에 붙여 넣습니다. 따옴표는 유지합니다.
4. 스프레드시트에서 **확장 프로그램 → Apps Script**를 엽니다. 기본 `Code.gs` 내용을 이 패키지의 `Code.gs` 내용으로 교체하고 저장합니다.
5. 함수 선택 메뉴에서 `setupSheet`를 선택하고 **실행**합니다. 최초 실행 시 권한 승인이 필요합니다. 정상 실행되면 `퀴즈 응답` 탭이 준비됩니다.
6. **배포 → 새 배포 → 유형 선택(톱니바퀴) → 웹 앱**으로 설정합니다.
   - 다음 사용자로 실행: **나**
   - 액세스 권한: 참여자가 로그인 없이 제출해야 한다면 조직 정책에 맞게 **모든 사용자** 등 허용 가능한 옵션을 선택합니다.
7. **배포**를 누르고 웹 앱 URL의 `/exec` 주소를 복사합니다.

## B. 웹 앱 URL을 HTML에 연결
1. `index.html`을 편집기로 엽니다.
2. `const GOOGLE_APPS_SCRIPT_URL = "...";` 부분을 찾습니다.
3. 따옴표 안을 방금 배포한 웹 앱 `/exec` URL로 바꾸고 저장합니다.
4. 수정한 `index.html`을 GitHub 저장소 `gmmh-child/mental-health-word-quiz`의 기존 `index.html`과 교체해 커밋합니다.
5. GitHub Pages 페이지에서 테스트 응답을 제출하고 Google 스프레드시트의 `퀴즈 응답` 탭에 새 행이 생기는지 확인합니다.

## C. GitHub Pages 배포
1. 저장소 `https://github.com/gmmh-child/mental-health-word-quiz`를 엽니다.
2. `index.html`을 새 버전으로 교체합니다.
3. `Code.gs`는 GitHub Pages에서 실행되는 파일이 아닙니다. Apps Script 편집기에 별도로 붙여 넣어야 합니다. 저장소에 보관할 수는 있지만, 실제 실행과 배포는 Apps Script에서 합니다.
4. GitHub Pages는 `index.html`을 공개합니다. 스프레드시트 ID를 HTML에 넣지 말고, 스프레드시트 공유 권한은 관리자만 접근하도록 제한하세요.

## 확인 사항
- HTML은 `respondent`, `phone`, `area`, `childAge`, `gender`, `privacyConsent`, `answers`, `score`, `total`, `submittedAt` 필드를 전송합니다.
- `Code.gs`는 위 필드를 `퀴즈 응답` 탭의 각 열에 저장합니다.
- HTML은 브라우저의 `no-cors` 방식으로 요청하므로 제출 화면만으로 저장 성공 여부를 확정할 수 없습니다. 테스트 후 스프레드시트에 행이 실제로 추가됐는지 확인하세요.
- 응답에는 이름과 연락처 등 개인정보가 포함될 수 있으므로, 수집 목적·보유기간·파기 방법을 기관의 개인정보 처리 기준에 맞게 확인하고 스프레드시트 접근 권한을 제한하세요.


## 기관 로고 수정
- 하단의 기관명 문구를 제거하고, 제공된 기관 로고만 작은 크기로 표시하도록 수정했습니다.
- 로고는 HTML에 포함되어 있어 별도 이미지 파일을 GitHub에 올릴 필요가 없습니다.
