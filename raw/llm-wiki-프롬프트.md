# LLM Wiki 환경 셋업 프롬프트

> 이 파일을 빈 디렉토리에서 Claude Code에 붙여넣으면 LLM Wiki 환경이 자동으로 구축됩니다.

---

## 사용법

1. 새 디렉토리(또는 빈 레포)에서 Claude Code를 실행한다
2. 이 파일의 내용 전체를 첫 번째 메시지로 붙여넣는다
3. Claude Code가 모든 파일을 자동으로 생성한다
4. `raw/` 폴더에 소스 파일을 넣고 `/ingest`로 시작한다

---

## 셋업 지시 (Claude Code에게)

아래 지시에 따라 현재 디렉토리에 LLM Wiki 환경을 구축해주세요.
**모든 파일을 실제로 생성**해야 합니다. 설명만 하지 말고 Write 도구로 파일을 만드세요.

### 1단계 — 디렉토리 구조 생성

다음 디렉토리와 파일을 생성합니다:

```
CLAUDE.md
index.md
log.md
raw/
raw/assets/
wiki/
wiki/overview.md
wiki/entities/
wiki/concepts/
wiki/sources/
wiki/answers/
.claude/
.claude/commands/
.claude/commands/ingest.md
.claude/commands/query.md
.claude/commands/lint.md
.claude/commands/file-answer.md
```

빈 디렉토리는 `.gitkeep` 파일로 자리를 잡아줍니다.

---

### 2단계 — CLAUDE.md 생성

`CLAUDE.md`를 아래 내용으로 생성합니다:

```markdown
# LLM Wiki — 팀 지식 베이스

## 개요

이 볼트는 Andrej Karpathy의 LLM Wiki 패턴을 팀 환경에 적용한 지식 베이스입니다.
RAG와 달리 소스를 인제스트 시점에 한 번 정리해두고, 이후 쿼리는 이미 구조화된 위키 위에서 실행합니다.
**LLM(Claude Code)이 위키를 작성·유지하고, 팀원은 소스 수집과 질문에 집중합니다.**

---

## 볼트 구조

​```
vault/
├── CLAUDE.md          ← 이 파일 (스키마 & 행동 규칙)
├── index.md           ← 전체 페이지 카탈로그 (자동 갱신)
├── log.md             ← 작업 이력 append-only (자동 갱신)
├── raw/               ← 원본 소스 (읽기 전용, 절대 수정 금지)
│   └── assets/        ← 첨부 이미지·파일
└── wiki/
    ├── overview.md    ← 위키 전체 요약 (자동 갱신)
    ├── entities/      ← 기업, 인물, 기술, 제품 페이지
    ├── concepts/      ← 개념, 패턴, 프레임워크, 방법론 페이지
    ├── sources/       ← 소스별 요약 페이지
    └── answers/       ← /file-answer로 저장된 답변 페이지
