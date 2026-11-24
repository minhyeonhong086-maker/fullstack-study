# SQL 기본 CRUD

## 1. SQL이란?
- Structured Query Language: 관계형 데이터베이스(MySQL, PostgreSQL 등)를 다루는 언어

## 2. 테이블 만들기
```sql
CREATE TABLE transactions (
  id INT AUTO_INCREMENT PRIMARY KEY,   -- PostgreSQL은 SERIAL 또는 GENERATED AS IDENTITY
  type VARCHAR(10) NOT NULL,
  category VARCHAR(30) NOT NULL,
  amount INT NOT NULL CHECK (amount > 0),
  memo VARCHAR(50),
  created_at DATE NOT NULL
);
```

## 3. Create - INSERT
```sql
INSERT INTO transactions (type, category, amount, memo, created_at)
VALUES ('expense', '식비', 12000, '점심', '2026-11-24');
```

## 4. Read - SELECT
```sql
SELECT * FROM transactions;                         -- 전체
SELECT category, amount FROM transactions
WHERE type = 'expense' AND amount >= 10000          -- 조건
ORDER BY created_at DESC                            -- 정렬
LIMIT 10;                                           -- 개수 제한
```

## 5. Update - UPDATE
```sql
UPDATE transactions SET amount = 15000 WHERE id = 1;
```

## 6. Delete - DELETE
```sql
DELETE FROM transactions WHERE id = 1;
```
> ⚠️ UPDATE·DELETE에서 **WHERE를 빼면 모든 행이 바뀌거나 삭제** 된다.

## 7. 집계
```sql
SELECT category, SUM(amount) AS total, COUNT(*) AS cnt
FROM transactions
WHERE type = 'expense'
GROUP BY category
HAVING SUM(amount) > 50000
ORDER BY total DESC;
```
- WHERE: 그룹 전 행 필터 / HAVING: 그룹 후 필터

## 정리
- CRUD = INSERT / SELECT / UPDATE / DELETE
- 실행 순서: FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT
