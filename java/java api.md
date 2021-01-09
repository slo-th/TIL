# Java api

## Optional

객체가 null이 될 수 있을 때 객체를 Optional로 감싸서 사용한다. 코드 가독성 향상 등의 효과가 있음.

|method|동작|
|---|---|
| `of()` | null을 허용하지 않음, NullPointerException 발생|
| `ofNullable()` | null을 허용함|
객체 생성 메소드

|method|값이 없을 때 동작|
|---|---|
`orElse()` | 인수로 전달된 값을 반환
`orElseGet()` | 인수로 전달된 람다식의 리턴값 반환
`orElseThrow()` | 인수로 전달된 예외 발생
값 반환 메소드, 모두 값이 존재하면 그 값을 반환한다.

## Stream

method|동작
---|---
`forEach()`|해당 스트림의 요소를 하나씩 소모하며 순차적으로 요소에 접근
`filter()`|필터링, 조건에 맞지 않는 요소를 걸러냄
`map()`|스트림의 요소마다 연산을 수행함

등등.. 아직 모르는게 많다.
