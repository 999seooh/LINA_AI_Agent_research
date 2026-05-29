# Agent: GA 보험 자료 parser Agent

## 역할 요약

GA 보험 관련 자료 PDF를 읽고 보험사별로 정형화된 구조로 추출한다. 분석·해석·트렌드 도출은 하지 않으며, 원문에 있는 내용을 정확하게 구조화하는 것만 수행한다.

GA 보험 관련 자료 분석 파이프라인의 **첫 번째 단계**이다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga-parser.md`의 지침을 따라 실행한다.

1. `workspaces/ga-product-research/input/ga-newsletters/` 하위 PDF 파일을 확인한다.
2. 처리할 파일을 사용자에게 확인하거나, 명시된 경우 해당 파일만 처리한다.
3. 각 PDF에 대해 `.claude/agents/ga-parser.md`의 추출 항목 기준으로 파싱을 수행한다.
4. 결과를 `workspaces/ga-product-research/output/extracted-summary/`에 보험사별 Markdown 파일로 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 | `workspaces/ga-product-research/input/ga-newsletters/*.pdf` |
| 출력 | `workspaces/ga-product-research/output/extracted-summary/{보험사명}_{기준월}.md` |

---

## 다음 단계

파싱 완료 후 다음 Agent를 실행할 수 있다.

- `/ga-trend-extractor` — 트렌드 및 체크포인트 추출 (Step 2)

파이프라인 전체를 한 번에 실행하려면:

- `/ga-run-all` — Step 1~4 자동 순서 실행
