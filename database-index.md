# 데이터베이스 인덱스

## 1. 인덱스란?
- 책의 **찾아보기(색인)** 처럼, 원하는 행을 빠르게 찾게 해주는 자료구조
- 대부분 **B-Tree** 계열 구조 사용

## 2. 인덱스가 없을 때
- WHERE 조건에 맞는 행을 찾기 위해 **테이블 전체를 훑음(Full Table Scan)**

## 3. 생성
```sql
CREATE INDEX idx_tx_user_date ON transactions (user_id, created_at);
```
- 기본키(PRIMARY KEY)와 UNIQUE 제약에는 자동으로 인덱스가 생긴다.

## 4. 장단점
| 장점 | 단점 |
|---|---|
| 조회(SELECT) 빨라짐 | 저장 공간 추가 사용 |
| 정렬·그룹 작업 도움 | INSERT/UPDATE/DELETE 시 인덱스도 갱신 → 쓰기 느려짐 |

## 5. 인덱스가 잘 맞는 컬럼
- WHERE, JOIN, ORDER BY에 자주 쓰이는 컬럼
- 값의 종류가 다양한 컬럼(카디널리티 높음): 이메일, 사용자 ID
- 성별처럼 값이 2~3개뿐인 컬럼은 효과가 적다.

## 6. 복합 인덱스 순서
- `(user_id, created_at)` 인덱스는
  - `WHERE user_id = 1` ✅
  - `WHERE user_id = 1 AND created_at >= '2026-11-01'` ✅
  - `WHERE created_at >= '2026-11-01'` 만 → 효율이 떨어짐 (왼쪽 컬럼부터 사용)

## 7. 인덱스를 못 타는 경우
```sql
WHERE YEAR(created_at) = 2026     -- 컬럼에 함수 적용
WHERE name LIKE '%길동'            -- 앞에 % 사용
```

## 8. 실행 계획 확인
```sql
EXPLAIN SELECT * FROM transactions WHERE user_id = 1;
```

## 정리
- 인덱스는 읽기를 빠르게, 쓰기를 조금 느리게 만든다.
