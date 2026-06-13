## 브랜치 전략

우리 팀은 `main`과 `dev`를 기준 브랜치로 사용합니다. 기본 브랜치는 `dev`입니다.

### 브랜치 역할

| 브랜치 | 역할 |
| --- | --- |
| `main` | 프로덕션 배포 이력을 관리하는 브랜치입니다. |
| `dev` | 다음 배포에 포함될 기능을 통합하는 기본 브랜치입니다. |
| `{태그}/{KNK-이슈번호}-{브랜치_제목}` | 기능 개발, 버그 수정, 문서 수정 등 실제 작업을 수행하는 브랜치입니다. |
| `release/v{버전}` | 배포 전 QA와 안정화 작업을 수행하는 브랜치입니다. |

### 작업 흐름

1. 모든 작업 브랜치는 `dev`에서 분기합니다.
2. 작업이 끝나면 `KNK-* → dev` 방향으로 PR을 생성합니다.
3. 기능 브랜치는 `dev`에 **Squash and Merge**로 머지합니다.
    - 기능 브랜치의 오타 수정, 리뷰 반영, 중간 저장 커밋을 하나로 정리하기 위해서입니다.
    - `dev`에는 기능 또는 작업 단위의 커밋만 남깁니다.
4. 배포 후보가 준비되면 `dev`에서 `release/v{버전}` 브랜치를 생성합니다.
5. 배포 준비가 끝나면 `release/v{버전} → main` 방향으로 PR을 생성하고 **Merge Commit**으로 머지합니다.
    - 배포 단위 이력을 명확하게 남기기 위해서입니다.
    - `main`과 배포 브랜치 사이의 그래프 연결을 유지합니다.
6. `release` 또는 `hotfix` 브랜치에서 발생한 수정 사항은 반드시 `dev`에도 반영합니다.
    - `release/v{버전} → dev` 또는 `hotfix/* → dev` 방향으로 PR을 생성합니다.
    - 이때 **Rebase and Merge**를 사용해 불필요한 머지 커밋을 남기지 않습니다.

### 보호 규칙

- `main`과 `dev`에는 직접 Push하지 않습니다.
- `main`과 `dev`의 변경은 반드시 PR로 반영합니다.
- `main`, `dev`, `release/*` 브랜치에는 Force Push하지 않습니다.

## 브랜치 이름 규칙

### 형식

```
{태그}/{KNK-Jira이슈번호}-{브랜치_제목}
```

### 작성 규칙

- 태그와 이슈 사이에는 `/`로 구분합니다.
- 이슈 번호와 태그 사이는 `-`로 구분합니다.
- 브랜치 제목의 단어 사이는 `-`로 구분합니다.
- 브랜치 태그는 소문자로 작성합니다.

### 태그

| 태그 | 사용 기준 |
| --- | --- |
| `feat` | 새로운 기능 추가 |
| `fix` | 버그 수정 |
| `docs` | 문서 수정 |
| `design` | UI, 스타일, 디자인 관련 수정 |
| `cicd` | 배포, CI/CD 설정 수정 |
| `refactor` | 기능 변화 없는 코드 구조 개선 |
| `chore` | 설정, 의존성, 기타 유지보수 작업 |

### 예시

```
feat/KNK-1-member-list_page
```

```
fix/KNK-12-overflow-in-login-page
```

## 커밋 메시지 규칙

### 형식

```
[KNK-{Jira이슈번호}] {태그}: {커밋 제목}

- {커밋 내용}
```

Jira 이슈 번호를 커밋 메시지에 포함하면 해당 이슈와 커밋이 연결됩니다.

### 작성 규칙

- 커밋 제목과 커밋 내용은 한국어로 작성합니다.
- 커밋 제목과 커밋 내용 사이는 한 줄을 띄웁니다.
- 만약 커밋 제목으로만 변경 사항을 표시할 수 있다면, 커밋  내용은 굳이 작성하지 않습니다.

### 태그

