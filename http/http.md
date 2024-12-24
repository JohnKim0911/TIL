# 모든 개발자를 위한 HTTP 웹 기본 지식

- 김영한의 스프링 완전 정복 로드맵
    - 3편) 모든 개발자를 위한 HTTP 웹 기본 지식


## 0. 목차

|    | 제목                                                | 강의 분량     | 교재 분량<br>(PPT 페이지) | 학습일                        |
|----|---------------------------------------------------|-----------|--------------------|----------------------------|
| 1  | [소개](#1-소개)                                       | 7분        | 0                  | 2024.12.23 (월)             |
| 2  | [인터넷 네트워크](#2-인터넷-네트워크)                           | 30분       | 46                 | 2024.12.23 (월) ~ 12.24 (화) |
| 3  | [URI와 웹 브라우저 요청 흐름](#3-uri와-웹-브라우저-요청-흐름)         | 16분       | 30                 | 2024.12.24 (화)             |
| 4  | [HTTP 기본](#4-http-기본)                             | 39분       |                    |                            |
| 5  | [HTTP 메서드](#5-http-메서드)                           | 35분       |                    |                            |
| 6  | [HTTP 메서드 활용](#6-http-메서드-활용)                     | 47분       |                    |                            |
| 7  | [HTTP 상태코드](#7-http-상태코드)                         | 43분       |                    |                            |
| 8  | [HTTP 헤더1 - 일반 헤더](#8-http-헤더1---일반-헤더)           | 52분       |                    |                            |
| 9  | [HTTP 헤더2 - 캐시와 조건부 요청](#9-http-헤더2---캐시와-조건부-요청) | 42분       |                    |                            |
| 10 | [다음으로](#10-다음으로)                                  | 25분       |                    |                            |
|    |                                                   | 총 5시간 40분 | 총 335 페이지          | 2024.12.23 (월) ~           |

### 참고

- 이 글의 목적
  - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
    - 제 기억을 살리기 위한 용도이다보니, 아래 글만으로는 이해가 어려울 수 있습니다.
      - 필요하시다면, 강의를 직접 수강하시는 것을 추천드립니다. (링크는 아래 `1.소개`에 있음)
    - 복습 방식:
      - 강의듣고, 끝나면 다시 교재를 보면서 중요 내용 위주로 정리하였습니다.

- 참고
  - 유료 강의이므로, 전체 PPT 수업 자료는 공유하지 않습니다.
    - 수업에서 사용한 PPT 이미지를 첨부하는게 이해하는데 훨씬 도움이 되지만, 
    - 강사님께서 한땀한땀 그리신것을 무단으로 배포하면 안될 것 같아서 이 글엔 최대한 안쓰려고 노력했습니다.
  - 이론 강의 입니다. 코드를 별도로 치진 않았습니다.


## 1. 소개

- 강의 소개 페이지 (인프런): https://inf.run/8ZEU8

## 2. 인터넷 네트워크

### ✔️ 인터넷 통신

- 인터넷에서 컴퓨터 둘은 어떻게 통신할까?
  - 복잡한 인터넷 망의 여러 노드를 거쳐서 통신한다.
  - 우선 IP에 대해 알아야 한다.

### ✔️ IP (인터넷 프로토콜)

- `인터넷 프로토콜` 역할
  - 지정한 IP 주소에 데이터 전달
  - 패킷(Packet)이라는 통신 단위로 데이터 전달

- IP `패킷 정보`
  - `출발지 IP`, `목적지 IP`, 기타... 포함.
  - `전송데이터`를 감싸고 있다.

> 참고) 패킷의 어원: 소포를 뜻하는 패키지(package)와 덩어리를 뜻하는 버킷(bucket)의 합성어.

- IP 프로토콜의 `한계`
  - `비연결성` : 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
  - `비신뢰성` : 중간에 패킷이 소실되거나, 패킷의 순서가 바뀔 수 있다.
  - `프로그램 구분` : 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 둘 이상이면 구별 할 수 없다.

### ✔️ TCP, UDP

- 인터넷 프로토콜 스택의 4계층
  - `애플리케이션 계층`: HTTP, FTP
  - `전송 계층`: TCP, UDP
  - `인터넷 계층`: IP
  - `네트워크 인터페이스 계층`

- 프로토콜 계층

  ![프로토콜 계층1](https://github.com/user-attachments/assets/c3dbb09d-ffb0-4ff5-8307-033a3cf861f4)
  
  ![프로토콜 계층2](https://github.com/user-attachments/assets/2b1d5d5b-1a13-415a-be8f-673f613e060b)

  - `TCP/IP 패킷` 정보
    - `IP 패킷` (바깥): 
      - `출발지 IP`, `목적지 IP`, `기타`... 포함.
    - `TCP 세그먼트` (내부):
      - `출발지 PORT`, `목적지 PORT`, `전송 제어`, `순서`, `검증 정보`... 포함.
      - `전송데이터`를 감싸고 있다.

- `TCP`: 전송 제어 프로토콜 (Transmission Control Protocol)

  - `TCP` 특징
    - 연결지향 - `TCP 3 way handshake` (가상 연결)
    - `데이터 전달 보증`
    - `순서 보장`
    - 신뢰할 수 있는 프로토콜
    - 현재는 대부분 TCP 사용

  - `TCP 3 way handshake` (connect, 연결과정)
    - 클라이언트 ➡️ 서버: `1. SYN` (접속 요청)
    - 클라이언트 ⬅️ 서버: `2. SYN + ACK` (요청 수락)
    - 클라이언트 ➡️ 서버: `3. ACK`
    - 클라이언트 ⬅️ 서버: `4. 데이터 전송`
    
  - `데이터 전달 보증`
    - 클라이언트 ➡️ 서버: `1. 데이터 전송`
    - 클라이언트 ⬅️ 서버: `2. 데이터 잘 받았음`
  
  - `순서 보장`
    - 클라이언트 : `1. 패킷1, 패킷2, 패킷3` 순서로 서버에 전송
    - ️서버: `2. 패킷1, 패킷3, 패킷2`순서로 도착
    - 서버 ➡️ 클라이언트: `3. 패킷2 부터 다시 보내~`

- `UDP`: 사용자 데이터그램 프로토콜 (User Datagram Protocol)
  - `UDP` 특징
    - 하얀 도화지에 비유 (기능이 거의 없음)
    - `연결지향 X` (TCP 3 way handshake X)
    - `데이터 전달 보증 X`
    - `순서 보장 X`
    - 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
    - 정리
      - `IP와 거의 같다.` + `PORT` + `체크섬 정도만 추가`
      - 애플리케이션에서 추가 작업 필요

> UDP가 최근 들어 뜨고있다. (여러 최적화가 가능하므로)

### ✔️ PORT

- 한번에 둘 이상 연결해야 하면?
  - 문제점
    - 클라이언트 1개가 서버 2개와 동시 연결시,
      - 예시)
        - `클라이언트` and `서버1`: 게임, 화상통화 진행
        - `클라이언트` and `서버2`: 웹 브라우저 요청
    - IP 만으로는 프로세스를 구별 할 수 없다.
  - 해결
    - `TCP/IP 패킷` 정보에는 `출발지 PORT`, `목적지 PORT` 정보를 보관한다.
    - `PORT`: 같은 IP 내에서 프로세스 구분
    - 예시)
      - 클라이언트
        - `PORT 8090`: 게임 (서버1과 연결)
        - `PORT 21000`: 화상통화 (서버1과 연결)
        - `PORT 10010`: 웹 브라우저 (서버2와 연결)
      - 서버 1
        - `PORT 11220` (클라이언트와 연결)
        - `PORT 32202` (클라이언트와 연결)
      - 서버 2
        - `PORT 80` (클라이언트와 연결)

- `PORT` 추가 설명
  - 0 ~ 65535 할당 가능
    - 0 ~ 1023: 잘 알려진 포트, 사용하지 않는 것이 좋음
    - FTP - 20, 21
    - TELNET - 23
    - HTTP - 80
    - HTTPS - 443

> 비유) IP가 아파트. PORT는 동, 호수

### ✔️ DNS

- IP의 문제점
  - IP는 기억하기 어렵다. (서버 IP가 뭐였더라?... 200.200.200.2 였나?...)
  - IP는 변경 될 수 있다. (과거: 200.200.200.2 ➡️ 신규: 200.200.200.3)

- `DNS`: 도메인 네임 시스템 (Domain Name System)
  - 전화번호부 같은 것.
  - 도메인 명을 IP 주소로 변환

- DNS 사용 예시
  - 1번) `클라이언트`가 도메인명 `google.com`을 입력.
  - 2번) `DNS 서버`가 해당 도메인명에 해당하는 `IP 주소`를 응답함. (`200.200.200.2`)
  - 3번) `클라이언트`가 해당 IP로 실제 `서버`에 `접속`함.

## 3. URI와 웹 브라우저 요청 흐름

### ✔️ URI

- `URI`는 `URL`, `URN`로 분류 될 수 있다.
  - `URI` (Uniform Resource `Identifier`)
    - `URL` (Uniform Resource `Locator`) // 위치
    - `URN` (Uniform Resource `Name`) // 이름
  
- `URL` vs `URN`
  - `URL`
    - 예) `foo`://`example.com:8042`/`over/there`?`name=ferret`#`nose`
      - scheme: `foo`
      - authority: `example.com:8042`
      - path: `over/there`
      - query: `name=ferret`
      - fragment: `nose`
  - `URN`
    - 예) `urn`:`example`:`animal`:`ferret`:`nose`
      - scheme: `foo`
      - path: `example:animal:ferret:nose`

- `URI` 단어 뜻
  - `U`niform: 리소스 식별하는 통일된 방식
  - `R`esource: 자원, `URI`로 식별할 수 있는 모든 것(제한 없음)
  - `I`dentier: 다른 항목과 구분하는데 필요한 정보
    - 예) 사람 - 주민등록번호

- `URL`, `URN` 단어 뜻
  - `URL` - Locator: 리소스가 있는 `위치`를 지정
  - `URN` - Name: 리소스에 `이름`을 부여
    - 예) urn:isbn:8960777331 (어떤 책의 isbn `URN`)
    - 위치는 변할 수 있지만, 이름은 변하지 않는다.
    - `URN` 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않음
  - 앞으로 `URI`를 `URL`과 같은 의미로 이야기하겠음. (`URN`은 잘 안쓰임)

- `URL` 분석
  - `https://www.google.com/search?q=hello&hl=ko`
    - `URL` 전체 문법
      - `scheme://[userinfo@]host[:port][/path][?query][#fragment]`
      - `https://www.google.com:443/search?q=hello&hl=ko`
        - 프로토콜(`https`)
        - 호스트명(`www.google.com`)
        - 포트 번호(`443`)
        - 패스(`/search`)
        - 쿼리 파라미터(`q=hello&hl=ko`)
      - URL `scheme` (`https`)
        - 주로 프로토콜 사용
        - 프로토콜: 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
          - 예) `http`, `https`, `ftp` 등등
        - `http`는 80 포트, `https`는 443 포트를 주로 사용, `포트는 생략 가능`
        - `https`는 `http`에 보안 추가 (HTTP Secure)
      - URL `userinfo` 
        - URL에 사용자정보를 포함해서 인증
        - 거의 사용하지 않음
      - URL `host` (`www.google.com`)
        - 호스트명
        - 도메인명 또는 IP 주소를 직접 사용가능
      - URL `PORT` (`443`)
        - 포트(PORT), 접속 포트
        - 일반적으로 생략, 생략시 `http`는 80, `https`는 443
      - URL `path` (`/search`)
        - 리소스 경로(path), 계층적 구조
        - 예)
          - /home/le1.jpg
          - /members
          - /members/100, /items/iphone12
      - URL `query` (`q=hello&hl=ko`)
        - key=value 형태
        - ?로 시작, &로 추가 가능 
          - ?keyA=valueA&keyB=valueB
        - query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자 형태
      - URL `fragment`
        - `scheme://[userinfo@]host[:port][/path][?query][#fragment]`
        - `https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html#getting-started-introducing-spring-boot`
          - 제일 끝에 있는 `#getting-started-introducing-spring-boot` 부분
          - html 내부 북마크 등에 사용
          - 서버에 전송하는 정보 아님

