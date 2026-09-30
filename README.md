# Superwork World Starter — Bootcamp Homework Edition

> **Build the World. Run the World. Try to break the World. Fix the World before the real world does.**

이 저장소에서 여러분은 **자신의 업무 하나를 World(실행 가능한 세계)로 모델링**하고,
그 World를 스스로 깨뜨려 보고, 고치고, 무엇을 왜 그렇게 결정했는지 기록합니다.

- 필요한 것: Node.js 18+, Git, (선택) Claude Code 같은 코딩 에이전트
- 필요 없는 것: Superwork 계정, 로그인, 초대, Studio 접근 — **이 숙제는 전부 로컬에서 완료됩니다.**

수업에서는 강사가 Superwork Studio로 같은 과정을 시연합니다. 여러분은 그 과정을
**직접 생각하며** 이 저장소에서 따라 합니다.

> **제출 마감: 2026-10-04 23:59 KST** (October 4, 2026, 11:59 PM Korea Standard Time)

---

## 0. 시작하기 (10분)

```bash
git clone https://github.com/swit001/superwork-starter.git && cd superwork-starter
npm install
npm run validate          # 템플릿 상태 그대로 통과해야 정상입니다
```

GitHub에 제출하려면 이 저장소를 여러분의 계정으로 가져가세요 (Fork 또는 새 저장소로 push).

---

## 1. 숙제의 흐름

```
CHOOSE → MODEL → VALIDATE → RUN → BREAK → FIX → RE-RUN → REFLECT → SUBMIT
```

| 단계 | 여러분이 하는 일 | 결과물 |
|---|---|---|
| **CHOOSE** | World로 만들 업무 하나를 고르고, World Model이 필요한 이유를 씁니다 | `assignment/world-fit.md` |
| **MODEL** | Entity · State · Transition · Constraint(ESTC)를 결정하고 `world.yaml`에 선언합니다 | `world.yaml`, `assignment/entity-decisions.md`, `assignment/modeling-decisions.md` |
| **VALIDATE** | `npm run validate` 로 World가 규격에 맞는지 확인합니다 | `evidence/` |
| **RUN** | 정상 시나리오 하나를 쓰고, `world.yaml`을 보며 손으로 판정(desk-check)합니다 | `scenarios/happy-path.yaml` |
| **BREAK** | World를 깨뜨릴 공격 시나리오 하나를 쓰고 판정합니다 | `scenarios/adversarial.yaml`, `assignment/break-fix.md` |
| **FIX** | 발견한 설계 빈틈을 **World 규칙을 바꿔서** 고칩니다 | `world.yaml`, `assignment/break-fix.md` |
| **RE-RUN** | 다시 validate하고, 같은 시나리오의 결과를 다시 판정합니다 | `assignment/break-fix.md`, `evidence/` |
| **REFLECT** | 배운 것을 짧게 씁니다 | `assignment/reflection.md` |
| **SUBMIT** | 저장소 URL(또는 zip)을 제출합니다 | 아래 체크리스트 |

자세한 과제 요건: [`assignment/README.md`](assignment/README.md)

---

## 2. 명령어

```bash
npm run validate      # World 규격 검사 — 문제가 있으면 어디가 왜 틀렸고 어떻게 고치는지 알려줍니다
npm run summary       # 요약 + 마지막 줄 READY FOR STUDIO IMPORT ✓
npm run evidence      # 요약 결과를 evidence/validate-summary.txt 로 저장 (제출 증거)
npx superwork explain <topic>   # DSL 도움말 (states | transitions | constraints | expressions)
```

### validate가 확인하는 것
- `world.yaml`이 `superwork.world/v1` 규격에 맞는지 (구조 · 참조 · transition · constraint 표현식 문법)
- 선언한 상태 · 역할 · 제약이 서로 올바르게 연결되어 있는지

### validate가 증명하지 **않는** 것
- 여러분의 업무 규칙이 **옳은지** — 셀프 승인을 막는 규칙이 빠져 있어도 World는 "valid"입니다.
- **규격에 맞는 World도 나쁜 업무 설계일 수 있습니다.** 그래서 BREAK 단계가 있습니다.

### RUN은 어떻게 하나요?
이 저장소에는 실행 엔진이 없습니다. 여러분은 각 시나리오를 `world.yaml`을 보며
**손으로 판정(desk-check)** 하고 예상 결과(ALLOW/DENY)와 이유를 기록합니다.
제출 후 리뷰에서는 강사가 여러분의 저장소를 Superwork Studio로 가져와
**같은 시나리오를 실제 Runtime으로 실행**하고, 여러분의 예측과 실제 결과를 함께 비교합니다.
판정 방법: [`scenarios/README.md`](scenarios/README.md)

---

## 3. 저장소 구조

