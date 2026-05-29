# Agent: GA 소식지 보고서 작성 Agent

## 역할 요약

앞선 모든 Agent의 산출물을 받아 업무 보고용 HTML 보고서를 작성한다. 새로운 분석을 추가하지 않으며, 입력받은 결과를 가독성 높은 보고서 형식으로 가공하는 역할만 수행한다.

GA 소식지 분석 파이프라인의 **마지막 단계**이다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga-report-writer.md`의 지침을 따라 실행한다.

1. 아래 입력 파일을 확인한다.
2. `.claude/agents/ga-report-writer.md`의 보고서 구성 기준으로 HTML 보고서를 작성한다.
3. 결과를 `workspaces/ga-product-research/output/final-report/`에 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 1 | `workspaces/ga-product-research/output/extracted-summary/*.md` |
| 입력 2 | `workspaces/ga-product-research/output/uw-insights/trend-checkpoints.md` |
| 입력 3 | `workspaces/ga-product-research/output/product-comparison/comparison-*.md` |
| 입력 4 | `workspaces/ga-product-research/output/uw-insights/uw-insights.md` |
| 출력 1 | `workspaces/ga-product-research/output/final-report/report.html` |
| 출력 2 | `workspaces/ga-product-research/output/final-report/style.css` |

입력 파일이 일부 없는 경우 있는 파일만으로 보고서를 작성하고 누락 항목은 "(미입력)"으로 공란 처리한다.

---

## 선행 조건

`/ga-uw-insights` 실행 완료 후 사용한다. (Step 3 산출물 필요, 또는 available한 입력 파일로 부분 생성 가능)

파이프라인 전체를 처음부터 한 번에 실행하려면:

- `/ga-run-all` — Step 1~4 자동 순서 실행

## PDF 저장

Agent는 직접 PDF 변환을 수행하지 않는다. PDF 저장은 사용자가 브라우저에서 `report.html`을 열고 인쇄 기능으로 직접 수행한다.