### ✔️ 웹 브라우저 요청 흐름

1. `https://www.google.com/search?q=hello&hl=ko` 입력
2. DNS 조회 (`www.google.com` ➡️ IP: `200.200.200.2`) & 포트 번호 추가 (`HTTPS` PORT 생략시, `443`)
   - `200.200.200.2:443`
3. HTTP 요청 메시지 생성
    ```
    GET /search?q=hello&hl=ko HTTP/1.1
    Host: www.google.com
    ```
4. HTTP 메시지 전송
   - 1번) 웹 브라우저가 HTTP 메시지 생성
   - 2번) SOCKET 라이브러리를 통해 전달
   - 3번) TCP/IP 패킷 생성, HTTP 메시지 포함
     - TCP/IP 패킷: `출발지 IP & PORT`, `도착지 IP & PORT` 포함
     
   > 참고) TCP, UDP에서 다뤘던 프로토콜 계층의 이미지와 거의 유사함.
5. 웹 브라우저 ➡️ 구글 서버: 요청 패킷 전달 & 도착
6. HTTP 응답 메시지 생성
    ```html
    HTTP/1.1 200 OK
    Content-Type: text/html;charset=UTF-8
    Content-Length: 3423
    
    <html>
        <body>...</body>
    </html>
    ```
7. 웹 브라우저 ⬅️ 구글 서버: 응답 패킷 전달 & 도착
8. 웹 브라우저 HTML 렌더링 (화면에 요청한 결과 보임!)

## 4. HTTP 기본

## 5. HTTP 메서드

## 6. HTTP 메서드 활용

## 7. HTTP 상태코드

## 8. HTTP 헤더1 - 일반 헤더

## 9. HTTP 헤더2 - 캐시와 조건부 요청

## 10. 다음으로