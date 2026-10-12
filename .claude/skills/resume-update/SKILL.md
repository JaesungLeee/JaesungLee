---
name: resume-update
description: Google Drive의 경력기술서(…_경력기술서_v.X.Y) 최신 버전을 복사해 새 버전 문서로 저장하고 수정 사항을 반영한다. 새 프로젝트·경력 추가, resume-reviewer 제안 반영, 오타·표현 수정 요청에 사용한다. 버전은 major/patch 규칙으로 정하고, 저장 전에 항상 사용자 확인을 받는다.
---

# resume-update

경력기술서의 새 버전을 만든다. **이전 버전 문서는 절대 수정하지 않는다.** 항상 최신 버전을 복사한 새 문서에만 쓴다.

## 입력

다음 중 하나 이상을 받는다.

- 새 항목 정보: Career, Work Experience, Personal Project 등에 추가할 내용. 메모 수준이어도 된다.
- 리뷰 제안 번호: 예) "1, 3, 5번 반영". `docs/resume/private/reviews/`의 가장 최근 리뷰(또는 지정한 리뷰 파일)에서 찾는다.
- 직접 수정 요청: 예) "Introduce 두 번째 문단 다듬어줘", "오타 고쳐줘"

## 개인 설정 불러오기 (항상 먼저)

1. `docs/resume/private/profile.md`를 Read로 읽어 **파일명 접두어**, **Drive 폴더 id**, **버전 관리 제외 파일**을 가져온다. 아래에서 `{파일명 접두어}`, `{폴더 id}`는 이 값을 뜻한다.
2. 파일이 없으면 여기서 멈춘다. `docs/resume/private.example/`를 `docs/resume/private/`로 복사해 값을 채우라고 안내한다.
3. `docs/resume/private/`는 gitignore되어 있다. Glob/Grep 검색에 안 잡힐 수 있으니 항상 정확한 경로로 Read한다.

## 참고 문서

- `docs/resume/style-guide.md`: 새 항목을 쓸 때 따르는 형식 규칙과 섹션별 템플릿
- `docs/resume/private/examples.md`: 섹션별 **복제 기준 항목**, 형식 현황
- `docs/resume/review-criteria.md`: 지킬 것, 제안 작성 규칙 (수치를 지어내지 않는다)
- `docs/resume/private/CHANGELOG.md`: 버전 이력과 문서 링크
- `docs/resume/versioning.md`: 파일명 형식과 버전 규칙

## 버전 규칙

새 버전을 정하기 전에 [versioning.md](../../../docs/resume/versioning.md)를 Read로 읽고 그 규칙(파일명 형식, major/patch 기준, 리뷰 제안의 "버전 영향" 열)을 따른다.

## 절차

### 1. 사전 확인 (문서를 건드리기 전에)

1. **Google Docs 편집 커넥터**가 있는지 확인한다. 도구 검색으로 `google docs`를 찾고, 문서 본문을 읽고 편집하는 도구(예: `read_doc`, `update_doc`)가 있어야 한다. Drive 커넥터만으로는 본문을 고칠 수 없다.
   - 없으면 여기서 멈춘다. claude.ai → Settings → Connectors에서 Google Docs를 연결하거나 이 채팅에서 켜 달라고 안내한다. 수정안 초안만 먼저 보고 싶은지 물어볼 수는 있지만, **새 문서는 만들지 않는다.**
2. `anthropic-skills:google-workspace` 스킬과 그 안의 `references/docs.md`를 읽는다. 위치 계산, `requiredRevisionId`, 검증 방법은 그 문서를 따른다.

### 2. 최신 버전 찾기

resume-reviewer의 "대상 문서 찾기"와 같은 방법을 쓴다.

- 폴더: `parentId = '{폴더 id}'`
- `title contains '{파일명 접두어}'`, `_v.(\d+).(\d+)`를 숫자로 비교해 가장 높은 버전을 고른다.
- `private/CHANGELOG.md`의 최신 버전과 다르면 사용자에게 알린다. 예: Drive에서 손으로 만든 버전이 있는 경우

