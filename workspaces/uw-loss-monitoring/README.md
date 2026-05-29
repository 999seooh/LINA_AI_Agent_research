# UW 손해율 모니터링 Workspace

## 목적

담보별 손해율 트렌드 진단 및 이상치 탐지 시스템 기획을 위한 자료 및 산출물 관리.

## 폴더 구조

```
uw-loss-monitoring/
├── input/
│   ├── loss-ratio-stats/    ← 손해율 통계 자료 (협회 공시, 감독기관 자료 등)
│   └── public-reports/      ← 공개 보고서 (보험연구원, CAS, Swiss Re 등)
│
└── output/
    ├── trend-analysis/      ← 모듈 A: 담보별 손해율 트렌드 진단 산출물
    ├── anomaly-detection/   ← 모듈 B: 이상치 탐지 산출물
    └── planning-docs/       ← 시스템 기획 문서
```

## 입력 자료 기준

- 손해보험협회(knia.or.kr) 공시 통계
- 금융감독원(fss.or.kr) 보험통계
- 보험연구원(kiri.or.kr) 공개 보고서
- 해외 공개 리포트 (CAS, Swiss Re, Munich Re 등)
- 비식별 더미 데이터 (테스트용)

## 보안 규칙

CLAUDE.md 보안 규칙 준수. 다음 자료는 입력 금지.

- 실제 계약·청구 원천 데이터
- 고객 식별 가능 정보
- 내부 DB 접속 정보
- 사내 비공개 손해율 원천 데이터

## 연관 문서

- `workspaces/insurance-law-ref/output/qa-log/담보별_손해율_트렌드진단_모듈리서치.md`
- `workspaces/insurance-law-ref/output/qa-log/이상치탐지_모듈리서치.md`
- `workspaces/insurance-law-ref/output/qa-log/중복가입_이상탐지_시스템_기획참고_통합본.md`
