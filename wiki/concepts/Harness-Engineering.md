---
title: "Harness Engineering"
type: concept
tags: [concept/framework, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 정의

AI가 혼자서도 잘 일할 수 있는 **작업 환경 자체를 설계하는 기술**. 프롬프트(말을 잘 하는 것)나 Context Engineering(배경지식을 주는 것)을 넘어, 맥락·제한·작업 흐름·검증을 모두 포괄하는 환경 설계 개념이다.

Prompt Engineering(Level 1) → Context Engineering(Level 2) → **Harness Engineering(Level 3)**으로 진화하는 흐름의 최상위 단계.

## 작동 원리

**6개 축의 순환 구조**:

```
구조(Scaffolding) → 맥락(Context) → 계획(Planning)
       ↑                                    ↓
개선(Compounding) ← 검증(Verification) ← 실행(Orchestration)
```

| 축 | 핵심 질문 | 주요 도구 |
|----|-----------|-----------|
| 구조(Scaffolding) | 뭘 깔아두는가 | 폴더 구조, CLAUDE.md, Skills, Hooks |
| 맥락(Context) | AI가 뭘 아는가 | CLAUDE.md 상속, .claude/rules/, Progressive Disclosure |
| 계획(Planning) | 뭘 할지 정하는가 | Plan Mode, AskUserQuestion, /specify |
| 실행(Orchestration) | 어떻게 시키는가 | 단일/Subagent/Team Mode, Ralph Loop |
| 검증(Verification) | 어떻게 믿는가 | Sprint Contract, Generator-Evaluator 분리 |
| 개선(Compounding) | 어떻게 나아지는가 | 세션 분석, 반복→Skill, 실수→Rule |

**3 레이어 구조**:
- Layer 1 (기반): 폴더 구조, CLAUDE.md, .claude/rules/, auto-memory
- Layer 2 (도구·연결): MCP 서버, 외부 API, CLI 도구
- Layer 3 (워크플로우): 범용 플러그인(gstack, oh-my-claudecode), 직접 만든 Skill/Agent/Hook

## 적용 사례

- **[[LangChain]]**: 동일 모델에서 하네스만 변경 → TerminalBench 52.8→66.5% (+14%p), 30위 → Top 5
- **[[OpenAI]]**: 엔지니어 3~7명, 5개월, 인간 코드 0줄로 100만 줄 코드베이스 구현 — "더 좋은 모델 써라"는 없음, 전부 환경 설계
- **[[Anthropic]]**: 싱글 에이전트 20분/$9 실패 → 3에이전트 하네스 6h/$200 완성 동작. 간소화 버전 $124로 품질 유지
- **[[Stripe]]**: 1,000 PR/주 완전 무인 자동 머지. 매 스텝 검증 게이트 + 정밀 컨텍스트 관리

## 관련 컨셉

- [[Context-Engineering]] — Harness의 맥락 축
- [[Scaffolding]] — Harness의 구조 축
- [[Orchestration-패턴]] — Harness의 실행 축
- [[Verification-전략]] — Harness의 검증 축
- [[Progressive-Disclosure]] — 맥락 관리 원칙
- [[AI-Slop]] — Harness 실패 시 발생하는 문제
- [[커밋-메시지-컨벤션]] — Harness 구조 요소의 예시

## 관련 엔티티

- [[이호연]] — 개념 발표자
- [[Anthropic]] — "규율은 코드가 아니라 스캐폴딩에서 드러난다"
- [[OpenAI]] — "사람이 방향을 잡고, 에이전트가 실행한다"
- [[Claude-Code]] — 주요 실행 환경

## 소스

- `[[sources/당근-하네스-교육-자료]]` — Harness Engineering 전체 개념 정의 및 6개 축 설명
