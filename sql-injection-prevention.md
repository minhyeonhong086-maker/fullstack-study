# SQL Injection과 방어

## 1. SQL Injection이란?
- 입력값에 SQL 구문을 끼워 넣어 **의도하지 않은 쿼리를 실행** 시키는 공격

## 2. 취약한 코드
```js
// 문자열을 이어 붙여 쿼리 생성 ❌
const sql = "SELECT * FROM users WHERE email = '" + email + "' AND password = '" + pw + "'";
```
- email에 `' OR '1'='1' -- ` 를 넣으면 조건이 항상 참 → 로그인 우회 가능

## 3. 방어: 파라미터 바인딩(Prepared Statement)
- 쿼리 구조와 값을 **분리** → 값은 항상 "데이터"로만 처리
```js
// Node.js (mysql2)
const [rows] = await db.execute(
  'SELECT * FROM users WHERE email = ?',
  [email]
);
```
```java
// Java JDBC
PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE email = ?");
ps.setString(1, email);
ResultSet rs = ps.executeQuery();
```
- JPA, MyBatis `#{}`도 바인딩 방식 (MyBatis `${}`는 문자열 치환이라 위험)

## 4. 추가 방어
- **최소 권한**: 애플리케이션 DB 계정에 DROP 등 불필요한 권한 주지 않기
- 입력값 검증(형식, 길이)
- 오류 메시지에 SQL·DB 구조 노출하지 않기
- 정렬 컬럼처럼 바인딩이 안 되는 부분은 **허용 목록(whitelist)** 으로 검사

## 정리
- 쿼리는 문자열 연결 대신 **항상 파라미터 바인딩** 을 사용한다.
