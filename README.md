# Superwork World Starter

> **Watch the world work. Then build your own.**

이 저장소에서 여러분은 **자신의 업무 도메인을 실행 가능한 세계(Agentic World)로 모델링**합니다.
강의(Day 1)에서 본 Expense Approval World와 같은 언어 — `superwork.world/v1` — 로,
여러분의 도메인(구매, 영업, CS, 채용, 계약, 장애 대응 …)을 선언합니다.

완료 기준은 하나입니다:

```
superwork validate --summary
```

의 마지막 줄이 **`READY FOR STUDIO IMPORT ✓`** 가 되는 것.
이 상태의 저장소만 Day 2 오전 **Import Showcase**에서 Superwork Studio에 올라가
실제로 실행되는 것을 볼 수 있습니다.

---

## 사전 과제 (Day 1 이전 · 10분)

수업 당일 환경 문제로 시간을 잃지 않기 위한 체크입니다.

```bash
# 1. 이 저장소를 clone
git clone <your-fork-url> && cd superwork-world-starter

# 2. 설치
npm install

# 3. 검증 실행 — 템플릿 상태 그대로 통과해야 정상입니다
npx superwork validate

# 4. world.yaml의 mission 한 줄을 여러분의 언어로 수정

# 5. 다시 검증
npx superwork validate

# 6. push
git add -A && git commit -m "pre-work: environment check" && git push
```

push까지 완료되면 다음 네 가지가 검증된 것입니다:

```
✓ Environment ready      ✓ Coding agent ready
✓ GitHub ready           ✓ Superwork CLI ready
```

코딩 에이전트(Claude Code 등)로 이 저장소를 열어두세요.
`AGENTS.md`가 에이전트에게 작업 규칙을 알려줍니다.

---

## Build Day 가이드 (10/1)

각 단계는 같은 패턴을 반복합니다:

```
Learn → Example → Ask your coding agent → Edit → Validate
```

막히면 언제든: `npx superwork explain <topic>`
(topics: `states` `transitions` `constraints` `expressions`)

### STEP 1 — Mission
*What work is this world trying to accomplish?*

`world.id`와 `mission`을 여러분의 도메인으로. mission은 이 세계가 완수하려는
**일** 한 문장입니다 — 기능 목록이 아니라 업무의 목적.

### STEP 2 — Entities
*What things must exist?*

이 일에 등장하는 것들을 선언합니다. 사람, 문서, 돈, 승인 대상…
상태기계를 갖는 엔티티(`owned_state: true`)는 **하나로 시작**하세요.
그 하나가 이 세계의 주인공입니다.

> 에이전트에게: "우리 회사의 ___ 업무에 등장하는 엔티티를 함께 정리하자.
> 내가 설명하면 너는 entities 초안을 제안하고, 내가 승인한 것만 반영해."

### STEP 3 — State
*What must the world know as fact?*

주인공 엔티티가 거치는 상태를 나열합니다. **State와 attribute의 구분**:
State는 흐름 속의 위치(어디까지 왔는가), attribute는 그 객체가 가진 값(얼마인가,
누구의 것인가)입니다. "승인됨"은 state, "승인 금액"은 attribute. 여기서 중요한 관점 하나 —
**State는 AI의 기억이 아니라, 실행 엔진이 쓰는 공식 사실**입니다.
끝나면 돌아올 수 없는 상태는 `terminal_states`로.

### STEP 4 — Transitions
*What is allowed to change?*

상태 사이의 허용된 변화를 선언합니다. 각 transition에는
**누가**(`principal_role`) 그 변화를 일으킬 수 있는지가 반드시 붙습니다.
`effects`는 상태 라벨 변경 이상의 인과(예산 예약 등)가 있을 때.

### STEP 5 — Constraints
*What must never be allowed?*

이 세계의 규칙을 선언합니다. Day 1의 그 장면을 기억하세요 —
같은 사람, 같은 상태, 같은 행동이었는데 **C4 하나가 실행을 막았습니다.**
여러분 도메인의 C4는 무엇입니까? 금액 한도? 셀프 승인 금지? 순서 강제?

각 constraint에는 사람이 읽는 `message`를, 대안 경로가 있으면
`on_fail_hint`를 붙이세요. 세계는 거부만 하지 않고 다음 경로를 알려줍니다.

### STEP 6 — Validate
*Does your world form a coherent executable model?*

```bash
npx superwork validate --summary
```

`READY FOR STUDIO IMPORT ✓` 가 나오면 push:

```bash
git add -A && git commit -m "build day: world v0.1.0" && git push
```

**마감: 10/1 자정.** Build & Review 티어는 이 시점의 저장소가
1:1 리뷰 세션의 입력물이 됩니다.

---

## Day 2 이후

- **Mini Build (Day 2 오후):** `scenarios/`에 시나리오를 추가하고
  agent 정의를 얹습니다 — 세션에서 안내합니다.
- **1주 Q&A 기간:** 이 세계를 계속 발전시키세요. `rejected → draft` 재제출
  경로를 추가하면 어떤 constraint와 audit 요구가 함께 생기는지 — 좋은 확장 과제입니다.

## 규칙 하나

검증 에러가 나면 **세계를 고치세요. 검증기를 고치지 마세요.**
(`AGENTS.md` 규칙 5 — 여러분의 코딩 에이전트도 같은 규칙을 따릅니다.)
