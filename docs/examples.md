# 도메인별 시작 예시

여러분의 도메인에서 "주인공 엔티티"와 "C4에 해당하는 규칙"을 찾는 것이 시작입니다.

| 도메인 | 주인공 | 대표 상태 흐름 | 여러분의 "C4" 후보 |
|---|---|---|---|
| Procurement | PurchaseRequest | draft→submitted→approved→ordered→received→closed | 금액별 승인 단계 |
| Sales | Opportunity | lead→qualified→proposal→negotiation→won/lost | 할인율 한도 |
| Support | Ticket | open→triaged→in_progress→resolved→closed | SLA 초과 시 에스컬레이션 |
| HR Onboarding | Candidate | offer→accepted→docs→provisioned→active | 서류 완비 전 계정 발급 금지 |
| Contract | Contract | draft→legal_review→countersign→executed | 법무 검토 없는 체결 금지 |
| IT Incident | Incident | detected→acknowledged→mitigating→resolved→postmortem | 승인 없는 프로덕션 변경 금지 |

전체 참조 구현: 강의의 Expense Approval World
(상태 7개 · transition 6개 · constraint 9개 · principal 4명)
