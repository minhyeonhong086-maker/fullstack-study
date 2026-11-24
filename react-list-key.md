# React 리스트 렌더링과 key

## 1. 배열을 화면에 그리기
```jsx
const fruits = ['사과', '바나나', '포도'];

<ul>
  {fruits.map((fruit) => (
    <li key={fruit}>{fruit}</li>
  ))}
</ul>
```
- `map()`으로 배열의 각 항목을 JSX로 바꾼다.

## 2. key가 필요한 이유
- React는 리스트가 바뀌었을 때 **어떤 항목이 추가·삭제·이동했는지** key로 구분한다.
- key가 없으면 콘솔에 경고가 나오고, 불필요하게 다시 그리거나 상태가 엉뚱한 항목에 붙을 수 있다.

## 3. 좋은 key
| key | 평가 |
|---|---|
| DB id, `crypto.randomUUID()`로 만든 id | ✅ 고유하고 변하지 않음 |
| 배열 index | ⚠️ 순서가 바뀌거나 중간 삭제가 있으면 문제 |
| `Math.random()` | ❌ 렌더링마다 바뀜 |

## 4. index key의 문제 예시
- 입력창이 있는 목록에서 첫 번째 항목을 삭제하면, 두 번째 항목의 입력값이 첫 번째 자리에 남는 현상이 생길 수 있다.

## 5. 객체 배열 렌더링
```jsx
{todos.map((todo) => (
  <TodoItem key={todo.id} todo={todo} onDelete={handleDelete} />
))}
```
- key는 컴포넌트에 props로 전달되지 않는다. 필요하면 `id`를 따로 넘긴다.

## 6. 조건 + 리스트
```jsx
{todos.length === 0 ? <p>할 일이 없습니다.</p> : <ul>{/* map */}</ul>}
```

## 정리
- 리스트에는 **고유하고 안정적인 key** 를 준다.
- key는 형제 사이에서만 고유하면 된다.
