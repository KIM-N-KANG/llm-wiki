---
title: "PR 검증 체크리스트"
type: concept
tags: [concept/pattern, stack/git]
sources: [Pull-Request-템플릿.md]
created: 2026-06-13
updated: 2026-06-13
confidence: high
---

## 정의

Pull Request 제출 전 테스트, 로컬 실행, 사용자 흐름, 보안·문서·영역별 변경 영향을 점검하도록 정리한 확인 항목 묶음.

## 작동 원리

**공통 점검:**
- PR 제목이 `[KNK-{이슈번호}] {Tag}: {제목}` 형식을 따르는지 확인
- 브랜치명이 `{tag}/KNK-{이슈번호}-{브랜치-제목}` 형식을 따르는지 확인
- Jira 이슈의 작업 범위와 완료 기준을 확인
- 실제 secret 또는 로컬 전용 파일 포함 여부 확인
- 동작이나 설정이 바뀐 경우 관련 문서 수정 여부 확인

**Web/Mobile 점검:**
- 테스트 실행, 로컬 실행, 주요 사용자 흐름 확인
- 반응형 화면 확인
- 로딩, 빈 상태, 에러 상태 확인
- UI 변경 시 기존 디자인 시스템 또는 팀 스타일 준수
- 접근성에 필요한 label, alt, focus 상태 확인
- API 연동 변경 시 요청/응답 계약 확인

**Backend server 점검:**
- `./gradlew test`
- 필요 시 로컬 실행, API 동작, DB 마이그레이션 동작 확인
- 필요 시 Swagger/OpenAPI 문서 확인
- 비즈니스 API의 `/api/v1` prefix 사용 여부 확인
- Security 설정 변경 시 공개/보호 엔드포인트 확인
- DB 변경 시 Flyway 마이그레이션 추가 또는 변경 사유 설명

**AI server 점검:**
- 대표 입력 수동 테스트
- 실패/예외 케이스 확인
- 필요 시 평가 결과 첨부
- 비용 또는 latency 영향 확인
- 개인정보/민감정보 노출 가능성 확인

**Infra 점검:**
- `docker compose config`
- 필요 시 `docker compose pull`, `docker compose up -d`, `docker compose ps`
- GHCR publish 이미지 실행만 사용하고 infra 레포에서 서비스 소스코드를 빌드하지 않는지 확인
- Dockerfile을 추가하지 않았는지 확인

## 적용 사례

프론트엔드 PR에서는 화면 변경 전후를 표로 첨부하고, 주요 사용자 흐름과 반응형·로딩·빈 상태·에러 상태를 확인합니다.

백엔드 PR에서는 API 변경이 있으면 Endpoint, Request, Response, Status code를 기록하고, DB 변경이 있으면 Flyway 마이그레이션 또는 변경 사유를 설명합니다.

AI server PR에서는 프롬프트나 모델 설정 변경 시 의도, 기대 동작, 비용·속도·품질 영향을 확인합니다.

Infra PR에서는 Docker Compose 설정 검증과 함께 Dockerfile 추가 여부, GHCR publish 이미지 사용 여부를 확인합니다.

## 관련 컨셉

- [[PR-템플릿]]
- [[PR-규칙]]
- [[브랜치-이름-규칙]]

## 관련 엔티티

없음

## 소스

- [[sources/Pull-Request-템플릿]]
