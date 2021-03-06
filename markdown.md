# md문법

## 코드

`(백틱) 을 사용  
1개로 감싸면 인라인. 3개로 감싸면 블록  
3개 뒤에 언어를 적을 수 있다

## 헤더

```md
# h1
## h2
### h3
#### h4
##### h5
###### h6
```

# h1
## h2
### h3
#### h4
##### h5
###### h6

## 리스트

```md
1. a
2. b
    1. bb
    - bbb
1. c
* d
+ e
```

1. a
2. b
    1. bb
    - bbb
1. c
* d
+ e

## 강조

```md
**bold**, *italic*, ***bold+italic***, ~~Strikethrough~~, <u>underline</u>
```

**bold**, *italic*, ***bold+italic***, ~~Strikethrough~~, <u>underline</u>

## 링크

```md
[Google](https://google.com)

[linux.md](./linux.md)

[naver][label]

https://youtube.com

[label]: https://naver.com "description"
```

[Google](https://google.com)

[linux.md](./linux.md)

[naver][label]

https://youtube.com

[label]: https://naver.com "description"

## 이미지

```md
![대체 텍스트](url)
```

## 이미지에 링크

```md
[![대체 텍스트](img url)](url)
```

## 표

```md
열1 | 열2 | 열3 
:---|:---:|---:
왼쪽 정렬||오른쪽 정렬
||가운데 정렬||
a|b|c
```

열1 | 열2 | 열3
:---|:---:|---:
왼쪽 정렬||오른쪽 정렬
||가운데 정렬||
a|b|c

## 인용문

```md
> blablabla
>>blabla2
>>blabla3
>>>bla4
```

> blablabla
>>blabla2
>>blabla3
>>>bla4

## 수평선

```md
--- (대시)
*** (별)
___ (언더바)
```

---
***
___

## 줄바꿈

```md
space 두번  
blabla
```

space 두번  
blabla

## 목차

```md
[코드](#코드)
<!-- 공백은 -(대시) , 대문자는 소문자로 작성 -->
```

[코드](#코드)
