# 0주차 — GitHub 협업 규칙

이 스터디의 모든 제출은 GitHub의 **브랜치 → Pull Request → 리뷰 → merge** 흐름으로 이루어집니다.
0주차의 목표는 이 흐름에 익숙해지는 것입니다.

## 핵심 개념 3줄 요약

- **main 브랜치**: 교재(원본 노트북)가 있는 곳. 직접 push 금지 — 보호 설정되어 있어 어차피 안 됩니다.
- **내 브랜치**: main에서 갈라져 나온 나만의 작업 공간. 여기서 뭘 해도 main은 안 바뀝니다.
- **Pull Request (PR)**: "내 브랜치의 변경사항을 main에 합쳐주세요"라는 요청. 스터디장이 리뷰(approve)하면 merge되어 main에 반영됩니다.

## 사전 준비 (최초 1회)

1. GitHub 계정 생성 후 스터디장에게 계정명 알려주기 → collaborator로 초대받기 (이메일 초대 수락 필수)
2. [Git 설치](https://git-scm.com/downloads)
3. 본인 정보 등록:

```bash
git config --global user.name "본인이름"
git config --global user.email "GitHub가입이메일"
```

4. repo clone:

```bash
git clone https://github.com/PassionChicken-Leesuin/Agentic-AI-Study-for-DDSI-Lab.git
cd Agentic-AI-Study-for-DDSI-Lab
```

## 매주 제출 흐름

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

### 3. 작업하기

해당 주차 폴더의 `submissions/본인이름/` 안에서만 작업합니다.
**원본 교재 파일(`notebooks/` 등)은 절대 수정하지 않습니다.**

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

**Q. 내 브랜치에서 실수하면 main도 망가지나요?**
A. 아니요. 브랜치는 완전히 독립된 작업 공간이고, main은 merge 전까지 절대 안 바뀝니다. 게다가 main은 보호되어 있어서 리뷰 없이는 merge 자체가 불가능합니다. 마음껏 실험하세요.

**Q. 다른 사람 제출물과 충돌(conflict)나지 않나요?**
A. 각자 `submissions/본인이름/` 폴더만 건드리므로 충돌이 생길 수 없습니다. 충돌이 났다면 자기 폴더 밖의 파일을 수정한 것이니 스터디장에게 문의하세요.

**Q. 브랜치를 잘못 만들었어요.**
A. 새로 만들면 됩니다. `git switch main` → `git switch -c week1/홍길동` 부터 다시.

**Q. push할 때 권한 오류가 나요.**
A. collaborator 초대를 수락했는지 확인하세요 (GitHub 가입 이메일로 초대장이 갑니다).