​```

---

## 페이지 포맷 규칙

### 모든 위키 페이지 공통 frontmatter

​```yaml
---
title: "페이지 제목"
type: entity | concept | source | answer
team: frontend | backend | ai | cross
tags: [entity/company, concept/pattern]
sources: [소스파일명1.md, 소스파일명2.md]
created: YYYY-MM-DD
updated: YYYY-MM-DD
confidence: high | medium | low
---
​```

`team` 필드 규칙:
- 특정 팀에만 해당하면 `frontend` / `backend` / `ai` 중 하나
- 두 팀 이상에 걸치면 `cross`
- 팀 구분이 모호하면 가장 관련 높은 팀으로 지정

### 엔티티 페이지 (wiki/entities/)

대상: 기업, 인물, 기술, 제품, 서비스처럼 고유 명사로 지칭되는 대상

구성 섹션:
1. **개요** — 한 문단 설명
2. **핵심 특징** — 3~5개 불릿
3. **관련 컨셉** — `[[컨셉명]]` 위키링크 목록
4. **관련 엔티티** — `[[엔티티명]]` 위키링크 목록
5. **소스** — 이 페이지 근거가 된 raw 소스 링크

### 컨셉 페이지 (wiki/concepts/)

대상: 개념, 프레임워크, 패턴, 방법론, 트렌드처럼 추상적 아이디어

구성 섹션:
1. **정의** — 한 문단 핵심 설명
2. **작동 원리** — 메커니즘 또는 구성 요소
3. **적용 사례** — 실제 사례 또는 예시
4. **관련 컨셉** — `[[컨셉명]]` 위키링크
5. **관련 엔티티** — `[[엔티티명]]` 위키링크
6. **소스** — 근거 소스 링크

### 소스 요약 페이지 (wiki/sources/)

구성 섹션:
1. **원본 링크** — `[[raw/파일명]]`
2. **한줄 요약** — 핵심 주장 한 문장
3. **핵심 내용** — 3~7개 불릿
4. **추출된 엔티티** — 이 소스에서 언급된 엔티티 링크
5. **추출된 컨셉** — 이 소스에서 언급된 컨셉 링크
6. **주목할 인사이트** — 다른 소스와 차별되는 독특한 관점
7. **신뢰도** — high / medium / low + 근거

### 답변 페이지 (wiki/answers/)

구성 섹션:
1. **질문** — 원래 질문 텍스트
2. **답변 요약** — 핵심 결론 한 문단
3. **상세 답변** — 근거와 함께 서술
4. **참조 페이지** — 답변에 사용된 위키 페이지 링크
5. **신뢰도** — high / medium / low + 이유
6. **후속 질문** — 이 답변에서 파생되는 탐구 질문 2~3개

---

## 분류 체계

### 엔티티 태그

- `entity/company` — 기업, 스타트업, 조직
- `entity/person` — 인물, 연구자, 경영자
- `entity/technology` — 기술, 플랫폼, 인프라
- `entity/product` — 제품, 서비스, 솔루션

### 컨셉 태그

- `concept/framework` — 프레임워크, 방법론
- `concept/pattern` — 패턴, 아키텍처
- `concept/trend` — 트렌드, 시장 동향
- `concept/research` — 연구 주제, 학술 개념
- `concept/spec` — 기술 스펙, 설계 문서
- `concept/issue` — 버그, 장애, 트러블슈팅 사례

### 기술 스택 태그 (소스 분류 보조용)

프론트엔드:
- `stack/react` `stack/nextjs` `stack/typescript` `stack/css`

백엔드:
- `stack/node` `stack/python` `stack/database` `stack/api` `stack/infra`

AI:
- `stack/llm` `stack/rag` `stack/prompt` `stack/vector-db` `stack/finetuning`

---

## 커맨드 정의

### /ingest [파일경로 또는 "all"]

**목적**: raw 폴더의 소스를 위키 페이지로 변환

**실행 순서**:
1. 지정된 파일(또는 raw/ 전체)을 읽는다
2. 소스 유형을 파악한다 (리포트, 기사, 회의록, 논문 등)
3. `wiki/sources/[파일명].md` 소스 요약 페이지를 생성한다
4. 소스에서 엔티티를 추출한다
   - 기존 엔티티 페이지가 있으면 업데이트하고 새 소스를 sources 목록에 추가한다
   - 없으면 새 엔티티 페이지를 생성한다
5. 소스에서 컨셉을 추출한다
   - 기존 컨셉 페이지가 있으면 업데이트한다
   - 없으면 새 컨셉 페이지를 생성한다
6. 모든 페이지 간 `[[위키링크]]`를 설정한다
7. `index.md`를 갱신한다 (새 페이지 추가, one-line 요약 포함)
8. `log.md`에 다음 형식으로 기록한다:
   `## [YYYY-MM-DD] ingest | 파일명 | 생성 N페이지, 업데이트 M페이지`
