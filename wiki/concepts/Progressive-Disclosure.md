---
title: "Progressive Disclosure (점진적 노출)"
type: concept
tags: [concept/pattern, stack/llm, stack/prompt]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 정의

AI에게 모든 정보를 한꺼번에 넘기는 대신, "이런 상황에서는 이걸 참고해"라고 안내해서 필요한 것만 읽게 하는 맥락 관리 원칙. [[Context-Engineering]]의 핵심 원칙 중 하나다. "한꺼번에 다 주면 AI도 헷갈린다."

## 작동 원리

**기본 아이디어**:
- SKILL.md 또는 CLAUDE.md 안에서 상황별로 참고 문서를 가리킨다
- 코드 작성 시 → `references/code-style.md` 참고
- 테스트 시 → `references/testing-guide.md` 참고
- API 설계 시 → `references/api-convention.md` 참고
- 배포 시 → `references/deploy-checklist.md` 참고

**구현 방식**:
```
my-skill/
  SKILL.md               ← 핵심만 30줄 + 상황별 참조 가이드
  references/
    code-style.md
    testing-guide.md
    api-convention.md
    deploy-checklist.md
```
- CLAUDE.md는 핵심만 30줄로 유지, 나머지는 docs/로 분리
- 프롬프트에 "이 상황에서는 이 문서를 읽어"라고 가이드 → AI가 동적으로 필요한 문서만 읽음

**.claude/rules/ 조건부 로드**:
- 파일명에 glob 패턴을 넣으면 해당 파일 작업 시에만 로드됨
  - `code-style.md` → 항상 로드
  - `testing.md` (glob: `**/*.test.*, **/__tests__/**`) → 테스트 파일 작업 시만
  - `security.md` (glob: `**/auth/**, *.sql`) → auth/sql 작업 시만

## 적용 사례

- CLAUDE.md 최대 200줄 원칙 — "너무 길어지면 AI 성능이 급격히 저하된다"
- gstack의 /scaffold 스킬: 처음 프로젝트 셋업 시 CLAUDE.md, rules/, 폴더 구조까지 한 번에 생성

## 관련 컨셉

- [[Context-Engineering]] — Progressive Disclosure가 속하는 상위 개념
- [[Scaffolding]] — Progressive Disclosure를 담는 구조적 기반
- [[Harness-Engineering]] — 맥락 관리의 전체 프레임

## 관련 엔티티

- [[Claude-Code]] — .claude/rules/ glob 패턴을 해석하는 실행 환경

## 소스

- `[[sources/당근-하네스-교육-자료]]` — Progressive Disclosure 원칙, .claude/rules/ 가이드 설명
