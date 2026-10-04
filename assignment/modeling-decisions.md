# 애매한 모델링 결정

좋은 모델러는 애매함을 없애는 사람이 아니라, **애매함을 알아채고 이유 있게 결정하는 사람**입니다.
하나의 개념이 여러 방식으로 모델링될 수 있을 때, 그 결정을 기록하세요.

최소 요건: **2개 이상.**

## 흔한 예

| 개념 | 가능한 모델링 |
|---|---|
| 승인 (Approval) | State(승인됨) · Transition(승인하다) · 별도 Entity(승인 기록) |
| 위험 평가 (Risk Assessment) | 별도 Entity · Attribute(위험 점수) |
| 약점 (Weak Point) | Entity · Attribute · 파생된 State |
| 법무 검토 (Legal Review) | State(검토 중) · 별도의 Work(담당자 · 마감이 있는 일) |

## 결정 1

- **개념:** 기업현황자료(CompanyReport)를 기업 단위로 할지 투자 단위로 할지
- **고려한 대안:** (최소 2개)
  - Company 기준
  - Investment 기준
- **최종 선택:** Company 기준으로 정함
- **이유:** 이 업무에서 무엇이 중요했는가? (기록이 남아야 하는가? 여러 번 일어날 수 있는가? 누가 했는지가 중요한가?)
  Investment가 여러 펀드에 걸쳐 여러번 일어났을 경우에도 기업 × 기간마다 한 번만 취합되는 의도를 구조로 표현. 
- **ESTC에 미친 영향:**
  - Entity: CompanyReport의 속성으로 company: ref(PortfolioCompany) 속성을 넣고 investment: ref(Investment)를 제거함. PortfolioCompany의 속성으로 investment_manager가 추가됨.
  - State: 영향 없음.
  - Transition: 여러 펀드에서 투자한 기업일 경우 여러 펀드 매니저가 있을 수 있어서 principal_role에서 fund_manager를 제거함. fund_manager 대신 investment_manager로도 충분할 것으로 판단되기 때문임. 
  - Constraint: C2와 C4에서 기존에 investment.company 참조에서 바로 company 참조로 변경함.

## 결정 2

- **개념:** 기업 담당자가 기업현황자료를 제출한 상태와 내부 담당자가 리뷰를 시작한 상태를 구분할지
- **고려한 대안:**
  - submitted 상태와 under_review 상태를 분리
  - submitted 상태와 under_review 상태를 통합
- **최종 선택:** submitted 상태와 under_review 상태를 통합. 같은 기준으로 additional_review 상태도 없앴음.
- **이유:** 두 상태에서 행동할 사람과 규칙이 동일했음.
- **ESTC에 미친 영향:**
  - Entity: 영향 없음.
  - State: submitted 상태로 under_review 상태가 통합됨.
  - Transition: start_review transition이 삭제됨. request_revision과 confirm(기존의 validate)이 출발하는 상태가 under_review에서 submitted로 변경됨.
  - Constraint: 영향 없음.
