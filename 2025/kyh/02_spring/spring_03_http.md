# (복습) 모든 개발자를 위한 HTTP 웹 기본 지식

- 김영한의 스프링 완전 정복 로드맵
    - 3편) 모든 개발자를 위한 HTTP 웹 기본 지식

|    | 제목                                                | 강의 분량     | 교재 분량<br>(PPT 페이지) | 학습일                        |
|----|---------------------------------------------------|-----------|--------------------|----------------------------|
| 1  | [소개](#1-소개)                                       | 7분        | 0                  | 2024.12.23 (월)             |
| 2  | [인터넷 네트워크](#2-인터넷-네트워크)                           | 30분       | 46                 | 2024.12.23 (월) ~ 12.24 (화) |
| 3  | [URI와 웹 브라우저 요청 흐름](#3-uri와-웹-브라우저-요청-흐름)         | 16분       | 30                 | 2024.12.24 (화)             |
| 4  | [HTTP 기본](#4-http-기본)                             | 39분       | 50                 | 2024.12.24 (화)             |
| 5  | [HTTP 메서드](#5-http-메서드)                           | 35분       | 45                 | 2024.12.25 (수)             |
| 6  | [HTTP 메서드 활용](#6-http-메서드-활용)                     | 47분       | 24                 | 2024.12.26 (목)             |
| 7  | [HTTP 상태코드](#7-http-상태코드)                         | 43분       | 35                 | 2024.12.26 (목)             |
| 8  | [HTTP 헤더1 - 일반 헤더](#8-http-헤더1---일반-헤더)           | 52분       | 63                 | 2024.12.26 (목)             |
| 9  | [HTTP 헤더2 - 캐시와 조건부 요청](#9-http-헤더2---캐시와-조건부-요청) | 42분       | 62                 | 2024.12.26 (목)             |
| 10 | [다음으로](#10-다음으로)                                  | 25분       | 0                  | 2024.12.26 (목)             |
|    |                                                   | 총 5시간 40분 | 총 335 페이지          | 2024.12.23 (월) ~ 12.26 (목) |

- 강의 내용을 개인적으로 복습하고자 정리하였습니다.
  - 방법: 각 강의가 끝나면, 교재를 보고 다시 내용을 정리함.
- `여기서는 목차만 공개`합니다.
  - 실제 내용은 `비공개 레포지토리`에 정리하였습니다.
    - 유료 이론 강의이고, 내용을 무단으로 배포하지 않기 위함.
    - `비공개 레포지토리`: 링크가 있긴하지만, 저만 볼 수 있습니다. (404 error 뜨는게 정상)
      - https://github.com/JohnKim0911/kyh_http/blob/master/README.md

## 1. 소개

- 강의 소개 페이지 (인프런): https://inf.run/8ZEU8

## 2. 인터넷 네트워크

- 인터넷 통신
- IP (인터넷 프로토콜)
- TCP, UDP
- PORT
- DNS

## 3. URI와 웹 브라우저 요청 흐름

- URI
- 웹 브라우저 요청 흐름

## 4. HTTP 기본

- 모든 것이 HTTP
- 클라이언트 서버 구조
- Stateful, Stateless
- 비 연결성 (connectionless)
- HTTP 메시지

## 5. HTTP 메서드

- HTTP API를 만들어보자
- HTTP 메서드 - GET, POST
- HTTP 메서드 - PUT, PATCH, DELETE
- HTTP 메서드의 속성

## 6. HTTP 메서드 활용

- 클라이언트에서 서버로 데이터 전송
- HTTP API 설계 예시

## 7. HTTP 상태코드

- HTTP 상태코드 소개
- 2xx - 성공
- 3xx - 리다이렉션1
- 3xx - 리다이렉션2
- 4xx - 클라이언트 오류, 5xx - 서버 오류

## 8. HTTP 헤더1 - 일반 헤더

- HTTP 헤더 개요
- 표현
- 콘텐츠 협상
- 전송 방식
- 일반 정보
- 특별한 정보
- 인증
- 쿠키

## 9. HTTP 헤더2 - 캐시와 조건부 요청

- 캐시 기본 동작
- 검증 헤더와 조건부 요청1
- 검증 헤더와 조건부 요청2
- 캐시와 조건부 요청 헤더
- 프록시 캐시
- 캐시 무효화

## 10. 다음으로

- 김영한의 스프링 완전 정복 로드맵
  - 4편) 스프링 MVC 1편 - 백엔드 웹 개발 핵심 기술
