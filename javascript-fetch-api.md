# fetch로 API 호출하기

## 1. fetch 기본
```js
const res = await fetch('https://jsonplaceholder.typicode.com/posts');
const posts = await res.json();
```
- `fetch`는 Promise를 반환
- `res.json()`도 Promise → `await` 필요

## 2. 주의: HTTP 오류는 reject되지 않음
- 404, 500 응답이어도 fetch는 **성공(resolve)** 으로 처리
- 네트워크 자체가 끊겼을 때만 reject
```js
const res = await fetch('/api/items');
if (!res.ok) {
  throw new Error(`요청 실패: ${res.status}`);
}
```

## 3. POST 요청
```js
const res = await fetch('/api/transactions', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ type: 'expense', amount: 12000 }),
});
const created = await res.json();
```
- 객체는 `JSON.stringify`로 문자열로 바꿔서 보냄

## 4. PATCH / DELETE
```js
await fetch('/api/transactions/3', {
  method: 'PATCH',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ amount: 15000 }),
});

await fetch('/api/transactions/3', { method: 'DELETE' });
```

## 5. 공통 함수로 묶기
```js
async function api(url, options = {}) {
  const res = await fetch(url, {
    headers: { 'Content-Type': 'application/json' },
    ...options,
  });
  if (!res.ok) throw new Error(`HTTP ${res.status}`);
  return res.status === 204 ? null : res.json();
}
```

## 정리
- fetch는 `res.ok`를 직접 확인해야 한다.
- 요청 함수를 한 곳에 모아두면 나중에 주소나 헤더를 바꾸기 쉽다.
