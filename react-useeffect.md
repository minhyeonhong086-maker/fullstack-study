# React useEffect

## 1. useEffect란?
- 렌더링 이후에 실행할 **부수 효과(side effect)** 를 처리하는 Hook
- 예: 데이터 불러오기, 타이머, 이벤트 등록, localStorage 저장

## 2. 기본 형태
```jsx
useEffect(() => {
  // 실행할 코드
  return () => {
    // 정리(cleanup) 코드 (선택)
  };
}, [의존성]);
```

## 3. 의존성 배열에 따른 실행 시점
| 형태 | 실행 시점 |
|---|---|
| 배열 생략 | 렌더링될 때마다 |
| `[]` | 처음 화면에 나타날 때 1번 |
| `[value]` | 처음 + value가 바뀔 때마다 |

## 4. 예시: 값이 바뀔 때 저장
```jsx
useEffect(() => {
  localStorage.setItem('todos', JSON.stringify(todos));
}, [todos]);
```

## 5. 예시: 이벤트 등록과 정리
```jsx
useEffect(() => {
  const onResize = () => setWidth(window.innerWidth);
  window.addEventListener('resize', onResize);
  return () => window.removeEventListener('resize', onResize);
}, []);
```
- 정리 함수가 없으면 컴포넌트가 사라져도 이벤트가 남아 **메모리 누수** 발생

## 6. 데이터 불러오기
```jsx
useEffect(() => {
  let ignore = false;
  async function load() {
    const res = await fetch('/api/items');
    const data = await res.json();
    if (!ignore) setItems(data);
  }
  load();
  return () => { ignore = true; };
}, []);
```
- effect 함수 자체를 async로 만들 수 없으므로 안쪽에 async 함수를 만든다.

## 7. 주의
- 개발 모드 `StrictMode`에서는 effect가 **두 번 실행** 될 수 있음 (정리 함수 점검 목적)
- 계산만 하는 값은 effect 대신 렌더링 중에 바로 계산

## 정리
- "렌더링 결과와 바깥 세계를 동기화"할 때 useEffect를 쓴다.
