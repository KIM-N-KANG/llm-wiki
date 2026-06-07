---
title: "Verification 전략 (검증)"
type: concept
tags: [concept/pattern, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 정의

AI가 만든 결과물을 어떻게 믿을 것인가에 대한 설계. [[Harness-Engineering]]의 6개 축 중 "검증(Verification)" 축에 해당한다. 기준 없이 시키면 AI가 끝없이 하거나 대충 끝냈다고 하기 때문에, 작업 전에 완료 기준을 명확히 정하는 것이 핵심이다.

## 작동 원리

**검증 원칙 4가지**:

**1. Sprint Contract (기준이 있어야 검증이 가능하다)**
- 작업 전에 "뭘 만들고 어떻게 검증할지" 합의
- 완료 조건을 측정 가능하게 쓴다: "잘 되게" (X) → "테스트 통과 + 빌드 성공" (O)
- 기준이 명확하면 [[Orchestration-패턴#Ralph Loop]]로 자동 반복 가능

**2. Generator-Evaluator 분리 (컨텍스트를 나누고, 관점을 분리한다)**
- 만드는 AI(Generator)와 평가하는 AI(Evaluator)를 반드시 분리
- 같은 컨텍스트에서 만들고 평가하면 quality가 mediocre해도 자신있게 칭찬함
- Evaluator를 회의적으로 튜닝하는 것이 Generator를 자기비판적으로 만드는 것보다 훨씬 쉬움
- "만든 AI와 확인하는 AI를 분리하는 것이 가장 강력한 레버"

**3. 모델·역할 분리 (모델도 나누고, 역할도 나눈다)**
- Codex: 코드 리뷰 (로직 오류, 보안 취약점, 테스트 누락 검출)
- Gemini: 문서 리뷰 (일관성, 정확성, 구조 검증)
- Opus: 복잡한 판단, 아키텍처 결정
- Sonnet: 빠른 확인, 반복 검증
- "Out of the box, Claude is a poor QA agent." — 검증 에이전트도 튜닝이 필요하다

**4. 안전장치 (실수해도 괜찮은 구조)**
- **되돌릴 수 있는 환경**: `git worktree add`로 브랜치 격리. 실수해도 메인은 안전
- **위험한 건 사람이 확인**: 삭제·배포·외부 발송 같은 작업은 Runtime Gate로 승인 후 실행
- **Dry-run 먼저**: "이렇게 할 건데 맞나?" 미리보기 후 실행

**에이전트에게 눈 달아주기**:
- Browser Agent (chrome-cdp / agent-browser): 실제 Chrome 브라우저를 제어해 웹앱 UX 직접 검증
- Computer Use (built-in MCP): 스크린샷 + 마우스/키보드로 모든 앱 제어
- 시각 검증 루프: 만든다 → 스크린샷 → 보고 판단 → 수정

## 적용 사례

- Sprint Contract 예시: "모바일 반응형 + Lighthouse 90점 이상 + 카피 3번 이상 퇴고" → Ralph Loop으로 4회 만에 완료
- [[Stripe]]: 매 스텝 검증 게이트 + 정밀 컨텍스트 관리로 1,000 PR/주 무인 처리

## 관련 컨셉

- [[Harness-Engineering]] — 검증을 포괄하는 상위 개념
- [[Orchestration-패턴]] — 검증 대상을 만드는 실행 단계
- [[AI-Slop]] — 검증 부재 시 발생하는 문제

## 관련 엔티티

- [[Anthropic]] — Generator-Evaluator 분리 원칙 제시
- [[Stripe]] — 검증 게이트 대규모 적용 사례
- [[Claude-Code]] — Browser Agent, Computer Use 실행 환경

## 소스

- `[[sources/당근-하네스-교육-자료]]` — Sprint Contract, Generator-Evaluator 분리, 안전장치 설명
