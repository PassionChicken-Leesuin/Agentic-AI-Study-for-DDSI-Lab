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

## 여러 컴퓨터에서 작업하기 (노트북 ↔ 연구실 PC)

브랜치를 push해두면 원격(GitHub)에 올라가 있어서, 어느 컴퓨터에서든 이어받을 수 있습니다.

**다른 PC에서 처음 이어받을 때:**

```bash
git clone https://github.com/PassionChicken-Leesuin/Agentic-AI-Study-for-DDSI-Lab.git   # 그 PC에 처음이면
cd Agentic-AI-Study-for-DDSI-Lab
git switch week1/홍길동    # 원격의 자기 브랜치로 전환 (자동으로 받아와짐)
```

**두 PC 모두 클론된 뒤로는, 이어서 작업할 때마다:**

```bash
git switch week1/홍길동
git pull                  # 다른 PC에서 푸시해둔 내용 받아오기
```

> 🚨 **철칙: 자리를 뜨기 전엔 push, 자리에 앉으면 pull.**
> 한쪽에서 push를 안 한 채 다른 PC에서 작업을 시작하면 같은 브랜치가 두 갈래로 갈라져 충돌이 납니다. 이 습관만 지키면 몇 대에서 작업하든 문제없어요.

---

처음이라면 [1주차 README](./1주차_Langgraph기본/README.md)의 환경 설정부터 시작하세요.
