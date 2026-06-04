---
title: "Git 브랜치 전략"
type: concept
team: cross
tags: [concept/pattern, stack/git]
sources: [팀-Git-컨벤션.md]
created: 2026-06-04
updated: 2026-06-04
confidence: high
---

## 정의

`main`과 `dev` 두 기준 브랜치를 중심으로 기능 개발, 배포 준비, 핫픽스를 관리하는 팀의 Git 브랜치 운영 방식.

## 작동 원리

| 브랜치 | 역할 |
|--------|------|
| `main` | 프로덕션 배포 이력 관리 |
| `dev` | 다음 배포 기능 통합 (기본 브랜치) |
| `{태그}/{KNK-이슈번호}-{제목}` | 실제 작업 수행 |
| `release/v{버전}` | 배포 전 QA 및 안정화 |

**작업 흐름:**
1. `dev`에서 작업 브랜치 분기
2. 작업 완료 후 `KNK-* → dev` PR 생성 (Squash and Merge)
3. 배포 준비 완료 시 `dev → release/v{버전}` 생성
4. QA 후 `release → main` PR (Merge Commit)
5. release 수정 사항은 반드시 `release → dev`로 역반영 (Rebase and Merge)

**보호 규칙:**
- `main`, `dev`에 직접 Push 금지
- `main`, `dev`, `release/*`에 Force Push 금지

## 적용 사례

```
dev
 ├── feat/KNK-12-add-google-login-button-ui → dev (Squash and Merge)
 └── release/v1.0.0
      ├── fix/KNK-20-fix-login-redirect-error → release (Squash and Merge)
      ├── release → main (Merge Commit)
      └── release → dev (Rebase and Merge)
```

## 관련 컨셉

- [[브랜치-이름-규칙]]
- [[머지-전략]]
- [[커밋-메시지-컨벤션]]
- [[PR-규칙]]

## 관련 엔티티

없음

## 소스

- [[sources/팀-Git-컨벤션]]
