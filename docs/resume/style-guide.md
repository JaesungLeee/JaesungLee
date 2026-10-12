# 경력기술서 작성 규칙

- 작성일: 2026-10-12
- 기준 문서: v.2.1
- 사용처: resume-update (새 항목 작성), resume-reviewer (형식 확인)

이 문서는 **어떻게 쓰는지(형식)**만 다룬다. 무엇이 좋은지(평가 기준)는 [review-criteria.md](review-criteria.md)에 있다. 새 항목을 쓸 때는 이 문서의 템플릿과 같은 섹션의 바로 옆 항목을 함께 본다.

규칙은 v.2.1에서 가장 많이 쓰인 형식을 기준으로 정했다. v.2.1 안에서도 형식이 섞인 곳("형식 현황")과 스타일을 복제할 기준 항목은 개인정보라서 `private/examples.md`에 따로 둔다 (git에 올라가지 않는다). 새 항목은 규칙을 따르고, 섞인 부분을 통일하는 일은 리뷰 제안으로 다룬다.

## 공통

| 항목 | 규칙 |
|---|---|
| 문장 끝 처리 | Introduce는 합니다체. 나머지 섹션의 제목과 bullet은 명사형 종결 ("~구현", "~개선", "~단축") |
| 날짜 | `YYYY.MM` (점 뒤 공백 없음) |
| 기간 | `YYYY.MM ~ YYYY.MM`, 진행 중이면 `YYYY.MM ~ 진행 중` |
| 기간 부가 정보 | 기간 뒤 괄호. Career는 총 기간 `(약 1년 7개월)`, Personal Project는 형태 `(개인 프로젝트)` / `(팀 프로젝트)` |
| 제목과 기간 사이 | 공백 4칸 |
| 근거 링크 (기사·블로그·스토어) | 문장 끝에 굵은 `(링크)` 하이퍼링크 |
| 저장소 링크 | `[Github]`, `[Pull Request]` 하이퍼링크. 둘 다 있으면 ` / `로 구분 |
| 발표·영상 링크 | 제목 텍스트 자체에 하이퍼링크 (예: "{발표 제목}에 대한 발표") |
| 기술명 | 공식 표기를 영문 그대로 (`Jetpack Compose`, `Kotlin`, `Coroutine`, `DataDog`, `Github`). 한글 음차 금지 |
| 수치 | 개선 전후를 함께 적을 때는 `약 N% (A → B)`처럼 비율 뒤 괄호에 `→` |
| 강조 | 핵심 성과 구절에만 밑줄 (예: <u>가입자 약 N% 증가</u>). 항목당 1개 이내 |
| 나열 | 쉼표 뒤 한 칸 띄운다 |

## 섹션별 형식

### 헤더

- 2열 표. 왼쪽 열은 이름(TITLE), 헤드라인 1줄(굵게), 빈 줄, 링크 4줄. 오른쪽 열은 생년월일, 이메일, 전화번호
- 링크 줄 형식: `서비스명 - 표시텍스트` (표시텍스트에 하이퍼링크, URL 프로토콜은 빼고 `github.com/...` 형태로)

### Introduce

- 3문단 서술형, 합니다체. bullet 없음
- 문단 주제: ① 도메인·기술 ② 일하는 방식 ③ 협업
- 문단당 2~3문장

### Career

- 정렬: 최신 회사가 위
- 회사 사이: 빈 줄 1개
- 새 항목 템플릿

```
{회사명}    {YYYY.MM} ~ {YYYY.MM} ({총 기간})
{조직} | {조직} | {직무} (총 {N}명)
{서비스 설명} “{서비스명}” {한 일 요약} (링크)
  ● {무엇을} + {결과 키워드} (명사형, 한 줄)
  ● ... (3~5개)
```

- bullet마다 Work Experience에 대응하는 항목이 있어야 한다.

### Work Experience

- 정렬: 회사는 최신순. 회사 안 항목은 비즈니스 임팩트가 큰 순서
- 레이아웃: 회사마다 1행 2열 표 하나. 왼쪽 열은 회사명, 오른쪽 열은 항목들
- 항목 사이: 빈 줄 1개
- 오른쪽 열 첫 줄은 회사 전체 업무 한 줄 요약
- 새 항목 템플릿 (유형별 필수 요소는 review-criteria.md의 Work Experience 표를 따른다)

