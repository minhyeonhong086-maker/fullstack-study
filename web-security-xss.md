# XSS(Cross-Site Scripting)와 대응

## 1. XSS란?
- 공격자가 웹 페이지에 **악성 스크립트를 넣어** 다른 사용자의 브라우저에서 실행시키는 공격
- 쿠키·토큰 탈취, 화면 조작, 원치 않는 요청 전송 등이 가능

## 2. 종류
| 종류 | 설명 |
|---|---|
| 저장형(Stored) | 게시글·댓글에 스크립트를 저장 → 보는 사람마다 실행 |
| 반사형(Reflected) | URL 파라미터 값이 그대로 화면에 출력되며 실행 |
| DOM 기반 | 클라이언트 JS가 입력값을 DOM에 그대로 넣으며 발생 |

## 3. 취약한 코드
```js
// 사용자 입력을 HTML로 그대로 삽입
comment.innerHTML = userInput;
```
- 입력값이 `<img src=x onerror="...">` 같은 형태면 스크립트 실행

## 4. 대응 방법
1. **출력 시 이스케이프**: `<` → `&lt;`, `>` → `&gt;`
2. 텍스트는 `textContent` 사용
```js
comment.textContent = userInput;  // 태그가 글자로만 표시됨
```
3. HTML 허용이 꼭 필요하면 **DOMPurify** 같은 라이브러리로 정제(sanitize)
4. 쿠키에 **HttpOnly** → 스크립트에서 쿠키 읽기 차단
5. **CSP(Content-Security-Policy)** 헤더로 실행 가능한 스크립트 출처 제한

## 5. React에서는?
- JSX의 `{value}`는 **자동 이스케이프** → 기본적으로 안전
- `dangerouslySetInnerHTML` 사용 시에는 반드시 정제 후 사용
- `href={userUrl}`에 `javascript:` 링크가 들어가지 않도록 검증

## 정리
- "사용자 입력은 믿지 않는다" → 입력 검증 + 출력 이스케이프
