# HTTP

## 1. 목차

- [1. 목차](#1-목차)
- [2. IP 스택 계층](#2-ip-스택-계층)
  - [2.1. 전달 과정](#21-전달-과정)
- [3. IP (Internet Protocol)](#3-ip-internet-protocol)
  - [3.1. IP 패킷 내용](#31-ip-패킷-내용)
  - [3.2. IP의 한계](#32-ip의-한계)
- [4. TCP(Transmission Control Protocol)](#4-tcptransmission-control-protocol)
  - [4.1. TCP 3 way handshake](#41-tcp-3-way-handshake)
  - [4.2. 데이터 전달 보증](#42-데이터-전달-보증)
  - [4.3. 순서 보장](#43-순서-보장)
- [5. UDP(User Datagram Protocol)](#5-udpuser-datagram-protocol)
- [6. PORT](#6-port)
- [7. DNS(Domain Name System)](#7-dnsdomain-name-system)
- [8. URI(Uniform Resource Identifier)](#8-uriuniform-resource-identifier)
- [9. URL 문법](#9-url-문법)
- [웹 통신 흐름](#웹-통신-흐름)

## 2. IP 스택 계층

1. 어플리케이션 계층 : HTTP, FTP
2. 전송 계층 : TCP, UDP
3. 인터넷 계층 : IP
4. 네트워크 인터페이스 계층

### 2.1. 전달 과정

1. 프로그램에서 Hello, World 메세지 생성
2. SOCKET 라이브러리를 통해서 OS로 전달
3. TCP 정보 생성(syn, syn+ack, ack), IP 패킷 생성, 데이터 포함해서 네트워크 인터페이스로 전달
4. Ethernet frame 씌워서 목적지로 전달

## 3. IP (Internet Protocol)

- 지정된 IP Address로 데이터 전달
- 패킷(Packet)이라는 통신 단위로 전달

### 3.1. IP 패킷 내용

- 출발지, 목적지 IP Address
- 전송 데이터
- 기타...

### 3.2. IP의 한계

- 비연결성
  - 패킷을 받을 대상이 없거나, 서비스 불능 상태에도 전송
- 비신뢰성
  - 패킷 손실
  - 패킷 순서 변경
- 프로그램 구분
  - 같은 IP를 사용하는 서버에서 통신하는 어플이 둘 이상일 때 구분 못함

## 4. TCP(Transmission Control Protocol)

- 연결지향 : TCP 3 way handshake(가상 연결)
- 데이터 전달 보증
- 순서 보장
- 신뢰할 수 있는 프로토콜

> 현재는 대부분 TCP를 사용

### 4.1. TCP 3 way handshake

- syn: 접속 요청
- ack: 요청 수락

1. client -> server: **syn**
2. server -> client: **syn + ack**
3. client -> server: **ack**
4. 데이터 전송

> 3번 과정과 함께 데이터 전송이 가능

### 4.2. 데이터 전달 보증

1. client -> server: 데이터 전송
2. server -> client: 데이터 받았음

### 4.3. 순서 보장

1. client -> server: 패킷1 2 3 순서로 전송
2. server: 패킷1 3 2 순서로 받음
3. server -> client: 패킷2 부터 다시 전송하라고 전달

## 5. UDP(User Datagram Protocol)

- IP + PORT + 체크섬 정도만 추가됨
- 단순하고 빠름

## 6. PORT

- 같은 IP 에서 프로세스를 구분
- 이 정보가 TCP, UDP에 들어있음
- 0 ~ 65535 할당 가능
  - 0 ~ 1023 : 잘 알려진 포트(well-known port)
    - 20, 21 : FTP
    - 22 : SSH
    - 80 : HTTP
    - 443 : HTTPS
  - 1024 ~ 49151 : 등록된 포트(registered port)
  - 49152 ~ 65535 : 동적 포트(dynamic port)

## 7. DNS(Domain Name System)

- IP는 기억하기 어렵고, 변경될 수 있다.
- 그래서 Domain Name을 IP주소로 변환해주는 시스템이 생겼다.

> domain: google.com -> ip: 172.217.161.78

## 8. URI(Uniform Resource Identifier)

- Uniform: 리소스를 식별하는 통일된 방식
- Resource: 자원. URI로 식별할 수 있는 모든 것
- Identifier: 다른 항목과 구분하는데 필요한 정보
- URI 안에 URL(Locator), URN(Name)이 있음

## 9. URL 문법

`scheme://[userinfo@]host[:port][/path][?query][#fragment]`

### 9.1. scheme <!-- omit in toc -->

- 주로 프로토콜 사용
  - 자원에 접근하는 방식을 규정
  - http, https, ftp 등

### 9.2. userinfo <!-- omit in toc -->

- 사용자 정보

> 거의 사용하지 않음

### 9.3. host <!-- omit in toc -->

- 호스트명
- 도메인명 또는 IP Address

### 9.4. port <!-- omit in toc -->

- http: 80, https: 443
- 생략 가능

### 9.5. path <!-- omit in toc -->

- 리소스 경로

### 9.6. query <!-- omit in toc -->

- `?`로 시작
- `&`로 추가
- `key=value` 형태

### 9.7. fragment <!-- omit in toc -->

- html 북마크 등에 사용(id로 북마크 가능)
- 서버에 전송되지 않음

## 웹 통신 흐름

1. `https://www.google.com/search?q=hello&hl=ko` URL로 요청
   1. DNS 조회
   2. PORT 443 생략
2. HTTP 요청 메세지 생성
   1. `GET /search?q=hello&hl=ko HTTP/1.1 Host: www.google.com`
3. 스택 계층을 통해서 전송
4. 도착
   1. TCP/IP 패킷을 까서 버림
5. HTTP 응답 메세지 생성
6. 전송
7. 도착
8. 웹 브라우저가 도착한 HTML을 렌더링