| 태그 | 사용 기준 |
| --- | --- |
| `Init` | 프로젝트 초기 생성 |
| `Feat` | 새로운 기능 추가 |
| `Fix` | 버그 수정 |
| `Docs` | 문서 수정 |
| `Design` | UI, 스타일, 디자인 관련 수정 |
| `CICD` | 배포, CI/CD 설정 수정 |
| `Refactor` | 기능 변화 없는 코드 구조 개선 |
| `Chore` | 설정, 의존성, 기타 유지보수 작업 |

### 예시

```
[KNK-1] Init: 프로젝트 생성

- 프로젝트 기본 구조 생성
- 초기 의존성 설정
```

```
[KNK-2] Feat: 로그인 페이지 구현

- 로그인 화면 추가
- 소셜 로그인 버튼 연결
```

## Pull Request 규칙

### 제목 형식

```
[KNK-{Jira이슈번호}] {태그}: {PR 제목}
```

### 작성 규칙

- PR 태그는 커밋 태그와 동일한 표기를 사용합니다.
- PR 본문에는 작업 내용을 구체적으로 작성합니다.
- UI 작업이 포함된 경우 모바일 또는 웹 화면 캡처를 첨부합니다.
- 테스트를 수행했다면 테스트 방법과 결과를 함께 작성합니다.

### 태그

| 태그 | 사용 기준 |
| --- | --- |
| `Feat` | 새로운 기능 추가 |
| `Fix` | 버그 수정 |
| `Docs` | 문서 수정 |
| `Design` | UI, 스타일, 디자인 관련 수정 |
| `CICD` | 배포, CI/CD 설정 수정 |
| `Refactor` | 기능 변화 없는 코드 구조 개선 |
| `Chore` | 설정, 의존성, 기타 유지보수 작업 |
| `Release` | 새로운 버전 배포 |

### 예시

```
[KNK-1] Feat: 멤버 목록 화면 UI 구현
```

```
[KNK-12] Fix: 로그인 페이지 오버플로우 수정
```

```
// release -> main으로 PR할 때
[KNK-45] Release: v1.1.0 배포
```

## Jira 백로그별 브랜치 및 커밋, PR 생성 예시

**[에픽] `KNK-10` 로그인 및 회원가입 시스템 구축**

- **[스토리] `KNK-11` 사용자는 구글 계정으로 가입하고 로그인할 수 있다.**
    - **[서브 태스크] `KNK-12` [FE] 구글 소셜 로그인 버튼 UI 퍼블리싱**
        - Branch: `feat/KNK-12-add-google-login-button_ui`
        - Commit: `[KNK-12] Feat: 구글 소셜 로그인 버튼 컴포넌트 퍼블리싱`
        - PR: `[KNK-12] Feat: 구글 소셜 로그인 버튼 UI 퍼블리싱`
    - **[서브 태스크] `KNK-13` [FE] 구글 로그인 API 연동**
        - Branch: `feat/KNK-13-integrate-google-login-api`
        - Commit: `[KNK-13] Feat: 구글 인가 코드 요청 및 API 통신 로직 구현`
        - PR: `[KNK-13] Feat: 구글 로그인 API 연동`
    - **[서브 태스크] `KNK-14` [BE] 구글 OAuth 검증 API 및 DB 로직 구현**
        - Branch: `feat/KNK-14-implement-google-oauth-api`
        - Commit: `[KNK-14] Feat: 구글 OAuth 토큰 검증 및 JWT 발급 API 추가`
        - PR: `[KNK-14] Feat: 구글 OAuth 검증 API 및 DB 로직 구현`
- **[태스크] `KNK-15` 로그인 관련 DB 인덱싱 및 성능 최적화**
    - **[서브 태스크] `KNK-16` User 테이블 이메일 칼럼 인덱스 추가**
        - Branch: `chore/KNK-16-add-email-index-to-user-table`
        - Commit: `[KNK-16] Chore: User 테이블 이메일 칼럼 인덱스 추가`
        - PR: `[KNK-16] Chore: User 테이블 이메일 칼럼 인덱스 추가`

## 전체 작업 흐름 예시

**목표:** `v1.0.0`에서 로그인 기능을 배포합니다.

