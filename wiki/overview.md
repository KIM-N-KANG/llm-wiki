# Wiki Overview

> 마지막 갱신: 2026-06-10
> 이 페이지는 `/ingest` 실행 시 자동으로 업데이트됩니다.

## 위키 현황

- 총 소스: 3개
- 추출된 엔티티: 7개
- 추출된 컨셉: 16개
- 저장된 답변: 0개

## 핵심 주제

1. **팀 Git 운영 규칙** — 브랜치 전략, 커밋 메시지, PR 작성, 머지 방식
2. **Harness Engineering** — AI가 잘 일하는 환경을 설계하는 기술 (구조·맥락·계획·실행·검증·개선)
3. **마냑 서비스 기획** — AI 인터랙티브 스토리 서비스, 단계별 제작 모드, 채팅 플레이, 초기 KPI 구조

## 주요 엔티티

- [[entities/Anthropic]] — AI 안전 연구·개발 회사, Harness Engineering 원칙 제시
- [[entities/OpenAI]] — 100만 줄 코드 인간 코드 0줄 달성, 하네스 설계 대표 사례
- [[entities/Stripe]] — 1,000 PR/주 완전 무인 자동 머지
- [[entities/LangChain]] — 하네스 변경만으로 TerminalBench +14%p 달성
- [[entities/Claude-Code]] — Harness 구현 주요 실행 환경
- [[entities/이호연]] — Harness Engineering 교육 자료 발표자
- [[entities/마냑]] — AI 인터랙티브 스토리 서비스, 단계별 제작 모드·채팅 플레이·운영 KPI

## 주요 컨셉

- [[concepts/Harness-Engineering]] — AI 작업 환경 설계의 전체 프레임워크
- [[concepts/Scaffolding]] — Monorepo 구조, 역할별 폴더링, 경계 설정
- [[concepts/Context-Engineering]] — CLAUDE.md 상속, rules/ 조건부 로드
- [[concepts/Orchestration-패턴]] — 단일/Subagent/Team Mode 실행 패턴
- [[concepts/Verification-전략]] — Sprint Contract, Generator-Evaluator 분리
- [[concepts/Progressive-Disclosure]] — 필요한 것만 필요할 때 제공
- [[concepts/AI-Slop]] — Harness 부재 시 발생하는 품질 저하 현상
- [[concepts/Git-브랜치-전략]] — main/dev 기반 브랜치 운영 전략
- [[concepts/커밋-메시지-컨벤션]] — Jira 이슈 번호 연동 커밋 메시지 형식
- [[concepts/브랜치-이름-규칙]] — 태그/KNK-이슈번호 형식의 브랜치 네이밍 규칙
- [[concepts/PR-규칙]] — PR 제목·본문·태그 작성 기준
- [[concepts/머지-전략]] — 브랜치 목적별 Squash/Merge Commit/Rebase 적용 규칙
- [[concepts/인터랙티브-스토리텔링]] — AI와 사용자가 협력해 이야기를 만드는 콘텐츠 형태
- [[concepts/스토리-제작-모드]] — 숙련도별 간편/일반/전문가 3단계 스토리 제작 패턴
- [[concepts/크레딧-시스템]] — LLM 비용을 가상 화폐로 추상화하는 AI 서비스 과금 모델
- [[concepts/AI-인터랙티브-스토리-KPI]] — AI 인터랙티브 스토리 서비스의 초기 성장·참여·완료율 지표

## 최근 인사이트

"모델 교체로 5% 개선하는 것보다 하네스 설계로 15% 개선하는 것이 현실적이다" (당근 하네스 교육 자료). 마냑 기획서는 기능 목록과 함께 월간 신규 등록 스토리 수, 메시지 참여도, 재방문율, 크레딧 사용률, 제작 퍼널 지표를 명시해 제작 진입 장벽 완화 효과를 KPI로 측정하려 한다.
