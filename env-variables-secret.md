# 환경변수(.env)와 비밀키 관리

## 1. 환경변수란?
- 코드 밖에서 주입하는 설정값 (DB 주소, API 키, 비밀키 등)
- 개발·운영 환경마다 값만 바꿔서 같은 코드를 실행할 수 있다.

## 2. 왜 코드에 직접 쓰면 안 되나?
- GitHub에 올리면 **누구나 키를 볼 수 있음** → 요금 폭탄, 데이터 유출
- 커밋 기록에 남아 나중에 지워도 이력에서 찾을 수 있음

## 3. Node.js
```bash
# .env
DB_PASSWORD=mysecret
JWT_SECRET=change-me
```
```js
// Node.js 20.6+ : node --env-file=.env server.js
// 또는 dotenv 패키지
require('dotenv').config();
console.log(process.env.DB_PASSWORD);
```

## 4. Vite(React)
```bash
# .env
VITE_API_URL=https://api.example.com
```
```js
const url = import.meta.env.VITE_API_URL;
```
- `VITE_`로 시작하는 값만 브라우저 코드에 노출된다.
- ⚠️ 프론트엔드 빌드에 들어간 값은 **사용자가 볼 수 있음** → 비밀키는 절대 넣지 않는다.

## 5. Spring Boot
```properties
# application.properties
spring.datasource.password=${DB_PASSWORD}
```

## 6. 꼭 지킬 것
- `.gitignore`에 `.env` 추가
- 팀원 공유용으로 값이 비어 있는 `.env.example` 제공
- 배포 서비스(Vercel, Render 등)의 **Environment Variables** 메뉴에 값 등록
- 키가 노출되면 **즉시 키를 재발급(rotate)** — 커밋 삭제만으로는 부족

## 정리
- 비밀값은 코드가 아니라 환경변수로 관리한다.
