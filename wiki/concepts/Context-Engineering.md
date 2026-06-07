---
title: "Context Engineering"
type: concept
tags: [concept/framework, stack/llm, stack/prompt]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 정의

AI에게 필요한 배경지식과 규칙을 체계적으로 제공하여 AI가 올바른 맥락 위에서 일하게 하는 기술. [[Harness-Engineering]]의 6개 축 중 "맥락(Context)" 축에 해당한다. Prompt Engineering이 "이렇게 말해봐"라면, Context Engineering은 "이런 배경지식을 줘봐"다.

## 작동 원리

**CLAUDE.md 3단계 상속 구조** (하위가 상위를 오버라이드):

```
USER     ~/.claude/CLAUDE.md       ← 모든 프로젝트 공통 (내 습관, 스타일)
              ↓ 상속
PROJECT  my-app/CLAUDE.md          ← 이 프로젝트 전용 (스택, 컨벤션)
              ↓ 상속 + 오버라이드
FOLDER   src/auth/CLAUDE.md        ← 이 폴더 작업 시만 (특수 규칙)
```

**핵심 원칙 3가지**:
1. **[[Progressive-Disclosure]]**: 필요한 것만 필요할 때 보여주기. 한꺼번에 다 주면 AI도 헷갈린다.
2. **.claude/rules/**: CLAUDE.md가 길어지면 주제별로 분리 + glob 패턴으로 조건부 로드
3. **Scope 계층**: User/Project/Folder 각 레벨에 맞는 정보 배치

**세션 맥락 관리**:
- ~20% 사용: 쾌적
- ~50%: `/compact` — 오래된 대화를 요약·압축
- ~80%: `/clear` 또는 새 세션
- 내 기준: **20~30% 되면 새로 시작**. 이어가야 하면 `handoff`로 맥락 넘긴다

**주기적 점검**:
- `/context`로 카테고리별 토큰 사용량 확인
- Skill·MCP는 생각보다 context를 많이 차지함 → 안 쓰는 것은 정리

## 적용 사례

- CLAUDE.md에 "직접 main push 금지" 작성 + Hook으로 `git push --force` 차단 → 이중 안전장치
- code-style.md (항상 로드): 함수 20줄 이내, camelCase, 주석은 영어
- security.md (glob: `**/auth/**, *.sql` 시만): .env 직접 수정 금지, SQL은 반드시 parameterized query
- react-*.md (glob: `*.tsx` 작업 시만): React 전용 규칙

## 관련 컨셉

- [[Harness-Engineering]] — Context Engineering을 포괄하는 상위 개념
- [[Scaffolding]] — 컨텍스트가 담기는 구조적 기반
- [[Progressive-Disclosure]] — 핵심 맥락 관리 원칙
- [[AI-Slop]] — 맥락 관리 실패 시 발생

## 관련 엔티티

- [[Claude-Code]] — CLAUDE.md, .claude/rules/ 등을 실제로 읽는 실행 환경
- [[Anthropic]] — Context Engineering 개념 제시

## 소스

- `[[sources/당근-하네스-교육-자료]]` — CLAUDE.md 상속 구조, Progressive Disclosure, 세션 관리 방법 설명
