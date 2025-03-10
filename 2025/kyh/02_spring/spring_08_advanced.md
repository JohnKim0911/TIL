# 스프링 핵심 원리 - 고급편

- 김영한의 스프링 완전 정복 로드맵
  - 8편) 스프링 핵심 원리 - 고급편

|    | 제목                                              | 강의 분량      | 교재 분량<br>(페이지) | 학습일                                    |
|----|-------------------------------------------------|------------|----------------|----------------------------------------|
| 1  | [소개](#1-소개)                                     | 3분         | 3              | 2025.02.20 (목)                         |
| 2  | [예제 만들기](#2-예제-만들기)                             | 1시간 14분    | 29             | 2025.02.20 (목)                         |
| 3  | [쓰레드 로컬 - ThreadLocal](#3-쓰레드-로컬---threadlocal) | 1시간 8분     | 33             | 2025.02.20 (목)                         |
| 4  | [템플릿 메서드 패턴과 콜백 패턴](#4-템플릿-메서드-패턴과-콜백-패턴)       | 1시간 52분    | 38             | 2025.02.21 (금)                         |
| 5  | [프록시 패턴과 데코레이터 패턴](#5-프록시-패턴과-데코레이터-패턴)         | 2시간 19분    | 54             | 2025.02.22 (토) ~ 2025.02.24 (월)        |
| 6  | [동적 프록시 기술](#6-동적-프록시-기술)                       | 1시간 20분    | 28             | 2025.02.24 (월)                         |
| 7  | [스프링이 지원하는 프록시](#7-스프링이-지원하는-프록시)               | 1시간 19분    | 30             | 2025.02.24 (월)                         |
| 8  | [빈 후처리기](#8-빈-후처리기)                             | 1시간 13분    | 23             | 2025.02.25 (화)                         |
| 9  | [@Aspect AOP](#9-aspect-aop)                    | 17분        | 7              | 2025.02.25 (화)                         |
| 10 | [스프링 AOP 개념](#10-스프링-aop-개념)                    | 41분        | 9              | 2025.02.25 (화)                         |
| 11 | [스프링 AOP 구현](#11-스프링-aop-구현)                    | 1시간 10분    | 25             | 2025.02.26 (수)                         |
| 12 | [스프링 AOP - 포인트컷](#12-스프링-aop---포인트컷)            | 1시간 52분    | 30             | 2025.02.26 (수)                         |
| 13 | [스프링 AOP - 실전 예제](#13-스프링-aop---실전-예제)          | 24분        | 8              | 2025.02.26 (수)                         |
| 14 | [스프링 AOP - 실무 주의사항](#14-스프링-aop---실무-주의사항)      | 1시간 9분     | 24             | 2025.02.27 (목)                         |
| 15 | [다음으로](#15-다음으로)                                | 35분        | 8              | 2025.02.27 (목)                         |
|    |                                                 | 총 16시간 44분 | 총 349 페이지      | 2025.02.20 (목) ~ 02.27 (목) <br>총 8일 소요 |

- 참고
  - 강의 학습 현황을 관리하기 위한 페이지 입니다.
  - `여기서는 목차만 공개`합니다.
  - 실제 내용은 `비공개 레포지토리`에 있습니다.
      - (링크가 있긴하지만, 저만 접근 가능합니다. 404 error 뜨는게 정상!)

## 1. 소개

- 강의 소개 페이지 (인프런): https://inf.run/FWeFN

## 2. 예제 만들기

- 프로젝트 생성
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_spring_advanced
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

- 프로젝트 생성
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_spring_advanced_part2_proxy
- 예제 프로젝트 만들기 v1
- 예제 프로젝트 만들기 v2
- 예제 프로젝트 만들기 v3
- 요구사항 추가
- 프록시, 프록시 패턴, 데코레이터 패턴 - 소개
- 프록시 패턴 - 예제 코드1
- 프록시 패턴 - 예제 코드2
- 데코레이터 패턴 - 예제 코드1
- 데코레이터 패턴 - 예제 코드2
- 데코레이터 패턴 - 예제 코드3
- 프록시 패턴과 데코레이터 패턴 정리
- 인터페이스 기반 프록시 - 적용
- 구체 클래스 기반 프록시 - 예제1
- 구체 클래스 기반 프록시 - 예제2
- 구체 클래스 기반 프록시 - 적용
- 인터페이스 기반 프록시와 클래스 기반 프록시

## 6. 동적 프록시 기술

- 리플렉션
- JDK 동적 프록시 - 소개
- JDK 동적 프록시 - 예제 코드
- JDK 동적 프록시 - 적용1
- JDK 동적 프록시 - 적용2
- CGLIB - 소개
- CGLIB - 예제 코드

## 7. 스프링이 지원하는 프록시

- 프록시 팩토리 - 소개
- 프록시 팩토리 - 예제 코드1
- 프록시 팩토리 - 예제 코드2
- 포인트컷, 어드바이스, 어드바이저 - 소개
- 예제 코드1 - 어드바이저
- 예제 코드2 - 직접 만든 포인트컷
- 예제 코드3 - 스프링이 제공하는 포인트컷
- 예제 코드4 - 여러 어드바이저 함께 적용
- 프록시 팩토리 - 적용1
- 프록시 팩토리 - 적용2

## 8. 빈 후처리기

- 빈 후처리기 - 소개
- 빈 후처리기 - 예제 코드1
- 빈 후처리기 - 예제 코드2
- 빈 후처리기 - 적용
- 빈 후처리기 - 정리
- 스프링이 제공하는 빈 후처리기1
- 스프링이 제공하는 빈 후처리기2
- 하나의 프록시, 여러 Advisor 적용

## 9. @Aspect AOP

- @Aspect 프록시 - 적용
- @Aspect 프록시 - 설명

## 10. 스프링 AOP 개념

- AOP 소개 - 핵심 기능과 부가 기능
- AOP 소개 - 애스펙트
- AOP 적용 방식
- AOP 용어 정리

## 11. 스프링 AOP 구현

- 프로젝트 생성
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_spring_advanced_part3_aop
- 예제 프로젝트 만들기
- 스프링 AOP 구현1 - 시작
- 스프링 AOP 구현2 - 포인트컷 분리
- 스프링 AOP 구현3 - 어드바이스 추가
- 스프링 AOP 구현4 - 포인트컷 참조
- 스프링 AOP 구현5 - 어드바이스 순서
- 스프링 AOP 구현6 - 어드바이스 종류

## 12. 스프링 AOP - 포인트컷

- 포인트컷 지시자
- 예제 만들기
- execution1
- execution2
- within
- args
- @target, @within
- @annotation, @args
- bean
- 매개변수 전달
- this, target

## 13. 스프링 AOP - 실전 예제

- 예제 만들기
- 로그 출력 AOP
- 재시도 AOP

## 14. 스프링 AOP - 실무 주의사항

- 프록시와 내부 호출 - 문제
- 프록시와 내부 호출 - 대안1 자기 자신 주입
- 프록시와 내부 호출 - 대안2 지연 조회
- 프록시와 내부 호출 - 대안3 구조 변경
- 프록시 기술과 한계 - 타입 캐스팅
- 프록시 기술과 한계 - 의존관계 주입
- 프록시 기술과 한계 - CGLIB
- 프록시 기술과 한계 - 스프링의 해결책

## 15. 다음으로

- 학습 내용 정리
- 다음으로
  - 스프링 데이터(DB) 접근 기술 안내
- 로드맵 소개
  - 스프링 완전 정복 시리즈
  - 스프링 부트와 JPA 실무 완전 정복 로드맵
- 하고 싶은 이야기
  - 기술적 겸손함
    - 기술적 겸손함이 없는 개발자: `"나 정도면 개발 잘한다"` 생각함. ➡️ 성장이 멈춤.
    - 기술적 겸손함이 있는 개발자: `"부족하다. 더 공부해야 한다"` 생각함. ➡️ 지속해서 성장.
