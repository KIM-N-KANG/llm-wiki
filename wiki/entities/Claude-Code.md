---
title: "Claude Code"
type: entity
tags: [entity/product, entity/technology, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 개요

Anthropic이 개발한 AI 코딩 도구(CLI). Harness Engineering 실습의 주요 실행 환경으로, CLAUDE.md, .claude/rules/, .claude/skills/, .claude/hooks/ 등의 설정 구조를 통해 Harness를 구현한다.

## 핵심 특징

- CLAUDE.md 계층 상속: User(~/.claude/) → Project → Folder 순으로 상속·오버라이드
- .claude/rules/: glob 패턴으로 상황별 규칙 조건부 로드
- .claude/skills/: 반복 작업 레시피 슬래시 명령 (`/commit`, `/review` 등)
- .claude/hooks/: Pre/Post/Stop/Notification 이벤트 기반 자동 안전장치
- Agent 파견, TaskCreate, TeamCreate 등 Orchestration 도구 내장
- `/context` 명령으로 카테고리별 토큰 사용량 실시간 확인
- `/compact`, `/clear`, `handoff`로 세션 맥락 관리

## 관련 컨셉

- [[Harness-Engineering]] — Claude Code가 Harness를 구현하는 주 실행 환경
- [[Scaffolding]] — .claude/ 폴더 구조, CLAUDE.md
- [[Context-Engineering]] — CLAUDE.md 상속, .claude/rules/ glob 패턴
- [[Progressive-Disclosure]] — 조건부 rules/ 로드
- [[Orchestration-패턴]] — Agent, Task, Team 도구
- [[커밋-메시지-컨벤션]] — Git 관련 컨벤션 준수

## 관련 엔티티

- [[Anthropic]] — Claude Code 개발사
- [[이호연]] — Claude Code 기반 Harness Engineering 발표

## 소스

- `[[sources/당근-하네스-교육-자료]]` — Harness 구현 실행 환경으로 전반적으로 언급
