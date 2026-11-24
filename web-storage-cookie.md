# localStorage · sessionStorage · 쿠키 비교

## 1. 한눈에 비교
| 항목 | localStorage | sessionStorage | 쿠키 |
|---|---|---|---|
| 유지 기간 | 직접 지울 때까지 | 탭을 닫으면 삭제 | 만료일까지 |
| 용량 | 약 5MB 내외 | 약 5MB 내외 | 약 4KB |
| 서버 전송 | ❌ | ❌ | ✅ 요청마다 자동 전송 |
| 접근 | JavaScript | JavaScript | JS + 서버 (HttpOnly면 JS 접근 불가) |

## 2. localStorage 사용법
```js
localStorage.setItem('theme', 'dark');
localStorage.getItem('theme');      // 'dark'
localStorage.removeItem('theme');

// 객체는 문자열로 변환해서 저장
localStorage.setItem('user', JSON.stringify({ name: '홍길동' }));
const user = JSON.parse(localStorage.getItem('user'));
```
- 문자열만 저장 가능 → JSON.stringify / JSON.parse

## 3. 쿠키 보안 속성
| 속성 | 의미 |
|---|---|
| HttpOnly | JavaScript에서 읽기 불가 → XSS로 탈취 어려움 |
| Secure | HTTPS에서만 전송 |
| SameSite | 다른 사이트 요청에 쿠키 전송 제한 (CSRF 완화) |

## 4. 보안 주의
- localStorage는 페이지의 모든 스크립트가 읽을 수 있다 → XSS에 취약
- 비밀번호, 카드번호 등 민감 정보는 브라우저 저장소에 저장하지 않는다.
- 로그인 토큰은 HttpOnly 쿠키에 보관하는 방식이 많이 권장된다.

## 5. 언제 무엇을?
- 테마·필터 설정 등 가벼운 값 → localStorage
- 한 탭에서만 쓰는 임시 값 → sessionStorage
- 서버가 알아야 하는 인증 정보 → 쿠키

## 정리
- 저장 위치는 "유지 기간, 서버 전송 여부, 보안"으로 고른다.
