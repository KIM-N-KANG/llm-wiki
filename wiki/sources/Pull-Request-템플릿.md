---
title: "Pull Request 템플릿"
type: source
tags: [concept/pattern, stack/git]
sources: [Pull-Request-템플릿.md]
created: 2026-06-13
updated: 2026-06-13
confidence: high
---

## 원본 링크

[[raw/Pull-Request-템플릿]]

## 한줄 요약

Web, Mobile, Backend server, AI server, Infra 작업 유형별 PR 본문 구조와 검증 체크리스트를 정의한 템플릿.

## 핵심 내용

- Web과 Mobile PR은 요약, 관련 이슈, 변경 사항, 화면, 검증, 체크리스트를 공통 구조로 사용
- Backend server PR은 서버 검증, API 변경, 체크리스트를 포함하며 `./gradlew test`, API 동작, DB 마이그레이션, Swagger/OpenAPI 확인 항목을 둠
- AI server PR은 Prompt, Model, Retrieval/RAG, Tool/Agent, Evaluation, Dataset 변경 범위와 AI 검증·평가 결과를 별도 섹션으로 둠
- Infra PR은 `docker compose config`, `docker compose pull`, `docker compose up -d`, `docker compose ps` 중심의 검증 항목을 둠
- 모든 유형은 PR 제목 `[KNK-{이슈번호}] {Tag}: {제목}`과 브랜치명 `{tag}/KNK-{이슈번호}-{브랜치-제목}` 형식 준수를 확인
- Web/Mobile은 UI 변경 시 화면 자료, 반응형, 로딩·빈 상태·에러 상태, 접근성 label·alt·focus 상태 확인을 요구
- 실제 secret 또는 로컬 전용 파일 포함 여부와 문서 수정 필요 여부를 공통적으로 점검

## 추출된 엔티티

없음

## 추출된 컨셉

- [[PR-템플릿]]
- [[PR-검증-체크리스트]]
- [[PR-규칙]]
- [[브랜치-이름-규칙]]

## 주목할 인사이트

하나의 PR 규칙을 모든 작업에 일괄 적용하기보다 Web/Mobile, Backend, AI, Infra의 변경 위험을 나누어 각 영역에 맞는 검증 항목을 템플릿에 직접 포함합니다.

## 신뢰도

high — 팀 내부 PR 작성 템플릿
