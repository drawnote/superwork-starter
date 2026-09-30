# Evidence — 제출할 증거

이 폴더에 다음을 넣으세요.

| 파일 | 내용 | 만드는 법 |
|---|---|---|
| `validate-before.txt` | FIX 이전 World의 검증 결과 | FIX 전에 `npm run evidence` 실행 후 파일 이름을 `validate-before.txt`로 변경 |
| `validate-after.txt` | FIX 이후 World의 검증 결과 | FIX 후에 `npm run evidence` 실행 후 파일 이름을 `validate-after.txt`로 변경 |
| (선택) 기타 | desk-check 메모, 스크린샷, 에이전트와의 대화 중 결정적이었던 부분 | 자유 |

`npm run evidence`는 `npm run summary`의 결과를 `evidence/validate-summary.txt`에 저장합니다.

> 검증 결과는 World가 **규격에 맞는다**는 증거일 뿐, **안전하다**는 증거가 아닙니다.
> 안전에 대한 여러분의 주장은 `scenarios/`와 `assignment/break-fix.md`의 판정과 이유로 보여주세요.
