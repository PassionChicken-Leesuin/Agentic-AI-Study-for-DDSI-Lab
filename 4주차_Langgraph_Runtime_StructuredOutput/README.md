# 4주차 — Runtime & Structured Output

3주차에서 `create_agent`로 에이전트를 만들고 도구·미들웨어를 붙였습니다. 그때 `runtime.context`, `runtime.store`, `request.runtime` 같은 게 조금씩 나왔죠. 4주차는 그 **Runtime을 한 번에 정리**하고, 에이전트의 답을 문자열 대신 **정해진 형식(Pydantic 객체 등)으로 받는 법**을 배우는 주입니다.

- **Runtime**: 도구·미들웨어가 쓸 수 있는 "바깥 정보" 세 가지 — `context`(호출자가 넘기는 읽기 전용 정보), `store`(호출을 넘어 남는 장기 메모리), `stream_writer`(진행률 같은 커스텀 스트리밍). 그리고 처음 나오는 `@before_agent`와 `jump_to`
- **Structured Output**: `response_format`으로 결과를 `structured_response` 키에 받기 — `ToolStrategy`/`ProviderStrategy`, Pydantic·dataclass·TypedDict 스키마, `Union`, `handle_errors` 재시도

두 노트북 모두 **3주차 Tools 노트북과 바로 이어집니다.** Runtime은 3주차 "컨텍스트 접근"·"Store"의 확장판이고, Structured Output의 `ToolStrategy`는 결국 3주차에 배운 **도구 호출**로 구현되어 있습니다. 이번 주도 "3주차에서 본 것"과 비교하며 보면 훨씬 잘 보입니다.

교재 노트북은 지금까지와 같은 소스([Langgraph_Study](https://github.com/PassionChicken-Leesuin/Langgraph_Study), Teddy님 LangGraph 튜토리얼 기반)의 PART02 Ch03·Ch04에서 가져왔고, 헷갈리기 쉬운 부분에 **"\*참고하십셔!"** 설명 박스를 추가했습니다.

## 폴더 구성

```
4주차_Langgraph_Runtime_StructuredOutput/
├─ README.md          ← 지금 보고 있는 파일
├─ pyproject.toml     ← 의존성 목록 (1·2·3주차와 동일)
├─ uv.lock            ← 버전 고정
├─ .python-version    ← Python 버전 고정
├─ .env.example       ← API 키 템플릿
├─ notebooks/         ← 교재 원본 노트북 (직접 수정하지 마세요!)
│  ├─ 04-LangGraph-Runtime.ipynb
│  └─ 05-LangGraph-Structured-Output.ipynb
└─ submissions/       ← 각자 자기 이름 폴더 안의 '본인 노트북'으로 학습·제출
   └─ 본인이름/
      ├─ 본인이름_04-LangGraph-Runtime.ipynb
      └─ 본인이름_05-LangGraph-Structured-Output.ipynb
```

## 환경 설정

3주차와 똑같습니다. 주차 폴더마다 가상환경이 따로 만들어지기 때문에 `uv sync`는 다시 한 번 실행해야 합니다.

```bash
cd 4주차_Langgraph_Runtime_StructuredOutput
uv sync
```

`.env`는 3주차 것을 그대로 복사하면 됩니다:

```bash
# macOS / Linux
cp ../3주차_Langgraph_Agent_Tool/.env .env
```

```powershell
# Windows (PowerShell)
Copy-Item ..\3주차_Langgraph_Agent_Tool\.env .env
```

> 처음 오신 분은 [1주차 README](../1주차_Langgraph기본/README.md)의 '사전 준비'와 '환경 설정'을 먼저 따라해 주세요.

노트북을 열면 우측 상단 **Select Kernel**에서 **이 폴더(4주차)의 `.venv`** Python을 선택하세요.

## 학습 및 퀴즈 제출 방법

흐름은 지금까지와 완전히 동일합니다. 브랜치 이름만 `week4`로 바뀝니다.

### 1. 최신 main 받아오고 내 브랜치 만들기

```bash
git switch main
git pull
git switch -c week4/홍길동
```

### 2. 학습 및 퀴즈 풀기

`submissions/본인이름/` 폴더의 본인 노트북 2개를 아래 순서로 학습하세요. (**원본 `notebooks/`는 절대 수정하지 않습니다.**)

1. `본인이름_04-LangGraph-Runtime.ipynb` — `context`·`store`·`stream_writer`, 미들웨어에서 Runtime 쓰기, `@before_agent` + `jump_to`
2. `본인이름_05-LangGraph-Structured-Output.ipynb` — `response_format`, `ToolStrategy`/`ProviderStrategy`, 스키마 3종, `Union`, `handle_errors`

각 노트북 끝의 🧩 퀴즈 빈칸(`________`)을 채우고, 셀을 실행해 통과를 확인하세요. 마지막 주관식 문항은 셀을 더블클릭해서 답을 적으면 됩니다.

> 💡 이번 주 퀴즈도 **API 키 없이 전부** 풀 수 있습니다. 3주차에서 쓴 **가짜 모델**(`EchoModel`, `ScriptedToolModel`)을 다시 씁니다. 퀴즈 맨 앞의 준비 셀은 **수정하지 말고 실행만** 하세요.
>
> 본문 예제 셀들은 실제 LLM을 부르므로 API 키가 필요합니다. Structured Output 노트북의 `ProviderStrategy` 예제(스키마를 `response_format`에 바로 넘기는 것)는 **OpenAI·Anthropic 등 네이티브 지원 모델에서만** 동작하니, 키가 없다면 읽고 넘어가도 괜찮습니다.

### 3. 커밋 → push → Pull Request

```bash
git add 4주차_Langgraph_Runtime_StructuredOutput/submissions/홍길동/
git status          # 의도한 파일만 올라가는지 확인! (.env 같은 게 섞이면 안 됨)
git commit -m "4주차 퀴즈 제출 - 홍길동"
git push -u origin week4/홍길동
```

push만 하면 PR이 자동으로 생기지 않습니다. GitHub 레포 페이지에 뜨는 **"Compare & pull request"** 버튼을 눌러 PR을 꼭 열어주세요.

- PR 제목: `[4주차] 홍길동 퀴즈 제출`
- PR 본문: 어려웠던 점, 질문 등 자유롭게

리뷰·merge 흐름과 자주 묻는 질문은 [1주차 README](../1주차_Langgraph기본/README.md)를 참고하세요.
