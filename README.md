# Agentic AI Study for DDSI Lab

DDSI Lab의 Agentic AI 스터디 저장소입니다. 매주 새로운 주차 폴더가 추가되며, 각 주차 폴더의 README를 따라 학습하고 퀴즈를 제출합니다.

## 주차별 자료

| 주차 | 주제 |
|---|---|
| [0주차](./0주차_Github%20협업/) | GitHub 협업으로 Contributor 되어보기 (사전 준비) |
| [1주차](./1주차_Langgraph기본/) | LangGraph 기본 — State, 모델, QuickStart |

## 매주 루틴

새 주차가 올라오면 아래 세 줄로 시작하세요:

```bash
git switch main
git pull                  # 새 주차 폴더 받아오기
git switch -c week2/홍길동  # 그 주차용 내 브랜치 만들기 (주차 번호와 본인 이름으로)
```

이후 흐름은 매주 동일합니다: **해당 주차 폴더의 README 따라 학습 → `submissions/본인이름/`의 본인 노트북에서 퀴즈 풀기 → 커밋 → 푸시 → Pull Request → 리뷰 후 merge**

> 💡 브랜치를 옮기기 전에 커밋 안 한 작업이 있다면 먼저 커밋하거나 `git stash -u`로 보관해두세요.

[1주차 README](./1주차_Langgraph기본/README.md)의 환경 설정부터 시작하세요.
