# 스프링 핵심 원리 - 고급편

- 김영한의 스프링 완전 정복 로드맵
  - 8편) 스프링 핵심 원리 - 고급편

|    | 제목                                              | 강의 분량      | 교재 분량<br>(페이지) | 학습일                          |
|----|-------------------------------------------------|------------|----------------|------------------------------|
| 1  | [소개](#1-소개)                                     | 3분         | 3              | 2025.02.20 (목)               |
| 2  | [예제 만들기](#2-예제-만들기)                             | 1시간 14분    | 29             | 2025.02.20 (목)               |
| 3  | [쓰레드 로컬 - ThreadLocal](#3-쓰레드-로컬---threadlocal) | 1시간 8분     | 33             | 2025.02.20 (목)               |
| 4  | [템플릿 메서드 패턴과 콜백 패턴](#4-템플릿-메서드-패턴과-콜백-패턴)       | 1시간 52분    | 38             | 2025.02.21 (금)               |
| 5  | [프록시 패턴과 데코레이터 패턴](#5-프록시-패턴과-데코레이터-패턴)         | 2시간 19분    |                |                              |
| 6  | [동적 프록시 기술](#6-동적-프록시-기술)                       | 1시간 20분    |                |                              |
| 7  | [스프링이 지원하는 프록시](#7-스프링이-지원하는-프록시)               | 1시간 19분    |                |                              |
| 8  | [빈 후처리기](#8-빈-후처리기)                             | 1시간 13분    |                |                              |
| 9  | [@Aspect AOP](#9-aspect-aop)                    | 17분        |                |                              |
| 10 | [스프링 AOP 개념](#10-스프링-aop-개념)                    | 41분        |                |                              |
| 11 | [스프링 AOP 구현](#11-스프링-aop-구현)                    | 1시간 10분    |                |                              |
| 12 | [스프링 AOP - 포인트컷](#12-스프링-aop---포인트컷)            | 1시간 52분    |                |                              |
| 13 | [스프링 AOP - 실전 예제](#13-스프링-aop---실전-예제)          | 24분        |                |                              |
| 14 | [스프링 AOP - 실무 주의사항](#14-스프링-aop---실무-주의사항)      | 1시간 9분     |                |                              |
| 15 | [다음으로](#15-다음으로)                                | 35분        |                |                              |
|    |                                                 | 총 16시간 44분 | 총 ? 페이지        | 2025.02.20 (목) ~ <br>총 ?일 소요 |

- 참고
  - 강의 학습 현황을 관리하기 위한 페이지 입니다.
  - `여기서는 목차만 공개`합니다.
  - 실제 내용은 `비공개 레포지토리`에 있습니다.
    - 비공개 레포지토리 1 : https://github.com/JohnKim0911/kyh_spring_advanced
      - (링크가 있긴하지만, 저만 접근 가능합니다. 404 error 뜨는게 정상!)

## 1. 소개

- 강의 소개 페이지 (인프런): https://inf.run/FWeFN

## 2. 예제 만들기

- 프로젝트 생성
- 예제 프로젝트 만들기 - V0
- 로그 추적기 - 요구사항 분석
- 로그 추적기 V1 - 프로토타입 개발
- 로그 추적기 V1 - 적용
- 로그 추적기 V2 - 파라미터로 동기화 개발
- 로그 추적기 V2 - 적용

## 3. 쓰레드 로컬 - ThreadLocal

- 필드 동기화 - 개발
- 필드 동기화 - 적용
- 필드 동기화 - 동시성 문제
- 동시성 문제 - 예제 코드
- ThreadLocal - 소개
- ThreadLocal - 예제 코드
- 쓰레드 로컬 동기화 - 개발
- 쓰레드 로컬 동기화 - 적용
- 쓰레드 로컬 - 주의사항

## 4. 템플릿 메서드 패턴과 콜백 패턴

- 템플릿 메서드 패턴 - 시작
- 템플릿 메서드 패턴 - 예제1
- 템플릿 메서드 패턴 - 예제2
- 템플릿 메서드 패턴 - 예제3
- 템플릿 메서드 패턴 - 적용1
- 템플릿 메서드 패턴 - 적용2
- 템플릿 메서드 패턴 - 정의
- 전략 패턴 - 시작
- 전략 패턴 - 예제1
- 전략 패턴 - 예제2
- 전략 패턴 - 예제3
- 템플릿 콜백 패턴 - 시작
- 템플릿 콜백 패턴 - 예제
- 템플릿 콜백 패턴 - 적용

## 5. 프록시 패턴과 데코레이터 패턴
## 6. 동적 프록시 기술
## 7. 스프링이 지원하는 프록시
## 8. 빈 후처리기
## 9. @Aspect AOP
## 10. 스프링 AOP 개념
## 11. 스프링 AOP 구현
## 12. 스프링 AOP - 포인트컷
## 13. 스프링 AOP - 실전 예제
## 14. 스프링 AOP - 실무 주의사항
## 15. 다음으로