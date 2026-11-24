# CSS Flexbox 정리

## 1. 기본 개념
- **1차원(한 방향)** 정렬 레이아웃
- 부모 = **flex container**, 자식 = **flex item**
```css
.container { display: flex; }
```

## 2. 축(Axis)
- **주축(main axis)**: `flex-direction` 방향 (기본: 가로 row)
- **교차축(cross axis)**: 주축과 수직

## 3. 부모(container) 속성
| 속성 | 역할 | 주요 값 |
|---|---|---|
| flex-direction | 주축 방향 | row, column |
| justify-content | 주축 정렬 | flex-start, center, space-between, space-around |
| align-items | 교차축 정렬 | stretch, center, flex-start |
| flex-wrap | 줄바꿈 | nowrap, wrap |
| gap | 아이템 간격 | 10px |

## 4. 자식(item) 속성
| 속성 | 역할 |
|---|---|
| flex-grow | 남는 공간을 차지하는 비율 |
| flex-shrink | 공간 부족 시 줄어드는 비율 |
| flex-basis | 기본 크기 |
| flex: 1 | grow 1, shrink 1, basis 0% 축약 |
| align-self | 해당 아이템만 교차축 정렬 |

## 5. 자주 쓰는 패턴
```css
/* 가운데 정렬 */
.center { display: flex; justify-content: center; align-items: center; }

/* 양 끝 배치 (헤더) */
.header { display: flex; justify-content: space-between; align-items: center; }

/* 사이드바 + 본문 */
.layout { display: flex; }
.sidebar { width: 240px; flex-shrink: 0; }
.main { flex: 1; min-width: 0; }
```

## 정리
- 한 줄 정렬은 Flexbox, 행·열 격자는 Grid
- `min-width: 0`은 긴 내용 때문에 flex item이 넘치는 문제를 막는다.