9. 작업 결과를 요약 보고한다 (생성/업데이트 페이지 목록)

**규칙**:
- raw 파일은 절대 수정하지 않는다
- 소스에 명시되지 않은 내용은 위키에 추가하지 않는다
- 불확실한 내용은 confidence: low로 표기하고 `> ⚠️ 불확실: 추가 검증 필요` 블록을 삽입한다

---

### /query [질문]

**목적**: 위키 전체를 검색해 출처 기반 종합 답변 생성

**실행 순서**:
1. `index.md`를 읽어 관련 페이지 후보를 파악한다
2. 관련 페이지들을 읽는다 (entities/, concepts/, sources/ 모두 탐색)
3. 페이지 간 교차 참조를 따라가며 추가 컨텍스트를 수집한다
4. 수집된 내용을 바탕으로 답변을 합성한다
5. 다음 형식으로 답변을 출력한다:

​```markdown
## 답변

[종합 답변 본문]

## 근거

- [[참조 페이지 1]] — 인용 내용 요약
- [[참조 페이지 2]] — 인용 내용 요약

## 신뢰도: high | medium | low

[신뢰도 판단 이유]

## 후속 탐구 질문

1. ...
2. ...
​```

6. 답변 후 `/file-answer`로 저장할지 물어본다

**규칙**:
- 위키에 없는 내용은 "위키에 해당 정보가 없습니다"라고 명시한다
- 추측하지 않는다. 근거 없는 내용은 포함하지 않는다

---

### /file-answer [선택: 제목]

**목적**: 가장 최근 /query 결과를 위키 답변 페이지로 저장

**실행 순서**:
1. 직전 /query 답변을 답변 페이지 포맷으로 변환한다
2. 제목이 없으면 질문에서 자동 생성한다
3. `wiki/answers/YYYY-MM-DD-[제목].md`로 저장한다
4. 답변에서 언급된 엔티티·컨셉 페이지에 이 답변 페이지 역참조를 추가한다
5. `index.md`를 갱신한다
6. `log.md`에 기록한다:
   `## [YYYY-MM-DD] answer | 제목 | 참조 N페이지`

---

### /lint

**목적**: 위키 전체의 품질 문제를 탐지하고 보고

**점검 항목**:
1. **고아 페이지** — 아무 페이지에서도 링크되지 않는 페이지
2. **깨진 링크** — 존재하지 않는 페이지를 가리키는 `[[링크]]`
3. **frontmatter 오류** — 필수 필드 누락, 잘못된 값
4. **소스 간 모순** — 동일 주제에 대해 상충되는 내용
5. **빈 섹션** — 구조는 있지만 내용이 없는 섹션
6. **링크 누락** — 본문에서 언급되지만 링크가 없는 엔티티·컨셉
7. **오래된 페이지** — 신규 소스 인제스트 후 업데이트되지 않은 관련 페이지

**출력 형식**:
​```markdown
## /lint 결과 — YYYY-MM-DD

### 🔴 즉시 수정 필요
- ...

### 🟡 검토 권장
- ...

### 🟢 개선 제안
- ...

### 통계
- 총 페이지: N
- 고아 페이지: N
- 깨진 링크: N
- 모순 감지: N
​```

수정할 항목을 확인 후 자동 수정할지 묻는다.

---

## index.md 형식

​```markdown
# Wiki Index

> 마지막 갱신: YYYY-MM-DD | 총 N페이지

## 엔티티 (N)
| 페이지 | 유형 | 요약 | 소스 수 |
|--------|------|------|---------|
| [[엔티티명]] | company | 한줄 설명 | 3 |

## 컨셉 (N)
| 페이지 | 태그 | 요약 | 소스 수 |
|--------|------|------|---------|
| [[컨셉명]] | concept/framework | 한줄 설명 | 5 |

## 소스 요약 (N)
| 페이지 | 날짜 | 한줄 요약 |
|--------|------|---------|
| [[sources/파일명]] | YYYY-MM-DD | 한줄 설명 |

## 답변 (N)
| 페이지 | 날짜 | 질문 요약 |
|--------|------|---------|
| [[answers/파일명]] | YYYY-MM-DD | 질문 요약 |
​```

