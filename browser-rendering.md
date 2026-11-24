# 브라우저 렌더링 과정

## 1. 전체 흐름
1. **HTML 파싱 → DOM 트리** 생성
2. **CSS 파싱 → CSSOM 트리** 생성
3. DOM + CSSOM → **렌더 트리** (화면에 보이는 요소만)
4. **레이아웃(Layout/Reflow)**: 위치·크기 계산
5. **페인트(Paint)**: 색·글자·그림자 등 픽셀 그리기
6. **합성(Composite)**: 레이어를 합쳐 화면에 표시

## 2. 렌더 트리 특징
- `display: none` → 렌더 트리에서 제외
- `visibility: hidden` → 공간은 차지(렌더 트리에 포함)

## 3. Reflow vs Repaint
| 구분 | 발생 원인 | 비용 |
|---|---|---|
| Reflow | width, height, margin, 요소 추가·삭제 | 큼 (레이아웃 재계산) |
| Repaint | color, background-color | 상대적으로 작음 |
| Composite만 | transform, opacity | 가장 작음 |

## 4. script 태그 위치
```html
<script src="app.js"></script>        <!-- HTML 파싱을 멈춤 -->
<script defer src="app.js"></script>  <!-- 파싱 후 순서대로 실행 -->
<script async src="ad.js"></script>   <!-- 다운로드 끝나는 즉시 실행 -->
```
- Vite의 `type="module"` 스크립트는 기본적으로 defer처럼 동작

## 5. 성능 팁
- 애니메이션은 `top/left` 대신 `transform` 사용
- 여러 번 스타일 변경 시 클래스 한 번에 교체

## 정리
- 화면 표시 = DOM + CSSOM → 레이아웃 → 페인트 → 합성
- Reflow를 줄이는 것이 렌더링 성능 개선의 기본
