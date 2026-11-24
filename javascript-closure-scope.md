# 스코프와 클로저

## 1. 스코프(Scope)
- 변수에 접근할 수 있는 범위
| 종류 | 설명 |
|---|---|
| 전역 스코프 | 어디서든 접근 |
| 함수 스코프 | 함수 안에서만 (`var`) |
| 블록 스코프 | `{ }` 안에서만 (`let`, `const`) |

```js
if (true) {
  var a = 1;
  let b = 2;
}
console.log(a); // 1
console.log(b); // ReferenceError
```

## 2. 렉시컬 스코프
- 함수가 **어디서 호출됐는지가 아니라 어디서 선언됐는지** 에 따라 상위 스코프가 결정됨

## 3. 클로저(Closure)
- 함수가 **선언될 때의 바깥 변수** 를 기억해서, 바깥 함수가 끝난 뒤에도 접근할 수 있는 것
```js
function createCounter() {
  let count = 0;            // 외부에서 직접 접근 불가
  return function () {
    count += 1;
    return count;
  };
}

const counter = createCounter();
counter(); // 1
counter(); // 2
```

## 4. 활용
- **정보 은닉**: `count`를 밖에서 마음대로 바꿀 수 없음
- **함수 공장**: 설정값을 기억하는 함수 만들기
```js
const multiply = (n) => (x) => x * n;
const double = multiply(2);
double(5); // 10
```
- React의 `useState`, 이벤트 핸들러도 클로저로 동작

## 5. 반복문과 클로저
```js
for (var i = 0; i < 3; i++) setTimeout(() => console.log(i)); // 3 3 3
for (let j = 0; j < 3; j++) setTimeout(() => console.log(j)); // 0 1 2
```
- `let`은 반복마다 새 블록 스코프를 만든다.

## 정리
- 클로저 = 함수 + 그 함수가 선언된 환경
- `var` 대신 `let`/`const`를 쓰는 이유 중 하나가 스코프 문제다.