---

## log.md 형식

​```markdown
# Wiki Log

## [YYYY-MM-DD] ingest | 파일명 | 생성 N페이지, 업데이트 M페이지
## [YYYY-MM-DD] query | 질문 요약 | 참조 N페이지
## [YYYY-MM-DD] answer | 답변 제목 | 저장 경로
## [YYYY-MM-DD] lint | 발견 N건 | 수정 M건
​```

---

## 행동 원칙

1. **원본 불변** — raw/ 파일은 읽기만 한다
2. **출처 기반** — 소스에 없는 내용은 위키에 쓰지 않는다
3. **링크 우선** — 새 페이지 생성 시 기존 페이지와 반드시 교차 링크한다
4. **confidence 표기** — 불확실하면 낮은 신뢰도를 명시한다
5. **index·log 항상 갱신** — 어떤 커맨드든 실행 후 두 파일을 업데이트한다
6. **팀 스키마 우선** — 이 CLAUDE.md의 규칙이 일반 동작보다 우선한다
```

---

### 3단계 — index.md 생성

`index.md`를 아래 내용으로 생성합니다:

```markdown
# Wiki Index

> 마지막 갱신: YYYY-MM-DD | 총 0페이지
> 운영 가이드: [[CLAUDE]]

## 엔티티 (0)

아직 추출된 엔티티가 없습니다.

## 컨셉 (0)

아직 추출된 컨셉이 없습니다.

## 소스 요약 (0)

아직 인제스트된 소스가 없습니다. `raw/` 폴더에 파일을 넣고 `/ingest`를 실행하세요.

## 답변 (0)

아직 저장된 답변이 없습니다. `/query [질문]` 후 `/file-answer`로 저장하세요.
```

`YYYY-MM-DD`는 오늘 날짜로 치환합니다.

---

### 4단계 — log.md 생성

`log.md`를 아래 내용으로 생성합니다:

```markdown
# Wiki Log

> append-only 이력 파일. 수동 수정 금지.

## [YYYY-MM-DD] init | 위키 환경 초기화 완료
```

`YYYY-MM-DD`는 오늘 날짜로 치환합니다.

---

### 5단계 — wiki/overview.md 생성

`wiki/overview.md`를 아래 내용으로 생성합니다:

```markdown
# Wiki Overview

> 마지막 갱신: YYYY-MM-DD
> 이 페이지는 `/ingest` 실행 시 자동으로 업데이트됩니다.

## 위키 현황

- 총 소스: 0개
- 추출된 엔티티: 0개
- 추출된 컨셉: 0개
- 저장된 답변: 0개

## 핵심 주제

아직 인제스트된 소스가 없습니다.

## 주요 엔티티

없음

## 주요 컨셉

없음

## 최근 인사이트

없음
```

`YYYY-MM-DD`는 오늘 날짜로 치환합니다.

---

### 6단계 — 커스텀 슬래시 명령어 생성

`.claude/commands/ingest.md`를 아래 내용으로 생성합니다:

```markdown
CLAUDE.md의 /ingest 커맨드 정의에 따라 다음을 실행하세요.

대상: $ARGUMENTS

실행 순서:
1. 지정된 파일(또는 raw/ 전체)을 읽는다
2. 소스 유형을 파악한다 (리포트, 기사, 회의록, 논문 등)
3. `wiki/sources/[파일명].md` 소스 요약 페이지를 생성한다
4. 소스에서 엔티티를 추출한다
   - 기존 엔티티 페이지가 있으면 업데이트하고 새 소스를 sources 목록에 추가한다
   - 없으면 새 엔티티 페이지를 생성한다
