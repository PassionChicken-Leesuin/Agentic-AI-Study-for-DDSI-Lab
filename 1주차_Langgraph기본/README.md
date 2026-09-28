# 1주차 — LangGraph 기본

LangGraph의 기본 개념(그래프 생성, 모델 연결, QuickStart)을 다룹니다.
교재 노트북은 [Langgraph_Study](https://github.com/PassionChicken-Leesuin/Langgraph_Study) (Teddy님 LangGraph 튜토리얼 기반)에서 가져왔으며, **이 폴더만으로 환경 구성이 끝나도록** 필요한 설정 파일을 모두 포함해 두었습니다. 다른 repo를 clone할 필요 없습니다.

> 0주차([GitHub 협업으로 Contributor 되어보기](../0주차_Github%20협업/README.md))를 먼저 완료하고 오시면, 이 문서의 제출 흐름이 훨씬 익숙하게 느껴질 거예요.

## 폴더 구성

```
1주차_Langgraph기본/
├─ README.md          ← 지금 보고 있는 파일
├─ pyproject.toml     ← 의존성 목록
├─ uv.lock            ← 버전 고정 (전원 동일한 환경 보장)
├─ .python-version    ← Python 버전 고정
├─ .env.example       ← API 키 템플릿
├─ notebooks/         ← 교재 원본 노트북 (직접 수정하지 마세요!)
│  ├─ 01-LangGraph-Introduction.ipynb
│  ├─ 01-LangGraph-Models.ipynb
│  └─ 01-QuickStart-LangGraph-Tutorial.ipynb
└─ submissions/       ← 각자 자기 이름 폴더 안의 '본인 노트북'으로 학습·제출
   └─ 본인이름/
      ├─ 본인이름_01-LangGraph-Introduction.ipynb
      ├─ 본인이름_01-LangGraph-Models.ipynb
      └─ 본인이름_01-QuickStart-LangGraph-Tutorial.ipynb
```

## 사전 준비 (최초 1회)

1. GitHub 계정 생성 후 스터디장에게 계정명 알려주기 → collaborator로 초대받기 (가입 이메일로 오는 초대 수락 필수)
2. [Git 설치](https://git-scm.com/downloads)
3. 본인 정보 등록:

```bash
git config --global user.name "본인이름"
git config --global user.email "GitHub가입이메일"
```

## 환경 설정 (최초 1회)

### 1. VS Code 준비

1. [VS Code 설치](https://code.visualstudio.com/) 후 실행합니다.
2. 왼쪽 확장(Extensions) 탭에서 **Python**과 **Jupyter** 확장을 설치합니다.
3. 상단 메뉴 **File → Open Folder...** 로 이 스터디 자료를 내려받을 폴더(예: `문서/스터디`)를 엽니다.
4. 상단 메뉴 **Terminal → New Terminal** (단축키 `` Ctrl+` ``)로 터미널을 엽니다.

> 아래의 모든 명령어는 이렇게 연 **VS Code 안의 터미널**에 입력하면 됩니다.

### 2. uv 설치

[uv](https://docs.astral.sh/uv/)는 Python 패키지 관리자입니다. 터미널에서:

```powershell
# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh
```

설치 후 터미널을 **새로 열고** `uv --version`이 찍히는지 확인하세요.

### 3. repo clone 및 의존성 설치

```bash
git clone https://github.com/PassionChicken-Leesuin/Agentic-AI-Study-for-DDSI-Lab.git
```

clone이 끝나면 **File → Open Folder...** 로 방금 생긴 `Agentic-AI-Study-for-DDSI-Lab` 폴더를 다시 엽니다.
(⚠️ 반드시 이 repo 폴더를 루트로 열어주세요 — 퀴즈용 워크스페이스 설정이 이때 적용됩니다.)

새로 열린 창에서 다시 터미널을 열고(`` Ctrl+` ``):

```bash
cd 1주차_Langgraph기본
uv sync
```

`uv sync` 한 번이면 Python 설치 + 가상환경 생성 + 모든 패키지 설치가 끝납니다. (몇 분 걸릴 수 있어요.)

### 4. API 키 설정

`.env.example`을 복사해서 같은 폴더에 `.env` 파일을 만들고, 본인의 API 키를 채워 넣으세요:

```bash
# macOS / Linux
cp .env.example .env
```

```powershell
# Windows (PowerShell)
Copy-Item .env.example .env
```

| 키 | 발급처 | 필수 여부 |
|---|---|---|
| `OPENAI_API_KEY` | https://platform.openai.com/api-keys | 필수 |
| `ANTHROPIC_API_KEY` | https://console.anthropic.com/ | 선택 |
| `LANGSMITH_API_KEY` | https://smith.langchain.com/ (무료) | 선택 (트레이싱 확인용, 추천) |
| `TAVILY_API_KEY` | https://tavily.com/ (무료) | 선택 |

> ⚠️ `.env`는 절대 커밋하지 마세요. `.gitignore`에 이미 등록되어 있지만, PR 올리기 전에 한 번 더 확인!

### 5. 노트북 실행

`submissions/본인이름/` 폴더의 본인 노트북을 열고, 우측 상단 **Select Kernel**에서 `.venv`의 Python을 선택하세요.

Jupyter를 직접 띄우려면:

```bash
uv run jupyter lab
```

## GitHub 협업 핵심 개념 3줄 요약

- **main 브랜치**: 교재(원본 노트북)가 있는 곳. 직접 push 금지 — 보호 설정되어 있어 어차피 안 됩니다.
- **내 브랜치**: main에서 갈라져 나온 나만의 작업 공간. 여기서 뭘 해도 main은 안 바뀝니다.
- **Pull Request (PR)**: "내 브랜치의 변경사항을 main에 합쳐주세요"라는 요청. 스터디장이 리뷰(approve)하면 merge되어 main에 반영됩니다.

> 🤖 **AI 도구 사용 원칙**: 퀴즈(파일 내용)를 푸는 데는 AI 도구를 참고할 수 있지만, 브랜치 생성·커밋·푸시·PR 등 **GitHub 협업 작업은 터미널에서 명령어를 직접 실행**하는 것을 기본 원칙으로 합니다. (0주차와 동일)

## 학습 및 퀴즈 제출 방법

### 1. 최신 main 받아오기

```bash
git switch main
git pull
```

### 2. 내 브랜치 만들기

브랜치 이름 규칙: `week{주차}/{본인이름}` (예: `week1/홍길동`)

```bash
git switch -c week1/홍길동
```

### 3. 학습 및 퀴즈 풀기

`submissions/본인이름/` 폴더에 **본인 이름이 붙은 노트북 3개**가 미리 들어 있습니다. 복사할 필요 없이 바로 열어서 아래 순서로 학습하세요. (**원본 `notebooks/`는 절대 수정하지 않습니다.**)

1. `본인이름_01-LangGraph-Introduction.ipynb` — LangGraph가 무엇인지, State 관리 체계 이해하기
2. `본인이름_01-LangGraph-Models.ipynb` — LLM 모델을 LangGraph에 연결하는 법
3. `본인이름_01-QuickStart-LangGraph-Tutorial.ipynb` — 처음부터 끝까지 그래프 만들어보기

각 노트북 끝의 🧩 퀴즈 빈칸(`________`)을 채우고, 셀을 실행해 통과를 확인하세요.

### 4. 커밋하기

```bash
git add 1주차_Langgraph기본/submissions/홍길동/
git status          # 의도한 파일만 올라가는지 확인! (.env 같은 게 섞이면 안 됨)
git commit -m "1주차 퀴즈 제출 - 홍길동"
```

### 5. push & Pull Request

```bash
git push -u origin week1/홍길동
```

push 후 GitHub repo 페이지에 뜨는 **"Compare & pull request"** 버튼을 누르거나,
`Pull requests` 탭 → `New pull request` → `base: main ← compare: week1/홍길동` 선택.

- PR 제목: `[1주차] 홍길동 퀴즈 제출`
- PR 본문: 어려웠던 점, 질문 등 자유롭게

### 6. 리뷰 & merge

스터디장이 PR을 확인하고 코멘트/approve 합니다.
수정 요청이 오면 **같은 브랜치에서** 고치고 다시 `git add` → `commit` → `push` 하면 PR에 자동 반영됩니다.
approve 후 merge되면 제출 완료! 🎉

## 자주 묻는 질문

**Q. 다음 주차가 올라오면 어떻게 받나요?**
A. 매주 세 줄이면 됩니다: `git switch main` → `git pull` → `git switch -c week2/본인이름`. 이후 흐름(풀기 → 커밋 → PR)은 이번 주와 동일해요.

**Q. 내 브랜치에서 실수하면 main도 망가지나요?**
A. 아니요. 브랜치는 완전히 독립된 작업 공간이고, main은 merge 전까지 절대 안 바뀝니다. 게다가 main은 보호되어 있어서 리뷰 없이는 merge 자체가 불가능합니다. 마음껏 실험하세요.

**Q. 내 브랜치를 만든 뒤에 main에 새 파일이 추가됐는데, 내 브랜치에는 안 보여요.**
A. 브랜치는 갈라져 나온 시점의 상태를 기준으로 하기 때문에, 그 이후 main의 변경사항은 자동으로 따라오지 않습니다. main을 내 브랜치로 merge해오면 됩니다:

```bash
git switch main
git pull
git switch week1/홍길동
git merge main
```

작업 시작 전에 한 번씩 해주는 습관을 들이면 나중에 PR 충돌이 줄어듭니다.

**Q. 다른 사람 제출물과 충돌(conflict)나지 않나요?**
A. 각자 `submissions/본인이름/` 폴더만 건드리므로 충돌이 생길 수 없습니다. 충돌이 났다면 자기 폴더 밖의 파일을 수정한 것이니 스터디장에게 문의하세요.

**Q. 브랜치를 잘못 만들었어요.**
A. 새로 만들면 됩니다. `git switch main` → `git switch -c week1/홍길동` 부터 다시.

**Q. push할 때 권한 오류가 나요.**
A. collaborator 초대를 수락했는지 확인하세요 (GitHub 가입 이메일로 초대장이 갑니다).