### 3. 읽고 수정안 작성

1. `read_file_content`로 최신 버전을 읽고, 바꿀 섹션과 그 주변 항목을 파악한다.
2. 수정안을 작성한다.
   - 새 항목: `style-guide.md`의 섹션 템플릿과 **같은 섹션의 바로 옆 항목**을 기준으로 쓴다. 제목 서식, 날짜 표기, bullet 수, 문장 끝 처리를 맞춘다.
   - 넣을 위치: 섹션 안의 정렬 규칙(최신순 등)을 따른다.
   - Career에 회사를 추가하면 Work Experience에도 대응 항목이 있는지 확인한다. 없으면 사용자에게 물어본다.
   - 모르는 수치나 사실은 지어내지 않는다. `[확인 필요: ...]`로 남기고 사용자에게 묻는다.
3. 수정안에 `[확인 필요]`가 남아 있으면 사용자 답을 받기 전에는 다음 단계로 가지 않는다.

### 4. 자동 검수

resume-reviewer를 **자동 검수 모드로 서브에이전트에서** 실행한다. 수정안을 쓴 맥락 없이 봐야 하므로 이 대화에서 직접 평가하지 않는다.

- 서브에이전트에게 넘길 것: 수정안 텍스트, 바뀌는 섹션의 기존 원문, 최신 버전 파일 id, `review-criteria.md`·`style-guide.md`·`private/examples.md` 경로
- 심각도 높음 제안이 나오면 수정안에 반영하거나, 반영하지 않는 이유를 사용자 확인 단계에서 함께 보여 준다.

### 5. 사용자 확인 (항상)

**문서를 복사하기 전에 반드시 확인을 받는다.** 판단이 명확해 보여도 생략하지 않는다. 다음을 한 번에 보여 준다.

```markdown
## 저장 전 확인
- 기준 문서: {파일명 접두어}2.1
- 새 문서: {파일명 접두어}3.0 (major: Work Experience에 새 항목 추가)

## 변경 내용
| # | 섹션 | 구분 | 현재 | 변경 후 |
|---|------|------|------|--------|
| 1 | Work Experience > OO사 | 추가 | - | (새 항목 전문) |
| 2 | Introduce | 수정 | "..." | "..." |

## 자동 검수 결과
- 수정 제안 없음 / 또는 반영한 것·반영하지 않은 것과 이유
```

- 사용자가 명시적으로 승인해야 진행한다. 수정을 요청하면 3단계로 돌아간다.
- 사용자가 버전을 바꾸라고 하면 그 버전을 따른다.

### 6. 복사하고 반영

1. Drive `copy_file`로 최신 버전을 복사한다. `title`은 새 파일명, `parentId`는 `{폴더 id}`로 준다.
2. Google Docs 편집 커넥터로 **복사본**을 읽고 수정한다. 원본 문서 id에는 쓰지 않는다.
   - 서식이 틀어지지 않도록 같은 섹션의 기존 항목(`private/examples.md`의 복제 기준 항목) 구조(제목 스타일, bullet, 들여쓰기, 표 셀)를 복제한 뒤 텍스트만 바꾼다.
   - 쓰기마다 `requiredRevisionId`를 붙인다 (google-workspace 스킬 규칙).
3. 복사본을 다시 읽어 변경 내용이 맞게 들어갔는지, 다른 부분이 바뀌지 않았는지 확인한다.
4. 반영 중 실패하면 복사본을 휴지통으로 보내지 않는다. 어디까지 반영됐는지 사용자에게 알리고 이어서 할지 묻는다.

### 7. 기록

1. `docs/resume/private/CHANGELOG.md` 맨 위에 새 버전 항목을 추가한다 (파일 안의 형식을 따른다).
2. 리뷰 제안을 반영했으면 해당 리뷰 파일의 제안 표 아래에 `반영: #1, #3 → v.X.Y` 줄을 추가한다.
3. 새 문서를 링크로 걸어 결과를 알린다.
