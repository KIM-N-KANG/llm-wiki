---
title: "PR 템플릿"
type: concept
tags: [concept/pattern, stack/git]
sources: [Pull-Request-템플릿.md]
created: 2026-06-13
updated: 2026-06-13
confidence: high
---

## 정의

작업 유형별 Pull Request 본문에 필요한 섹션과 체크 항목을 미리 정해, 변경 내용·검증·위험 요소를 일관되게 기록하도록 하는 문서화 패턴.

## 작동 원리

PR 템플릿은 Web, Mobile, Backend server, AI server, Infra 다섯 유형으로 나뉩니다.

**공통 구조:**
- 요약
- 관련 이슈
- 변경 사항
- 검증 또는 영역별 검증
- 체크리스트

**유형별 추가 섹션:**

| 유형 | 추가 섹션 또는 강조 항목 |
|------|--------------------------|
| Web | 화면, Before/After 표, 반응형·상태·접근성 확인 |
| Mobile | 화면, Before/After 표, 반응형·상태·접근성 확인 |
| Backend server | 서버 검증, API 변경 |
| AI server | AI 변경 범위, AI 검증, 평가 결과 |
| Infra | Infra 검증, API 변경 |

모든 유형의 체크리스트는 PR 제목과 브랜치명 형식을 확인하도록 구성됩니다.

## 적용 사례

Web 또는 Mobile PR은 UI 변경이 있으면 스크린샷이나 화면 녹화를 첨부하고, UI 변경이 없으면 화면 섹션에 "해당 없음"으로 작성합니다.

Backend server PR은 API 변경이 없으면 API 변경 섹션에 "없음"으로 적고, 변경이 있다면 Endpoint, Request, Response, Status code를 기록합니다.

AI server PR은 Prompt, Model, Retrieval/RAG, Tool/Agent, Evaluation, Dataset 중 해당하는 변경 범위만 남기고, 대표 입력 테스트와 비용 또는 latency 영향을 확인합니다.

Infra PR은 `docker compose config`를 기본 검증으로 두고, 필요 시 pull, up, ps 명령 확인을 추가합니다.

## 관련 컨셉

- [[PR-규칙]]
- [[PR-검증-체크리스트]]
- [[브랜치-이름-규칙]]

## 관련 엔티티

없음

## 소스

- [[sources/Pull-Request-템플릿]]
