# Platen 작업 안내 (에이전트용)

이 파일은 이 폴더에서 일하는 에이전트(Hermes 쌤)가 먼저 읽는다. 사용자는 Git 과 웹 개발이 처음인 대학원생이다. 설명은 짧게, 질문은 한 번에 하나, 실행 전에 무엇을 할지 한 줄로 말한다.

## 프로젝트

- `index.html` 한 파일이 전부다. 빌드·서버·패키지 없음. 외부 라이브러리를 넣지 않는다 (Google Fonts 예외).
- 파일을 나누지 않는다. CSS·JS 는 `index.html` 안의 `<style>`·`<script>` 에 둔다.
- 기존 기능을 지키면서 작은 기능 하나를 더한다: 타이핑과 한글 자모 조합, 램프 슬라이더 세 개, 램프 켜고 끄기, 자동 타이핑, 리셋, 타자 소리.

## Git 규칙

1. 시작할 때 `git status` 와 `git branch --show-current` 를 본다. **`main` 에서는 작업하지 않는다.** 브랜치가 `main` 이면 `git switch -c feat/<이름>-<기능>` 으로 새 브랜치를 만든다 (영문 소문자, 하이픈).
2. 큰 변경 직전에는 커밋한다. 커밋이 세이브 포인트다.
3. 변경을 마치면 사용자에게 **브라우저에서 `index.html` 을 열어 직접 확인**하라고 요청하고, 괜찮다는 답을 받은 뒤에 커밋한다. 커밋 메시지는 한국어 한 줄, "무엇을 왜" (예: `램프 색 선택 버튼: 따뜻함/차가움 두 단계`).
4. PR 은 `git push -u origin <브랜치>` 뒤 `gh pr create --title "[분반] 이름: 기능" --body "..."` 로 만든다. 분반과 이름을 모르면 묻는다. 본문은 `.github/pull_request_template.md` 의 네 항목(무엇을·왜·어떻게 확인·화면)을 채운다.
5. 원본 최신으로 맞추기: `git fetch upstream && git rebase upstream/main`. 작업 중 변경이 있으면 `git stash` → rebase → `git stash pop`. 충돌이 나면 충돌 난 부분을 사용자에게 보여 주고 어느 쪽을 남길지 같이 정한다. rebase 뒤 이미 올린 브랜치를 다시 올릴 때만 `git push --force-with-lease origin <내 브랜치>` 를 쓴다.
6. 하지 않는다: `main` 으로 push, `main` 이나 남의 브랜치에 force push, 묻지 않고 `git reset --hard`, 다른 사람 브랜치 수정, 토큰·키·이메일을 파일에 쓰기.

## 작업 순서

superpowers 가 있으면 `brainstorming` 으로 기능의 범위를 한 문장으로 좁히고, 사용자 승인 뒤 구현한다. 없으면 같은 순서를 직접 지킨다: 무엇을 만들지 한 문장 → 승인 → 구현 → 사용자 확인 → 커밋 → PR.

## Cursor Cloud specific instructions

- 패키지 설치와 빌드는 없다. `npm install` 을 하지 않는다. 앱은 `index.html` 하나다.
- 부팅되면 `python3 -m http.server 8000 --bind 0.0.0.0` 가 이미 떠 있다. 8000 포트가 열려 있으면 서버를 또 띄우지 않는다. 주소는 http://127.0.0.1:8000
- 확인은 브라우저에서 한다. 자동 타이핑으로 글자 수가 늘어나는지, 종이를 누른 뒤 자판 `r` `k` 가 `가` 로 조합되는지, 램프 슬라이더 세 개와 램프 버튼, 오른쪽 잉크병(글자 크기), 왼쪽 화살표 리셋이 되는지 본다.
- Google Fonts 가 늦어도 타이핑과 램프는 동작한다.
