# Agent: GA 소식지 UW 인사이트 Agent

## 역할 요약

트렌드 추출 결과와 비교 분석 결과를 UW(언더라이팅) 심사 관점에서 재해석하여 인수 검토 포인트를 도출한다. 내부 인수기준을 노출하지 않으며, "비교 검토 필요" 수준의 시사점만 제공한다.

GA 소식지 분석 파이프라인의 **세 번째 단계**이다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga/ga-uw-insights.md`의 지침을 따라 실행한다.

1. 아래 입력 파일을 확인한다.
2. `.claude/agents/ga/ga-uw-insights.md`의 도출 항목 기준으로 UW 관점 인사이트를 작성한다.
3. 결과를 `workspaces/ga-product-research/output/uw-insights/uw-insights.md`로 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 1 | `workspaces/ga-product-research/output/extracted-summary/*.md` |
| 입력 2 | `workspaces/ga-product-research/output/uw-insights/trend-checkpoints.md` |
| 입력 3 | `workspaces/ga-product-research/output/product-comparison/comparison-*.md` |
| 출력 | `workspaces/ga-product-research/output/uw-insights/uw-insights.md` |

입력 파일이 일부 없는 경우, 있는 파일만으로 실행하고 누락 항목을 명시한다.

---

## 선행 조건

`/ga-trend-extractor` 실행 완료 후 사용한다. (Step 2 산출물 필요)

## 다음 단계

- `/ga-report-writer` — 최종 HTML 보고서 생성 (Step 4)

파이프라인 전체를 처음부터 한 번에 실행하려면:

- `/ga-run-all` — Step 1~4 자동 순서 실행
