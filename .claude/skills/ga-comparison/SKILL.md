# Agent: GA 소식지 보험사 간 비교 분석 Agent

## 역할 요약

파서 Agent의 구조화된 출력을 입력받아 보험사 간 상품·담보·인수조건을 비교하는 표를 생성한다. 보험사를 가로축, 비교 항목을 세로축으로 배치한 비교표를 작성하며, 우열 판단이나 평가는 하지 않는다.

GA 소식지 분석 파이프라인의 **두 번째 단계**이며, 트렌드 추출 Agent와 병렬로 실행 가능하다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga-comparison.md`의 지침을 따라 실행한다.

1. `workspaces/ga-product-research/output/extracted-summary/` 하위 파일 전체를 입력으로 사용한다.
2. `.claude/agents/ga-comparison.md`의 비교표 유형별 기준으로 비교표를 작성한다.
3. 결과를 `workspaces/ga-product-research/output/product-comparison/`에 비교 기준별로 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 | `workspaces/ga-product-research/output/extracted-summary/*.md` |
| 출력 | `workspaces/ga-product-research/output/product-comparison/comparison-*.md` |

출력 파일 목록 (소식지에 정보가 있는 경우에 한해 생성):

| 파일명 | 내용 |
|---|---|
| `comparison-coverage.md` | 담보별 보장금액 비교 |
| `comparison-uw-criteria.md` | 고지 유형·인수조건 비교 |
| `comparison-plan.md` | 플랜 구성 비교 |
| `comparison-premium.md` | 보험료 비교 |

---

## 선행 조건

`/ga-parser` 실행 완료 후 사용한다.

## 다음 단계

- `/ga-uw-insights` — UW 관점 인사이트 도출 (트렌드 추출 완료 후 함께 입력)
