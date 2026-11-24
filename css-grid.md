# CSS Grid 정리

## 1. 기본 개념
- **2차원(행 + 열)** 레이아웃
```css
.grid { display: grid; }
```

## 2. 열·행 정의
```css
.grid {
  display: grid;
  grid-template-columns: 200px 1fr 1fr; /* 고정 1개 + 남는 공간 2등분 */
  grid-template-rows: auto;
  gap: 20px;
}
```
- **fr**: 남은 공간을 나누는 비율 단위
- `repeat(4, 1fr)` = `1fr 1fr 1fr 1fr`

## 3. 반응형 카드 목록
```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
  gap: 16px;
}
```
- 화면 폭에 맞춰 열 개수가 자동으로 바뀜 (미디어 쿼리 없이 가능)

## 4. 아이템 위치 지정
```css
.wide { grid-column: span 2; }        /* 2칸 차지 */
.full { grid-column: 1 / -1; }        /* 처음부터 끝까지 */
```

## 5. grid-template-areas
```css
.page {
  display: grid;
  grid-template-columns: 240px 1fr;
  grid-template-areas:
    "side header"
    "side main";
}
.sidebar { grid-area: side; }
header   { grid-area: header; }
main     { grid-area: main; }
```

## 6. auto-fill vs auto-fit
- auto-fill: 빈 칸을 유지
- auto-fit: 빈 칸을 접고 아이템을 늘림

## 정리
- 대시보드 카드 배치처럼 행과 열이 함께 필요한 화면은 Grid가 편하다.
