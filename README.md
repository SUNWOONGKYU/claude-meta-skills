# claude-meta-skills

Claude Code용 메타 스킬 2종 — "스킬을 만드는 스킬" + "에이전트를 만드는 스킬".

## 두 스킬

### `/skill-create` — 스킬 제조 공장
Claude Code 스킬(SKILL.md)을 9-Phase 방식으로 만든다. 발굴 → 분해 → 검증 → 조립 → QC 출하검사 → 운영 루프. 단일 책임·자기완결·500줄 권장.

- 모드: 단일 / 배치
- 산출물: `~/.claude/skills/{name}/SKILL.md`

### `/llm-dependent-agent-create` ★ **별칭: 에신 (에이전트의 신)** — LLM 의존형 에이전트 제조 공장
LLM(두뇌) 의존형 AI 에이전트를 9-Phase 방식으로 만든다. 출하 형태는 9가지 구동 방식(웹·데스크톱·모바일·메신저봇·확장·데몬·API·스케줄·포털) 중 자동 결정.

사용자는 `"에신아 ~하는 에이전트 만들어줘"` 같이 별칭으로 호출 가능.

- 모드: 단일 / 배치 / 포털
- 인프라: A (Supabase 있음) / B (DB 없음, .py + API 키)
- 산출물: 운영 가능한 에이전트 자산 (코드·UI·DB·설정)

## 두 공장의 양방향 관계

같은 도메인 지식을 두 형태로 포장 가능:
- 스킬 → 에이전트: SKILL.md의 INSTRUCTION을 에이전트의 system_prompt로 재포장
- 에이전트 → 스킬: 에이전트 system_prompt를 SKILL.md로 추출

---

## ⚡ 가장 빠른 설치 — Claude Code에게 시키기

명령어 직접 입력하기 귀찮으시면, 본인의 Claude Code 세션에 **아래 한 줄을 그대로 붙여넣으세요.** Claude Code가 알아서 다운받고 `~/.claude/skills/`에 설치합니다.

### 둘 다 설치하기

> **"https://github.com/SUNWOONGKYU/claude-meta-skills 에서 두 메타 스킬을 받아서 내 `~/.claude/skills/` 폴더에 설치해 줘."**

또는 더 짧게:

> **"`SUNWOONGKYU/claude-meta-skills` 설치해 줘."**

### 하나만 설치하기 (둘 중 하나만 필요할 때)

**에이전트 만드는 스킬만 받기** (`/llm-dependent-agent-create`)
> **"`SUNWOONGKYU/claude-meta-skills` 에서 `llm-dependent-agent-create`만 받아서 내 `~/.claude/skills/`에 설치해 줘."**

**스킬 만드는 스킬만 받기** (`/skill-create`)
> **"`SUNWOONGKYU/claude-meta-skills` 에서 `skill-create`만 받아서 내 `~/.claude/skills/`에 설치해 줘."**

### 공통 사항

설치 후 새 Claude Code 세션에서 `/skill-create` 또는 `/llm-dependent-agent-create`를 호출하면 됩니다. Windows·macOS·Linux 모두 동일.

업데이트도 똑같은 방식:

> **"`claude-meta-skills` 최신 버전으로 업데이트해 줘."**

---

## 다운로드 방법 4가지 (직접 명령어 입력)

위 "Claude Code에게 시키기"가 안 되거나 직접 명령어로 하고 싶을 때.

### 방법 1 — `git clone` (가장 권장)

업데이트(`git pull`)로 V3.6·V3.7 갱신을 받기 쉬워서 가장 권장.

**Windows (PowerShell·Git Bash·WSL 공통)**
```bash
git clone https://github.com/SUNWOONGKYU/claude-meta-skills.git
cp -r claude-meta-skills/skill-create "$env:USERPROFILE\.claude\skills\"
cp -r claude-meta-skills/llm-dependent-agent-create "$env:USERPROFILE\.claude\skills\"
```

**macOS·Linux**
```bash
git clone https://github.com/SUNWOONGKYU/claude-meta-skills.git
cp -r claude-meta-skills/skill-create ~/.claude/skills/
cp -r claude-meta-skills/llm-dependent-agent-create ~/.claude/skills/
```

### 방법 2 — ZIP 다운로드 (Git 모르는 분용)

