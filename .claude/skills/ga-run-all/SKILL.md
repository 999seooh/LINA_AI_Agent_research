# Skill: GA 소식지 분석 파이프라인 전체 실행

## 역할 요약

GA 소식지 분석 파이프라인 4단계를 순서대로 자동 실행한다.
각 단계의 산출물이 정상 생성된 것을 확인한 뒤 다음 단계로 진행한다.

---

## 실행 순서

이 Skill이 호출되면 아래 4단계를 순서대로 실행한다.
단계 사이에 사용자 개입 없이 자동으로 이어서 실행한다.

```
[Step 1] ga-parser
  입력: workspaces/ga-product-research/input/ga-newsletters/*.pdf
  출력: workspaces/ga-product-research/output/extracted-summary/{보험사명}_{기준월}.md
  지침: .claude/agents/ga/ga-parser.md

[Step 2] ga-trend-extractor
  입력: output/extracted-summary/*.md (Step 1 산출물 전체)
  출력: output/uw-insights/trend-checkpoints.md
  지침: .claude/agents/ga/ga-trend-extractor.md

[Step 3] ga-uw-insights
  입력: output/uw-insights/trend-checkpoints.md + output/extracted-summary/*.md
  출력: output/uw-insights/uw-insights.md
  지침: .claude/agents/ga/ga-uw-insights.md

[Step 4] ga-report-writer
  입력: output/extracted-summary/*.md + output/uw-insights/*.md
  출력: output/final-report/report.html + output/final-report/style.css
  지침: .claude/agents/ga/ga-report-writer.md
```

---

## 실행 전 확인 사항

1. `workspaces/ga-product-research/input/ga-newsletters/` 에 PDF 파일이 있는지 확인한다.
2. 파일이 없으면 실행을 중단하고 사용자에게 안내한다.
3. 기존 output 파일이 있으면 덮어쓴다 (단, 덮어쓰기 전 기존 파일을 Read로 확인한다).

---

## 단계별 완료 기준

| 단계 | 완료 기준 |
|---|---|
| Step 1 | `extracted-summary/` 에 보험사별 .md 파일 생성 완료 |
| Step 2 | `uw-insights/trend-checkpoints.md` 생성 완료 |
| Step 3 | `uw-insights/uw-insights.md` 생성 완료 |
| Step 4 | `final-report/report.html` 및 `final-report/style.css` 생성 완료 |

각 단계 완료 후 "[Step N 완료] → Step N+1 시작" 형태로 진행 상황을 보고한다.

---

## 완료 후 안내

모든 단계 완료 후 다음을 안내한다.

- 최종 보고서 경로: `workspaces/ga-product-research/output/final-report/report.html`
- PDF 저장 방법: 브라우저에서 파일을 열고 `Cmd+P` → PDF로 저장
- 각 단계 산출물 위치 목록

---

## 독립 실행 Skill (이 파이프라인과 별도)

| Skill | 용도 |
|---|---|
| `/ga-terms-analyzer` | 약관 PDF 분석 — 파이프라인과 무관하게 단독 실행 |
| `/insurance-law-ref` | 법령 조문 질의응답 — 대화형, 순서 없음 |
