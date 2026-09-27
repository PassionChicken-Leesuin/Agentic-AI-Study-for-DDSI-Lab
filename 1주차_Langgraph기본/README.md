# 1주차 — LangGraph 기본

LangGraph의 기본 개념(그래프 생성, 모델 연결, QuickStart)을 다룹니다.
교재 노트북은 [Langgraph_Study](https://github.com/PassionChicken-Leesuin/Langgraph_Study) (Teddy님 LangGraph 튜토리얼 기반)에서 가져왔으며, **이 폴더만으로 환경 구성이 끝나도록** 필요한 설정 파일을 모두 포함해 두었습니다. 다른 repo를 clone할 필요 없습니다.

## 폴더 구성

```
1주차_Langgraph기본/
├─ README.md          ← 지금 보고 있는 파일
├─ pyproject.toml     ← 의존성 목록
├─ uv.lock            ← 버전 고정 (전원 동일한 환경 보장)
├─ .python-version    ← Python 버전 고정
├─ .env.example       ← API 키 템플릿
├─ notebooks/         ← 교재 노트북 (직접 수정하지 마세요!)
│  ├─ 01-LangGraph-Introduction.ipynb
│  ├─ 01-LangGraph-Models.ipynb
│  └─ 01-QuickStart-LangGraph-Tutorial.ipynb
└─ submissions/       ← 퀴즈 제출 폴더 (각자 자기 이름 폴더에 제출)
```

## 환경 설정 (최초 1회)

### 1. uv 설치

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

### 2. repo clone 및 의존성 설치

```bash
git clone https://github.com/PassionChicken-Leesuin/Agentic-AI-Study-for-DDSI-Lab.git
cd Agentic-AI-Study-for-DDSI-Lab/1주차_Langgraph기본
uv sync
```

`uv sync` 한 번이면 Python 설치 + 가상환경 생성 + 모든 패키지 설치가 끝납니다. (몇 분 걸릴 수 있어요.)

### 3. API 키 설정

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

### 4. 노트북 실행

VS Code 사용 시: 노트북을 열고 우측 상단에서 커널을 `.venv`의 Python으로 선택하세요.

Jupyter를 직접 띄우려면:

```bash
uv run jupyter lab
```

## 학습 순서

1. `01-LangGraph-Introduction.ipynb` — LangGraph가 무엇인지, 왜 쓰는지
2. `01-LangGraph-Models.ipynb` — LLM 모델을 LangGraph에 연결하는 법
3. `01-QuickStart-LangGraph-Tutorial.ipynb` — 처음부터 끝까지 그래프 만들어보기

각 노트북 끝의 **퀴즈 셀**을 풀어서 제출하면 그 주차 학습 완료입니다.

## 퀴즈 제출 방법

자세한 브랜치/PR 규칙은 [0주차 README](../0주차_Github%20협업/README.md)를 참고하세요. 요약하면:

```bash
# 1. 최신 main에서 자기 브랜치 생성 (이름은 본인 이름으로)
git switch main
git pull
git switch -c week1/홍길동

# 2. notebooks/의 노트북 3개를 submissions/본인이름/ 폴더로 복사
#    (본인 이름 폴더는 이미 만들어져 있습니다. 원본 notebooks/ 는 절대 수정하지 않습니다)
cp notebooks/*.ipynb submissions/홍길동/

# 3. 복사본에서 퀴즈 셀을 풀고 커밋
git add submissions/홍길동/
git commit -m "1주차 퀴즈 제출 - 홍길동"

# 4. 브랜치 push 후 GitHub에서 Pull Request 생성
git push -u origin week1/홍길동
```

PR 제목: `[1주차] 홍길동 퀴즈 제출` — 리뷰(approve) 후 merge됩니다.
