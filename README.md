# claude-meta-skills

Claude Code용 메타 스킬 2종 — "스킬을 만드는 스킬" + "에이전트를 만드는 스킬".

## 두 스킬

### `/skill-create` — 스킬 제조 공장
Claude Code 스킬(SKILL.md)을 9-Phase 방식으로 만든다. 발굴 → 분해 → 검증 → 조립 → QC 출하검사 → 운영 루프. 단일 책임·자기완결·500줄 권장.

- 모드: 단일 / 배치
- 산출물: `~/.claude/skills/{name}/SKILL.md`

### `/llm-dependent-agent-create` — LLM 의존형 에이전트 제조 공장
LLM(두뇌) 의존형 AI 에이전트를 9-Phase 방식으로 만든다. 출하 형태는 9가지 구동 방식(웹·데스크톱·모바일·메신저봇·확장·데몬·API·스케줄·포털) 중 자동 결정.

- 모드: 단일 / 배치 / 포털
- 인프라: A (Supabase 있음) / B (DB 없음, .py + API 키)
- 산출물: 운영 가능한 에이전트 자산 (코드·UI·DB·설정)

## 두 공장의 양방향 관계

같은 도메인 지식을 두 형태로 포장 가능:
- 스킬 → 에이전트: SKILL.md의 INSTRUCTION을 에이전트의 system_prompt로 재포장
- 에이전트 → 스킬: 에이전트 system_prompt를 SKILL.md로 추출

## 설치

```bash
# 1. clone
git clone https://github.com/wksun999/claude-meta-skills.git

# 2. ~/.claude/skills/에 두 스킬 폴더를 심는다
cp -r claude-meta-skills/skill-create ~/.claude/skills/
cp -r claude-meta-skills/llm-dependent-agent-create ~/.claude/skills/

# 3. Claude Code 재시작 또는 새 세션에서 /skill-create, /llm-dependent-agent-create 사용 가능
```

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

- 현재: V3.5 Round 9 (2026-05-28)
- changelog는 각 SKILL.md 헤더 주석 누적 보존
- 자기완결 원칙 (V3.4+): 외부 스킬·외부 AI 호출 금지, 핵심 절차 본문 내장

## 라이선스

MIT — 본인 본인 의도로 자유롭게 fork·수정·재배포 가능.

## 외부 검토 환영

issue·pull request 환영. 본인 (PO) 본인이 운영하는 단일 메인테이너 repo.

---

🤖 Generated and maintained with Claude Code.
