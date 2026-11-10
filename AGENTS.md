# AGENTS.md

이 레포에서 작업하는 AI 도구(Claude Code, Codex, ChatGPT 등)를 위한 안내.

## 프로젝트

디자인 시안과 PRD 사이의 빈칸(정해지지 않은 화면 상태)을 찾아, 기획자에게는 선택형 질문으로, 디자이너에게는 할 일로 나눠 주는 AI 스킬이다. 코드가 아니라 마크다운 지침이 결과물이다.

## 파일 역할

| 파일 | 역할 |
|---|---|
| `design-gap-check/SKILL.md` | 스킬 본체. 언제 쓰는지(frontmatter의 description)와 동작 순서 |
| `design-gap-check/references/states-checklist.md` | 화면 유형별로 확인할 상태와 원칙 코드. 결과의 질을 가장 크게 좌우한다 |
| `design-gap-check/references/question-guide.md` | 기획자 질문 쓰는 법 |
| `design-gap-check/templates/report.md` | 검수 모드 출력 형식 |
| `design-gap-check/templates/prd-update.md` | 반영 모드 출력 형식 |
| `gpt/instructions.md` | ChatGPT GPTs에 붙여 넣는 지침. SKILL.md를 줄인 것 |
| `examples/study-app/` | 테스트용 입력(prd.md, screens.md, answers.md)과 기대 결과(expected-*.md) |

## 규칙

- 모든 지침과 결과물은 한국어로 쓴다.
- `SKILL.md`와 `gpt/instructions.md`는 같은 동작을 해야 한다. 하나를 고치면 다른 하나에도 반영한다.
- `gpt/instructions.md`는 GPTs 지침 제한 때문에 8000자를 넘기지 않는다.
- `SKILL.md`에는 순서와 판단 기준만 두고, 긴 목록이나 예시는 `references/`로 뺀다.
- 체크리스트에 상태를 추가할 때는 "정해야 할 것", "보통 누가", "원칙" 칸을 모두 채운다.
- 체크리스트, 질문 가이드, 템플릿을 바꾸면 `examples/study-app/expected-*.md`가 여전히 맞는지 확인하고 필요하면 함께 고친다.

## 테스트하는 법

1. 새 대화에서 스킬을 불러온 상태로 `examples/study-app/prd.md`와 `screens.md`를 넣고 검수를 요청한다.
2. 결과를 `expected-report.md`와 비교한다. 문장이 같을 필요는 없고 아래를 본다.
   - 승인 화면이 없다는 것(흐름이 끊기는 빈칸)을 가장 먼저 묻는가
   - 이미 있는 F2(참여한 스터디 없음)를 빠졌다고 하지 않는가
   - 로딩, 오류 문구처럼 디자이너가 정할 일을 기획 질문으로 보내지 않았는가
   - 범위 밖(채팅, 출석, 결제)을 묻지 않는가
   - 선택지마다 사용자가 보게 될 모습이 있고, 추천에 원칙 코드가 있는가
   - PRD에 없는 기능(알림 등)이 필요한 선택지에 "새 기능 필요" 표시가 있고, 그 선택지를 추천하지 않았는가
   - 문장이나 질문 개수는 실행마다 달라도 된다. 위 기준을 지키는지가 중요하다.
3. 이어서 `answers.md`를 보내고 결과를 `expected-prd-update.md`와 비교한다. 답에 없는 정책을 지어내지 않았는지 본다.

## 커밋

`타입: 한글 설명` 한 줄로 쓴다. 타입은 feat(스킬 동작 추가, 변경), fix(잘못된 판단 수정), docs(README 등 안내), chore(예시, 설정).