```text
world.yaml                  여러분의 World (루트에 있어야 합니다 — 위치를 옮기지 마세요)
seed.yaml                   시나리오의 시작 상태가 되는 샘플 레코드
scenarios/
  README.md                 시나리오 형식과 desk-check 방법
  happy-path.yaml           정상 시나리오
  adversarial.yaml          공격(Break) 시나리오
assignment/
  README.md                 과제 요건
  world-fit.md              왜 World Model이 필요한가
  entity-decisions.md       개념 → 분류 → 이유
  modeling-decisions.md     애매했던 모델링 결정
  break-fix.md              BEFORE → FIX → AFTER
  reflection.md             회고
  claude-code-prompt.md     코딩 에이전트와 함께 할 때
evidence/
  README.md                 제출할 증거
docs/                       개념 · 도메인 예시 · DSL 레퍼런스
AGENTS.md                   코딩 에이전트의 작업 규칙
.superwork/schema-version   언어 버전 (수정하지 마세요)
```

---

## 4. 코딩 에이전트와 함께

Claude Code 등을 써도 좋습니다. 단, **결정은 여러분이 합니다.**
에이전트가 답을 먼저 쓰지 않고 여러분에게 묻도록 하는 시작 프롬프트:
[`assignment/claude-code-prompt.md`](assignment/claude-code-prompt.md).
에이전트는 `AGENTS.md`의 규칙을 따릅니다.

---

## 5. 제출 체크리스트

- [ ] `world.yaml` — 여러분의 World (`npm run validate` 통과)
- [ ] `assignment/world-fit.md` — World Model이 필요한 이유 3–6문장
- [ ] `assignment/entity-decisions.md` — 최종 Entity 3개 이상, Entity가 **아닌** 개념 2개 이상, 각각 이유
- [ ] `assignment/modeling-decisions.md` — 애매했던 결정 2개 이상 (대안 · 선택 · 이유 · ESTC 영향)
- [ ] `scenarios/happy-path.yaml` — 정상 시나리오 1개 + 예상 판정과 이유
- [ ] `scenarios/adversarial.yaml` — 공격 시나리오 1개 + 예상 판정과 이유
- [ ] `assignment/break-fix.md` — 발견한 설계 빈틈(또는 이미 막혀 있던 실패) · 수정 · 같은 시나리오 재판정
- [ ] `evidence/` — 수정 전/후 validate 결과
- [ ] `assignment/reflection.md` — 짧은 회고

**제출 마감: 2026-10-04 23:59 KST** (October 4, 2026, 11:59 PM Korea Standard Time)

**제출 방법**
1. **기본:** GitHub 저장소 URL (공개 저장소, 또는 강사를 collaborator로 초대)
2. **대체:** 저장소 전체를 zip으로 압축해 제출 (`node_modules/` 제외)

---

## 규칙 하나

검증 에러가 나면 **World를 고치세요. 검증기를 고치지 마세요.**
그리고 BREAK에서 빈틈을 찾으면 **프롬프트가 아니라 World를 고치세요.**

---

## 라이선스와 소유권

Copyright © 2026 Josh Lee. All rights reserved.

이 저장소는 **소스 공개(source-available)이지만 오픈소스가 아닙니다.**
저장소의 원본 콘텐츠는 **Educational Use Only License**([`LICENSE`](LICENSE))에 따라
**Agentic World Bootcamp 참여와 개인 교육용 숙제**에만 사용할 수 있습니다.
상업적 사용, 프로덕션 사용, 경쟁 제품 개발, 제품 · 템플릿 · 프레임워크로의 재배포,
제3자 제품이나 서비스에의 포함은 허용되지 않습니다.

- **Josh Lee**가 이 저장소의 원본 코드 · 템플릿 · 문서 · 예시 및 기타 Superwork 저작물을 소유합니다.
- **여러분**은 이 저장소를 이용해 직접 만든 숙제 결과물(여러분의 World · 답안 · 시나리오 · 증거)의 소유권을 가집니다.
- 숙제 결과물을 소유한다고 해서, 그 안에 쓰인 스타터의 템플릿 · 문서 · 예시 등 Superwork 저작물을
  Educational Use 라이선스 밖에서 재사용하거나 재배포할 권리가 생기지는 않습니다.
- npm 의존성은 원래의 라이선스를 따르며 이 라이선스로 바뀌지 않습니다
  (`@superwork/world-spec`, `@superwork/cli` — MIT, `yaml` — ISC).

GitHub 이용약관에 따른 공개 저장소의 열람 · Fork 권리는 그대로 유지되며, Fork도 이 라이선스를 따릅니다.
자세한 내용: [`LICENSE`](LICENSE), [`NOTICE`](NOTICE)

*Copyright © 2026 Josh Lee. All rights reserved. This repository is source-available, not open source. Its original content is
licensed only for Agentic World Bootcamp participation and personal educational homework; participants own their original homework,
which does not grant rights to the starter materials beyond that license; third-party MIT/ISC components keep their licenses —
see [`LICENSE`](LICENSE) and [`NOTICE`](NOTICE).*
