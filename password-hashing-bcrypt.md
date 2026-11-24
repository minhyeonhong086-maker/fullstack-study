# 비밀번호 해싱과 bcrypt

## 1. 비밀번호를 그대로 저장하면 안 되는 이유
- DB가 유출되면 모든 사용자 비밀번호가 그대로 노출
- 같은 비밀번호를 다른 사이트에도 쓰는 사용자가 많아 피해가 커짐

## 2. 암호화 vs 해싱
| 구분 | 암호화 | 해싱 |
|---|---|---|
| 복원 | 키로 복호화 가능 | **되돌릴 수 없음(단방향)** |
| 용도 | 주고받을 데이터 보호 | 비밀번호 저장 |

## 3. 일반 해시(SHA-256)만 쓰면 부족한 이유
- 너무 빠름 → 무차별 대입(brute force)에 취약
- 같은 비밀번호 = 같은 해시 → 미리 계산된 표(레인보우 테이블) 공격

## 4. 솔트(Salt)
- 비밀번호마다 **랜덤 값** 을 붙여 해싱 → 같은 비밀번호도 해시가 달라짐

## 5. bcrypt
- 솔트 자동 포함 + **cost(작업 강도)** 로 일부러 느리게 계산
- 결과 예: `$2b$10$...` (알고리즘 버전, cost, 솔트+해시)
- 그 밖의 권장 알고리즘: Argon2, scrypt

## 6. Node.js 예시
```js
const bcrypt = require('bcrypt');

// 회원가입: 해시 저장
const hash = await bcrypt.hash(plainPassword, 10);

// 로그인: 비교
const ok = await bcrypt.compare(inputPassword, hash);
```

## 7. Spring 예시
```java
PasswordEncoder encoder = new BCryptPasswordEncoder();
String hash = encoder.encode(rawPassword);
boolean ok = encoder.matches(rawPassword, hash);
```

## 정리
- 비밀번호는 **해싱 + 솔트 + 느린 알고리즘(bcrypt/Argon2)** 으로 저장한다.
- 로그인 시에는 해시를 풀지 않고 "다시 해싱해서 비교"한다.