5. 소스에서 컨셉을 추출한다
   - 기존 컨셉 페이지가 있으면 업데이트한다
   - 없으면 새 컨셉 페이지를 생성한다
6. 모든 페이지 간 `[[위키링크]]`를 설정한다
7. `index.md`를 갱신한다 (새 페이지 추가, one-line 요약 포함)
8. `log.md`에 다음 형식으로 기록한다:
   `## [YYYY-MM-DD] ingest | 파일명 | 생성 N페이지, 업데이트 M페이지`
9. 작업 결과를 요약 보고한다 (생성/업데이트 페이지 목록)

규칙:
- raw 파일은 절대 수정하지 않는다
- 소스에 명시되지 않은 내용은 위키에 추가하지 않는다
- 불확실한 내용은 confidence: low로 표기하고 `> ⚠️ 불확실: 추가 검증 필요` 블록을 삽입한다
- 페이지 포맷과 frontmatter는 CLAUDE.md의 규칙을 따른다
```

`.claude/commands/query.md`를 아래 내용으로 생성합니다:

```markdown
CLAUDE.md의 /query 커맨드 정의에 따라 다음 질문에 답하세요.

질문: $ARGUMENTS

실행 순서:
1. `index.md`를 읽어 관련 페이지 후보를 파악한다
2. 관련 페이지들을 읽는다 (entities/, concepts/, sources/ 모두 탐색)
3. 페이지 간 교차 참조를 따라가며 추가 컨텍스트를 수집한다
4. 수집된 내용을 바탕으로 답변을 합성한다
5. 다음 형식으로 답변을 출력한다:

## 답변
[종합 답변 본문]

## 근거
- [[참조 페이지 1]] — 인용 내용 요약

## 신뢰도: high | medium | low
[신뢰도 판단 이유]

## 후속 탐구 질문
1. ...
2. ...

6. 답변 후 `/file-answer`로 저장할지 물어본다

규칙:
- 위키에 없는 내용은 "위키에 해당 정보가 없습니다"라고 명시한다
- 추측하지 않는다. 근거 없는 내용은 포함하지 않는다
- log.md에 `## [YYYY-MM-DD] query | 질문 요약 | 참조 N페이지` 형식으로 기록한다
```

`.claude/commands/lint.md`를 아래 내용으로 생성합니다:

```markdown
CLAUDE.md의 /lint 커맨드 정의에 따라 위키 전체 품질 점검을 실행하세요.

점검 항목:
1. **고아 페이지** — 아무 페이지에서도 링크되지 않는 페이지
2. **깨진 링크** — 존재하지 않는 페이지를 가리키는 `[[링크]]`
3. **frontmatter 오류** — 필수 필드 누락, 잘못된 값
4. **소스 간 모순** — 동일 주제에 대해 상충되는 내용
5. **빈 섹션** — 구조는 있지만 내용이 없는 섹션
6. **링크 누락** — 본문에서 언급되지만 링크가 없는 엔티티·컨셉
7. **오래된 페이지** — 신규 소스 인제스트 후 업데이트되지 않은 관련 페이지

점검 완료 후 수정할 항목을 확인하고, 자동 수정할지 사용자에게 물어본다.
log.md에 `## [YYYY-MM-DD] lint | 발견 N건 | 수정 M건` 형식으로 기록한다.
```

`.claude/commands/file-answer.md`를 아래 내용으로 생성합니다:

```markdown
CLAUDE.md의 /file-answer 커맨드 정의에 따라 가장 최근 /query 결과를 답변 페이지로 저장하세요.

제목 (선택): $ARGUMENTS

