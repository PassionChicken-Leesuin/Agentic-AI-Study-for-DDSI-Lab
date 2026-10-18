# 3주차 — Agent & Tool

1·2주차에는 `StateGraph`로 노드와 엣지를 **직접 조립**해서 에이전트를 만들었습니다. 3주차는 같은 에이전트를 LangChain의 **`create_agent` 한 줄**로 만들고, 미들웨어와 도구로 원하는 대로 바꿔보는 주입니다.

- **Agents**: `create_agent`로 에이전트 만들기 — 동적 모델 선택, 동적 시스템 프롬프트, 미들웨어(`wrap_model_call`, `dynamic_prompt`, `before_model`/`after_model`)
- **Tools**: 도구 제대로 만들기 — `@tool`, Pydantic 입력 스키마, `ToolRuntime`(state·context·store 접근), 도구에서 `Command`로 상태 업데이트

`create_agent`가 내부에서 만드는 그래프도 결국 1·2주차에 배운 State·노드·리듀서로 이루어져 있습니다. "직접 조립했던 것"과 "완성품"을 비교하며 보면 훨씬 잘 보입니다.

교재 노트북은 1·2주차와 같은 소스([Langgraph_Study](https://github.com/PassionChicken-Leesuin/Langgraph_Study), Teddy님 LangGraph 튜토리얼 기반)의 PART02에서 가져왔고, 헷갈리기 쉬운 부분에 **"\*참고하십셔!"** 설명 박스를 추가했습니다.

## 폴더 구성

```
3주차_Langgraph_Agent_Tool/
├─ README.md          ← 지금 보고 있는 파일
├─ pyproject.toml     ← 의존성 목록 (1·2주차와 동일)
├─ uv.lock            ← 버전 고정
├─ .python-version    ← Python 버전 고정
├─ .env.example       ← API 키 템플릿
├─ notebooks/         ← 교재 원본 노트북 (직접 수정하지 마세요!)
│  ├─ 03-LangGraph-Agents.ipynb
│  ├─ 03-LangGraph-Tools.ipynb
│  └─ assets/         ← 노트북 이미지
└─ submissions/       ← 각자 자기 이름 폴더 안의 '본인 노트북'으로 학습·제출
   └─ 본인이름/
      ├─ 본인이름_03-LangGraph-Agents.ipynb
      └─ 본인이름_03-LangGraph-Tools.ipynb
```

## 환경 설정

2주차와 똑같습니다. 주차 폴더마다 가상환경이 따로 만들어지기 때문에 `uv sync`는 다시 한 번 실행해야 합니다.

```bash
cd 3주차_Langgraph_Agent_Tool
uv sync
```

`.env`는 2주차 것을 그대로 복사하면 됩니다:

```bash
# macOS / Linux
cp ../2주차_Langgraph_GraphAPI/.env .env
```

```powershell
# Windows (PowerShell)
Copy-Item ..\2주차_Langgraph_GraphAPI\.env .env
```

> 처음 오신 분은 [1주차 README](../1주차_Langgraph기본/README.md)의 '사전 준비'와 '환경 설정'을 먼저 따라해 주세요.

노트북을 열면 우측 상단 **Select Kernel**에서 **이 폴더(3주차)의 `.venv`** Python을 선택하세요.

## 학습 및 퀴즈 제출 방법

흐름은 1·2주차와 완전히 동일합니다. 브랜치 이름만 `week3`로 바뀝니다.

### 1. 최신 main 받아오고 내 브랜치 만들기

```bash
git switch main
git pull
git switch -c week3/홍길동
```

### 2. 학습 및 퀴즈 풀기

`submissions/본인이름/` 폴더의 본인 노트북 2개를 아래 순서로 학습하세요. (**원본 `notebooks/`는 절대 수정하지 않습니다.**)

1. `본인이름_03-LangGraph-Agents.ipynb` — `create_agent`, 동적 모델 선택, 동적 시스템 프롬프트, 미들웨어
2. `본인이름_03-LangGraph-Tools.ipynb` — `@tool`, Pydantic 입력 스키마, `ToolRuntime`, `Command`, Store

각 노트북 끝의 🧩 퀴즈 빈칸(`________`)을 채우고, 셀을 실행해 통과를 확인하세요. 마지막 주관식 문항은 셀을 더블클릭해서 답을 적으면 됩니다.

> 💡 이번 주 퀴즈는 **API 키 없이 전부** 풀 수 있습니다. 채점을 위해 실제 LLM 대신 **가짜 모델**(`EchoModel`, `ScriptedToolModel`)을 씁니다. 퀴즈 맨 앞의 준비 셀은 **수정하지 말고 실행만** 하세요. 이 코드는 배운 내용이 아니라서 이해하지 않아도 괜찮습니다.

### 3. 커밋 → push → Pull Request

```bash
git add 3주차_Langgraph_Agent_Tool/submissions/홍길동/
git status          # 의도한 파일만 올라가는지 확인! (.env 같은 게 섞이면 안 됨)
git commit -m "3주차 퀴즈 제출 - 홍길동"
git push -u origin week3/홍길동
```

push만 하면 PR이 자동으로 생기지 않습니다. GitHub 레포 페이지에 뜨는 **"Compare & pull request"** 버튼을 눌러 PR을 꼭 열어주세요.

- PR 제목: `[3주차] 홍길동 퀴즈 제출`
- PR 본문: 어려웠던 점, 질문 등 자유롭게

리뷰·merge 흐름과 자주 묻는 질문은 [1주차 README](../1주차_Langgraph기본/README.md)를 참고하세요.
