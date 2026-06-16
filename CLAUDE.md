# CLAUDE.md

## Project Purpose

이 프로젝트는 보험 UW 업무에서 사용하는 비식별 업무 보조 Agent를 구성하기 위한 프로젝트이다.

주요 목적은 다음과 같다.

1. UW Rule 변경 및 화면 개선 요청 전 테스트 시나리오 구조화

2. GA 소식지 및 외부 공개자료 기반 보험상품 동향 분석

3. 데이터 분석 로직, 집계 기준, 검증 절차 정리

4. 보고용 산출물 초안 작성

## Security Rules

절대 입력하지 말아야 할 정보:

- 고객명

- 주민등록번호

- 증권번호 원문

- 청약번호 원문

- 연락처

- 주소

- 계약자/피보험자 식별 가능 정보

- 실제 청구 상세 원천 데이터

- 내부 DB 접속 정보

- 사내 계정, 비밀번호, 서버 주소

허용 가능한 정보:

- 비식별 컬럼명

- 업무 로직 설명

- 집계 단위

- 룰 조건

- 예시용 더미 데이터

- 공개자료

- 비식별 테스트 케이스

## Output Style

답변은 다음 기준을 따른다.

1. 업무 보고용 문체로 작성한다.

2. 불확실한 내용은 단정하지 않는다.

3. 개발 요청 문서는 목적, 현행, 변경, 테스트 기준, 기대효과 순서로 작성한다.

4. 데이터 분석 문서는 기준일, 집계 단위, 필터 조건, 검증 포인트를 반드시 포함한다.

5. 산출물은 표 또는 체크리스트 중심으로 작성한다.

# Project Folder Rules

이 프로젝트의 Skill 정의 파일과 실제 작업 파일은 분리한다.

## Skill Definition

`.claude/skills/` 하위 폴더에는 Skill 실행 지침, 템플릿, 참고 기준만 저장한다.

실제 업무용 PDF, Excel, CSV, 분석 결과물은 `.claude/skills/`에 저장하지 않는다.

## Workspace

실제 작업 파일은 `workspaces/` 하위에 업무별로 분리한다.

- `workspaces/uw-test-scenario/`
- `workspaces/ga-product-research/`
- `workspaces/insurance-law-ref/`
- `workspaces/uw-report-automation/`
- `workspaces/uw-product-planning/`

각 업무 폴더는 `input/`과 `output/`을 별도로 가진다.

## Input / Output Rule

UW 테스트 시나리오 관련 입력물은 다음 위치에 저장한다.

- `workspaces/uw-test-scenario/input/`

UW 테스트 시나리오 산출물은 다음 위치에 저장한다.

- `workspaces/uw-test-scenario/output/`

GA 상품 리서치 관련 입력물은 다음 위치에 저장한다.

- `workspaces/ga-product-research/input/`

GA 상품 리서치 산출물은 다음 위치에 저장한다.

- `workspaces/ga-product-research/output/`

보험 법령 참조 관련 입력물(법령 PDF, 감독규정)은 다음 위치에 저장한다.

- `workspaces/insurance-law-ref/input/laws/` (법령 원문)
- `workspaces/insurance-law-ref/input/guidelines/` (감독규정·지침)

보험 법령 참조 산출물(Q&A 로그)은 다음 위치에 저장한다.

- `workspaces/insurance-law-ref/output/qa-log/`

UW 리포트 자동화 관련 입력물은 다음 위치에 저장한다.

- `workspaces/uw-report-automation/input/` (요구사항 정의서)
- `workspaces/uw-report-automation/input/masked-data/` (마스킹 처리 데이터)
- `workspaces/uw-report-automation/input/dummy-data/` (더미데이터)

UW 리포트 자동화 산출물은 다음 위치에 저장한다.

- `workspaces/uw-report-automation/output/` (모델 설계안, 대시보드 설계안, 리포트 초안)

UW 상품 기획 관련 입력물은 다음 위치에 저장한다.

- `workspaces/uw-product-planning/input/` (기획 요청 자료, 기초서류 참고본)

UW 상품 기획 산출물은 다음 위치에 저장한다.

- `workspaces/uw-product-planning/output/` (인수기준 검토 초안, 담보 한도 기획안, 상품 개정 검토 문서)
