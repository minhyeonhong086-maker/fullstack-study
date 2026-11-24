# React 폼 처리 (제어 컴포넌트)

## 1. 제어 컴포넌트란?
- 입력창의 값을 **React state가 관리** 하는 방식
```jsx
const [name, setName] = useState('');

<input value={name} onChange={(e) => setName(e.target.value)} />
```
- 화면의 값 = state의 값 → 항상 일치

## 2. 여러 입력을 객체 하나로 관리
```jsx
const [form, setForm] = useState({ email: '', password: '' });

const handleChange = (e) => {
  const { name, value } = e.target;
  setForm((prev) => ({ ...prev, [name]: value }));
};

<input name="email" value={form.email} onChange={handleChange} />
<input name="password" type="password" value={form.password} onChange={handleChange} />
```
- `[name]`: 계산된 속성 이름 → input의 name과 같은 키를 수정

## 3. 제출 처리
```jsx
const handleSubmit = (e) => {
  e.preventDefault();               // 페이지 새로고침 막기
  if (!form.email.includes('@')) {
    setError('이메일 형식이 올바르지 않습니다.');
    return;
  }
  // 저장 또는 API 요청
};

<form onSubmit={handleSubmit}> ... <button type="submit">저장</button></form>
```

## 4. 입력 종류별 값
| 입력 | 읽는 값 |
|---|---|
| text, number, date | `e.target.value` (number도 **문자열**) |
| checkbox | `e.target.checked` |
| select | `e.target.value` |

- 숫자 입력은 `Number(value)`로 변환 후 검증

## 5. 비제어 컴포넌트
- `useRef`로 DOM 값을 직접 읽는 방식. 파일 업로드 등에 사용

## 정리
- 입력값 검증·초기화·조건부 버튼 활성화가 필요하면 제어 컴포넌트가 편하다.
