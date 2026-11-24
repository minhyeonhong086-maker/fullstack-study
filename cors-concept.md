# CORS 이해하기

## 1. 출처(Origin)란?
- **프로토콜 + 도메인 + 포트**
- `http://localhost:5173` 과 `http://localhost:3000`은 포트가 달라 **다른 출처**

## 2. 동일 출처 정책(SOP)
- 브라우저는 보안을 위해 **다른 출처의 응답을 JS가 읽지 못하게** 막는다.

## 3. CORS란?
- Cross-Origin Resource Sharing
- 서버가 응답 헤더로 "이 출처는 허용한다"고 알려주면 브라우저가 접근을 허용하는 방식

## 4. 대표 오류
```
Access to fetch at 'http://localhost:3000/api' from origin 'http://localhost:5173'
has been blocked by CORS policy
```
- **서버 쪽 설정** 으로 해결해야 한다. (프론트 코드만 고쳐서는 안 됨)

## 5. 해결 예시
```js
// Express
const cors = require('cors');
app.use(cors({ origin: 'http://localhost:5173', credentials: true }));
```
```java
// Spring
@CrossOrigin(origins = "http://localhost:5173")
@RestController
public class ApiController { }
```
```js
// Vite 개발 서버 프록시 (vite.config.js)
server: { proxy: { '/api': 'http://localhost:3000' } }
```

## 6. Preflight 요청
- PUT/DELETE, JSON Content-Type, 커스텀 헤더 등은 본 요청 전에 **OPTIONS** 요청으로 허용 여부를 먼저 확인

## 7. 주의
- 쿠키를 함께 보낼 때는 `Access-Control-Allow-Origin: *` 사용 불가 → 정확한 출처를 지정
- CORS는 **브라우저** 의 정책 → Postman이나 서버 간 요청에는 적용되지 않음

## 정리
- CORS 오류 = 서버가 허용 헤더를 안 줬다는 뜻 → 백엔드에서 허용 출처를 설정한다.
