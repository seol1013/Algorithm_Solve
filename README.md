# 알고리즘 스터디 — Main README

> 이 저장소는 코딩테스트 학습과 스터디 운영을 위해 설계되었습니다.
> 초보부터 중급 개발자까지 함께 문제를 풀고 코드 리뷰, 자동 검증을 통해 역량을 향상시키는 것을 목표로 합니다.

---

## 📌 목적

* 문제(Problem)와 풀이(Solution)를 명확히 분리하여 체계적으로 관리
* PR 기반 코드 리뷰와 GitHub Actions를 통한 자동 실행으로 품질 보증
* 초보자가 따라오기 쉬운 규칙과 체크리스트 제공

---

## 📁 저장소 구조 (권장)

```
algorithm-study/
├─ README.md                 # 이 파일
├─ problems/                 # 문제 모음 (설명, 링크, 조건 등)
│  ├─ week01/
│  │  └─ problem_1234.md
│  └─ week02/
├─ solutions/                # 풀이 코드
│  ├─ week01/
│  │  ├─ jay/
│  │  │  └─ boj_1234.py
│  │  └─ member2/
│  └─ week02/
├─ tests/                    # 자동 테스트용 input/output (옵션)
│  └─ week01/
│     ├─ 1234_input.txt
│     └─ 1234_output.txt
└─ .github/
   └─ workflows/             # GitHub Actions 워크플로우
      └─ run-tests.yml
```

---

## 🧭 브랜치 정책 (간단)

* `main` : 최종 통합본 (직접 푸시 금지 — PR로만 병합)
* `problems/weekXX` : 문제 등록 전용 브랜치 (문제 담당자 사용)
* `solutions/<name>` : 개인 풀이 브랜치 (예: `solutions/jay`)

**Merge 순서 권장**: `problems/weekXX` → 먼저 `main`에 Merge → `solutions/*` Merge

---

## ✅ 파일/폴더 규칙

* 문제 파일: `problems/weekXX/problem_문제번호.md`

  * 제목, 출처(예: BOJ 링크), 문제 설명, 제약조건, 예제 입력/출력 포함
* 풀이 파일: `solutions/weekXX/<이름>/` 아래에 저장

  * 파일명 예시: `boj_1234_이름.py` 또는 `boj_1234.cpp`
* 테스트 파일: `tests/weekXX/문제번호_input.txt`, `..._output.txt`

---

## PR 규칙 (Pull Request)

1. PR 제목: `weekXX: [문제번호] 간단설명 - 이름` (예: `week01: 1234 - 두 수 더하기 - jay`)
2. PR 본문 템플릿:

   * 문제 링크:
   * 풀이 요약(아이디어):
   * 시간/공간 복잡도:
   * 테스트 케이스(특이점):
3. 최소 1명 이상 리뷰 후 Merge
4. `main`에 Merge하기 전에 GitHub Action 통과 필수

---

## 코드 스타일 & 제출 규칙

* 언어별 기본 규칙 따르기 (Python: PEP8 권장 / C++: 표준 헤더 및 네임스페이스 명확화)
* 입력은 온라인 저지 형식 그대로 처리
* 불필요한 디버그 출력 제거
* 주석은 핵심 알고리즘 설명 중심으로

---

## 자동 검증 (GitHub Actions) — 권장 예시

* 목적: PR 시 코드가 정상 실행되는지 확인
* 간단 워크플로우 예시 파일: `.github/workflows/run-tests.yml`

  * 이벤트: `push`, `pull_request`
  * 동작: 저장소 체크아웃 → 필요한 런타임 세팅 → 각 `solutions/*`에 대해 `python file < tests/..._input.txt` 실행

(실제 워크플로우는 언어/테스트 방식에 따라 맞춤 설정 필요)

---

## 운영 프로세스 (주간 루틴 예시)

1. 스터디장 또는 문제 담당자가 `problems/weekXX` 브랜치로 문제 업로드
2. 모든 팀원이 `main`을 pull하여 최신 문제를 가져감
3. 각자 `solutions/<name>` 브랜치에서 풀이 작성
4. `solutions/<name>` → `main` 으로 PR 생성 (문제는 이미 main에 존재해야 함)
5. 자동 테스트 통과 및 리뷰 후 Merge
6. Merge 후 모든 팀원이 `git pull origin main`으로 최신화

---

## 자주 사용하는 Git 명령어 (초보용 치트시트)

```bash
# 저장소 복사
git clone <repo-url>

# 브랜치 생성(처음)
git checkout -b solutions/jay

# 변경사항 확인
git status

# 스테이징 & 커밋
git add .
git commit -m "week01: 1234 풀이 추가 - jay"

# 원격에 푸시
git push origin solutions/jay

# main 최신화
git checkout main
git pull origin main

# 내 브랜치에 main 합치기
git checkout solutions/jay
git merge main

# 로컬 브랜치 삭제(병합 후)
git branch -d solutions/jay
```

---

## 리뷰 체크리스트 (리뷰어가 확인할 항목)

* [ ] 문제 조건을 정확히 이해했는가
* [ ] 예제 케이스를 통과하는가
* [ ] 시간/공간 복잡도가 적절한가
* [ ] 코드가 간결하고 가독성이 좋은가
* [ ] 경계값(엣지 케이스)에 대한 처리 여부

---

## 이슈 템플릿 (간단)

* 제목: `weekXX - 문제번호 - 이슈 요약`
* 본문:

  * 재현 방법:
  * 기대 동작:
  * 실제 동작:
  * 관련 파일/라인:

---

## 권장 추가 기능 (옵션)

* `CODE_OF_CONDUCT.md`, `CONTRIBUTING.md` 작성
* 언어별 `template` 폴더(예: `templates/python_main.py`) 추가
* GitHub Pages로 문제집(문제 md) 정적 사이트 배포
* 문제 태그(그리디/그래프/DP 등) 메타데이터 추가

---

## 마무리 멘트

이 README는 스터디 운영 기준의 **기본 템플릿**입니다. 팀 특성(난이도, 인원, 리뷰 방식 등)에 맞춰 `README.md`와 `CONTRIBUTING.md`를 수정해 주세요.

필요하면 PR 템플릿, Issue 템플릿, GitHub Actions 예시 파일까지 **구체적으로 생성해 줄게요.** 원하면 어떤 언어를 우선적으로 자동 검증할지 알려줘!
