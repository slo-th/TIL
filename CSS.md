# CSS Cascading Style Sheet

## display

### inline

- width, height 속성이 없음

### block

- 옆에 아무 것도 올 수 없음

### inline-block

- 반응형 디자인을 지원하지 않음 -> 쓰지 말자

### flexbox

- 자식에게 명시하지 않고 부모에게 명시함
  - 부모에 display:flex 명시하여 flex container로 만듦
- justify-content : main axis(default: horizontal)에 적용
  - flex-start
  - center
  - flex-end
  - space-between
  - space-around
  - space-evenly
- align-items : cross axis(default: vertical)에 적용
  - flex-start
  - center
  - flex-end
- flex-direction
  - row(default) : main-수평, cross-수직
  - column : main, cross axis 전환
- flex-wrap
  - wrap: 겹치지 않게 함
  - nowrap: 겹칠 수 있음(default)

## properties

- margin
- padding
- opacity : 투명도

### margin

> border의 바깥

- 값이 1개: 모든 방향
- 값이 2개: 상하 / 좌우
- 값이 3개: 상 / 우 / 하 / 좌 (시계방향)

Collapsing margin:
두 block의 border가 만나면 두 block의 Margin이 하나가 됨. Top, Bottom에서 발생

### padding

> border의 안쪽

### position

- fixed : 레이어를 변경 또는 위치를 고정(스크롤 해도 그 자리에 있음)
- relative: element가 처음 위치한 곳을 기준으로 위치를 정함
  - top, left, bottom, right
- absolute: relative 부모를 기준으로 위치를 정함
- static(default)

## selector

| selector              | 의미                          |
| --------------------- | ----------------------------- |
| NAME                  | tag                           |
| `#`                   | id                            |
| `.`                   | class                         |
| `a b`                 | a의 자손 b                    |
| `a > b`               | a의 자식 b                    |
| `a + b`               | a의 바로 다음 형제 b          |
| `a ~ b`               | a의 다음 형제 b               |
| `:nth-child(n)`       | n번째 자식                    |
| `:first-child`        | 첫번째 자식                   |
| `:last-child`         | 마지막 자식                   |
| `NAME[ATTR="VALUE"]`  | ATTR="VALUE"인 tag            |
| `NAME[ATTR~="VALUE"]` | ATTR에 "VALUE"를 포함하는 tag |
