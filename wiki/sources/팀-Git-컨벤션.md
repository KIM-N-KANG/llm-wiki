---
title: "팀 Git 컨벤션"
type: source
tags: [concept/pattern, stack/git]
sources: [팀-Git-컨벤션.md]
created: 2026-06-04
updated: 2026-06-04 (브랜치 이름 예시 수정)
confidence: high
---

## 원본 링크

[[Git-컨벤션]]

## 한줄 요약

`main`/`dev` 기반 브랜치 전략과 Jira 이슈 번호 연동 커밋·PR 컨벤션을 정의한 팀 Git 운영 규칙.

## 핵심 내용

- 기준 브랜치는 `main`(프로덕션)과 `dev`(통합) 두 개이며 기본 작업 브랜치는 `dev`
- 작업 브랜치 이름 형식: `{태그}/{KNK-이슈번호}-{브랜치_제목}`
- 커밋 메시지 형식: `[KNK-{이슈번호}] {태그}: {제목}`
- 기능 브랜치 → dev: **Squash and Merge** (커밋 정리 목적)
- release → main: **Merge Commit** (배포 이력 명확화 목적)
- release → dev: **Rebase and Merge** (불필요한 머지 커밋 방지)
- `main`, `dev`, `release/*`에는 직접 Push 및 Force Push 금지

## 추출된 엔티티

없음

## 추출된 컨셉

- [[Git-브랜치-전략]]
- [[브랜치-이름-규칙]]
- [[커밋-메시지-컨벤션]]
- [[PR-규칙]]
- [[머지-전략]]

## 주목할 인사이트

머지 방식을 상황별로 다르게 지정한 점이 특징적입니다. 기능 브랜치는 Squash, 배포 브랜치는 Merge Commit, 동기화는 Rebase로 구분해 브랜치별 커밋 그래프의 목적을 명확히 유지합니다.

## 신뢰도

high — 팀 내부 공식 문서
