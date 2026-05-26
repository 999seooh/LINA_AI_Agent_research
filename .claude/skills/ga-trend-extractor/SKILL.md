# Agent: GA 소식지 트렌드 추출 Agent

## 역할 요약

파서 Agent의 구조화된 출력을 입력받아 업계 공통 트렌드와 주요 체크포인트를 추출한다. 개별 보험사 내용을 재서술하지 않으며, 2개 이상 보험사에서 공통으로 나타나는 흐름만 트렌드로 분류한다.

GA 소식지 분석 파이프라인의 **두 번째 단계**이며, 비교 분석 Agent와 병렬로 실행 가능하다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga-trend-extractor.md`의 지침을 따라 실행한다.

1. `workspaces/ga-product-research/output/extracted-summary/` 하위 파일 전체를 입력으로 사용한다.
2. `.claude/agents/ga-trend-extractor.md`의 추출 항목 기준으로 트렌드를 도출한다.
3. 결과를 `workspaces/ga-product-research/output/uw-insights/trend-checkpoints.md`로 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 | `workspaces/ga-product-research/output/extracted-summary/*.md` |
| 출력 | `workspaces/ga-product-research/output/uw-insights/trend-checkpoints.md` |

---

## 선행 조건

`/ga-parser` 실행 완료 후 사용한다.

## 다음 단계

- `/ga-uw-insights` — UW 관점 인사이트 도출 (비교 분석 완료 후)
