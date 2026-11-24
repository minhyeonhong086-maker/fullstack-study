# 트랜잭션과 ACID

## 1. 트랜잭션이란?
- **함께 성공하거나 함께 실패해야 하는 작업 묶음**
- 예: 계좌 이체 = A 출금 + B 입금 → 하나만 성공하면 안 됨

## 2. 기본 사용
```sql
START TRANSACTION;
UPDATE accounts SET balance = balance - 10000 WHERE id = 1;
UPDATE accounts SET balance = balance + 10000 WHERE id = 2;
COMMIT;      -- 모두 반영
-- 문제가 생기면 ROLLBACK; 으로 전부 취소
```

## 3. ACID
| 성질 | 의미 |
|---|---|
| Atomicity (원자성) | 전부 성공 또는 전부 실패 |
| Consistency (일관성) | 실행 전후 데이터가 규칙(제약 조건)을 지킴 |
| Isolation (격리성) | 동시에 실행되는 트랜잭션이 서로 간섭하지 않음 |
| Durability (지속성) | 커밋된 결과는 장애가 나도 유지 |

## 4. 격리 수준과 문제 현상
| 격리 수준 | Dirty Read | Non-Repeatable Read | Phantom Read |
|---|---|---|---|
| READ UNCOMMITTED | 발생 | 발생 | 발생 |
| READ COMMITTED | 방지 | 발생 | 발생 |
| REPEATABLE READ | 방지 | 방지 | 발생 가능* |
| SERIALIZABLE | 방지 | 방지 | 방지 |
- *MySQL InnoDB는 REPEATABLE READ가 기본이며 대부분의 팬텀 리드를 막는다.
- PostgreSQL 기본은 READ COMMITTED

## 5. Spring에서
```java
@Transactional
public void transfer(Long from, Long to, int amount) {
    accountRepository.withdraw(from, amount);
    accountRepository.deposit(to, amount);
}   // 런타임 예외가 발생하면 자동 롤백
```

## 정리
- 돈·재고처럼 중간 상태가 남으면 안 되는 작업은 반드시 트랜잭션으로 묶는다.
