# 2주차 — Messages & Graph API

1주차 QuickStart에서 챗봇을 "일단 돌려봤다"면, 2주차는 그때 그냥 지나쳤던 것들을 제대로 이해하는 주입니다.

- **Messages**: 챗봇과 주고받던 `HumanMessage`, `AIMessage`가 정확히 뭐였는지 — 4가지 메시지 유형과 도구 호출 대화 흐름
- **Graph API**: 그래프가 실제로 어떻게 동작하는지 — State·Reducer 심화, 조건부 엣지, 병렬 실행, `Send`, `Command`

교재 노트북은 1주차와 같은 소스([Langgraph_Study](https://github.com/PassionChicken-Leesuin/Langgraph_Study), Teddy님 LangGraph 튜토리얼 기반)에서 가져왔습니다.

## 폴더 구성

```
2주차_Langgraph_GraphAPI/
├─ README.md          ← 지금 보고 있는 파일
├─ pyproject.toml     ← 의존성 목록 (1주차와 동일)
├─ uv.lock            ← 버전 고정
├─ .python-version    ← Python 버전 고정
├─ .env.example       ← API 키 템플릿
├─ notebooks/         ← 교재 원본 노트북 (직접 수정하지 마세요!)
│  ├─ 02-LangGraph-Messages.ipynb
│  └─ 02-QuickStart-LangGraph-Graph-API.ipynb
└─ submissions/       ← 각자 자기 이름 폴더 안의 '본인 노트북'으로 학습·제출
   └─ 본인이름/
      ├─ 본인이름_02-LangGraph-Messages.ipynb
      └─ 본인이름_02-QuickStart-LangGraph-Graph-API.ipynb
```

## 환경 설정

1주차에서 환경 구성을 마쳤다면 두 단계면 끝납니다. 주차 폴더마다 가상환경이 따로 만들어지기 때문에 `uv sync`는 다시 한 번 실행해야 합니다.

```bash
cd 2주차_Langgraph_GraphAPI
uv sync
```

`.env`는 1주차 것을 그대로 복사하면 됩니다:

```bash
# macOS / Linux
cp ../1주차_Langgraph기본/.env .env
```

```powershell
# Windows (PowerShell)
Copy-Item ..\1주차_Langgraph기본\.env .env
```

> 처음 오신 분은 [1주차 README](../1주차_Langgraph기본/README.md)의 '사전 준비'와 '환경 설정'을 먼저 따라해 주세요.

노트북을 열면 우측 상단 **Select Kernel**에서 **이 폴더(2주차)의 `.venv`** Python을 선택하세요.

## 학습 및 퀴즈 제출 방법

흐름은 1주차와 완전히 동일합니다. 브랜치 이름만 `week2`로 바뀝니다.

### 1. 최신 main 받아오고 내 브랜치 만들기

```bash
git switch main
git pull
git switch -c week2/홍길동
```

### 2. 학습 및 퀴즈 풀기

`submissions/본인이름/` 폴더의 본인 노트북 2개를 아래 순서로 학습하세요. (**원본 `notebooks/`는 절대 수정하지 않습니다.**)

1. `본인이름_02-LangGraph-Messages.ipynb` — 메시지 유형(System/Human/AI/Tool)과 도구 호출 대화 흐름
2. `본인이름_02-QuickStart-LangGraph-Graph-API.ipynb` — State·Reducer 심화, 조건부 엣지, Send, Command

각 노트북 끝의 🧩 퀴즈 빈칸(`________`)을 채우고, 셀을 실행해 통과를 확인하세요.

> 💡 퀴즈 ②(Graph API)는 API 키 없이 전부 풀 수 있습니다. 퀴즈 ①의 Q3만 OpenAI API 키가 필요해요.

### 3. 커밋 → push → Pull Request

```bash
git add 2주차_Langgraph_GraphAPI/submissions/홍길동/
git status          # 의도한 파일만 올라가는지 확인! (.env 같은 게 섞이면 안 됨)
git commit -m "2주차 퀴즈 제출 - 홍길동"
git push -u origin week2/홍길동
```

- PR 제목: `[2주차] 홍길동 퀴즈 제출`
- PR 본문: 어려웠던 점, 질문 등 자유롭게

리뷰·merge 흐름과 자주 묻는 질문은 [1주차 README](../1주차_Langgraph기본/README.md)를 참고하세요.