실행 순서:
1. 직전 /query 답변을 답변 페이지 포맷으로 변환한다
2. 제목이 없으면 질문에서 자동 생성한다
3. `wiki/answers/YYYY-MM-DD-[제목].md`로 저장한다 (오늘 날짜 사용)
4. 답변에서 언급된 엔티티·컨셉 페이지에 이 답변 페이지 역참조를 추가한다
5. `index.md`를 갱신한다
6. `log.md`에 기록한다:
   `## [YYYY-MM-DD] answer | 제목 | 참조 N페이지`
```

---

### 7단계 — 빈 디렉토리 자리 잡기

`raw/assets/.gitkeep`, `wiki/entities/.gitkeep`, `wiki/concepts/.gitkeep`, `wiki/sources/.gitkeep`, `wiki/answers/.gitkeep`을 빈 파일로 생성합니다.

---

### 8단계 — Obsidian Git 플러그인 설정

`.obsidian/plugins/obsidian-git/data.json`을 아래 내용으로 생성합니다:

```json
{
  "commitMessage": "Chore: vault backup {{date}}",
  "autoCommitMessage": "Chore: vault backup {{date}}",
  "commitMessageScript": "",
  "commitDateFormat": "YYYY-MM-DD HH:mm:ss",
  "autoSaveInterval": 5,
  "autoPushInterval": 10,
  "autoPullInterval": 10,
  "autoPullOnBoot": true,
  "autoCommitOnlyStaged": false,
  "disablePush": false,
  "pullBeforePush": true,
  "disablePopups": false,
  "showErrorNotices": true,
  "disablePopupsForNoChanges": false,
  "listChangedFilesInMessageBody": false,
  "showStatusBar": true,
  "updateSubmodules": false,
  "syncMethod": "merge",
  "mergeStrategy": "none",
  "customMessageOnAutoBackup": false,
  "autoBackupAfterFileChange": false,
  "treeStructure": false,
  "refreshSourceControl": true,
  "basePath": "",
  "differentIntervalCommitAndPush": false,
  "changedFilesInStatusBar": false,
  "showBranchStatusBar": true,
  "setLastSaveToLastCommit": false,
  "submoduleRecurseCheckout": false,
  "gitDir": "",
  "showFileMenu": true,
  "authorInHistoryView": "hide",
  "dateInHistoryView": false,
  "diffStyle": "split"
}
```

설정 값 요약:
- `autoSaveInterval: 5` — 5분마다 자동 커밋
- `autoPushInterval: 10` — 10분마다 자동 push
- `autoPullInterval: 10` — 10분마다 자동 pull
- `autoPullOnBoot: true` — Obsidian 실행 시 자동 pull
- `pullBeforePush: true` — push 전 pull 먼저 실행

> ⚠️ 플러그인 코드(main.js)는 이 설정으로 자동 설치되지 않습니다.
> Obsidian 앱에서 설정 → 커뮤니티 플러그인 → **Obsidian Git** 을 직접 설치해야 합니다.
> 설치 후 위 data.json 설정이 자동으로 적용됩니다.

---

### 9단계 — 완료 보고

모든 파일 생성 후 다음을 출력합니다:

```
LLM Wiki 환경 셋업 완료

생성된 파일:
- CLAUDE.md
- index.md
- log.md
- wiki/overview.md
- wiki/entities/.gitkeep
- wiki/concepts/.gitkeep
- wiki/sources/.gitkeep
- wiki/answers/.gitkeep
- raw/assets/.gitkeep
- .claude/commands/ingest.md
- .claude/commands/query.md
- .claude/commands/lint.md
- .claude/commands/file-answer.md
- .obsidian/plugins/obsidian-git/data.json

다음 단계:
1. Obsidian 앱에서 커뮤니티 플러그인 → Obsidian Git 설치 (자동 커밋·push·pull 활성화)
2. raw/ 폴더에 정리할 소스 파일(md, txt, pdf 등)을 넣는다
3. /ingest [파일명] 으로 위키 페이지를 자동 생성한다
4. /query [질문] 으로 위키를 검색한다
5. /lint 로 위키 품질을 점검한다
```
