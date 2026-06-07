---
title: "LangChain"
type: entity
tags: [entity/company, entity/technology, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: medium
---

## 개요

LLM 애플리케이션 개발을 위한 오픈소스 프레임워크. Harness Engineering 맥락에서 하네스 설계의 효과를 보여주는 주요 사례로 언급된다.

## 핵심 특징

- GPT-5.2-Codex 모델 고정 상태에서 하네스만 변경
- 셀프 검증 루프 + 컨텍스트 자동 수집 + 덤 루프 탐지 추가
- TerminalBench 점수 52.8% → 66.5% (+14%p) 달성
- 벤치마크 순위 30위 → Top 5 진입

> ⚠️ 불확실: 구체적인 하네스 변경 내용(셀프 검증 루프, 덤 루프 탐지)의 정확한 구현 방식은 소스에 요약만 제시됨. 추가 검증 필요.

## 관련 컨셉

- [[Harness-Engineering]] — LangChain 사례가 핵심 증거로 사용됨
- [[Verification-전략]] — 셀프 검증 루프 적용 사례

## 관련 엔티티

- [[OpenAI]] — 동시 언급되는 하네스 적용 사례

## 소스

- `[[sources/당근-하네스-교육-자료]]` — "같은 모델, 하네스만 변경 30위 → Top 5" 사례로 인용