```
{항목 제목 (명사형)}
  ● {상황·문제}
  ● {원인 분석 또는 기법}
  ● {해결·대응}
  ● {결과, 핵심 수치는 밑줄}
```

- 날짜별 하위 항목이 필요하면 1단계 bullet을 굵은 `YYYY.MM {하위 제목}`으로 쓰고, 내용은 2단계 bullet(○)으로 쓴다. 예: 연도별 정책 대응
- 하위 bullet은 2단계까지만 쓴다.

### Personal Project

- 정렬: 최신 프로젝트가 위
- 새 항목 템플릿

```
{한글명} ({영문명})    {YYYY.MM} ~ {YYYY.MM} ({개인 프로젝트 | 팀 프로젝트})   [Github]
{한 줄 소개}
{직군} {N}명, 기여도 {N}% ({측정 기준})        ← 팀 프로젝트만
  ● {기술 성과} (2~4개, 핵심 수치는 밑줄)
```

### Activity

- 정렬: 최신순
- 형식: `{단체·활동명}    {YYYY.MM} ~ {YYYY.MM}` 다음 bullet
- 단체 설명 줄은 넣지 않는다. 필요하면 활동명에 녹인다
- 발표는 "{발표 제목}에 대한 발표" + 제목에 링크
- 활동 사이: 작은 빈 줄 1개

### OpenSource Contribute

- 형식: `{저장소명}    [Github] / [Pull Request]` 다음 bullet 2개 (프로젝트 소개, 기여 내용)
- 제목은 일반 문단(아래 서식 메모 참고)을 쓴다.

### Education

- 형식: `{학교명}    {YYYY.MM} ~ {YYYY.MM}` 다음 bullet `{학과} {학위}`

## Google Docs 서식 메모

새 항목을 넣을 때는 **같은 섹션의 기존 항목 문단을 기준으로 스타일을 복제**한다. 아래 값은 v.2.1에서 읽은 것이다.

### 문서 기본값

- 페이지: Letter (612×792pt), 여백 왼쪽 28.3pt / 오른쪽 56.7pt / 위 0
- 본문 글꼴: 대부분 `Nanum Gothic`으로 직접 지정 (NORMAL_TEXT 기본값은 Proxima Nova 11pt이므로, 새 텍스트에도 Nanum Gothic을 지정해야 한다)
- 섹션 제목: HEADING_1, 15~16pt, 파란색(rgb 0.29/0.53/0.91). 제목 끝에 마침표 (`Career.`)
- bullet: 1단계 `●`, 2단계 `○`
- 표: 테두리 1pt 흰색 (보이지 않음)

### 섹션별 서식

| 요소 | 문단 스타일 | 글자 |
|---|---|---|
| Career 회사명 | NORMAL_TEXT | 굵게 13pt |
| Career 기간·조직 줄 | 회사명과 같은 문단, 줄바꿈(Shift+Enter)으로 이어짐 | 10pt |
| Career 서비스 줄 | NORMAL_TEXT | 굵게 11pt, `(링크)`는 굵게+밑줄+링크 |
| Career bullet | NORMAL_TEXT, bullet 1단계, 들여쓰기 36pt | 11pt |
| Work Experience 표 | 1행 2열, 열 너비 104pt / 487pt | - |
| Work Experience 회사명 (왼쪽 열) | NORMAL_TEXT | 굵게 14pt |
| Work Experience 항목 제목 | NORMAL_TEXT, 들여쓰기 21.3pt | 굵게 13pt |
| Work Experience bullet | 1단계 들여쓰기 35.4pt, 2단계 49.6pt | 11pt |
| Personal Project 제목 줄 | HEADING_2. 제목·기간·링크·소개를 한 문단에 두고 소개 앞은 줄바꿈 | 제목 13pt, 기간 10pt, `[Github]` 10pt 밑줄+링크, 소개 10pt |
| Personal Project bullet | 들여쓰기 14.2pt | 11pt |
| Activity·Education·OpenSource 제목 줄 | NORMAL_TEXT | 이름 굵게 13pt, 공백 굵게 12pt, 기간·링크 10pt |
| Activity·Education·OpenSource bullet | 들여쓰기 14.2pt | 11pt |
| 활동 사이 빈 줄 | NORMAL_TEXT | 6pt |

### 복제 기준 항목

새 항목을 넣을 때 스타일을 복제할 기존 항목은 섹션마다 `private/examples.md`의 "복제 기준 항목" 표에 있다.
