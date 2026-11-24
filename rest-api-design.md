# REST API 설계 원칙

## 1. REST란?
- REpresentational State Transfer
- **자원(Resource)** 을 URL로 표현하고, **행위** 는 HTTP 메서드로 표현하는 설계 방식

## 2. 핵심 규칙
1. URL에는 **명사(자원)**, 동작은 **메서드**로
2. 자원은 **복수형** 사용
3. 계층 관계는 `/`로 표현
4. 소문자, 단어 구분은 하이픈(`-`)
5. 파일 확장자·동사(`/getUsers`)는 URL에 넣지 않음

## 3. 좋은 예 / 나쁜 예
| 목적 | 나쁜 예 | 좋은 예 |
|---|---|---|
| 목록 조회 | GET /getTransactions | GET /transactions |
| 단건 조회 | GET /transaction?id=3 | GET /transactions/3 |
| 생성 | POST /createTransaction | POST /transactions |
| 수정 | POST /updateTransaction | PATCH /transactions/3 |
| 삭제 | GET /deleteTransaction/3 | DELETE /transactions/3 |

## 4. 계층·필터 표현
```
GET /users/7/transactions              # 7번 사용자의 거래
GET /transactions?month=2026-11&type=expense   # 조건 필터는 쿼리 스트링
```

## 5. 응답 설계
- 생성 성공: **201 Created** + 생성된 데이터
- 삭제 성공: **204 No Content**
- 오류 응답은 형식을 통일
```json
{ "status": 400, "message": "금액은 0보다 커야 합니다." }
```

## 정리
- "무엇을(URL) 어떻게(메서드)"를 분리하면 API가 읽기 쉬워진다.
- 일관된 규칙이 협업과 유지보수를 쉽게 만든다.
