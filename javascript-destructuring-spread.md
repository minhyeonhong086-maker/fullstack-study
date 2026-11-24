# 구조 분해 할당과 스프레드 문법

## 1. 배열 구조 분해
```js
const [first, second] = ['사과', '바나나', '포도'];
// first = '사과', second = '바나나'

const [count, setCount] = useState(0); // React에서 자주 보는 형태
```

## 2. 객체 구조 분해
```js
const user = { name: '홍길동', age: 25, city: '서울' };
const { name, age } = user;

// 이름 바꾸기 + 기본값
const { city: location = '미정', job = '학생' } = user;
```

## 3. 함수 매개변수에서
```js
function Profile({ name, age }) {   // React props 구조 분해
  return `${name} (${age})`;
}
```

## 4. 스프레드(...) - 펼치기
```js
const a = [1, 2];
const b = [...a, 3];                 // [1, 2, 3]

const base = { theme: 'light', lang: 'ko' };
const next = { ...base, theme: 'dark' }; // 뒤에 쓴 값이 덮어씀
```
- React state를 **불변성** 을 지키며 바꿀 때 필수
```js
setTodos((prev) => [...prev, newTodo]);
setForm((prev) => ({ ...prev, email: value }));
```

## 5. 나머지(rest) - 모으기
```js
const { password, ...safeUser } = user;  // password만 빼고 나머지 모으기
function sum(...nums) { return nums.reduce((s, n) => s + n, 0); }
```

## 6. 주의: 얕은 복사
```js
const copy = { ...obj };  // 1단계만 복사, 안쪽 객체는 같은 참조
const deep = structuredClone(obj); // 깊은 복사
```

## 정리
- 구조 분해 = 꺼내기, 스프레드 = 펼치기, rest = 모으기
