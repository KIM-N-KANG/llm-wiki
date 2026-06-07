---
title: "Scaffolding (구조)"
type: concept
tags: [concept/pattern, stack/llm]
sources: [당근 하네스 교육 자료.pdf]
created: 2026-06-07
updated: 2026-06-07
confidence: high
---

## 정의

AI가 일할 수 있는 물리적 기반을 설계하는 것. 프로젝트 폴더 구조, 도구 배치, 경계 설정을 한 번 해두면 계속 쓰는 구조다. [[Harness-Engineering]]의 6개 축 중 "구조" 축에 해당하며, 모든 레이어를 감싸는 컨테이너가 된다.

## 작동 원리

**권장 폴더 구조**:
```
my-project/
├── src/         # 비즈니스 로직
├── docs/        # AI의 참고서 (사람이 관리)
├── tests/       # 검증 인프라
├── .dev/        # AI가 남기는 기록·작업의 흔적
├── .claude/     # AI 설정
│   ├── rules/   # 주제별 규칙 (glob 패턴으로 조건부 로드)
│   ├── skills/  # 반복 작업 레시피
│   └── hooks/   # 자동 안전장치
├── out/         # 빌드 산출물
└── CLAUDE.md    # 프로젝트 지도
```

**사람 문서 vs AI 문서 분리**:
- `docs/` (사람 관리): 비즈니스 룰·도메인 정의, 체크리스트·온보딩 가이드, ADR·API 스펙·외부 연동 규격
- `.dev/` (AI가 남김): learnings·troubleshooting 기록, 작업 로그·디버깅 히스토리, 실험 결과·스크래치패드

**AI 도구 유형**:
- **Skills**: 반복 작업의 레시피화. /commit, /review 같은 슬래시 명령
- **Hooks**: 자동 안전장치. Pre(차단) / Post(검사) / Stop(일지) / Notification(알림)
- **Agents**: 전문가 팀원. 서브에이전트 파견 또는 팀 구성
- **MCP**: 외부 시스템 연결. DB, Slack, Linear 등 연동
- **Plugins**: 위 컴포넌트를 하나의 패키지로 묶어서 배포/공유

**경계 설정**:
- 뭘 알려줄까: CLAUDE.md·rules/에 프로젝트 규칙, 코딩 스타일, 금기사항 작성
- 어디까지 허용할까: settings.json Permission Mode (plan / auto / bypass)
- 뭘 막을까: .claude/hooks/로 위험한 명령을 실행 전에 자동 차단

**아키텍처가 품질을 결정**:
- 클린 아키텍처(도메인/서비스/인프라 분리) → 새 기능 = 기존 패턴 복제 → 시간이 갈수록 AI 품질 상승 (3개월 후 30% → 85%)
- 구조 없음 → 파일 100개가 평면적으로 나열 → 시간이 갈수록 AI 품질 하락

## 적용 사례

- gstack: "Solo shipping at team velocity" — src/docs/tests/.claude/ 구조로 혼자서 팀처럼 출하
- karpathy의 CLAUDE.md가 바이럴 → subagent 형태로 뽑아내서 자신의 워크플로우에 꽂음
- CLAUDE.md에 "직접 main push 금지" + Hook으로 `git push --force` 차단 → 이중 안전장치

## 관련 컨셉

- [[Harness-Engineering]] — Scaffolding을 포괄하는 상위 개념
- [[Context-Engineering]] — Scaffolding 위에 쌓이는 맥락
- [[Git-브랜치-전략]] — 구조 설계의 브랜치 관리 사례
- [[커밋-메시지-컨벤션]] — 구조 내 규칙 적용 사례

## 관련 엔티티

- [[Claude-Code]] — .claude/ 폴더, CLAUDE.md, rules/, skills/, hooks/를 실제로 읽는 주체
- [[이호연]] — 구조 설계 원칙 발표

## 소스

- `[[sources/당근-하네스-교육-자료]]` — 폴더 구조, 도구 배치, 경계 설정 방법 상세 설명
