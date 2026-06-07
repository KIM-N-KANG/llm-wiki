---
title: "Anthropic"
type: entity
tags: [entity/company, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 개요

AI 안전 연구·개발 회사. Claude 모델 개발사. Harness Engineering 맥락에서 에이전트 하네스 설계 원칙의 이론적 근거로 자주 인용된다.

## 핵심 특징

- 싱글 에이전트 20분/$9 실패 → 3에이전트 하네스 6h/$200 완성 동작. 간소화 버전 $124로 품질 유지
- "규율은 코드가 아니라 스캐폴딩에서 드러난다" (anthropic.com/engineering/harness-design)
- "Harness의 모든 구성요소는 모델이 혼자서는 못 하는 것에 대한 가정을 담고 있다"
- "Harness의 공간은 모델이 좋아져도 줄어들지 않는다. 이동할 뿐이다."
- Generator-Evaluator 분리 원칙: "만든 AI와 확인하는 AI를 분리하는 것이 가장 강력한 레버"

## 관련 컨셉

- [[Harness-Engineering]] — Anthropic이 정의한 개념의 핵심 출처
- [[Scaffolding]] — "규율은 스캐폴딩에서 드러난다" 원칙
- [[Verification-전략]] — Generator-Evaluator 분리 원칙 제시
- [[Context-Engineering]] — Claude Code의 CLAUDE.md, .claude/rules/ 구조

## 관련 엔티티

- [[Claude-Code]] — Anthropic이 개발한 AI 코딩 도구
- [[OpenAI]] — Harness 적용 사례로 함께 언급

## 소스

- `[[sources/당근-하네스-교육-자료]]` — $9 vs $200 사례, 스캐폴딩 원칙, Generator-Evaluator 분리로 인용
