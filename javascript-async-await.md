# JavaScript 비동기: 콜백, Promise, async/await

## 1. 비동기가 필요한 이유
- JavaScript는 **싱글 스레드**: 한 번에 하나의 작업만 실행
- 네트워크 요청·타이머처럼 오래 걸리는 작업을 기다리는 동안 화면이 멈추지 않도록 **비동기**로 처리

## 2. 콜백
```js
setTimeout(() => {
  console.log('1초 후 실행');
}, 1000);
```
- 콜백 안에 콜백이 계속 중첩되면 **콜백 지옥** 발생

## 3. Promise
- 미래의 결과를 담는 객체. 상태: **pending → fulfilled / rejected**
```js
const wait = (ms) => new Promise((resolve) => setTimeout(resolve, ms));

wait(1000)
  .then(() => console.log('완료'))
  .catch((err) => console.error(err));
```

## 4. async / await
```js
async function loadUser() {
  try {
    const res = await fetch('https://jsonplaceholder.typicode.com/users/1');
    const user = await res.json();
    console.log(user.name);
  } catch (err) {
    console.error('요청 실패', err);
  }
}
```
- `async` 함수는 항상 Promise를 반환
- `await`는 Promise가 끝날 때까지 **해당 함수 안에서만** 기다림
- 오류 처리는 `try...catch`

## 5. 여러 요청 동시에
```js
const [a, b] = await Promise.all([fetch('/a'), fetch('/b')]);
```
- 하나라도 실패하면 전체 reject → 일부 실패를 허용하려면 `Promise.allSettled`

## 6. 실행 순서 예시
```js
console.log(1);
setTimeout(() => console.log(2), 0);
Promise.resolve().then(() => console.log(3));
console.log(4);
// 출력: 1 4 3 2  (마이크로태스크(Promise)가 매크로태스크(setTimeout)보다 먼저)
```

## 정리
- 콜백 → Promise → async/await 순으로 가독성이 좋아졌다.
- 실무에서는 async/await + try/catch 조합을 가장 많이 사용한다.
