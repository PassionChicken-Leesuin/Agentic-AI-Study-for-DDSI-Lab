# Agentic AI Study for DDSI Lab

본 레포지토리는 **서울대학교 Data Driven Service Innovation Lab(DDSI Lab)** 에서 진행하는 Agentic AI Study 중 **코딩 학습**을 위한 저장소입니다.

석사과정 **이수인**이 주도하며, 주 참여원으로는 **우명균, 이진수, 최우진**이 있습니다.

## 스터디 소개

Agentic AI 스터디는 크게 두 축으로 진행됩니다.

### 1️⃣ Agentic AI 구축에 필요한 필수 코딩 학습 — 이 레포지토리

- **목표**: 실제 Agentic AI 시스템을 구축하는 데 필요한 코딩 지식을 학습합니다. 단순히 코드를 따라 치는 수준을 넘어, "Agentic AI 시스템을 개발·연구해봤다"고 말할 수 있을 만큼 **연구 단계의 시스템 구현 코드를 이해하고 직접 다루는 것**을 목표로 합니다. Production 수준의 서비스 개발보다는 **연구 및 프로토타이핑 수준**의 시스템 구축에 초점을 둡니다.
- **소스**: [Braincrew Lab의 LangGraph 강의 코드](https://github.com/braincrew-lab/langgraph-v1-tutorial)를 기반으로, 학습에 적합한 내용을 스터디장이 선별·수정하여 주차별 폴더로 제공합니다.

### 2️⃣ 『AI Agents in Depth』 교재 학습 — 대면 세미나

- **목표**: Agentic AI 시스템을 설계·구축할 때 고려해야 하는 핵심 개념과 전반적인 흐름을 학습합니다.
- **소스**: [AI Agents in Depth (교재 GitHub)](https://github.com/bojieli/ai-agent-book) — 매주 스터디장이 핵심 내용을 정리해 공유하므로, 교재를 미리 다 읽어올 필요는 없습니다.

## 운영 방식 (코딩 학습)

매주 아래 사이클로 진행됩니다:

> **간단한 설명 (대면, 10~20분) → 일주일 간 자기주도 학습 → GitHub 제출 (Submission 폴더에 커밋·푸시) → 리뷰 (다음 모임 첫 10분)**

매주 월요일 모임에서 다음 주까지 학습할 코드가 Agentic AI 시스템에서 **왜 필요한지, 어떤 맥락에서 쓰이는지**를 먼저 설명한 뒤, 각자 일주일간 학습하고 퀴즈 풀이를 제출합니다.

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

[1주차 README](./1주차_Langgraph기본/README.md)의 환경 설정부터 시작하세요.
