# Express로 REST API 서버 만들기

## 1. Express란?
- Node.js에서 웹 서버와 API를 쉽게 만들게 해주는 프레임워크

## 2. 설치
```bash
mkdir express-api && cd express-api
npm init -y
npm install express
```

## 3. 기본 서버
```js
// server.js
const express = require('express');
const app = express();

app.use(express.json()); // 요청 body(JSON)를 객체로 변환

app.get('/', (req, res) => {
  res.send('서버 동작 중');
});

app.listen(3000, () => console.log('http://localhost:3000'));
```
```bash
node server.js
```

## 4. CRUD API (메모리 배열 사용)
```js
let items = [];
let nextId = 1;

app.get('/api/items', (req, res) => res.json(items));

app.post('/api/items', (req, res) => {
  const { name } = req.body;
  if (!name) return res.status(400).json({ message: 'name은 필수입니다.' });
  const item = { id: nextId++, name };
  items.push(item);
  res.status(201).json(item);
});

app.patch('/api/items/:id', (req, res) => {
  const item = items.find((i) => i.id === Number(req.params.id));
  if (!item) return res.status(404).json({ message: '없는 항목입니다.' });
  item.name = req.body.name ?? item.name;
  res.json(item);
});

app.delete('/api/items/:id', (req, res) => {
  items = items.filter((i) => i.id !== Number(req.params.id));
  res.status(204).end();
});
```

## 5. 요청 값 위치
| 위치 | 예시 | 읽는 방법 |
|---|---|---|
| 경로 변수 | /items/3 | `req.params.id` |
| 쿼리 | /items?page=2 | `req.query.page` |
| 본문 | JSON body | `req.body` |

## 6. 테스트
- Postman 또는 VS Code REST Client로 요청 확인

## 정리
- 메모리 배열은 서버를 껐다 켜면 사라진다 → 실제 서비스는 DB와 연결해야 한다.
