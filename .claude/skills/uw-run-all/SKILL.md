# Skill: UW 리포트 자동화 파이프라인 전체 실행

## 역할 요약

UW 리포트 자동화 파이프라인 3단계를 순서대로 자동 실행한다.
(데이터 처리가 필요한 경우 Step 0으로 먼저 실행한다.)
각 단계의 산출물이 정상 생성된 것을 확인한 뒤 다음 단계로 진행한다.

---

## 실행 전 판단

파이프라인 시작 전 다음을 확인한다:

1. 사용자가 실데이터 또는 더미데이터 생성을 요청한 경우 → **Step 0** 먼저 실행
2. `workspaces/uw-report-automation/input/requirements.md`가 이미 있는 경우 → **Step 1** 생략 가능 (사용자 확인 후 결정)
3. 요구사항 정의서가 없는 경우 → **Step 1**부터 시작

---

## 실행 순서

```
[Step 0 - 선택] uw-data-processor  ← 실데이터 마스킹 또는 더미데이터 생성이 필요한 경우만
  입력: 사용자 제공 컬럼 정의 또는 실데이터
  출력:
    - 마스킹 시: workspaces/uw-report-automation/input/masked-data/
    - 더미 생성 시: workspaces/uw-report-automation/input/dummy-data/
  지침: .claude/agents/uw-report/uw-data-processor.md

[Step 1] uw-req-analyst
  입력: 사용자 자연어 요청 (+ Step 0 산출물이 있으면 함께 참조)
  출력: workspaces/uw-report-automation/input/requirements.md
  지침: .claude/agents/uw-report/uw-req-analyst.md

[Step 2] uw-model-builder
  입력: workspaces/uw-report-automation/input/requirements.md
  출력: workspaces/uw-report-automation/output/model-design.md
  지침: .claude/agents/uw-report/uw-model-builder.md

[Step 3] uw-dashboard-writer
  입력:
    - workspaces/uw-report-automation/input/requirements.md
    - workspaces/uw-report-automation/output/model-design.md
  출력:
    - workspaces/uw-report-automation/output/dashboard-design.md
    - workspaces/uw-report-automation/output/report-draft.md
  지침: .claude/agents/uw-report/uw-dashboard-writer.md
```

---

## 단계별 완료 기준

| 단계 | 완료 기준 |
|---|---|
| Step 0 (선택) | `masked-data/` 또는 `dummy-data/` 에 처리 완료 파일 생성 |
| Step 1 | `input/requirements.md` 생성 완료 (분석목적·데이터구조·산출물요건 포함) |
| Step 2 | `output/model-design.md` 생성 완료 (목적→현행→변경→테스트기준→기대효과) |
| Step 3 | `output/dashboard-design.md` + `output/report-draft.md` 생성 완료 |

각 단계 완료 후 아래 형태로 진행 상황을 보고한다:

```
[Step N 완료] → Step N+1 시작
```

---

## 고도화 모드 (기존 산출물 있는 경우)

`output/model-design.md`가 이미 존재하는 경우:
- Step 1: 고도화 요구사항을 기존 정의서에 추가하여 업데이트
- Step 2: 기존 모델 설계안의 변경 이력 섹션에 변경 사항 누적 기록
- Step 3: 기존 대시보드 설계안과 리포트 초안을 갱신

---

## 완료 후 안내

파이프라인 완료 시 다음 정보를 사용자에게 안내한다:

```
[UW 리포트 자동화 파이프라인 완료]

생성된 산출물:
- 요구사항 정의서: workspaces/uw-report-automation/input/requirements.md
- 모델 설계안:    workspaces/uw-report-automation/output/model-design.md
- 대시보드 설계:  workspaces/uw-report-automation/output/dashboard-design.md
- 리포트 초안:    workspaces/uw-report-automation/output/report-draft.md

다음 단계 옵션:
1. 모델 고도화 → uw-model-builder 단독 실행
2. 대시보드 수정 → uw-dashboard-writer 단독 실행
3. 데이터 추가 처리 → uw-data-processor 단독 실행
4. 전체 재실행 → /uw-run-all 재호출
```

---

## 보안 규칙

파이프라인 전 단계에 걸쳐 다음 정보는 처리하거나 출력에 포함하지 않는다:
- 고객명, 주민등록번호, 증권번호·청약번호 원문
- 연락처, 주소, 계약자/피보험자 식별 가능 정보
- 내부 DB 접속 정보, 사내 계정/비밀번호/서버 주소
