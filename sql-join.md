# SQL JOIN

## 1. JOIN이란?
- 여러 테이블을 **공통 컬럼(보통 외래 키)** 으로 연결해서 조회하는 것

## 2. 예시 테이블
```sql
users(id, name)
transactions(id, user_id, amount)   -- user_id → users.id (외래 키)
```

## 3. INNER JOIN
- 양쪽에 **모두 일치하는 행** 만
```sql
SELECT u.name, t.amount
FROM transactions t
INNER JOIN users u ON t.user_id = u.id;
```

## 4. LEFT JOIN
- 왼쪽 테이블은 **전부**, 오른쪽은 일치하는 것만 (없으면 NULL)
```sql
-- 거래가 없는 사용자도 포함
SELECT u.name, COUNT(t.id) AS tx_count
FROM users u
LEFT JOIN transactions t ON t.user_id = u.id
GROUP BY u.id, u.name;
```
- `COUNT(t.id)`는 NULL을 세지 않으므로 거래 없는 사용자는 0

## 5. 종류 비교
| JOIN | 결과 |
|---|---|
| INNER | 교집합 |
| LEFT | 왼쪽 전체 + 일치하는 오른쪽 |
| RIGHT | 오른쪽 전체 + 일치하는 왼쪽 |
| FULL OUTER | 양쪽 전체 (MySQL은 미지원 → UNION으로 대체) |
| CROSS | 모든 조합 (행 수 = A × B) |

## 6. 거래가 없는 사용자 찾기
```sql
SELECT u.*
FROM users u
LEFT JOIN transactions t ON t.user_id = u.id
WHERE t.id IS NULL;
```

## 정리
- 실무에서는 INNER와 LEFT JOIN을 가장 많이 쓴다.
- 테이블 별칭(u, t)을 쓰면 쿼리가 짧고 읽기 쉬워진다.