### **1. 기능 브랜치 생성**

`KNK-12` 이슈를 처리하기 위해 `dev`에서 기능 브랜치를 생성합니다.

```
dev
└── feat/KNK-12-add-google-login-button-ui
```

### **2. 기능 개발 후 커밋**

기능 브랜치에서 작업을 완료한 뒤 커밋합니다.

```
[KNK-12] Feat: 구글 소셜 로그인 버튼 UI 퍼블리싱
```

### **3. 기능 브랜치를 dev에 머지**

작업이 끝나면 아래 방향으로 PR을 생성합니다.

```
feat/KNK-12-add-google-login-button-ui → dev
```

PR 제목은 아래처럼 작성합니다.

```
[KNK-12] Feat: 구글 소셜 로그인 버튼 UI 퍼블리싱
```

머지 방식은 **Squash and Merge**를 사용합니다.

### **4. 배포 브랜치 생성**

배포할 기능이 모두 `dev`에 모이면 `dev`에서 `release` 브랜치를 생성합니다.

```
dev
└── release/v1.0.0
```

브랜치 이름은 아래처럼 작성합니다.

```
release/v1.0.0
```

### **5. release 브랜치에서 QA 및 수정**

`release/v1.0.0` 브랜치에서 QA를 진행합니다.

QA 중 `KNK-20` 이슈가 발견되었다면 `release/v1.0.0`에서 수정 브랜치를 생성합니다.

```
release/v1.0.0
└── fix/KNK-20-fix-login-redirect-error
```

수정 커밋은 아래처럼 작성합니다.

```
[KNK-20] Fix: 로그인 성공 후 리다이렉트 오류 수정
```

수정이 끝나면 아래 방향으로 PR을 생성합니다.

```
fix/KNK-20-fix-login-redirect-error → release/v1.0.0
```

PR 제목은 아래처럼 작성합니다.

```
[KNK-20] Fix: 로그인 성공 후 리다이렉트 오류 수정
```

머지 방식은 **Squash and Merge**를 사용합니다.

### **6. release 브랜치를 main에 머지**

QA가 끝나고 배포 준비가 완료되면 아래 방향으로 PR을 생성합니다.

```
release/v1.0.0 → main
```

PR 제목은 아래처럼 작성합니다.

```
[KNK-30] Release: v1.0.0 배포
```

머지 방식은 **Merge Commit**을 사용합니다.

### **7. release 수정 사항을 dev에 반영**

`release/v1.0.0`에서 QA 수정이 발생했으므로 해당 수정 사항을 `dev`에도 반영해야 합니다.

아래 방향으로 PR을 생성합니다.

```
release/v1.0.0 → dev
```

PR 제목은 아래처럼 작성합니다.

```
[KNK-30] Release: v1.0.0 QA 수정 사항 dev 반영
```

머지 방식은 **Rebase and Merge**를 사용합니다.

이 단계가 끝나면 `main`과 `dev` 모두 `v1.0.0` 배포 수정 사항을 포함합니다.

## 흐름 요약

```
dev
 ├── feat/KNK-12-add-google-login-button-ui
 │    └── PR: [KNK-12] 구글 로그인 버튼 UI 구현
 │        └── Squash and Merge
 │
 ├── feat/KNK-13-integrate-google-login-api
 │    └── PR: [KNK-13] 구글 로그인 API 연동
 │        └── Squash and Merge
 │
 └── release/v1.0.0
      ├── fix/KNK-20-fix-login-redirect-error
      │    └── PR: [KNK-20] 로그인 리다이렉트 에러 수정
      │        └── Squash and Merge
      │
      ├── PR: [KNK-30] Release: v1.0.0 배포 → main
      │   └── Merge Commit
      │
      └── PR: [KNK-30] Release: v1.0.0 QA 수정 사항 dev 반영 → dev
          └── Rebase and Merge
```

핵심은 이렇습니다.

```
기능 개발: dev → feature → dev
배포 준비: dev → release
배포 반영: release → main
QA 수정 동기화: release → dev
```