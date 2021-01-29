# HTTP (HyperText Transfer Protocol)

- 거의 모든 형태의 데이터를 전송 가능
- 서버간 통신에도 사용

## 목차 <!-- omit in toc -->

- [1. HTTP 버전](#1-http-버전)
- [2. HTTP의 특징](#2-http의-특징)
  - [2.1. 무상태](#21-무상태)
  - [2.2. 비연결성](#22-비연결성)
- [3. HTTP 메시지](#3-http-메시지)
  - [3.1. start-line](#31-start-line)
    - [3.1.1. request-line (request)](#311-request-line-request)
    - [3.1.2. status-line (response)](#312-status-line-response)
  - [3.2. header](#32-header)
  - [3.3. empty line](#33-empty-line)
  - [3.4. message body](#34-message-body)
- [4. HTTP method](#4-http-method)
- [5. HTTP method의 속성](#5-http-method의-속성)
- [6. HTTP STATUS CODE](#6-http-status-code)
  - [6.1. 1xx Informational](#61-1xx-informational)
  - [6.2. 2xx Successful](#62-2xx-successful)
  - [6.3. 3xx Redirection](#63-3xx-redirection)
    - [6.3.1. PRG Post/Redirect/Get](#631-prg-postredirectget)
  - [6.4. 4xx Client Error](#64-4xx-client-error)
  - [6.5. 5xx Server Error](#65-5xx-server-error)
- [7. HTTP Header](#7-http-header)
  - [7.1. Representation Header](#71-representation-header)
  - [7.2. Negotiation Header](#72-negotiation-header)
    - [7.2.1. 우선 순위 Quality Values(q)](#721-우선-순위-quality-valuesq)
  - [7.3. 전송 방식](#73-전송-방식)
  - [7.4. 일반 정보 헤더](#74-일반-정보-헤더)
  - [7.5. 특별 정보 헤더](#75-특별-정보-헤더)
  - [7.6. 인증 헤더](#76-인증-헤더)
  - [7.7. 쿠키 헤더](#77-쿠키-헤더)
  - [7.8. 캐시](#78-캐시)
    - [7.8.1. 검증, 조건부 요청 헤더](#781-검증-조건부-요청-헤더)
    - [7.8.2. 프록시 캐시](#782-프록시-캐시)
    - [7.8.3. 캐시 무효화](#783-캐시-무효화)

## 1. HTTP 버전

1. HTTP/0.9
2. HTTP/1.0
3. HTTP/1.1 (1997)
   1. 가장 많이 사용
   2. RFC2068(1997) --> RFC2616(1999) --> RFC7230~7235(2014)
4. HTTP/2 (2015)
   1. 성능개선
5. HTTP/3 (진행중)
   1. UDP 사용, 성능 개선

## 2. HTTP의 특징

### 2.1. 무상태

- 서버가 클라이언트의 상태를 보존하지 않음

#### 장점 <!-- omit in toc -->

서버 확장성 높음

> 요청마다 필요한 데이터를 모두 전송해야함 -> 응답 서버가 바뀌어도 됨

#### 단점 <!-- omit in toc -->

클라이언트가 추가 데이터 전송

### 2.2. 비연결성

- 응답후에 연결을 종료

#### 장점 <!-- omit in toc -->

서버 자원을 효율적으로 사용

#### 단점 <!-- omit in toc -->

- html, css, js, 리소스 파일 등을 요청시마다 연결
- TCP/IP 연결을 새로 맺어야 함
  - 3 way handshake 시간 추가

> 현재는 지속 연결(Persistent Connections)로 문제 해결  
> HTTP/2, HTTP/3에서 많은 최적화가 이루어짐

## 3. HTTP 메시지

### 3.1. start-line

#### 3.1.1. request-line (request)

`GET /search?q=hello&hl=ko HTTP/1.1`  
method 공백 request-target 공백 HTTP-version 줄바꿈

- method: HTTP 메서드
- request-target: /search?q=hello&hl=ko
  - 절대경로로 시작
- HTTP version: HTTP/1.1

#### 3.1.2. status-line (response)

`HTTP/1.1 200 OK`  
HTTP-version 공백 status-code 공백 reason-phrase 줄바꿈

- HTTP version
- HTTP status code
- 이유 문구: 사람이 이해할 수 있는 상태코드 짧은 설명

### 3.2. header

field-name:[공백]field-value[공백]  
field-name은 대소문자 구분하지 않음

- HTTP 전송에 필요한 모든 부가 정보
- 필요 시 임의 헤더 추가 가능

### 3.3. empty line

### 3.4. message body

- 실제 전송할 데이터. byte로 표현가능한 모든 데이터 전송 가능

## 4. HTTP method

| method | 행동                       | 기타                                            |
| ------ | -------------------------- | ----------------------------------------------- |
| GET    | 리소스 조회                | 데이터를 query parameter(string)로 전달         |
| POST   | 요청 데이터 처리           | 데이터를 message body로 전달                    |
| PUT    | 리소스 등록, 대체          | 리소스가 있으면 덮어씀. 클라이언트가 URI를 지정 |
| PATCH  | 리소스 수정                |
| DELETE | 리소스 삭제                |
| HEAD   | start-line과 header만 받음 |

> html form에선 GET, POST만 사용 가능

## 5. HTTP method의 속성

| 속성                | 의미                            | 기타            |
| ------------------- | ------------------------------- | --------------- |
| 안전(Safe)          | 호출해도 리소스를 변경하지 않음 |
| 멱등(Idempotent)    | 몇 번을 호출해도 결과가 같음    | GET POST DELETE |
| 캐시가능(Cacheable) | 응답 결과를 캐시할 수 있음      | GET HEAD        |

## 6. HTTP STATUS CODE

### 6.1. 1xx Informational

### 6.2. 2xx Successful

| CODE           | 의미                                 | 기타               |
| -------------- | ------------------------------------ | ------------------ |
| 200 OK         | 성공                                 |
| 201 Created    | 요청 성공해서 새로운 리소스가 생성됨 | Location 헤더 전송 |
| 202 Accepted   | 요청 접수, 처리 미완                 |
| 204 No Content | 요청 성공, 본문에 보낼 데이터가 없음 |

### 6.3. 3xx Redirection

웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, 자동으로 Redirect함

| CODE                   | 의미                                                                       |
| ---------------------- | -------------------------------------------------------------------------- |
| **영구 이동**          | URI 영구 이동, 원래 URI 사용 안함. 검색엔진이 인지                         |
| 301 Moved Permanently  | 메서드가 GET로 변경될 수도 있으며, 본문이 제거될 수도 있음                 |
| 308 Permanent Redirect | 메서드와 본문 유지                                                         |
| ---                    | ---                                                                        |
| **일시 이동**          | URI 일시적 변경, 검색엔진이 URL을 변경하지 않음                            |
| 302 Found              | 메서드가 GET으로 변경될 수도 있으며, 본문이 제거될 수도 있음               |
| 303 See other          | 메서드가 GET으로 변경됨                                                    |
| 307 Temporary Redirect | 메서드와 본문 유지                                                         |
| ---                    | ---                                                                        |
| 304 Not Modified       | 리소스가 수정되지 않음, message body를 포함하지 않음, GET HEAD 요청에 사용 |

#### 6.3.1. PRG Post/Redirect/Get

POST로 주문 후에 새로고침 -> 다시 요청 -> 중복 주문 발생

1. POST로 주문 후 결과화면을 GET으로 redirect
2. 새로고침 해도 결과화면만 나옴

### 6.4. 4xx Client Error

| CODE             | 의미                                                                                                        |
| ---------------- | ----------------------------------------------------------------------------------------------------------- |
| 400 Bad Request  | 잘못된 요청                                                                                                 |
| 401 Unauthorized | 클라이언트가 해당 리소스에 대한 인증(Authentication)이 필요함, WWW-Authenticate헤더와 함께 인증 방법을 설명 |
| 403 Forbidden    | 요청을 이해했지만 승인을 거부(권한 불충분)                                                                  |
| 404 Not Found    | 요청 리소스가 서버에 없음, 또는 리소스를 숨기고 싶음                                                        |

> 인증 Authentication: 본인 확인(로그인)  
> 인가 Authorization: 권한

### 6.5. 5xx Server Error

| CODE                    | 의미                                                            |
| ----------------------- | --------------------------------------------------------------- |
| 503 Service Unavailable | 서비스 이용 불가, Retry-After 헤더로 복구 시각을 전달할 수 있음 |

## 7. HTTP Header

| HEADER         | 의미                                     | 예시                        |
| -------------- | ---------------------------------------- | --------------------------- |
| General        | 메시지 전체에 적용되는 정보              | Connection: close           |
| Request        | 요청 정보                                | User-Agent:...              |
| Response       | 응답 정보                                | Server: Apache              |
| Representation | 전달할 실제 데이터를 해석할 수 있는 정보 | Content-Type: text/html;... |
| Negotiation    | 클라이언트가 선호하는 표현 정보          | Accept                      |

### 7.1. Representation Header

| field-name       | 의미                    | 예시                                                 |
| ---------------- | ----------------------- | ---------------------------------------------------- |
| Content-Type     | 표현 데이터의 형식      | text/html;charset=utf-8, application/json, image/png |
| Content-Encoding | 표현 데이터의 압축 방식 | gzip, deflate, identity(무압축)                      |
| Content-Language | 표현 데이터의 자연 언어 | ko, en, en-US                                        |
| Content-Length   | 표현 데이터의 길이      |

### 7.2. Negotiation Header

| field-name      | 의미                              |
| --------------- | --------------------------------- |
| Accept          | 클라이언트가 선호하는 미디어 타입 |
| Accept-Charset  | 클라이언트가 선호하는 미디어 타입 |
| Accept-Encoding | 클라이언트가 선호하는 압축 인코딩 |
| Accept-Language | 클라이언트가 선호하는 자연 언어   |

> 요청에만 사용

#### 7.2.1. 우선 순위 Quality Values(q)

1. 0~1, 클수록 높은 우선순위
   - 생략=1
   - `Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7`
2. 구체적인 것이 높은 우선순위
   - `Accept: text/*, text/plain, text/plain;format=flowed, */*`
   1. `text/plain;format=flowed`
   2. `text/plain`
   3. `text/*`
   4. `*/*`
3. 미디어 타입
   - `Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1, text/html;level=2;q=0.4, */*;q=0.5`

| Media Type        | Quality |
| ----------------- | ------- |
| text/html;level=1 | 1       |
| text/html         | 0.7     |
| text/plain        | 0.3     |
| image/jpeg        | 0.5     |
| text/html;level=2 | 0.4     |
| text/html;level=3 | 0.7     |

### 7.3. 전송 방식

1. 단순 전송: Content-Length
2. 압축 전송: Content-Length + Content-Encoding
3. 분할 전송: Transfer-Encoding: chunked
4. 범위 전송: Range(request), Content-Range(response)

### 7.4. 일반 정보 헤더

- From
  - 유저 에이전트의 이메일
  - 잘 안씀, 검색 엔진에서 주로 사용
  - request에서 사용
- Referer
  - 요청된 페이지의 이전 페이지 주소
  - 요청에서 사용
  - referrer의 오타
- User-Agent
  - 클라이언트의 애플리케이션 정보
  - 요청에서 사용
   Server
  - 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
  - 응답에서 사용
- Date
  - 메시지가 발생한 날짜와 시간
  - 응답에서 사용

### 7.5. 특별 정보 헤더

- Host
  - 요청한 호스트 정보(도메인)
  - 요청에서 사용, 필수
  - 하나의 IP 주소에 여러 도메인이 적용되어 있을 때
- Location
  - 페이지 리다이렉션
  - 응답에서 사용
- Allow
  - 허용 가능한 HTTP 메서드 종류
  - 405 Method Not Allowed에서 사용
- Retry-After
  - 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
  - 503 Service Unavailable에서 사용
  - 날짜, 초단위 표기 가능

### 7.6. 인증 헤더

- Authorization
  - 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate
  - 리소스 접근시 필요한 인증 방법 정의
  - 401 Unauthorized에 사용

### 7.7. 쿠키 헤더

- Set-Cookie
  - 서버에서 클라이언트로 쿠키 전달
  - sessionId
  - expires, max-age
  - path
  - domain
  - Secure, HttpOnly, SameSite
- Cookie
  - 클라이언트가 서버에서 받은 쿠키를 저장, 요청 시 서버로 전달

### 7.8. 캐시

- cache-control
  - 캐시 제어
  - max-age
    - 유효 시간, 초 단위
  - no-cache
    - 캐시해도 되지만, 항상 ORIGIN 서버에 검증 후 사용
  - no-store
    - 캐시하면 안됨

#### 7.8.1. 검증, 조건부 요청 헤더

- Last-Modified
  - 응답
  - UTC 시간 사용
- if-modified-since
  - 요청
  - UTC 시간 사용  
- ETag
  - 응답
  - 캐시의 데이터에 이름을 붙임
- If-None-Match
  - 요청
  - 이름
  
> ETag는 캐시 제어 로직을 서버에서 관리

수정되지 않았으면 `304 Not Modified` 응답, 수정되었으면 `200 OK + 데이터` 응답

#### 7.8.2. 프록시 캐시

- 프록시 캐시 서버에 캐시를 저장
- Cache-Control
  - public: 응답이 public(프록시 캐시 서버) 캐시에 저장되어도 됨
  - private: 응답이 사용자만을 위한 것, private(클라이언트) 캐시에 저장
  - s-maxage: 프록시 캐시에 적용되는 max-age
- Age: ORIGIN 서버에서 응답 후 프록시 캐시 내에 머문 시간(초)

#### 7.8.3. 캐시 무효화

- Cache-Control: no-cache, no-store, must-revalidate
  - must-revalidate
    - ORIGIN 서버 접근 실패시 오류 발생 - 504 Gateway Timeout
    - 캐시 만료 후 조회 시 ORIGIN 서버에서 검증해야함
    - 만료 전이라면 캐시를 사용 -> no-store
- Pragma: no-cache
  - HTTP 1.0 하위 호환