브라우저 1회 클릭으로 받기.

1. https://github.com/SUNWOONGKYU/claude-meta-skills 접속
2. 녹색 `Code` 버튼 → `Download ZIP`
3. 압축 풀고 두 폴더(`skill-create`, `llm-dependent-agent-create`)를 `~/.claude/skills/` 안으로 복사

### 방법 3 — GitHub CLI (gh)

이미 `gh` 설치·로그인된 환경이면:
```bash
gh repo clone SUNWOONGKYU/claude-meta-skills
```
이후 방법 1과 동일하게 두 폴더 복사.

### 방법 4 — 개별 SKILL.md만 raw 다운로드 (둘 중 하나만 필요할 때)

폴더 구조(`_design/`·`docs/`) 없이 SKILL.md 본문만 빠르게 받고 싶을 때.

**Windows PowerShell**
```powershell
$skillsDir = "$env:USERPROFILE\.claude\skills"

# /skill-create
New-Item -ItemType Directory -Force "$skillsDir\skill-create" | Out-Null
Invoke-WebRequest "https://raw.githubusercontent.com/SUNWOONGKYU/claude-meta-skills/main/skill-create/SKILL.md" `
    -OutFile "$skillsDir\skill-create\SKILL.md"

# /llm-dependent-agent-create
New-Item -ItemType Directory -Force "$skillsDir\llm-dependent-agent-create" | Out-Null
Invoke-WebRequest "https://raw.githubusercontent.com/SUNWOONGKYU/claude-meta-skills/main/llm-dependent-agent-create/SKILL.md" `
    -OutFile "$skillsDir\llm-dependent-agent-create\SKILL.md"
```

**macOS·Linux (curl)**
```bash
mkdir -p ~/.claude/skills/skill-create ~/.claude/skills/llm-dependent-agent-create

curl -L https://raw.githubusercontent.com/SUNWOONGKYU/claude-meta-skills/main/skill-create/SKILL.md \
     -o ~/.claude/skills/skill-create/SKILL.md

curl -L https://raw.githubusercontent.com/SUNWOONGKYU/claude-meta-skills/main/llm-dependent-agent-create/SKILL.md \
     -o ~/.claude/skills/llm-dependent-agent-create/SKILL.md
```

---

## 설치 확인

```bash
# ~/.claude/skills/ 에 두 폴더가 보이면 OK
ls ~/.claude/skills/ | grep -E "skill-create|llm-dependent-agent-create"
```

Claude Code 새 세션에서 다음 명령이 자동 인식되면 정상 설치:
- `/skill-create [만들 스킬 설명]`
- `/llm-dependent-agent-create [만들 에이전트 설명]`

설치 시점에 Claude Code가 이미 실행 중이었다면 한 번 재시작해야 인식됩니다.

---

## 핵심 원칙 (8대 철칙)

1. **발굴물 무신뢰** — 공개 저장소도 통째 신뢰 금지
2. **부품 단위 선별** — 함수·블록·체크리스트 단위
3. **운용 충돌 0건 — 타협 불가**
4. **스무고개 항상 강제** — 막연한 요청 금지 (V3.5: 10라운드 기본)
5. **MBO 승인 게이트**
6. **자기검증 금지** — 별도 Verification Subagent
7. **"curl 200 ≠ 동작함"** — 사용자 화면 직접 확인
8. **자산화·운영까지가 완료**

## 버전 정책

- 현재: **V3.5 Round 9** (2026-05-28)
- changelog는 각 SKILL.md 헤더 주석에 누적 보존 — V3.0·V3.1·V3.2·V3.3·V3.4·V3.5 R4·R6·R7·R8·R9 모두 추적 가능
- 자기완결 원칙 (V3.4+): 외부 스킬·외부 AI 호출 금지, 핵심 절차 본문 내장
- Phase별 1장 요약표 (V3.5): 각 Phase의 입력/작업/출력/완료 조건 한눈에

## 라이선스

[MIT](LICENSE) — 자유롭게 fork·수정·재배포 가능.

## 기여·제보 환영

[Issues](https://github.com/SUNWOONGKYU/claude-meta-skills/issues) / [Pull Requests](https://github.com/SUNWOONGKYU/claude-meta-skills/pulls) 환영.

---

🤖 Generated and maintained with Claude Code.
