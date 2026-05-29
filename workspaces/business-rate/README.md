# Business Rate Workspace

## 목적

최적기초율 및 사업비 계리가정 수립을 위한 자료 및 산출물 관리.
요율 산출 기준, IFRS17 사업비 배분 기준, 경험위험률 관련 분석을 지원한다.

## 폴더 구조

```
business-rate/
├── input/
│   └── guidelines/      ← 내부 지침 (최적기초율 산출 지침, 사업비 분류 지침 등)
│
└── output/
    ├── assumption-review/   ← 계리가정 검토 산출물
    └── planning-docs/       ← 기획 문서
```

## 입력 자료 기준

- 사내 최적기초율 산출 지침 (사규)
- 사내 IFRS17 사업비 분류·배분 지침 (사규)
- 금융위원회·금융감독원 계리감독 관련 공개자료

## 보안 규칙

CLAUDE.md 보안 규칙 준수. 다음 자료는 입력 금지.

- 실제 계약·청구 원천 데이터
- 고객 식별 가능 정보
- 내부 DB 접속 정보
- 사내 미공개 경험통계 원천 데이터

## 연관 문서

- `workspaces/uw-loss-monitoring/` — 담보별 손해율 모니터링
- `workspaces/insurance-law-ref/` — 보험 법령·감독규정 참조
