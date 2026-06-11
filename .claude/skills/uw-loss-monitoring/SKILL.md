# Skill: UW 손해율 모니터링

## 역할 요약

담보별 손해율 트렌드 진단(모듈 A)과 이상치 탐지(모듈 B)를 실행한다.
모듈은 독립적으로 호출하거나 함께 실행할 수 있다.

---

## 실행 전 판단

호출 시 다음을 확인한다:

1. 분석 대상 모듈 확인
   - 트렌드 악화·수준 전환 감지 → **모듈 A** 실행
   - 급등·비정상 패턴 즉시 감지 → **모듈 B** 실행
   - 둘 다 → **모듈 A → 모듈 B** 순서로 실행
2. `workspaces/uw-loss-monitoring/input/` 에 분석 가능한 자료가 있는지 확인
3. 자료가 없으면 더미데이터 생성 여부를 사용자에게 확인

---

## 실행 순서

```
[모듈 A] 트렌드 진단 (선택)
  입력: workspaces/uw-loss-monitoring/input/loss-ratio-stats/
        workspaces/uw-loss-monitoring/input/public-reports/
  출력: workspaces/uw-loss-monitoring/output/trend-analysis/
  지침: .claude/agents/uw-monitoring/uw-loss-monitoring.md
  기법: EWMA, STL, SPC, BF법
  산출: 경보 등급(🔴/🟡/🟢) 포함 트렌드 리포트

[모듈 B] 이상치 탐지 (선택)
  입력: workspaces/uw-loss-monitoring/input/loss-ratio-stats/
        (모듈 A 산출물 있으면 함께 참조)
  출력: workspaces/uw-loss-monitoring/output/anomaly-detection/
  지침: .claude/agents/uw-monitoring/uw-loss-monitoring.md
  기법: Isolation Forest, SARIMA 잔차, Prophet
  산출: 이상 스코어 + 원인 변수 분류표
```

---

## 단계별 완료 기준

| 모듈 | 완료 기준 |
|---|---|
| 모듈 A | `output/trend-analysis/` 에 트렌드 리포트 생성, 경보 등급 포함 |
| 모듈 B | `output/anomaly-detection/` 에 이상치 탐지 결과 생성, 원인 변수 분류 포함 |

각 모듈 완료 후 "[모듈 N 완료]" 형태로 진행 상황을 보고한다.

---

## 입력 자료 기준

| 유형 | 위치 | 허용 출처 |
|---|---|---|
| 손해율 통계 | `input/loss-ratio-stats/` | 손해보험협회, 금융감독원 공시 통계 |
| 공개 보고서 | `input/public-reports/` | 보험연구원, CAS, Swiss Re, Munich Re 등 |
| 더미데이터 | (직접 생성) | 테스트 목적, [더미데이터] 표기 필수 |

---

## 보안 규칙

다음 자료는 입력하지 않는다:
- 실제 계약·청구 원천 데이터
- 고객 식별 가능 정보
- 내부 DB 접속 정보
- 사내 비공개 손해율 원천 데이터

---

## 완료 후 안내

실행 완료 시 다음을 안내한다:

```
[UW 손해율 모니터링 완료]

생성된 산출물:
- 트렌드 진단 리포트: workspaces/uw-loss-monitoring/output/trend-analysis/
- 이상치 탐지 결과:   workspaces/uw-loss-monitoring/output/anomaly-detection/

다음 단계 옵션:
1. 모듈 A 재실행 (기간·담보 범위 변경) → /uw-loss-monitoring 재호출
2. 모듈 B 재실행 (탐지 기법 변경)     → /uw-loss-monitoring 재호출
3. 기획 문서 작성                      → 산출물 기반 planning-docs/ 저장
```
