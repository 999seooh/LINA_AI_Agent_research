# Agent: 보험 약관 분석 Agent

## 역할 요약

보험사 공개 약관 PDF를 읽고 보장 범위·면책 조항·가입 자격·고지의무 관련 조항을 구조화한다. GA 소식지 분석 파이프라인과 독립적으로 실행되며, 약관 원문 기반의 정확한 조문 구조화가 목적이다. 법적 해석이나 판단은 하지 않는다.

---

## 실행 방법

이 Skill이 호출되면 `.claude/agents/ga-terms-analyzer.md`의 지침을 따라 실행한다.

1. `workspaces/ga-product-research/input/terms/` 하위 약관 PDF 파일을 확인한다.
2. 처리할 파일을 사용자에게 확인하거나, 명시된 경우 해당 파일만 처리한다.
3. `.claude/agents/ga-terms-analyzer.md`의 추출 항목 기준으로 조문을 구조화한다.
4. 결과를 `workspaces/ga-product-research/output/terms-analysis/`에 약관별 Markdown 파일로 저장한다.

---

## 입력 / 출력

| 구분 | 경로 |
|---|---|
| 입력 | `workspaces/ga-product-research/input/terms/*.pdf` |
| 출력 | `workspaces/ga-product-research/output/terms-analysis/{보험사명}_{상품명}_{기준년월}_terms.md` |

---

## 파이프라인 연계 (선택)

약관 분석 결과를 소식지 분석 파이프라인에 보조 입력으로 연계할 수 있다.

| 연계 가능 Agent | 연계 방식 |
|---|---|
| `/ga-comparison` | 소식지 비교표와 약관 기준 비교표를 병렬로 제공 |
| `/ga-uw-insights` | 면책·가입 자격 조항 기반 UW 체크포인트 보강 |
| `/ga-report-writer` | 약관 분석 요약을 보고서 별첨 섹션으로 추가 |

연계는 선택 사항이며, 독립 산출물로만 활용해도 무방하다.

---

## 주의사항

- 공개된 약관 PDF만 입력 대상이다. 사내 내부 기준문서·심사지침은 입력하지 않는다.
- 법적 해석, 소송 관련 의견은 제공하지 않는다.
- 산출물은 참고용 초안이며, 법적 해석의 근거 문서가 아님을 명시한다.
