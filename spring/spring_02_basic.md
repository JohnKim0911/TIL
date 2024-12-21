# (복습) 스프링 핵심 원리 - 기본편

- 김영한의 스프링 완전 정복 로드맵
    - 2편) 스프링 핵심 원리 - 기본편

|    | 제목                                                            | 강의 분량     | 교재 분량 (페이지) | 복습일                        |
|----|---------------------------------------------------------------|-----------|-------------|----------------------------|
| 1  | [강의 소개](#1-강의-소개)                                             | 4분        | 3           | 2024.12.16 (월)             |
| 2  | [객체 지향 설계와 스프링](#2-객체-지향-설계와-스프링)                             | 1시간 16분   | 65          | 2024.12.17 (화)             |
| 3  | [스프링 핵심 원리 이해1 - 예제 만들기](#3-스프링-핵심-원리-이해1---예제-만들기)           | 1시간 1분    | 20          | 2024.12.17 (화)             |
| 4  | [스프링 핵심 원리 이해2 - 객체 지향 원리 적용](#4-스프링-핵심-원리-이해2---객체-지향-원리-적용) | 1시간 38분   | 30          | 2024.12.17 (화)             |
| 5  | [스프링 컨테이너와 스프링 빈](#5-스프링-컨테이너와-스프링-빈)                         | 1시간 19분   | 19          | 2024.12.18 (수)             |
| 6  | [싱글톤 컨테이너](#6-싱글톤-컨테이너)                                       | 1시간 15분   | 16          | 2024.12.18 (수)             |
| 7  | [컴포넌트 스캔](#7-컴포넌트-스캔)                                         | 51분       | 12          | 2024.12.19 (목)             |
| 8  | [의존관계 자동 주입](#8-의존관계-자동-주입)                                   | 1시간 53분   | 21          | 2024.12.19 (목)             | 
| 9  | [빈 생명주기 콜백](#9-빈-생명주기-콜백)                                     | 35분       | 10          | 2024.12.20 (금)             |
| 10 | [빈 스코프](#10-빈-스코프)                                            | 1시간 44분   | 30          | 2024.12.20 (금) - 12.21 (토) |
| 11 | [다음으로](#11-다음으로)                                              | 25분       |             |                            |
|    |                                                               | 총 12시간 5분 |             |                            |

## 1. 강의 소개

- 강의 소개 페이지: https://inf.run/kCYMv

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
        - 제 기억을 살리기 위한 용도이다보니, 아래 글만으로는 이해가 어려울 수 있습니다.
            - 필요하시다면, 위 강의를 직접 수강하시는 것을 추천드립니다.
        - 방식:
            - 강의를 들으면서 코드를 직접 치고,
            - 강의가 끝나면 다시 교재를 보면서 중요 내용 위주로 정리하였습니다.
    - 유료 강의이므로, 실제 작성한 전체 코드는 비공개 합니다. (저작권...)
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_spring_basic
            - 링크가 있긴하지만, 저만 볼 수 있습니다. (404 error 뜨는게 정상)

## 2. 객체 지향 설계와 스프링

> 참고) <2. 객체 지향 설계와 스프링>는 강의에 코드 작성없이, 이론적인 내용만 다루었다.

### 이야기 - 자바 진영의 추운 겨울과 스프링의 탄생

- 옛날 옛적에... 자바에서 만든 `EJB` 가 있었다. (`EJB`: Enterprise Java Beans)
    - `EJB` 지옥...
        - 개발자가 쓰기 어려웠다.
        - `"순수한 자바로 돌아가자"`는 말도 있었다.
            - `POJO`라는 용어 등장. (`POJO`: Plain Old Java Object)

- `EJB`쓰던 개발자가 답답해서 오픈소스로 직접 만들었다.
    - 스프링
        - `EJB` 컨테이너 대체
        - 현재 사실상 표준 기술
    - 하이버네이트
        - `EJB` 엔티티빈 기술을 대체
        - 자바가 하이버네이트를 만든 개발자를 모셔와서 자바 표준(`JPA`)을 만들었다. (`JPA`: Java Persistence API)
        - `JPA`가 인터페이스고, `하이버네이트`가 구현체다.

          ![JPA](https://github.com/user-attachments/assets/12e797d2-094d-4fb7-8c6c-6ae40a5064dc)

- 스프링 역사
    - 2002년, `로드 존슨`이 책 출간하면서 시작.
        - `EJB`의 문제점 지적
        - `EJB` 없이도 충분히 고품질의 확장 가능한 애플리케이션을 개발할 수 있음을 보여주고, 30,000 라인 이상의 기반 기술을 예제 코드로 선보임
        - 여기에 지금의 스프링 핵심 개념과 기반 코드가 들어가 있음
            - `BeanFactory`, `ApplicationContext`, `POJO`, `제어의 역전`, `의존관계 주입`
        - 책이 유명해지고, 개발자들이 책의 예제 코드를 프로젝트에 사용
    - 책 출간 직후,
        - `Juergen Hoeller(유겐 휠러)`, `Yann Caro(얀 카로프)`가 `로드 존슨`에게 오픈소스 프로젝트를 제안
        - 스프링의 핵심 코드의 상당수는 `유겐 휠러`가 지금도 개발
        - `스프링 이름`은 전통적인 `J2EE(EJB)`라는 `겨울을 넘어 새로운 시작`이라는 뜻으로 지음

    - 릴리즈
        - 2003년 스프링 프레임워크 1.0 출시 - XML
        - 2006년 스프링 프레임워크 2.0 출시 - XML 편의 기능 지원
        - 2009년 스프링 프레임워크 3.0 출시 - 자바 코드로 설정
        - 2013년 스프링 프레임워크 4.0 출시 - 자바8
        - 2014년 스프링 부트 1.0 출시
        - 2017년 스프링 프레임워크 5.0, 스프링 부트 2.0 출시 - 리엑티브 프로그래밍 지원
        - 2020년 9월 현재 스프링 프레임워크 5.2.x, 스프링 부트 2.3.x

### 스프링이란?

- 스프링 생태계

  ![스프링 생태계](https://github.com/user-attachments/assets/23b5e6ba-203a-4233-8453-e85223a4f07e)

    - https://spring.io/projects 에서 더 자세히 확인할 수 있다. (많다...)

- `스프링 프레임워크`
    - 핵심 기술: `스프링 DI 컨테이너`, `AOP`, `이벤트`, 기타
    - 웹 기술: `스프링 MVC`, `스프링 WebFlux`
    - 데이터 접근 기술: `트랜잭션`, `JDBC`, `ORM` 지원, `XML` 지원
    - 기술 통합: `캐시`, `이메일`, `원격접근`, `스케줄링`
    - 테스트: 스프링 기반 테스트 지원
    - 언어: 코틀린, 그루비
    - 최근에는 `스프링 부트`를 통해서 스프링 프레임워크의 기술들을 편리하게 사용
        - 예전에는 스프링의 반은 설정이다 하는 말이 있었다... 설정하다가 포기할 수 있음... `스프링 부트`를 쓰자.

- `스프링 부트`
    - `스프링`을 편리하게 사용할 수 있도록 지원, 최근에는 기본으로 사용
    - 단독으로 실행할 수 있는 스프링 애플리케이션을 쉽게 생성
    - `Tomcat` 같은 웹 서버를 내장해서 별도의 웹 서버를 설치하지 않아도 됨
        - 예전엔 스프링에서 빌드해서 `war`파일을 만들고 서버에 밀어넣는 일들을 했었음...
    - 손쉬운 빌드 구성을 위한 starter 종속성 제공
    - 스프링과 3rd party(외부) 라이브러리 자동 구성
    - 메트릭, 상태 확인, 외부 구성 같은 프로덕션 준비 기능 제공
    - 관례에 의한 간결한 설정

- `스프링`은 왜 만들었나?
    - 스프링의 핵심 개념, 컨셉?
        - 핵심이 아닌 것:
            - 웹 애플리케이션 만들고, DB 접근 편리하게 해주는 기술?
            - 전자정부 프레임워크?
            - 웹 서버도 자동으로 띄워주고?
            - 클라우드, 마이크로서비스?
        - 핵심:
            - 스프링은 `자바` 언어 기반의 프레임워크
                - `자바` 언어의 가장 큰 특징 - `객체 지향` 언어
            - 스프링은 `객체 지향` 언어가 가진 강력한 특징을 살려내는 프레임워크
            - 스프링은 좋은 `객체 지향` 애플리케이션을 개발할 수 있게 도와주는 프레임워크

### 좋은 객체 지향 프로그래밍이란?

- 이전에 `김영한의 실전 자바 - 기본편`에서 다뤘던 `다형성과 설계`의 내용과 동일한 내용을 다뤘다.
    - 이번 강의에선 코드까지 직접 치진 않았고, 이론 위주로 설명만 하였다.
    - (이전에 정리해뒀던 내용) :
        - https://github.com/JohnKim0911/TIL/blob/master/java/java_02_basic.md#13-%EB%8B%A4%ED%98%95%EC%84%B1%EA%B3%BC-%EC%84%A4%EA%B3%84
    - 요점
        - `객체지향 프로그래밍` 특징 4가지:
            - `추상화`, `캡슐화`, `상속`, `다형성`
            - 이 중에서 `다형성`이 제일 중요하다.
        - `다형성`의 본질
            - 클라이언트를 변경하지 않고, 서버의 구현 기능을 유연하게 변경할 수 있다.
                - 인터페이스를 구현한 객체 인스턴스를 실행 시점에 유연하게 변경할 수 있다.
            - 역할과 구현을 분리
        - `스프링`은 `다형성`을 극대화해서 이용할 수 있게 도와준다.

### 좋은 객체 지향 설계의 5가지 원칙(SOLID)

-  면접에 나올 수 있는 질문이다.

- `클린코드`로 유명한 `로버트 마틴`이 좋은 객체 지향 설계의 5가지 원칙을 정리하였다.
    - 이전 부터 있던 내용인데, 이 분이 잘 정리했다.

- `SOLID`
    - `SRP`: `단일 책임 원칙` (Single Responsibility Principle)
    - `OCP`: `개방-폐쇄 원칙`⭐ (Open/closed principle) --> 이게 가장 중요하다.
    - `LSP`: `리스코프 치환 원칙` (Liskov substitution principle)
    - `ISP`: `인터페이스 분리 원칙` (Interface segregation principle)
    - `DIP`: `의존관계 역전 원칙` (Dependency inversion principle)

- `SRP`, 단일 책임 원칙
    - **한 클래스는 하나의 책임만** 가져야 한다.
    - 하나의 책임이라는 것은 모호한데, 중요한 기준은 변경이다.
        - 변경이 있을 때 파급 효과가 적으면, 단일 책임 원칙을 잘 따른 것.

- `OCP`, 개방-폐쇄 원칙
    - 확장에는 열려 있으나, 변경에는 닫혀 있어야 한다.
    - 다형성 생각해보면 된다.
        - 역할과 구현의 분리
        - 인터페이스를 구현한 새로운 클래스를 하나 만들어서 새로운 기능을 구현
    - 문제점 ⭐
        - 구현 객체를 변경하려면, 클라이언트 코드를 변경해야 한다.
            - 변경이 없을 줄 알았지만, 결국 변경해야한다.
            - `MemberService` 클라이언트가 구현 클래스를 직접 선택
                - `MemberRepository m = new MemoryMemberRepository();` //기존 코드
                - `MemberRepository m = new JdbcMemberRepository();` //변경 코드
        - 분명 다형성을 사용했지만 `OCP` 원칙을 지킬 수 없다.
        - 객체를 생성하고, 연관관계를 맺어주는 별도의 조립, 설정자가 필요하다. ⭐

- `LSP`, 리스코프 치환 원칙
    - 하위 클래스는 인터페이스 규약을 다 지켜야 한다는 것.
        - 다형성을 지원하기 위한 원칙, 인터페이스를 구현한 구현체는 믿고 사용하려면, 이 원칙이 필요하다.
    - 예시)
        - 자동차 인터페이스의 엑셀은 앞으로 가라는 기능, 뒤로 가게 구현하면 `LSP` 위반, 느리더라도 앞으로 가야함.

- `ISP`, 인터페이스 분리 원칙
    - 인터페이스 여러 개가 범용 인터페이스 하나보다 낫다.
        - 즉, 인터페이스를 작게 분리하면 더 좋다.
    - 예시)
        - 자동차 인터페이스 -> 운전 인터페이스, 정비 인터페이스로 분리
        - 사용자 클라이언트 -> 운전자 클라이언트, 정비사 클라이언트로 분리
    - 분리하면 정비 인터페이스 자체가 변해도 운전자 클라이언트에 영향을 주지 않음.
    - 인터페이스가 명확해지고, 대체 가능성이 높아진다.

- `DIP`, 의존관계 역전 원칙
    - "추상화에 의존해야지, 구체화에 의존하면 안된다."
        - 구현 클래스에 의존하지 말고, 인터페이스에 의존하라는 뜻
    - 문제점 ⭐
        - `OCP`에서 설명한 `MemberService`는 인터페이스에 의존하지만, 구현 클래스도 동시에 의존한다.
            - `MemberService` 클라이언트가 구현 클래스를 직접 선택
                - `MemberRepository m = new MemoryMemberRepository();`
        - `DIP` 위반!

- 정리 ⭐
    - 객체 지향의 핵심은 `다형성`
    - 근데 `다형성` 만으로는...
        - 구현 객체를 변경할 때 클라이언트 코드도 함께 변경된다.
        - `OCP`, `DIP`를 지킬 수 없다.
    - 뭔가 더 필요하다.

### 객체 지향 설계와 스프링

- 스프링은 다음 기술로 `다형성` + `OCP`, `DIP`를 가능하게 지원한다. ⭐
    - `DI`: `의존관계, 의존성 주입` (DI: Dependency Injection)
    - `DI 컨테이너` 제공

- 스프링이 없던 시절...
    - 옛날 어떤 개발자가 좋은 `객체 지향` 개발을 하려고 `OCP`, `DIP` 원칙을 지키면서 개발을 해보니, 너무 할일이 많았다. 배보다 배꼽이 크다. 그래서 `프레임워크`로 만들어버렸다.
    - 순수하게 자바로 `OCP`, `DIP` 원칙들을 지키면서 개발을 해보면, 결국 `스프링 프레임워크`를 만들게 된다. (더 정확히는 DI 컨테이너)

- 정리
    - 모든 설계에 역할과 구현을 분리하자.
    - 이상적으로는 모든 설계에 인터페이스를 부여하자.
        - 하지만 인터페이스를 도입하면 추상화라는 비용이 발생한다.
            - 개발자가 코드를 한번 더 타고 들어가야한다.
                - 코드를 타고 들어갈 때, 구현 클래스를 바로 보지 못하고, 인터페이스 코드가 보여지게 됨.
            - 기능을 확장할 가능성이 없다면, 구체 클래스를 직접 사용하고, 향후 꼭 필요할 때 리팩터링해서 인터페이스를 도입하는 것도 방법이다.

## 3. 스프링 핵심 원리 이해1 - 예제 만들기

### 프로젝트 생성

- 사전 준비물
    - `Java 17` 이상 설치
        - 나는 `Java 23` 사용
    - IDE: `IntelliJ `사용

- 스프링 프로젝트 생성
    - 스프링 부트 스타터 사이트에서 생성 (https://start.spring.io/)

      ![프로젝트 세팅](https://github.com/user-attachments/assets/31d39164-f2ba-4bc5-af50-c36d3afc62fa)

        - `Artifact`: 프로젝트 빌드명
    - 위 그림처럼 설정 후, `GENERATE`로 생성하고, 압축파일 받아서 원하는 경로에 압축풀기.

- 프로젝트 열기
    - `인텔리제이`로 해당 프로젝트 폴더안에 `build.gradle`을 통해 열기.

      ![open project](https://github.com/user-attachments/assets/ea4b38f0-b918-4c16-ac26-761ce5b8d92f)

- Gradle 세팅
    - 기본 설정인 `Gradle` 통해서 실행하면 느린데,
    - 이렇게 설정을 바꾸면 `인텔리제이` 통해서 자바를 바로 실행해서 실행속도가 빠르다.

      ![gradle setting](https://github.com/user-attachments/assets/95446bec-4ec7-4fc4-9814-9dca7ea31445)

    - 주의!
        - `스프링 부트 3.2` 부터 `Gradle` 옵션을 선택하자. `IntelliJ IDEA`를 선택하면 몇가지 오류가 발생한다.
        - 내 경우
            - 강의 끝나고 나서야, 내가 `IntelliJ IDEA`로 세팅 하면 안된다는 것을 찾았다.
            - 나는 `스프링 부트 3.4.0`인데, `IntelliJ IDEA` 선택했었는데, 오류가 안난다...
            - 우선 당장은 문제가 안되지만, 혹시 모르니 나중을 위해서 다시 `Gradle`로 변경하였다.

              ![gradle로 재변경](https://github.com/user-attachments/assets/b77b0361-f26c-47b7-b429-ae2b3dced834)

- 프로젝트 실행해 보기
    - 기본 메인 클래스 실행 (`CoreApplication.main()`)

      ![run project](https://github.com/user-attachments/assets/758221b0-88bd-459a-b011-a165294bb649)

    - 이번 강의에선 순수 자바 코드로 진행하고, 나중에 점차 코드를 바꿔나간다.
        - 지금은 스프링이 뜨긴했지만, 웹 앱을 올린게 아니라서 바로 종료되는게 정상이다.

### 비즈니스 요구사항과 설계

- 회원
    - `회원`을 `가입`하고 `조회`할 수 있다.
    - 회원은 `일반`과 `VIP` 두 가지 등급이 있다.
    - 회원 데이터는 `자체 DB`를 구축할 수 있고, `외부 시스템`과 연동할 수 있다. (미확정)

- 주문과 할인 정책
    - 회원은 `상품`을 `주문`할 수 있다.
    - `회원 등급`에 따라 `할인 정책`을 적용할 수 있다.
    - `할인 정책`은 모든 `VIP`는 1000원을 할인해주는 `고정 금액 할인`을 적용해달라. (나중에 변경 될 수 있다.)
    - `할인 정책`은 변경 가능성이 높다. 회사의 기본 할인 정책을 아직 정하지 못했고, 오픈 직전까지 고민을 미루고 싶다.
        - 최악의 경우, 할인을 적용하지 않을 수 도 있다. (미확정)

- 지금은 `스프링` 없는 `순수한 자바`로만 개발을 진행한다!
    - 프로젝트 환경설정을 편리하게 하려고 `스프링 부트`를 사용한 것이다.
    - `스프링` 관련은 한참 뒤에 등장한다.

### 회원 도메인 설계

- 회원 도메인 협력 관계

  ![회원 도메인 협력 관계](https://github.com/user-attachments/assets/37c1bf09-241c-4915-92a4-8c9f4cfce022)

- 회원 클래스 다이어그램 (정적)

  ![회원 클래스 다이어그램](https://github.com/user-attachments/assets/408da51b-b788-40a8-b545-226f767ffba9)

    - `회원 클래스 다이어그램`으로는 실제 어떤 인스턴스가 사용되는지 알 수 없다.
        - 런타임에 어떤구현체를 넣어서 사용할지 결정되기 때문...
        - 따라서 `회원 객체 다이어그램`이 별도로 필요하다.

- 회원 객체 다이어그램 (동적)
    - 실제 인스턴스 들의 관계를 나타낸다.

  ![회원 객체 다이어그램](https://github.com/user-attachments/assets/cb322020-b3d0-458f-9261-72b5fc69e0ad)

### 회원 도메인 개발

- 소스코드 (비공개 레포지토리):
    - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/member

- 회원 엔티티
    - `Grade`: 회원 등급
        - `enum`으로 `BASIC`과 `VIP`를 선언했다.
    - `Member`: 회원 엔티티
        - `id`, `name`, `grade`를 필드로 가진다.

- 회원 저장소
    - `MemberRepository`: 인터페이스
        - `save()`: 회원 가입
        - `findById()`: 회원 조회
    - `MemoryMemberRepository`: 구현체 (메모리)
        - `HashMap`으로 `Member`를 보관한다.

- 회원 서비스
    - `MemberService`: 인터페이스
        - `join()`: 회원 가입
        - `findMember()`: 회원 조회
    - `MemberServiceImpl`: 구현체

### 회원 도메인 실행과 테스트

- 회원 가입 `main`
    - 콘솔에 출력해서 제대로 회원가입이 되는지 확인했다.
    - 소스 코드 (비공개 레포지토리): `MemberApp`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/MemberApp.java
    - 애플리케이션 로직으로 이렇게 테스트 하는 것은 좋은 방법이 아니다. `JUnit` 테스트를 사용하자.

- 회원 가입 `JUnit 테스트`
    - 소스 코드 (비공개 레포지토리): `MemberServiceTest`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/member/MemberServiceTest.java
            - `Assertions.assertThat(member).isEqualTo(findMember);` 사용

- 회원 도메인 설계의 문제점
    - `MemberServiceImpl`
        - `private final MemberRepository memberRepository = new MemoryMemberRepository();`
            - 여기서 `OCP`, `DIP`가 안 지켜지고 있다.
            - 의존관계가 인터페이스 뿐만 아니라 구현까지 모두 의존하는 문제점이 있음.
            - 소스 코드 (비공개 레포지토리):
                - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemberServiceImpl.java
    - 주문까지 만들고나서 문제점과 해결 방안을 설명.

### 주문과 할인 도메인 설계

- 주문 도메인 전체

  ![주문 도메인 전체](https://github.com/user-attachments/assets/24bff942-9db3-46cb-b47e-38c7dba87d39)

    - 참고: 실제로는 `주문 데이터`를 DB에 저장하겠지만, 예제가 너무 복잡해 질 수 있어서 생략하고, 단순히 `주문 결과`를 반환한다.

- 주문 도메인 클래스 다이어그램

  ![주문 도메인 클래스 다이어그램](https://github.com/user-attachments/assets/5ea2f7c4-23a1-46e1-a15f-31a09b4ab741)

- 주문 도메인 객체 다이어그램

  ![주문 도메인 객체 다이어그램1](https://github.com/user-attachments/assets/e4f7c208-3e08-42cc-b17e-b7d6d6b87a5b)

  ![주문 도메인 객체 다이어그램2](https://github.com/user-attachments/assets/7002e746-dbe9-4d92-bcfd-7c236a39ca3b)

    - `회원 저장소`와 `할인 정책`을 바꾸어도, `주문 서비스`를 변경하지 않아도 된다.

### 주문과 할인 도메인 개발


- 할인
    - 소스 코드 (비공개 레포지토리):
        - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/discount
    - `DiscountPolicy`: 할인 정책 인터페이스
        - `discount()`: 할인 금액 반환
    - `FixDiscountPolicy`: 정액 할인 정책 구현체
        - VIP면 1000원 할인, 아니면 할인 없음

- 주문
    - 소스 코드 (비공개 레포지토리):
        - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/order
    - `Order`: 주문 엔티티
        - `memberId`, `itemName`, `itemPrice`, `discountPrice` 보관
        - `calculatePrice()`: 할인 적용된 금액 반환
    - `OrderService`: 주문 서비스 인터페이스
        - `createOrder()`: 주문하기
    - `OrderServiceImpl`: 주문 서비스 구현체
        - `메모리 회원 리포지토리`와, `고정 금액 할인 정책`을 구현체로 생성한다. (`MemoryMemberRepository`, `FixDiscountPolicy`)
        - 주문 생성 요청이 오면, 회원 정보를 조회하고, 할인 정책을 적용한 다음, 주문 객체를 생성해서 반환한다.

### 주문과 할인 도메인 실행과 테스트

- 주문과 할인 정책 `main`
    - 소스 코드 (비공개 레포지토리): `OrderApp`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/OrderApp.java
            - 실행결과: `order = Order{memberId=1, itemName='itemA', itemPrice=10000, discountPrice=1000}`
    - 애플리케이션 로직으로 이렇게 테스트 하는 것은 좋은 방법이 아니다. `JUnit` 테스트를 사용하자.

- 주문과 할인 정책 `JUnit 테스트`
    - 소스 코드 (비공개 레포지토리): `OrderServiceTest`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/order/OrderServiceTest.java
            - `Assertions.assertThat(order.getDiscountPrice()).isEqualTo(1000);` 사용

- 전체 테스트
    - 모든 패키지의 테스트를 한번에 실행하였다.

      ![전체 테스트 실행_단위테스트가 중요](https://github.com/user-attachments/assets/3ff98e52-380a-4c68-9007-eb44090e0af3)

    - 스프링이 띄워지는 `CoreApplicationTests`는 테스트 소요시간이 긴 것을 확인 할 수 있다.
        - (단순히 자바 코드로만 이뤄진 `단위테스트`에 비해서.)
        - 나중에 라이브러리를 많이 쓰게 되면 훨씬 더 차이가 벌어진다.
    - 그래서 되도록 `단위테스트`를 사용하는게 좋다.

## 4. 스프링 핵심 원리 이해2 - 객체 지향 원리 적용

### 새로운 할인 정책 개발

- 참고: 애자일 소프트웨어 개발 선언
    - https://agilemanifesto.org/iso/ko/manifesto.html

- 주문한 금액의 10%를 할인해주는 새로운 할인 정책을 추가하자.
    - 할인 정책 추가
        - 소스 코드 (비공개 레포지토리): `RateDiscountPolicy`
            - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/discount/RateDiscountPolicy.java
                - `DiscountPolicy` 인터페이스를 구현하기만 하면 된다.
    - 테스트 코드 작성
        - 소스 코드 (비공개 레포지토리): `RateDiscountPolicyTest`
            - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/discount/RateDiscountPolicy.java

### 새로운 할인 정책 적용과 문제점

- 방금 추가한 할인 정책을 적용해보자.
- 문제점
    - 할인 정책을 변경하려면, 클라이언트인 `OrderServiceImpl` 코드를 고쳐야 한다.

      ```java
      public class OrderServiceImpl implements OrderService {
          // private final DiscountPolicy discountPolicy = new FixDiscountPolicy();
          private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
      }
      ```

    - 기대했던 의존관계

      ![기대했던 의존관계](https://github.com/user-attachments/assets/51b44301-cfd6-41d9-b218-7176b85773ea)

    - 실제 의존관계

      ![실제 의존관계](https://github.com/user-attachments/assets/3ef70568-780a-4acf-b554-99c14d78201f)

        - `DIP` 위반.
            - 클라이언트인 `OrderServiceImpl`이 `DiscountPolicy` 인터페이스 뿐만 아니라, `FixDiscountPolicy`인 구체 클래스도 함께 의존하고 있다.

    - 정책 변경시 의존관계

      ![정책 변경](https://github.com/user-attachments/assets/98e0e535-c710-4e9d-a3a5-85ccac7da319)

        - `OCP` 위반
            - `FixDiscountPolicy`를 `RateDiscountPolicy`로 변경하는 순간, 클라이언트인 `OrderServiceImpl`의 소스 코드도 함께 변경해야 한다!

- 어떻게 문제를 해결할 수 있을까?
    - 추상(인터페이스)에만 의존하도록 변경

        ```java
        public class OrderServiceImpl implements OrderService {
            //private final DiscountPolicy discountPolicy = new RateDiscountPolicy();
            private DiscountPolicy discountPolicy;
        }
        ```
    - 실행하면, `null pointer exception`이 발생한다.
      - 구현체가 없기 때문...
    
    - 해결방안
      - 누군가가 클라이언트인 `OrderServiceImpl`에 `DiscountPolicy`의 구현 객체를 대신 생성하고 주입해주어야 한다.

### 관심사의 분리

- `애플리케이션`과 `공연` 비유
  - 공연을 준비할 때, `배우`가 `상대방 배우`를 정하지 않는다.
    - `남자주인공 역할(인터페이스)`을 하는 `이병헌(구현체, 배우)`이 `여자주인공 역할(인터페이스)`을 하는 `김태리(구현체, 배우)`를 직접 초빙하는 것과 같다.
  - `배우`는 배역을 수행하는 것에 집중 해야하고,
  - `공연기획자`가 공연을 구성하고, 역할에 맞는 배우를 지정한다.
    - 애플리케이션에서 `AppConfig`가 이런 역할을 한다.

- `AppConfig` 등장
  - 애플리케이션의 전체 동작 방식을 구성(config)하기 위해, 구현 객체를 생성하고, 연결하는 책임을 가지는 별도의 설정 클래스를 만들자.
    - 소스 코드 (비공개 레포지토리): `AppConfig`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java
        - `AppConfig`는 애플리케이션의 실제 동작에 필요한 구현 객체를 생성한다.
          - `MemberServiceImpl`
          - `MemoryMemberRepository`
          - `OrderServiceImpl`
          - `FixDiscountPolicy`
        - `AppConfig`는 생성한 객체 인스턴스의 참조(레퍼런스)를 `생성자를 통해서 주입(연결)`해준다.
          - `MemberServiceImpl`에 `MemoryMemberRepository` 주입
          - `OrderServiceImpl`에 `MemoryMemberRepository`, `FixDiscountPolicy` 주입

  - `MemberServiceImpl` 변경 (생성자 주입)
    - 소스 코드 (비공개 레포지토리): 
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemberServiceImpl.java
        - `생성자 주입`을 할 수 있도록 변경
        - `MemoryMemberRepository`에 의존하지 않고, `MemberRepository`(인터페이스)에만 의존하도록 변경
          - `DIP` 충족!
        - `MemberServiceImpl`은 이제부터 의존관계에 대한 고민은 외부에 맡기고 실행에만 집중하면 된다.
        - 객체의 생성과 연결은 `AppConfig`가 담당한다.
    - 그림 - 클래스 다이어그램
    
      ![클래스 다이어그램_MemberServiceImpl](https://github.com/user-attachments/assets/d0665ec5-780c-4dd4-b894-beae256b0b7e)

    - 그림 - 회원 객체 인스턴스 다이어그램

      ![회원 객체 인스턴스 다이어그램](https://github.com/user-attachments/assets/aff80eb7-28e5-4eb5-95e0-82521a5bd7bf)

      - `appConfig` 객체는 `memoryMemberRepository` 객체를 생성하고, 그 참조값을 `memberServiceImpl`을 생성하면서 생성자로 전달한다.
      - `DI(Dependency Injection)`: `의존관계 주입` or `의존성 주입`
        - 클라이언트인 `memberServiceImpl` 입장에서 보면, 의존관계를 마치 외부에서 주입해주는 것 같다.

  - `OrderServiceImp` 변경 (생성자 주입)
    - 소스 코드 (비공개 레포지토리):
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
        - `생성자 주입`을 할 수 있도록 변경
        - `FixDiscountPolicy`에 의존하지 않고, `DiscountPolicy`(인터페이스)에만 의존하도록 변경
        - `OrderServiceImpl`의 생성자를 통해서 어떤 구현 객체을 주입할지는 오직 외부(`AppConfig`)에서 결정한다.
       
- `AppConfig` 실행
  - 소스 코드 (비공개 레포지토리): `MemberApp` (main method)
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/MemberApp.java
      - `AppConfig()`에서 `memberService`를 받아서 사용한다.
        - `AppConfig appConfig = new AppConfig();`
        - `MemberService memberService = appConfig.memberService();`
  - 소스 코드 (비공개 레포지토리): `OrderApp` (main method)
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/OrderApp.java
      - `AppConfig()`에서 `memberService`, `orderService`를 받아서 사용한다.
        - `AppConfig appConfig = new AppConfig();`
        - `MemberService memberService = appConfig.memberService();`
        - `OrderService orderService = appConfig.orderService();`
  - `테스트 코드` 오류 수정
    - 소스 코드 (비공개 레포지토리): `MemberServiceTest`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/member/MemberServiceTest.java
        - `@BeforeEach`를 통해서 각 테스트 실행 전에 `AppConfig()`으로부터 `memberService`를 받아옴.
    - 소스 코드 (비공개 레포지토리): `OrderServiceTest`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/order/OrderServiceTest.java
        - `@BeforeEach`를 통해서 각 테스트 실행 전에 `AppConfig()`으로부터 `memberService`, `orderService` 를 받아옴.

- 정리
  - `AppConfig`는 `공연 기획자`다.
  - 이제 각 `배우`들은 담당 기능을 실행하는 책임만 지면 된다.

### AppConfig 리팩터링

- 리팩터링 전
  - `AppConfig`를 보면 중복이 있고, `역할`에 따른 `구현`이 잘 안보인다.
  - 리팩터링 전 코드는 별도로 주석처리해서 남겨놓진 않았다.
- 리팩터링 후 
  - `AppConfig`를 보면 `역할`과 `구현` 클래스가 한눈에 들어온다.
    - 애플리케이션 `전체 구성`이 어떻게 되어있는지 빠르게 파악할 수 있다.
  - 소스 코드 (비공개 레포지토리): `AppConfig`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java

### 새로운 구조와 할인 정책 적용

- 다시 돌아가서 할인정책을 바꿔보자.
  - `FixDiscountPolicy`에서 `RateDiscountPolicy`로 변경.

- `AppConfig`의 등장으로 애플리케이션이 크게 `사용` 영역과, 객체를 생성하고 `구성`(Configuration)하는 영역으로 분리되었다.

  ![사용, 구성의 분리](https://github.com/user-attachments/assets/26fc49e8-e8ac-4bde-bfdf-1e1424a3955f)

- `FixDiscountPolicy`에서 `RateDiscountPolicy`로 변경해도, `구성 영역`만 영향을 받고 `사용 영역`은 전혀 영향을 받지 않는다.

  ![그림 - 할인 정책의 변경](https://github.com/user-attachments/assets/85b4a81c-9722-4774-b699-08e652704283)

- 소스 코드 (비공개 레포지토리): `AppConfig`
  - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java
    - `discountPolicy()` 부분 변경
      - `FixDiscountPolicy`에서 `RateDiscountPolicy`로 변경

  - 이제 할인 정책을 변경해도,
    - 애플리케이션의 `구성` 역할을 담당하는 `AppConfig`만 변경하면 된다.
    - `클라이언트 코드`인 `OrderServiceImpl`를 포함해서 `사용` 영역의 어떤 코드도 변경할 필요가 없다.
  - `구성 영역`은 당연히 변경된다.
    - 구성 역할을 담당하는 `AppConfig`를 애플리케이션이라는 `공연의 기획자`로 생각하자.
    - `공연 기획자`는 `공연 참여자`인 `구현 객체들`을 모두 알아야 한다.

### 전체 흐름 정리

- 중복내용이므로 별도로 다루지 않겠다. 필요하면 교재 p.19 ~ 20 참고 할 것.

### 좋은 객체 지향 설계의 5가지 원칙의 적용

- 이번 예제에서 3가지 적용함. (`SRP`, `DIP`, `OCP`)

- `SRP, 단일 책임 원칙`
  - **한 클래스는 하나의 책임만 가져야 한다.**
    - 관심사를 분리해서 하나의 책임만 가지도록 함.
      - 구현 객체를 생성하고 연결하는 책임은 `AppConfig`가 담당
      - `클라이언트 객체`는 실행하는 책임만 담당

- `DIP, 의존관계 역전 원칙`
  - **구체화에 의존하지 않고, 추상화에 의존한다.**
    - `의존성 주입`은 이 원칙을 따르는 방법 중 하나다.
      - `클라이언트` 코드가 추상화(`인터페이스`)에만 의존하도록 코드를 변경했다.
        - 하지만 `클라이언트` 코드는 `인터페이스`만으로는 아무것도 실행할 수 없다
      - `AppConfig`가 객체 인스턴스를 생성해서 `클라이언트` 코드에 의존관계를 주입했다.

- `OCP`
  - 소프트웨어 요소는 **확장에는 열려 있으나 변경에는 닫혀 있어야 한다.**
    - 애플리케이션을 `사용 영역`과 `구성 영역`으로 나눔
    - `AppConfig`가 의존관계 변경해서 `클라이언트` 코드에 주입하므로, `클라이언트` 코드는 변경하지 않아도 됨.
    - 소프트웨어 요소를 새롭게 확장해도 사용 영역의 변경은 닫혀 있다!

### IoC, DI, 그리고 컨테이너

- `제어의 역전` IoC (Inversion of Control)
  - 프로그램의 `제어 흐름`을 `직접 제어`하는 것이 아니라 `외부에서 관리`하는 것.
    - 기존: `직접 제어`
      - 기존 프로그램은 `클라이언트 구현 객체`가 스스로 필요한 `서버 구현 객체`를 생성하고, 연결하고, 실행했다. 
      - `구현 객체`가 프로그램의 제어 흐름을 스스로 조종했다.
      - 개발자 입장에서는 자연스러운 흐름이다.
    - `AppConfig`가 등장한 이후: `외부에서 관리`
      - 프로그램의 제어 흐름은 이제 `AppConfig`가 가져간다.
      - 구현 객체는 자신의 로직을 실행하는 역할만 담당한다.
        - 예를 들어서 `OrderServiceImpl`은 필요한 인터페이스들을 호출하지만, 어떤 구현 객체들이 실행될지 모른다.

- `프레임워크` vs `라이브러리`
  - `프레임워크`: 내가 작성한 코드를 `프레임워크`가 제어하고, 대신 실행. (예시: `JUnit`)
  - `라이브러리`: 내가 작성한 코드가 직접 제어의 흐름을 담당.

- `의존관계 주입` DI(Dependency Injection)
  - `정적인 클래스 의존관계` vs `동적인 객체(인스턴스) 의존 관계`
    - `정적인 클래스 의존관계`
      - 클래스가 사용하는 import 코드만 보고 의존관계를 쉽게 판단할 수 있다.
      - 애플리케이션을 실행하지 않아도 분석할 수 있다.
      - `클래스 다이어그램`을 보자.
    - `동적인 객체 인스턴스 의존 관계`
      - 애플리케이션 실행 시점에 실제 생성된 객체 인스턴스의 참조가 연결된 의존 관계다.
      - `객체 다이어그램`을 보자.
  - `의존관계 주입`이란?
    - 애플리케이션 실행 시점(런타임)에 외부에서 실제 구현 객체를 생성하고, 클라이언트에 전달해서 클라이언트와 서버의 실제 의존관계가 연결 되는 것.
  - `의존관계 주입`의 이점
    - 클라이언트 코드를 변경하지 않고, 클라이언트가 호출하는 대상의 타입 인스턴스를 변경할 수 있다.
    - `정적인 클래스 의존관계`를 변경하지 않고, `동적인 객체 인스턴스 의존관계`를 쉽게 변경 할 수 있다.

- `IoC 컨테이너`, `DI 컨테이너`
  - `AppConfig`처럼 객체를 생성하고 관리하면서 의존관계를 연결해 주는 것을 `IoC 컨테이너` 또는 `DI 컨테이너`라 한다.
  - 최근에는 주로 `DI 컨테이너`라 한다.
  - `어샘블러`, `오브젝트 팩토리` 등으로 불리기도 한다.

### 스프링으로 전환하기

- 지금까지 순수한 자바 코드만으로 DI를 적용했다. 이제 스프링을 사용해보자.

- `AppConfig` 스프링 기반으로 변경
  - 소스 코드 (비공개 레포지토리): 
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java
      - `AppConfig`에 설정을 구성한다는 뜻의 `@Configuration`을 붙여준다.
      - 각 메서드에 `@Bean`을 붙여준다. 이렇게 하면 스프링 컨테이너에 스프링 빈으로 등록한다.
      
- `MemberApp`(main 메서드) 에 스프링 컨테이너 적용
  - 소스 코드 (비공개 레포지토리): 
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/MemberApp.java
      - `AppConfig()` 관련 코드를 아래 2줄로 변경
        - `ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);`
        - `MemberService memberService = applicationContext.getBean("memberService", MemberService.class);`

- `OrderApp`(main 메서드)에 스프링 컨테이너 적용
  - 소스 코드 (비공개 레포지토리):
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/OrderApp.java
      - `AppConfig()` 관련 코드를 아래 3줄로 변경
        - `ApplicationContext applicationContext = new AnnotationConfigApplicationContext(AppConfig.class);`
        - `MemberService memberService = applicationContext.getBean("memberService", MemberService.class);`
        - `OrderService orderService = applicationContext.getBean("orderService", OrderService.class);`

- 스프링 컨테이너
  - `ApplicationContext`를 `스프링 컨테이너`라 한다.
  - 기존에는 개발자가 `AppConfig`를 사용해서 직접 객체를 생성하고 DI를 했지만, 이제부터는 `스프링 컨테이너`를 통해서 사용한다.
  - 스프링 컨테이너는 `@Configuration`이 붙은 `AppConfig`를 설정(구성) 정보로 사용한다. 
    - 여기서 `@Bean` 이라 적힌 메서드를 모두 호출해서 반환된 객체를 `스프링 컨테이너`에 등록한다.
    - 이렇게 `스프링 컨테이너`에 등록된 객체를 `스프링 빈`이라 한다.
  - 스프링 빈은 `@Bean`이 붙은 메서드의 명을 스프링 빈의 이름으로 사용한다. (`memberService`, `orderService`)
  - 이전에는 개발자가 필요한 객체를 `AppConfig`를 사용해서 직접 조회했지만, 이제부터는 `스프링 컨테이너`를 통해서 필요한 `스프링 빈`(객체)를 찾아야 한다.
    - `스프링 빈`은 `applicationContext.getBean()` 메서드를 사용해서 찾을 수 있다.

- 코드가 약간 더 복잡해진 것 같은데, `스프링 컨테이너`를 사용하면 어떤 장점이 있을까?... 다음 시간에~

- 참고
  - `스프링 부트 3.1` 이상 - 로그 출력 안되는 문제 해결
    - 원인 & 결과
      - 원인: 나는 `스프링 부트 3.4`를 쓰고 있어서 로그가 강의처럼 출력되지 않았다.
      - 결과: 교재에 나온대로 조치하였더니, 해결되었다.
    - 조치 전
      - 로그가 출력되지 않는다.    

        ![조치전](https://github.com/user-attachments/assets/cf8290de-c597-401d-954f-e07b94c654fd)

    - 조치 후 
      - 빈 생성되는 로그가 정상적으로 출력된다.
      
      ![조치후](https://github.com/user-attachments/assets/345ef094-d06a-4368-8c34-7c7371db2b0b)

    - 조치방법
      - 아래 파일을 만들어 넣으면 된다.
        - 소스 코드 (비공개 레포지토리): `src/main/resources/logback.xml`
          - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/resources/logback.xml

## 5. 스프링 컨테이너와 스프링 빈

### 스프링 컨테이너 생성

```java
//스프링 컨테이너 생성
ApplicationContext applicationContext =  new AnnotationConfigApplicationContext(AppConfig.class); 
```

- `ApplicationContext`를 `스프링 컨테이너`라 한다.
  - `ApplicationContext`는 인터페이스이다.
  - `new AnnotationConfigApplicationContext(AppConfig.class);`는 `ApplicationContext` 인터페이스의 구현체이다.

- `스프링 컨테이너`는 2가지 방법으로 만들 수 있다.
  - `XML`을 기반으로 만들 수 있고,
  - `애노테이션` 기반의 자바 설정 클래스로 만들 수 있다.
    - 예) 직전에 `AppConfig`를 사용했던 방식

- 참고:
  - 더 정확히는 `스프링 컨테이너`를 부를 때 `BeanFactory`, `ApplicationContext`로 구분해서 이야기 한다.
    - `BeanFactory`를 직접 사용하는 경우는 거의 없으므로, 일반적으로 `ApplicationContext`를 `스프링 컨테이너`라 한다.

- 스프링 컨테이너의 생성 과정

  - 스프링 컨테이너 생성

    - `new AnnotationConfigApplicationContext(AppConfig.class)`
      - 스프링 컨테이너를 생성할 때는 구성 정보(`AppConfig.class`)를 지정해주어야 한다.

    ![1  스프링 컨테이너 생성](https://github.com/user-attachments/assets/7b44bb00-98f0-488a-af25-5fb04bfda42d)
  
  - 스프링 빈 등록
    - 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 스프링 빈을 등록한다.
    
    ![2  스프링 빈 등록](https://github.com/user-attachments/assets/9908b4ef-82ee-4271-9e2c-da623e36ce8b)

    - 빈 이름
      - 빈 이름은 메서드 이름을 사용한다.
      - 빈 이름을 직접 부여할 수 도 있다.
        - 예시) `@Bean(name="memberService2")`
      - 주의: 
        - 빈 이름은 항상 다른 이름을 부여해야 한다.
          - 같은 이름을 부여하면, 다른 빈이 무시되거나, 기존 빈을 덮어버리거나 설정에 따라 오류가 발생한다.
          - 빈 이름이 중복되면, 애초부터 중복되지 않도록 바꾸자. 중복된 걸 어떻게 해결하려고 하지 말기.
          
  - 스프링 빈 의존관계 설정 - 준비

    ![3  스프링 빈 의존관계 설정 - 준비](https://github.com/user-attachments/assets/918a8a60-0326-4205-84fe-fd08e15d110f)

      - (초록색이 각각의 빈이다.)

  - 스프링 빈 의존관계 설정 - 완료
    - 스프링 컨테이너는 설정 정보를 참고해서 의존관계를 주입(DI)한다
    
    ![4  스프링 빈 의존관계 설정 - 완료](https://github.com/user-attachments/assets/581015dc-47ea-49c2-98c7-23244d6cc1ca)

    - 단순히 자바 코드를 호출하는 것 같지만, 차이가 있다.
      - 뒤에 싱글톤 컨테이너에서 설명한다.

- 정리
  - `스프링 컨테이너`를 생성하고, 설정(구성) 정보를 참고해서 `스프링 빈`도 등록하고, 의존관계도 설정했다.

### 컨테이너에 등록된 모든 빈 조회

- `스프링 컨테이너`에 실제 `스프링 빈`들이 잘 등록 되었는지 확인해보자.
  - 소스 코드 (비공개 레포지토리): `ApplicationContextInfoTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/beanfind/ApplicationContextInfoTest.java
      - 모든 빈 출력하기
        - 스프링이 내부에서 사용하는 빈 + 내가 등록한 빈 둘 다 출력.
        - `ac.getBeanDefinitionNames()` : 스프링에 등록된 모든 빈 이름을 조회
        - `ac.getBean()` : 빈 이름으로 빈 객체(인스턴스)를 조회
      - 애플리케이션 빈 출력하기
        - 내가 등록한 빈만 출력. (스프링이 내부에서 사용하는 빈은 제외)
        - `BeanDefinition beanDefinition = ac.getBeanDefinition(beanDefinitionName);` : `BeanDefinition` 반환
        - `if (beanDefinition.getRole() == BeanDefinition.ROLE_APPLICATION) {...}`
          - 스프링이 내부에서 사용하는 빈은 `getRole()`로 구분할 수 있다.
            - `ROLE_APPLICATION` : 일반적으로 `사용자`가 정의한 빈
            - `ROLE_INFRASTRUCTURE` : `스프링 내부`에서 사용하는 빈

### 스프링 빈 조회 - 기본

- `스프링 컨테이너`에서 `스프링 빈`을 찾는 가장 기본적인 조회 방법
  - `ac.getBean(빈이름, 타입)`
  - `ac.getBean(타입)`
  - 조회 대상 `스프링 빈`이 없으면 예외 발생한다.
    - `NoSuchBeanDefinitionException: No bean named 'xxxxx' available`

- 예제 코드
  - 소스 코드 (비공개 레포지토리): `ApplicationContextBasicFindTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/beanfind/ApplicationContextBasicFindTest.java
      - 테스트 케이스
        - 빈 이름으로 조회: `ac.getBean(빈이름, 타입)`
          - 에러 상황해봄. (빈 이름으로 조회X)
        - 이름 없이 타입만으로 조회: `ac.getBean(타입)`
        - 구체 타입으로 조회: `ac.getBean(빈이름, 구체 타입)` //권장하지 않는다. 변경시 유연성 떨어짐.
      - 공통적으로 사용된 코드
        - 해당 타입이 맞는지 확인: 
          - `assertThat(memberService).isInstanceOf(MemberServiceImpl.class);`
        - 빈이 없을때 에러가 나는지 확인: 
          - `Assertions.assertThrows(NoSuchBeanDefinitionException.class, 실행코드);`
            - 실행코드를 실행했을때, 좌측의 예외가 나는지 확인.
      
### 스프링 빈 조회 - 동일한 타입이 둘 이상

- 타입으로 조회시, 같은 타입의 `스프링 빈`이 둘 이상이면 오류가 발생한다. 이때는 빈 이름을 지정하자.
  - 소스 코드 (비공개 레포지토리): `ApplicationContextSameBeanFindTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/beanfind/ApplicationContextSameBeanFindTest.java
      - 정적 중첩 클래스(`SameBeanConfig`)로 설정파일을 지정하였다.
      - 테스트 케이스
        - "타입으로 조회시, 같은 타입이 둘 이상 있으면, 중복 오류가 발생한다."
        - "타입으로 조회시, 같은 타입이 둘 이상 있으면, 빈 이름을 지정하면 된다."
        - "특정 타입을 모두 조회하기."
          - `Map<String, MemberRepository> beansOfType = ac.getBeansOfType(MemberRepository.class);`
            - `ac.getBeansOfType()`: 해당 타입의 모든 빈 조회

### 스프링 빈 조회 - 상속 관계

- 부모 타입으로 조회하면, 자식 타입도 함께 조회한다
  - 그래서 모든 자바 객체의 최고 부모인 `Object` 타입으로 조회하면, 모든 스프링 빈을 조회한다.

  ![스프링 빈 조회 - 상속 관계](https://github.com/user-attachments/assets/5d433bfe-7a1a-48ee-8a8b-f4d60da2f22f)

- 예제 코드 
  - 소스 코드 (비공개 레포지토리): `ApplicationContextExtendsFindTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/beanfind/ApplicationContextExtendsFindTest.java
      - 정적 중첩 클래스(`TestConfig`)로 설정파일을 지정하였다.
      - 테스트 케이스
        - "부모 타입으로 조회시, 자식이 둘 이상 있으면, 중복 오류가 발생한다."
        - "부모 타입으로 조회시, 자식이 둘 이상 있으면, 빈 이름을 지정하면 된다."
        - "특정 하위 타입으로 조회"
        - "부모 타입으로 모두 조회하기"
        - "부모 타입으로 모두 조회하기 - Object"

### BeanFactory와 ApplicationContext

![BeanFactory, ApplicationContext](https://github.com/user-attachments/assets/b61fd3e7-d032-45a4-9f42-7848b76ea54d)

- `BeanFactory`
  - 스프링 컨테이너의 최상위 인터페이스다.
  - 스프링 빈을 관리하고 조회하는 역할을 담당한다.
  - `getBean()`을 제공한다.
  - 지금까지 우리가 사용했던 대부분의 기능은 `BeanFactory`가 제공하는 기능이다.

- `ApplicationContext`
  - `BeanFactory` 기능을 모두 상속받아서 제공한다.
  - `ApplicatonContext`가 제공하는 부가기능

    ![ApplicatonContext](https://github.com/user-attachments/assets/100ab02b-6b3b-49db-a198-d3910fea3468)

    - 메시지소스를 활용한 국제화 기능
      - 예를 들어서 한국에서 들어오면 한국어로, 영어권에서 들어오면 영어로 출력
    - 환경변수
      - 로컬, 개발, 운영등을 구분해서 처리
    - 애플리케이션 이벤트
      - 이벤트를 발행하고 구독하는 모델을 편리하게 지원
    - 편리한 리소스 조회
      - 파일, 클래스패스, 외부 등에서 리소스를 편리하게 조회

- 정리
  - `BeanFactory`를 직접 사용할 일은 거의 없다. 부가기능이 포함된 `ApplicationContext`를 사용한다.
  - `BeanFactory`나 `ApplicationContext`를 `스프링 컨테이너`라 한다.

### 다양한 설정 형식 지원 - 자바 코드, XML

- `스프링 컨테이너`는 다양한 형식의 설정 정보를 받아들일 수 있게 유연하게 설계되어 있다.
  - 자바 코드, XML, Groovy 등등
  
  ![다양한 설정 형식 지원](https://github.com/user-attachments/assets/9866660d-6ad1-4802-9a3d-417f5437f2ec)

- 애노테이션 기반 자바 코드 설정 사용:
  - 지금까지 했던 것 (`new AnnotationConfigApplicationContext(AppConfig.class)`)
- XML 설정 사용:
  - 최근에는 `스프링 부트`를 많이 사용하면서 XML기반의 설정은 잘 사용하지 않는다.
  - 아직 많은 `레거시 프로젝트` 들이 XML로 되어 있고, 또 XML을 사용하면 컴파일 없이 빈 설정 정보를 변경할 수 있는 장점도 있다.
  - `GenericXmlApplicationContext`를 사용하면서 xml 설정 파일을 넘기면 된다.

- XML 설정 사용 예시
  - 소스 코드 (비공개 레포지토리): 
    - `src/main/resources/appConfig.xml` (xml 기반의 스프링 빈 설정 정보)
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/resources/appConfig.xml
        - 자바 코드로 된 `AppConfig.java` 설정 정보를 비교해보면 거의 비슷하다.
          - `AppConfig.java`: https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java
    - `XmlAppContext` (자바 테스트 코드)
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/xml/XmlAppContext.java

### 스프링 빈 설정 메타 정보 - BeanDefinition

- 스프링은 어떻게 이런 다양한 설정 형식을 지원하는 것일까?
  - 그 중심에는 `BeanDefinition`이라는 추상화가 있다.

![BeanDefinition](https://github.com/user-attachments/assets/3ee4de54-5648-4056-b177-b236cc7f9b65)

- `역할`과 `구현`을 개념적으로 나누었다.
  - XML을 읽어서 `BeanDefinition`을 만들면 된다.
  - 자바 코드를 읽어서 `BeanDefinition`을 만들면 된다.
  - `스프링 컨테이너`는 자바 코드인지, XML인지 몰라도 된다. 오직 `BeanDefinition`만 알면 된다.
- `BeanDefinition`을 `빈 설정 메타정보`라 한다.
  - `@Bean`, `<bean>`당 각각 하나씩 `메타 정보`가 생성된다.
- `스프링 컨테이너`는 이 `메타정보`를 기반으로 `스프링 빈`을 생성한다.

- 코드 레벨로 조금 더 깊이 있게 들어가보자.

  ![BeanDefinition_코드 레벨](https://github.com/user-attachments/assets/66a59ad7-fdfa-4d74-8eb0-61a3bc82aaef)

    - `AnnotationConfigApplicationContext`는 `AnnotatedBeanDefinitionReader`를 사용해서 `AppConfig.class`를 읽고 `BeanDefinition`을 생성한다.

- `BeanDefinition` 살펴보기
  - 잘 몰라도 되는 내용이다. 이런게 있구나 참고만 하자.
  - `BeanDefinition` 정보
    - 아래 예제에서 콘솔에 찍히는 내용을 이해하고 싶다면, 교재 p.17 참고. 
  - 소스 코드 (비공개 레포지토리): `BeanDefinitionTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/beandefinition/BeanDefinitionTest.java
      - 빈 설정 메타정보 확인

- 정리
  - `BeanDefinition`을 직접 생성해서 `스프링 컨테이너`에 등록할 수 도 있다. 하지만 실무에서 `BeanDefinition`을 직접 정의하거나 사용할 일은 거의 없다.
  - 스프링이 다양한 형태의 설정 정보를 `BeanDefinition`으로 추상화해서 사용하는 것 정도만 이해하면 된다.
    - 너무 깊이있게 이해 할 필요 없다.
  - 가끔 스프링 코드나 스프링 관련 오픈 소스의 코드를 볼 때, `BeanDefinition`이 보일 때가 있다. 이때 이러한 메커니즘을 떠올리면 된다.

## 6. 싱글톤 컨테이너

### 웹 애플리케이션과 싱글톤

- 서론
  - 스프링은 태생이 기업용 온라인 서비스 기술을 지원하기 위해 탄생했다.
  - 대부분의 스프링 애플리케이션은 웹 애플리케이션이다. 웹이 아닌 애플리케이션 개발도 얼마든지 개발할 수 있다.
  - **웹 애플리케이션은 보통 여러 고객이 동시에 요청을 한다.**

- 스프링 없는 순수한 DI 컨테이너

    - 우리가 만들었던 스프링 없는 순수한 DI 컨테이너인 `AppConfig`는 요청을 할 때 마다 객체를 새로 생성한다.
  
    ![스프링 없는 순수한 DI 컨테이너](https://github.com/user-attachments/assets/9db9097c-ed39-4358-9f16-3be004e7a68e)

    - 소스 코드 (비공개 레포지토리): `SingletonTest`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/SingletonTest.java
        - 호출할 때 마다 객체를 생성한다.
          - `appConfig.memberService();`를 두번 호출했고, 서로 다른 참조값을 가지고 있는 것을 확인했다.
        - 문제점 : 메모리 낭비가 심하다.
          - 고객 트래픽이 초당 100이 나오면 초당 100개 객체가 생성되고 소멸된다!
        - 해결방안: 해당 객체가 딱 1개만 생성되고, 공유하도록 설계하면 된다. (`싱글톤 패턴`)

### 싱글톤 패턴

- 클래스의 인스턴스가 딱 1개만 생성되는 것을 보장하는 디자인 패턴이다.
  - 객체 인스턴스를 2개 이상 생성하지 못하도록 막아야 한다.
    - `private` 생성자를 사용해서 외부에서 임의로 `new` 키워드를 사용하지 못하도록 막아야 한다.

- 싱글톤 패턴을 적용한 예제
  - 소스 코드 (비공개 레포지토리): `SingletonService` (test 코드에 작성)
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/SingletonService.java
      - `static` 영역에 객체를 딱 1개만 생성해둔다.
      - 객체 인스턴스가 필요하면 `getter`을 통해서 조회하도록 한다.
      - 생성자를 `private`으로 선언해서 외부에서 `new` 키워드를 사용한 객체 생성을 못하게 막는다.
  - `SingletonService` 테스트
    - 소스 코드 (비공개 레포지토리): `SingletonTest`의 `singletonServiceTest()` 참조
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/SingletonTest.java
        - 호출할 때 마다 같은 객체 인스턴스를 반환하는 것을 확인할 수 있다.

- 정리
  - 싱글톤 패턴을 적용하면, 고객의 요청이 올 때 마다 객체를 생성하는 것이 아니라, 이미 만들어진 객체를 공유해서 효율적으로 사용할 수 있다.
  - 하지만 싱글톤 패턴은 다음과 같은 수 많은 문제점들을 가지고 있다.

- 싱글톤 패턴 문제점
  - 싱글톤 패턴을 구현하는 코드 자체가 많이 들어간다.
  - 의존관계상 클라이언트가 구체 클래스에 의존한다. `DIP`를 위반한다.
  - 클라이언트가 구체 클래스에 의존해서 `OCP` 원칙을 위반할 가능성이 높다.
  - 테스트하기 어렵다.
  - 내부 속성을 변경하거나 초기화 하기 어렵다.
  - `private` 생성자로 자식 클래스를 만들기 어렵다.
  - 결론적으로 유연성이 떨어진다.
  - 안티패턴으로 불리기도 한다.

### 싱글톤 컨테이너

- `스프링 컨테이너`는 싱글톤 패턴의 문제점을 해결하면서, 객체 인스턴스를 `싱글톤`(1개만 생성)으로 관리한다.
  - 지금까지 우리가 학습한 `스프링 빈`이 바로 `싱글톤`으로 관리되는 빈이다.

- 싱글톤 컨테이너
  - `스프링 컨테이너`는 `싱글턴 패턴`을 적용하지 않아도, 객체 인스턴스를 `싱글톤`으로 관리한다.
  - `스프링 컨테이너`는 `싱글톤 컨테이너` 역할을 한다. 이렇게 `싱글톤` 객체를 생성하고 관리하는 기능을 `싱글톤 레지스트리`라 한다.
  - `스프링 컨테이너`의 이런 기능 덕분에 `싱글턴 패턴`의 모든 단점을 해결하면서 객체를 `싱글톤`으로 유지할 수 있다.
    - `싱글톤 패턴`을 위한 지저분한 코드가 들어가지 않아도 된다.
    - `DIP`, `OCP`, 테스트, `private` 생성자로 부터 자유롭게 `싱글톤`을 사용할 수 있다.

- `스프링 컨테이너`를 사용하는 테스트 코드
  - 소스 코드 (비공개 레포지토리): `SingletonTest`의 `springContainer()` 참조
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/SingletonTest.java
      - 스프링 컨테이너 사용
        - `ApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);`
      - 스프링 컨테이너에서 스프링 빈을 받아와서 사용한다.
        - `ac.getBean("memberService", MemberService.class);`
      - 결과:
        - 호출할 때 마다 같은 객체 인스턴스를 반환하는 것을 확인할 수 있다.

- `싱글톤 컨테이너` 적용 후

  ![싱글톤 컨테이너 적용 후](https://github.com/user-attachments/assets/c6d63c16-01e4-4ca7-b7fd-bb7550cc869c)

    - `스프링 컨테이너` 덕분에 고객의 요청이 올 때 마다 객체를 생성하는 것이 아니라, 이미 만들어진 객체를 공유해서 효율적으로 재사용할 수 있다.

### 싱글톤 방식의 주의점

- `싱글톤` 객체는 상태를 `유지(stateful)`하게 설계하면 안된다. 
  - 객체 인스턴스를 하나만 생성해서 공유하는 `싱글톤` 방식은 여러 클라이언트가 하나의 같은 객체 인스턴스를 공유하기 때문에 정말 위험하다. ⭐
  - `싱글톤 패턴`이든, 스프링같은 `싱글톤 컨테이너`를 사용하든,  모든 `싱글톤` 방식에 해당.

- `무상태(stateless)`로 설계해야 한다!
  - 특정 클라이언트에 의존적인 필드가 있으면 안된다.
  - 특정 클라이언트가 값을 변경할 수 있는 필드가 있으면 안된다!
  - 가급적 읽기만 가능해야 한다.
  - 필드 대신에 자바에서 공유되지 않는, 지역변수, 파라미터, ThreadLocal 등을 사용해야 한다
- 스프링 빈의 필드에 공유 값을 설정하면 정말 큰 장애가 발생할 수 있다!!!

- 상태를 유지할 경우 발생하는 문제점 예시
  - 소스 코드 (비공개 레포지토리): 
    - `StatefulService`: https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/StatefulService.java
    - `StatefulServiceTest`: https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/StatefulServiceTest.java
      - 발생한 문제
        - `A 사용자`가 10000원 주문 후, `B 사용자`도 20000원 주문했는데,
        - `A 사용자` 주문금액 출력해보니 20000원으로 출력됨.
      - 원인
        - 서로 다른 인스턴스를 만들긴 했지만, 실제로는 공유되는 필드를 사용하고 있어서.
      - 실무에서 몇년에 한번씩 볼 수 있는 문제...
        - 정말 해결하기 어려운 큰 문제들이 터진다. (복구하는데 몇개월 걸리고, 보상해주고, 서비스 닫고... 진짜 난리난다.)
      - 진짜 `공유필드`는 조심해야 한다! 스프링 빈은 항상 `무상태(stateless)`로 설계하자.

### @Configuration과 싱글톤

- `AppConfig`에 이상한 점이 있다.
  - 소스 코드 (비공개 레포지토리): `AppConfig`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AppConfig.java
      - `new MemoryMemberRepository()`가 중복 호출 되는데, 싱글톤이 깨지는거 아닌가?
        - `memberService` -> `new MemoryMemberRepository()`
        - `orderService` -> `new MemoryMemberRepository()`
  - 검증 용도의 코드 추가
    - 소스 코드 (비공개 레포지토리): `MemberServiceImpl`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemberServiceImpl.java
        - 테스트를 위해서 `memberRepository`를 반환하는 `getter`를 추가하였다.
  - 테스트 코드
    - 소스 코드 (비공개 레포지토리): `ConfigurationSingletonTest`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/ConfigurationSingletonTest.java
        - `memberService`, `orderService`, `memberRepository`의 스프링 빈을 받아서 참조값을 비교해보았다.
          - 3개 다 값이 같다.
          - 호출이 안되는건가 싶어서 `AppConfig`에 호출 로그 남겨보았다.
            - `memberRepository()`가 3번 호출 되어야 한다고 예상했는데, 실제로는 1번만 호출된다.

### @Configuration과 바이트코드 조작의 마법

- 서론
  - `스프링 컨테이너`는 `싱글톤 레지스트리`다. 따라서 `스프링 빈`이 `싱글톤`이 되도록 보장해주어야 한다.
  - 그런데 `스프링`이 자바 코드까지 어떻게 하기는 어렵다. 저 자바 코드를 보면 분명 3번 호출되어야 하는 것이 맞다.
  - 그래서 `스프링`은 클래스의 바이트코드를 조작하는 라이브러리를 사용한다. 
    - 모든 비밀은 `@Configuration`을 적용한 `AppConfig`에 있다.

- 소스 코드 (비공개 레포지토리): `ConfigurationSingletonTest`의 `configurationDeep()` 참고
  - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/singleton/ConfigurationSingletonTest.java
    - `AppConfig`을 스프링 빈으로 등록하고, 클래스 정보를 출력해본다.
      - 순수한 클래스라면 다음과 같이 출력되어야 한다: `class hello.core.AppConfig`
      - 실제 출력 결과: `class hello.core.AppConfig$$SpringCGLIB$$0`
- 클래스 명에 `xxxCGLIB`가 붙었다.
  - 이것은 내가 만든 클래스가 아니라, `스프링`이 `CGLIB`라는 바이트코드 조작 라이브러리를 사용해서 `AppConfig` 클래스를 상속받은 임의의 다른 클래스(`AppConfig@CGLIB`)를 만들고, 스프링 빈으로 등록한 것이다!
  - 그림
  
    ![CGLIB](https://github.com/user-attachments/assets/8e746fd1-c959-4c2e-a2f9-32c2e46714e4)

    - 그 임의의 다른 클래스가 바로 싱글톤이 보장되도록 해준다. 
    - 아마도 다음과 같이 바이트 코드를 조작해서 작성되어 있을 것이다.
      - (실제로는 CGLIB의 내부 기술을 사용하는데 매우 복잡하다.)

  - `AppConfig@CGLIB` 예상 코드

      ```java
      @Bean
      public MemberRepository memberRepository() {
    
          if (memoryMemberRepository가 이미 스프링 컨테이너에 등록되어 있으면?) {
              return 스프링 컨테이너에서 찾아서 반환;
          } else { //스프링 컨테이너에 없으면
              기존 로직을 호출해서 MemoryMemberRepository를 생성하고 스프링 컨테이너에 등록
              return 반환
          }
      }
      ```

      - `@Bean`이 붙은 메서드마다 이미 `스프링 빈`이 존재하면 존재하는 `빈`을 반환하고,
        - `스프링 빈`이 없으면 생성해서 `스프링 빈`으로 등록하고 반환하는 코드가 동적으로 만들어진다.
      - 덕분에 `싱글톤`이 보장된다.

- `AppConfig`에 `@Configuration`을 적용하지 않고, `@Bean`만 적용한다면?
  - 위 테스트를 다시 실행해보면, 이렇게 출력된다.
    - `class hello.core.AppConfig` //순수한 `AppConfig`로 스프링 빈에 등록됨.
    - `MemberRepository`가 총 3번 호출된다.
      - 서로 다른 인스턴스를 가지게 되고, 테스트도 실패한다.
  - 즉, `@Bean`만 사용해도 `스프링 빈`으로 등록되지만, `싱글톤`을 보장하지 않는다.

- 정리
  - 스프링 설정 정보(`AppConfig`)는 항상 `@Configuration`을 사용하자.

## 7. 컴포넌트 스캔

### 컴포넌트 스캔과 의존관계 자동 주입 시작하기

- 지금까지 `스프링 빈`을 등록할 때는 자바 코드의 `@Bean`이나 `XML`의 `<bean>` 등을 통해서 설정 정보(`AppConfig`)에 직접 등록할 `스프링 빈`을 나열했다.
- 스프링은...
  - 설정 정보가 없어도 자동으로 `스프링 빈`을 등록하는 `컴포넌트 스캔` 기능을 제공한다.
    - `@Component` 애노테이션이 붙은 클래스를 스캔해서 `스프링 빈`으로 등록.
  - 또 의존관계도 자동으로 주입하는 `@Autowired` 라는 기능도 제공한다

- 기존 `AppConfig.java`는 남겨두고, 새로운 `AutoAppConfig.java`를 만들자.
  - 소스 코드 (비공개 레포지토리): `AutoAppConfig`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AutoAppConfig.java
      - `@ComponentScan`을 붙여주었다.
      - 기존의 `AppConfig`와는 다르게 `@Bean`으로 등록한 클래스가 하나도 없다!
      - 참고
        - `컴포넌트 스캔`을 사용하면 `@Configuration`이 붙은 설정 정보도 자동으로 등록되기 때문에,
          `AppConfig`, `TestConfig` 등 앞서 만들어두었던 설정 정보도 함께 등록되고, 실행되어 버린다.
          - 그래서 `excludeFilters`를 이용해서 설정정보는 `컴포넌트 스캔` 대상에서 제외했다.
          - `@Configuration` 소스코드를 열어보면 `@Component` 애노테이션이 붙어있다.
        - 보통 설정 정보를 `컴포넌트 스캔` 대상에서 제외하지는 않지만, 기존 예제 코드를 최대한 남기고 유지하기 위해서 이 방법을 선택했다.

- 각 클래스가 `컴포넌트 스캔`의 대상이 되도록 `@Component` 애노테이션을 붙여주자.
  - (아래 각 링크는 비공개 레포지토리임!)
  - `MemoryMemberRepository`: `@Component` 추가
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemoryMemberRepository.java
  - `RateDiscountPolicy`: `@Component` 추가
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/discount/RateDiscountPolicy.java
  - `MemberServiceImpl`: `@Component`, `@Autowired` 추가
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemberServiceImpl.java
      - `@Autowired`는 의존관계를 자동으로 주입해준다.
        - 이전에 `AppConfig`에서는 `@Bean`으로 직접 설정 정보를 작성했고, 의존관계도 직접 명시했다.
        - 이제는 이런 설정 정보 자체가 없기 때문에, 의존관계 주입도 이 클래스 안에서 해결해야 한다.
  - `OrderServiceImpl`: `@Component`, `@Autowired` 추가
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
      - `@Autowired`를 사용하면 생성자에서 여러 의존관계도 한번에 주입받을 수 있다.
- 테스트 코드: `AutoAppConfigTest`
  - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scan/AutoAppConfigTest.java
    - 설정 정보로 `AutoAppConfig` 클래스를 넘겨준다.
    - 로그를 잘 보면 `컴포넌트 스캔`이 잘 동작하는 것을 확인할 수 있다.

- `컴포넌트 스캔`, `자동 의존관계 주입` 동작 방식
  - `@ComponentScan`
  
    ![ComponentScan](https://github.com/user-attachments/assets/14d077b1-45a0-4b81-8d38-c5dae88ebd41)

    - `@ComponentScan`은 `@Component`가 붙은 모든 클래스를 `스프링 빈`으로 등록한다.
    - 이때` 스프링 빈`의 기본 이름은 클래스명을 사용하되 맨 앞글자만 소문자를 사용한다.
      - **빈 이름 기본 전략**: `MemberServiceImpl` 클래스 --> `memberServiceImpl`
      - **빈 이름 직접 지정**: 만약 스프링 빈의 이름을 직접 지정하고 싶으면
        - 예시) `@Component("memberService2")`

  - `@Autowired` 의존관계 자동 주입

    ![Autowired](https://github.com/user-attachments/assets/54f86fd7-73bd-472d-91b3-9242c54581ba)

    - 생성자에 `@Autowired`를 지정하면, `스프링 컨테이너`가 자동으로 해당 `스프링 빈`을 찾아서 주입한다.
    - 이때 기본 조회 전략은 타입이 같은 빈을 찾아서 주입한다.
      - `getBean(MemberRepository.class)`와 동일하다고 이해하면 된다.
    - 생성자에 파라미터가 많아도 다 찾아서 자동으로 주입한다. (아래 그림 참고)
    
      ![Autowired2](https://github.com/user-attachments/assets/0bb40663-4e36-4752-a11a-500bd10b3e7a)

### 탐색 위치와 기본 스캔 대상

- 탐색할 패키지의 시작 위치 지정
  - 모든 자바 클래스를 다 컴포넌트 스캔하면 시간이 오래 걸린다. 그래서 꼭 필요한 위치부터 탐색하도록 시작 위치를 지정할 수 있다.
  - 소스 코드 (비공개 레포지토리): `AutoAppConfig`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AutoAppConfig.java
      - 위 링크 안의 주석 참고할 것. (`basePackages`, `basePackageClasses`, `지정하지 않을시 default 값`)
      - 추가 내용) 여러 시작 위치를 지정할 수도 있다.
          - 예시) `basePackages = {"hello.core", "hello.service"}`
- 권장하는 방법
  - 패키지 위치를 지정하지 않고, 설정 정보 클래스의 위치를 `프로젝트 최상단`에 두는 것을 권장한다.
    - 최근 `스프링 부트`도 이 방법을 기본으로 제공한다.
  - 예시)
    - `com.hello` --> 프로젝트 시작 루트, 
      - 여기에 `AppConfig` 같은 메인 설정 정보를 두고, `@ComponentScan` 애노테이션을 붙이고, `basePackages` 지정은 생략한다.
      - 이렇게 하면 `com.hello` 를 포함한 하위는 모두 자동으로 `컴포넌트 스캔`의 대상이 된다.
  - 참고
    - `스프링 부트`를 사용하면 `스프링 부트`의 대표 시작 정보인 `@SpringBootApplication` 를 이 프로젝트 시작 루트 위치에 두는 것이 관례이다.
      - (그리고 이 설정안에 바로 `@ComponentScan` 이 들어있다!)

- `컴포넌트 스캔` 기본 대상
  - `컴포넌트 스캔`은 `@Component` 뿐만 아니라 다음과 내용도 추가로 대상에 포함한다.
    - `@Component` : 컴포넌트 스캔에서 사용
    - `@Controller` : 스프링 MVC 컨트롤러에서 사용
    - `@Service` : 스프링 비즈니스 로직에서 사용
    - `@Repository` : 스프링 데이터 접근 계층에서 사용
    - `@Configuration` : 스프링 설정 정보에서 사용
  - 다음 해당 클래스들의 소스 코드를 보면 `@Component`를 포함하고 있다.
    - `Controller`, `Service`, `Repository` 인터테이스
- 참고: 
  - 애노테이션에는 상속관계라는 것이 없다.
  - 애노테이션이 특정 애노테이션을 들고 있는 것을 인식할 수 있는 것은 
    - `자바` 언어가 지원하는 기능은 아니고,
    - `스프링`이 지원하는 기능이다.
- `컴포넌트 스캔`의 용도 뿐만 아니라 다음 애노테이션이 있으면 스프링은 부가 기능을 수행한다.
  - `@Controller` : 스프링 MVC 컨트롤러로 인식
  - `@Repository` : 스프링 데이터 접근 계층으로 인식하고, 데이터 계층의 예외를 스프링 예외로 변환해준다.
  - `@Configuration` : 앞서 보았듯이 스프링 설정 정보로 인식하고, 스프링 빈이 싱글톤을 유지하도록 추가 처리를 한다.
  - `@Service` : 사실 특별한 처리를 하지 않는다. 대신 개발자들이 핵심 비즈니스 로직이 여기에 있겠구나 라고 비즈니스 계층을 인식하는데 도움이 된다.

- 참고: 
  - `useDefaultFilters` 옵션은 기본으로 켜져있는데, 이 옵션을 끄면 기본 스캔 대상들이 제외된다.
    - 그냥 이런 옵션이 있구나 정도 알고 넘어가자.

### 필터

- 필터를 쓰지 않고 기본(`@ComponentScan()`) 그대로 쓰는 것을 권장한다.
  - 지금은 이런게 있구나 정도 참고만 하자.

- 설정 정보의 `@ComponentScan()`에 옵션을 주어 필터를 지정할 수 있다.
  - `includeFilters` : `컴포넌트 스캔` 대상을 추가로 지정한다. `(거의 사용 안함)`
  - `excludeFilters` : `컴포넌트 스캔`에서 제외할 대상을 지정한다. `(간혹 사용함)`

- 소스 코드 (비공개 레포지토리):
  - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/test/java/hello/core/scan/filter
    - 사용할 애노테이션을 직접 만든다.
      - `MyIncludeComponent`: 컴포넌트 스캔 대상에 추가할 애노테이션
      - `MyExcludeComponent`: 컴포넌트 스캔 대상에서 제외할 애노테이션
    - 빈 2개를 만든다.
      - `BeanA`: 컴포넌트 스캔 대상에 추가할 클래스. `@MyIncludeComponent` 적용
      - `BeanB`: 컴포넌트 스캔 대상에서 제외할 클래스. `@MyExcludeComponent` 적용
    - 설정 정보와 전체 테스트 코드 작성: `ComponentFilterAppConfigTest`
        - 중첩 클래스로 설정 정보 클래스 생성 (`ComponentFilterAppConfig`)
          - `@ComponentScan()`에 필터를 추가한다.
            - `includeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class)`
              - `BeanA`가 스프링 빈에 등록된다.
            - `excludeFilters = @Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class)`
              - `BeanB`는 스프링 빈에 등록되지 않는다.

- `FilterType` 5가지 옵션
  - `ANNOTATION`: 기본값, 애노테이션을 인식해서 동작한다.
    - ex) `org.example.SomeAnnotation`
  - `ASSIGNABLE_TYPE`: 지정한 타입과 자식 타입을 인식해서 동작한다.
    - ex) `org.example.SomeClass`
  - `ASPECTJ`: AspectJ 패턴 사용
    - ex) `org.example..*Service+`
  - `REGEX`: 정규 표현식
    - ex) `org\.example\.Default.*`
  - `CUSTOM`: TypeFilter 이라는 인터페이스를 구현해서 처리
    - ex) `org.example.MyTypeFilter`

- 예시) `BeanA`도 빼고 싶으면 다음과 같이 추가하면 된다.
    ```java
    //ComponentFilterAppConfigTest의 일부 코드
    
    @Configuration
    @ComponentScan(
        includeFilters = {
                @Filter(type = FilterType.ANNOTATION, classes = MyIncludeComponent.class)
        },
        excludeFilters = {
                @Filter(type = FilterType.ANNOTATION, classes = MyExcludeComponent.class), 
                @Filter(type = FilterType.ASSIGNABLE_TYPE, classes = BeanA.class) //추가. BeanA도 빼기
        }
    )
    static class ComponentFilterAppConfig {
    }
    ```
    - 원본 소스코드 (비공개 레포지토리): `ComponentFilterAppConfigTest`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scan/filter/ComponentFilterAppConfigTest.java

- 정리: 
  - `@Component`면 충분하기 때문에, `includeFilters`를 사용할 일은 거의 없다.
  - `excludeFilters`는 여러가지 이유로 간혹 사용할 때가 있지만 많지는 않다.
  - 최근 `스프링 부트`는 `컴포넌트 스캔`을 기본으로 제공하는데, 옵션을 변경하면서 사용하기 보다는 스프링의 기본 설정에 최대한 맞추어 사용하는 것을 권장한다.

### 중복 등록과 충돌

- `컴포넌트 스캔`에서 같은 빈 이름을 등록하면? 2가지 상황으로 나누어 보자.
  - `자동 빈 등록` vs `자동 빈 등록 `
  - `수동 빈 등록` vs `자동 빈 등록`

- `자동 빈 등록` vs `자동 빈 등록`
  - `컴포넌트 스캔`에 의해 자동으로 `스프링 빈`이 등록되는데, 그 이름이 같은 경우 스프링은 `오류`를 발생시킨다. (`ConflictingBeanDefinitionException`)

- `수동 빈 등록` vs `자동 빈 등록`
  - 수동 빈 등록이 우선권을 가졌었으나 문제가 많아, 최신 `스프링 부트`에서는 `오류`가 나도록 기본 값을 바꾸었다.
  - 소스 코드 (비공개 레포지토리):
    - 수동 빈 등록: `AutoAppConfig`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/AutoAppConfig.java
          - `@Bean(name = "memoryMemberRepository")`
    - 자동 빈 등록: `MemoryMemberRepository`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/member/MemoryMemberRepository.java
          - `@Component`
          - `public class MemoryMemberRepository implements MemberRepository {}`
  - 이전에는...
    - 수동 빈 등록이 우선권을 가졌었다. (수동 빈이 자동 빈을 오버라이딩 해버린다.)
    - 문제점
      - 여러명이서 개발을 하다보니, 설정들이 꼬여서 잡기 어려운 버그가 만들어진다.
        - 누구는 수동을 고려해서 하고, 누구는 자동으로만 하는데, 결국 수동이 다 오버라이딩 해버린다.
        - 그래서 예상치 못한 문제들이 발생한다...
  - 최근에는...
    - 그래서 최근에는 `스프링 부트`에서는 `수동 빈 등록`과 `자동 빈 등록`이 충돌나면 `오류`가 발생하도록 기본 값을 바꾸었다.
      - 스프링 부트인 `CoreApplication`을 실행해보면 오류를 볼 수 있다.

## 8. 의존관계 자동 주입

### 다양한 의존관계 주입 방법

- 의존관계 주입은 크게 4가지 방법이 있다.
  - `생성자 주입`
  - `수정자 주입`(`setter 주입`)
  - `필드 주입`
  - `일반 메서드 주입`

- `생성자 주입`
  - 특징
    - 생성자 호출시점에 딱 1번만 호출되는 것이 보장된다.
    - `불변`, `필수` 의존관계에 사용
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (2. 생성자 주입) 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
      - 중요: 생성자가 딱 1개만 있으면 `@Autowired`를 생략해도 자동 주입 된다. ⭐

- `수정자 주입(setter 주입)`
  - 특징
    - `선택`, `변경` 가능성이 있는 의존관계에 사용
    - `자바빈 프로퍼티 규약`의 수정자 메서드 방식을 사용하는 방법이다.
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (3. setter 주입) 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
      - 참고: `@Autowired`의 기본 동작은 주입할 대상이 없으면 오류가 발생한다.
        - 주입할 대상이 없어도 동작하게 하려면 `@Autowired(required = false)`로 지정하면 된다.
  - `자바빈 프로퍼티 규약`

    ```java
    class Data {
        private int age;
        
        public void setAge(int age) {
            this.age = age;
        }
        
        public int getAge() {
            return age;
        }
    }
    ```

- `필드 주입` // 왠만하면 사용하지 말자.
  - 특징
    - 코드가 간결해서 많은 개발자들을 유혹하지만, 외부에서 변경이 불가능해서 테스트 하기 힘들다는 치명적인 단점이 있다.
    - DI 프레임워크가 없으면 아무것도 할 수 없다.
    - 사용하지 말자!
    - 아래 경우만 사용을 고려하자.
      - 애플리케이션의 실제 코드와 관계 없는 테스트 코드
      - 스프링 설정을 목적으로 하는 `@Configuration` 같은 곳에서만 특별한 용도로 사용
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (4. 필드 주입) 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
  - 참고: `순수한 자바 테스트 코드`에는 당연히 `@Autowired`가 동작하지 않는다. 
    - `@SpringBootTest`처럼 `스프링 컨테이너`를 테스트에 통합한 경우에만 가능하다.

- `일반 메서드 주입` // 잘 사용하지 않는다.
  - 특징
    - 한번에 여러 필드를 주입 받을 수 있다.
    - 일반적으로 잘 사용하지 않는다.
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (5. 일반 메서드 주입) 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java

### 옵션 처리

<details>
<summary>(에러 디버깅) 스프링 부트 3.2 매개변수 이름 인식 문제 💦</summary>

- 개요
    - "옵셥 처리" 초반에, 그동안 작성한 테스트 코드가 정상 작동하는지 확인하였다.
    - 강사님 말씀대로 따랐는데, 강의에선 잘 되나, 나는 해결 되지 않는 에러가 1개 있었다.

      ![error](https://github.com/user-attachments/assets/158fda54-514f-4901-bb43-f62d29ca1299)

    - 찾아보니, 세팅 문제였다.
        - 참고 링크: [(인프런 Q&A) 스프링 부트 3.2 매개변수 이름 인식 문제](https://www.inflearn.com/community/questions/1089023/%EC%84%B9%EC%85%98-7-%EC%98%B5%EC%85%98-%EC%B2%98%EB%A6%AC-%EC%A0%84%EC%B2%B4-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A4%91-coreapplicationtests-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%9D%98-contextloads-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%8B%A4%ED%8C%A8-%EC%A7%88%EB%AC%B8%EC%9E%85%EB%8B%88%EB%8B%A4)
            - 강사님 답변 중 해결방안 3번을 따랐더니 해결이 되었다.

              ![setting](https://github.com/user-attachments/assets/ea6079aa-3b06-4e7e-86f4-50e2a1a40355)

                - 강의 초반에는 `Gradle`로 설정했었으나, 테스트 속도가 느려서 `IntellJ`로 바꿨더니 빨라졌다.
                - 그래서 그대로 사용하고 있었는데, 여기서 에러가 났던 것이다.

</details>

- 옵션 처리 서론
  - 주입할 `스프링 빈`이 없어도 동작해야 할 때가 있다.
  - 그런데 `@Autowired`만 사용하면 `required` 옵션의 기본값이 `true`로 되어 있어서 `자동 주입 대상`이 없으면 오류가 발생한다.

- `자동 주입 대상`을 `옵션`으로 처리하는 방법
  - `@Autowired(required=false)`: 자동 주입할 대상이 없으면 수정자 메서드 자체가 호출 안됨
  - `@Nullable`(org.springframework.lang.@Nullable): 자동 주입할 대상이 없으면 `null`이 입력된다.
  - `Optional<>` : 자동 주입할 대상이 없으면 `Optional.empty`가 입력된다.
  - 소스코드 (비공개 레포지토리): `AutowiredTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/autowired/AutowiredTest.java
  - 참고:` @Nullable`, `Optional`은 스프링 전반에 걸쳐서 지원된다. 
    - 예를 들어서 생성자 자동 주입에서 특정 필드에만 사용해도 된다.

### 생성자 주입을 선택해라!

- 추세
  - 과거에는 `수정자 주입`과 `필드 주입`을 많이 사용했지만, 
  - 최근에는 스프링을 포함한 DI 프레임워크 대부분이 `생성자 주입`을 권장한다.

- 왜 `생성자 주입`을 권장하나?
  - `불변`
    - 대부분의 의존관계 주입은 한번 일어나면 애플리케이션 종료시점까지 의존관계를 변경할 일이 없다. 
      - 오히려 대부분의 의존관계는 애플리케이션 종료 전까지 변하면 안된다.(불변해야 한다.)
    - 수정자 주입을 사용하면, `setXxx` 메서드를 `public`으로 열어두어야 한다.
      - 누군가 실수로 변경할 수 도 있고, 변경하면 안되는 메서드를 열어두는 것은 좋은 설계 방법이 아니다.
    - 생성자 주입은 객체를 생성할 때 딱 1번만 호출되므로 이후에 호출되는 일이 없다. 따라서 불변하게 설계할 수 있다.
  - `누락`
    - 소스 코드 (비공개 레포지토리): 
      - `OrderServiceImpl`: (3. setter 주입) 참고
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
      - `OrderServiceImplTest`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/order/OrderServiceImplTest.java
    - 프레임워크 없이 순수한 자바 코드를 단위 테스트 하는 경우에 의존관계 주입이 누락될 수 있다.
      - `컴파일러`가 에러를 발생시키지 않고 실행된다. 실행 후에야 문제를 찾을 수 있다.
      - 반면, `생성자 주입`을 사용하면 주입 데이터를 누락 했을 때 `컴파일 오류`가 발생한다.
  - `final` 키워드
    - `생성자 주입`을 사용하면 필드에 `final` 키워드를 사용할 수 있다. 
      - 그래서 `생성자`에서 혹시라도 값이 설정되지 않는 오류를 `컴파일 시점`에 막아준다.
    - 참고: 오직 `생성자 주입 방식`만 `final` 키워드를 사용할 수 있다.
      - `수정자 주입`을 포함한 `나머지 주입 방식`은 모두 `생성자` 이후에 호출되므로, 필드에 `final` 키워드를 사용 할 수 없다.

- 정리
  - `생성자 주입` 방식을 선택하는 이유는 여러가지가 있지만, 프레임워크에 의존하지 않고, `순수한 자바` 언어의 특징을 잘 살리는 방법이기도 하다.
  - 기본으로 `생성자 주입`을 사용하고, 필수 값이 아닌 경우에는 `수정자 주입` 방식을 옵션으로 부여하면 된다. 
    - `생성자 주입`과 `수정자 주입`을 동시에 사용할 수 있다.
  - 항상 `생성자 주입`을 선택해라! 
    - 그리고 가끔 옵션이 필요하면 `수정자 주입`을 선택해라. 
    - `필드 주입`은 사용하지 않는 게 좋다.

### 롬복과 최신 트랜드

- 서론
  - 막상 개발을 해보면, 대부분이 다 불변이다.
    - 필드에 `final` 키워드를 사용하고, `생성자`도 만들어야 하고, 주입 받은 값을 `대입하는 코드`도 만들어야 한다.
    - 이런 반복적인 코드를 좀 편리하게 사용하는 방법? --> `롬복`


- 롬봄 라이브러리 적용 방법
  - `인텔리제이`에 롬복 설치
    - 롬복 설치

      ![install lombok](https://github.com/user-attachments/assets/7165b06a-b7d8-4e22-949b-72f73473d936)

    - 세팅 (`Annotation Processors` --> `Enable annotation processing`)

      ![annotaion processors](https://github.com/user-attachments/assets/9122bcf7-b148-4c7f-aead-987d999c66bf)

  - `build.gradle`에 라이브러리 및 환경 추가
    - 소스 코드 (비공개 레포지토리):
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/build.gradle

- 롬복 테스트
  - 소스 코드 (비공개 레포지토리): `HelloLombok`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/HelloLombok.java
      - `Lombok`을 사용하면, 적용한 애노테이션에 따라서 `getter`, `setter`, `생성자`, `toString` 등을 자동으로 만들어준다. (실무에서 많이 쓴다!!) ⭐
        - `@Getter`
        - `@Setter`
        - `@NoArgsConstructor`
        - `@ToString`

- 롬봄 적용
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (7. 롬봄 사용) 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
      - `@RequiredArgsConstructor`: 롬복이 `final`로 되어있는 필드를 보고 자동으로 생성자를 만들어준다. ⭐
        - 많이 사용한다!! 
          - 개발자가 별도로 해줄게 없다. 애노테이션만 붙이면 된다. 편하다!!!
        - 롬복이 자바의 애노테이션 프로세서라는 기능을 이용해서 컴파일 시점에 생성자 코드를 자동으로 생성해준다.
          - 실제 `class`파일을 열어보면 확인할 수 있다.

### 조회 빈이 2개 이상 - 문제

- `@Autowired`는 `타입(Type)`으로 조회한다.
  - 타입으로 조회하기 때문에, 마치 다음 코드와 유사하게 동작한다. (실제로는 더 많은 기능을 제공한다.) 
    - `ac.getBean(DiscountPolicy.class)`
  - 타입으로 조회하면 선택된 빈이 2개 이상일 때 문제가 발생한다.
    - `NoUniqueBeanDefinitionException` 발생
      - 예시) `DiscountPolicy` 인터페이스의 구현체인 `FixDiscountPolicy`, `RateDiscountPolicy` 둘다 스프링 빈으로 선언시
        - 즉, 2개 모두 `@Component`가 붙어있을시...
        - 하나의 빈을 기대했는데 `fixDiscountPolicy`, `rateDiscountPolicy` 2개가 발견되었다고 에러로 알려준다.

- 해결방법: `@Autowired` 필드 명, `@Qualifier`, `@Primary`
  - `하위 타입`으로 지정할 수 도 있지만, 하위 타입으로 지정하는 것은 `DIP`를 위배하고 `유연성`이 떨어진다. 
  - 그리고 이름만 다르고, 완전히 `똑같은 타입의 스프링 빈이 2개 있을 때` 해결이 안된다.
  - `스프링 빈을 수동 등록`해서 문제를 해결해도 되지만, `의존 관계 자동 주입`에서 해결하는 여러 방법이 있다.
  - 바로 아래에서 다룬다..

### @Autowired 필드 명, @Qualifier, @Primary

- 조회 대상 빈이 2개 이상일 때 해결 방법
  - `@Autowired` 필드 명 매칭
  - `@Qualifier` --> `@Qualifier`끼리 매칭 --> 빈 이름 매칭
  - `@Primary` 사용

- `@Autowired` 필드 명 매칭
  - `@Autowired`는 `타입` 매칭을 시도하고, 이때 여러 빈이 있으면 `필드 이름`, `파라미터 이름`으로 빈 이름을 추가 매칭한다.
  - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (8. 파리미터명으로 빈 이름 매칭) 참고
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
  - `@Autowired` 매칭 우선순위 정리
    - 1순위) `타입` 매칭
    - 2순위) `타입` 매칭의 결과가 2개 이상일 때 `필드 명`, `파라미터 명`으로 빈 이름 매칭

- `@Qualifier` 사용
  - 개요
    - `@Qualifier`는 추가 구분자를 붙여주는 방법이다. 
    - 주입시 추가적인 방법을 제공하는 것이지, 빈 이름을 변경하는 것은 아니다.
  - 방법
    - 빈 등록시 `@Qualifier`를 붙여 준다.
      - 소스 코드 (비공개 레포지토리): `RateDiscountPolicy`, `FixDiscountPolicy` 참고
        - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/discount
          - `@Qualifier("mainDiscountPolicy")`
          - `@Qualifier("fixDiscountPolicy")`
    - 주입시에 `@Qualifier`를 붙여주고 등록한 이름을 적어준다.
        - 소스 코드 (비공개 레포지토리): `OrderServiceImpl` (9. @Qualifier 사용 ) 참고
          - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
            - `public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {...}`

- `@Primary` 사용
  - `@Autowired`시에 여러 빈이 매칭되면 `@Primary`가 우선권을 가진다.
  - 소스 코드 (비공개 레포지토리):
    - `RateDiscountPolicy`: `@Primary` 추가
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/discount/RateDiscountPolicy.java
    - `OrderServiceImpl`: 사용 코드
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java

- `@Primary` vs `@Qualifier` 
  - 차이점
    - `@Qualifier`의 단점은 주입 받을 때 다음과 같이 모든 코드에 `@Qualifier`를 붙여주어야 한다는 점이다.
    - `public OrderServiceImpl(MemberRepository memberRepository, @Qualifier("mainDiscountPolicy") DiscountPolicy discountPolicy) {...}`
    - 반면에 `@Primary`를 사용하면 이렇게 `@Qualifier`를 붙일 필요가 없다.
  - 활용방법:
    - 자주 `@primary`,  특별: `@Qualifier`
    - 예시)
      - 코드에서 `자주 사용하는 메인` 데이터베이스의 커넥션을 획득하는 스프링 빈이 있고, 코드에서 특별한 기능으로 `가끔 사용하는 서브` 데이터베이스의 커넥션을 획득하는 스프링 빈이 있다고 생각해보자.
        - `메인` 데이터베이스의 커넥션을 획득하는 스프링 빈은 `@Primary`를 적용해서 조회하는 곳에서 `@Qualifier` 지정 없이 편리하게 조회하고,
        - `서브` 데이터베이스 커넥션 빈을 획득할 때는 `@Qualifier`를 지정해서 `명시적으로` 획득 하는 방식으로 사용하면 코드를 깔끔하게 유지할 수 있다. 
  - 우선순위
    - `@Primary` < `@Qualifier`
      - `@Primary`는 기본값 처럼 동작하는 것이고,` @Qualifier`는 매우 상세하게 동작한다.
      - 스프링은 `자동`보다는 `수동`이, `넒은 범위의 선택권` 보다는 `좁은 범위의 선택권`이 우선 순위가 높다. 
      - 따라서 여기서도 `@Qualifier`가 우선권이 높다.

### 애노테이션 직접 만들기

- `@Qualifier("mainDiscountPolicy")` 이렇게 `문자`를 적으면 컴파일시 타입 체크가 안되는데, `애노테이션`을 직접 만들면 문제를 해결할 수 있다.
- 예시
  - 애노테이션 생성
    - 소스 코드 (비공개 레포지토리): `MainDiscountPolicy`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/annotation/MainDiscountPolicy.java
        - 생성시 `@interface` 키워드 사용
        - 애노테이션 총 4개 추가
          - `Qualifier` 클래스(애노테이션)에 붙어있는 애노테이션 3줄 복사해왔다. (`@Target(...)`, `@Retention(...)`, `@Inherited`)
          - `@Qualifier("mainDiscountPolicy")` 추가 --> 이게 실제 애노테이션 명칭이 됨. (`@MainDiscountPolicy`)
  - 애노테이션 사용
    - 소스 코드 (비공개 레포지토리): `OrderServiceImpl`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/order/OrderServiceImpl.java
        - `public OrderServiceImpl(MemberRepository memberRepository, @MainDiscountPolicy DiscountPolicy discountPolicy) {...}`
          - `@MainDiscountPolicy` 사용
- 참고
  - 애노테이션에는 `상속`이라는 개념이 없다. 
  - 이렇게 여러 애노테이션을 모아서 사용하는 기능은 `스프링`이 지원해주는 기능이다. 
  - `@Qualifier` 뿐만 아니라 다른 애노테이션들도 함께 조합해서 사용할 수 있다. 
    - 단적으로 `@Autowired`도 재정의 할 수 있다. 
      - 물론 스프링이 제공하는 기능을 뚜렷한 목적 없이 무분별하게 재정의 하는 것은 유지보수에 더 혼란만 가중할 수 있다.

### 조회한 빈이 모두 필요할 때, List, Map

- 서론
  - 해당 타입의 `스프링 빈`이 다 필요한 경우도 있다.
    - 예시) 할인 서비스를 제공하는데, 클라이언트가 할인의 종류(rate, fix)를 선택할 수 있다고 가정해보자. 
  - 스프링을 사용하면 소위 말하는 전략 패턴을 매우 간단하게 구현할 수 있다.

- 소스 코드 (비공개 레포지토리): `AllBeanTest`
  - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/autowired/AllBeanTest.java
    - `DiscountPolicy`의 하위 타입인 `fixDiscountPolicy`, `rateDiscountPolicy` 스프링빈을 모두 불러와서 하나의 `List`, `Map`에 각각 저장해놓고 원하는 빈을 꺼내어 사용한다.

### 자동, 수동의 올바른 실무 운영 기준

- 편리한 `자동` 기능을 기본으로 사용하자.
  - 스프링, 스프링 부트의 추세가 `자동`임. (자세한 내용은 교재 p.20 참고)
- `수동 빈 등록`은 언제?
  - 애플리케이션은 크게 `업무 로직`과 `기술 지원 로직`으로 나눌 수 있다.
    - `업무 로직 빈`: 
      - 웹을 지원하는 `컨트롤러`, 핵심 비즈니스 로직이 있는 `서비스`, 데이터 계층의 로직을 처리하는 `리포지토리`등이 모두 업무 로직이다. 
      - 보통 비즈니스 요구사항을 개발할 때 추가되거나 변경된다.
    - `기술 지원 빈`: 
      - `기술적인 문제`나 `공통 관심사(AOP)`를 처리할 때 주로 사용된다. 
      - 데이터베이스 연결이나, 공통 로그처리 처럼 업무 로직을 지원하기 위한 `하부 기술`이나 `공통 기술`들이다.
  - `업무 로직`은 숫자도 매우 많고, 한번 개발해야 하면 컨트롤러, 서비스, 리포지토리 처럼 어느정도 유사한 패턴이 있다. 
    - 이런 경우 `자동 기능`을 적극 사용하는 것이 좋다. 
    - 보통 문제가 발생해도 어떤 곳에서 문제가 발생했는지 명확하게 파악하기 쉽다.
  - `기술 지원 로직`은 업무 로직과 비교해서 그 수가 매우 적고, 보통 애플리케이션 전반에 걸쳐서 광범위하게 영향을 미친다. 
    - 그리고 업무 로직은 문제가 발생했을 때 어디가 문제인지 명확하게 잘 드러나지만, 기술 지원 로직은 적용이 잘 되고 있는지 아닌지 조차 파악하기 어려운 경우가 많다.
    - 그래서 이런 기술 지원 로직들은 가급적 `수동 빈 등록`을 사용해서 명확하게 드러내는 것이 좋다. ⭐
      - 설정 정보에 한눈에 딱! 바로 나타나게 하는 것이 유지보수 하기 좋다.
- 비즈니스 로직 중에서 `다형성`을 적극 활용할 때
  - 위 `AllBeanTest` 예시
    - `DiscountService`가 의존관계 자동 주입으로 `Map<String, DiscountPolicy>`에 주입을 받는 상황.
      - 여기에 어떤 빈들이 주입될 지, 각 빈들의 이름은 무엇일지 코드만 보고 한번에 쉽게 파악하기 어렵다.
    - `다형성`이 내가 작성한거면 이해가 잘 되는데, 다른 사람 코드는 파악하기 너무 어렵다.
      - 이런 경우 `수동 빈으로 등록`하거나 또는 `자동`으로하면 `특정 패키지에 같이 묶어`두는게 좋다!
    - 이 부분을 별도의 `설정 정보`로 만들고, `수동으로 등록`하면 다음과 같다.

      ```java
      @Configuration
      public class DiscountPolicyConfig {
        
          @Bean
          public DiscountPolicy rateDiscountPolicy() {
              return new RateDiscountPolicy();
          }
        
          @Bean
          public DiscountPolicy fixDiscountPolicy() {
              return new FixDiscountPolicy();
          }
      }
      ```
      - 이 `설정 정보`만 봐도 한눈에 빈의 이름은 물론이고, 어떤 빈들이 주입될지 파악할 수 있다.
      - 그래도 `빈 자동 등록`을 사용하고 싶으면 파악하기 좋게 `DiscountPolicy`의 구현 빈들만 따로 모아서 `특정 패키지`에 모아두자.

- 정리
  - 편리한 `자동 기능`을 `기본`으로 사용하자.
  - 직접 등록하는 기술 지원 객체는 `수동 등록`.
  - 다형성을 적극 활용하는 비즈니스 로직은 `수동 등록`을 고민해보자.

## 9. 빈 생명주기 콜백

### 빈 생명주기 콜백 시작

- 서론
  - 데이터베이스 커넥션 풀이나, 네트워크 소켓처럼...
    - 애플리케이션 `시작 시점`에 필요한 연결을 미리 해두고, 
    - 애플리케이션 `종료 시점`에 연결을 모두 종료하는 작업을 진행하려면, 객체의 `초기화`와 `종료` 작업이 필요하다.
  - 스프링을 통해 이러한 `초기화` 작업과 `종료` 작업을 어떻게 진행하는지 알아보자.

- `초기화 콜백`, `소멸전 콜백`
  - `스프링 빈`은 간단하게 다음과 같은 라이프사이클을 가진다.
    - 객체 생성 ➡️ 의존관계 주입
  - `의존관계 주입`이 모두 완료된 시점을 알아야 한다.
    - `스프링 빈`은 객체를 생성하고, `의존관계 주입`이 다 끝난 다음에야 필요한 데이터를 사용할 수 있는 준비가 완료된다. 
    - 따라서 `초기화` 작업은 `의존관계 주입`이 모두 완료되고 난 다음에 호출해야 한다. 
    - 그런데 개발자가 `의존관계 주입`이 모두 완료된 시점을 어떻게 알 수 있을까?
  - `콜백 메서드`
    - `스프링`은 `의존관계 주입`이 완료되면 `스프링 빈`에게 `콜백 메서드`를 통해서 `초기화 시점`을 알려주는 다양한 기능을 제공한다. 
    - 또한 `스프링`은 스프링 컨테이너가 `종료되기 직전`에 `소멸 콜백`을 준다. 따라서 안전하게 종료 작업을 진행할 수 있다.
  - `스프링 빈`의 이벤트 라이프사이클
    - 스프링 컨테이너 생성 ➡️ 스프링 빈 생성 ➡️ 의존관계 주입 ➡️ `초기화 콜백` ➡️ 사용 ➡️ `소멸전 콜백` ➡️ 스프링 종료
  - 정리
    - `초기화 콜백`: 빈이 생성되고, 빈의 의존관계 주입이 완료된 후 호출
    - `소멸전 콜백`: 빈이 소멸되기 직전에 호출

- 참고: 객체의 `생성`과 `초기화`를 `분리`하자.
  - `생성자` 안에서 무거운 `초기화` 작업을 함께 하는 것 보다는, 객체를 `생성`하는 부분과 `초기화` 하는 부분을 명확하게 나누는 것이 유지보수 관점에서 좋다. 
    - `생성자`는 객체를 생성하는 책임을 가진다. 
    - `초기화`는 외부 커넥션을 연결하는등 무거운 동작을 수행한다.
  - 물론 `초기화` 작업이 내부 값들만 약간 변경하는 정도로 단순한 경우에는 `생성자`에서 한번에 다 처리하는게 더 나을 수 있다.

- 예제
  - 소스 코드 (비공개 레포지토리):
    - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/test/java/hello/core/lifecycle
      - `NetworkClient` 참고.
      - `BeanLifeCycleTest` 참고. // 스프링 환경설정과 실행
    - 4번으로 나누어 비교해보았다.
      - 1번) 초기 실행 
        - 출력결과가 예상했던대로 나오지 않는다... 그래서 해결방법을 아래와 같이 알아봤다.
    - 스프링은 크게 3가지 방법으로 `빈 생명주기 콜백`을 지원한다.
      - 2번) `InitializingBean`, `DisposableBean` 적용 // `이 방법은 거의 사용하지 않는다.`
      - 3번) `@Bean(initMethod = "init", destroyMethod = "close")` 적용 //`4번)을 못쓸때 사용` (외부 라이브러리)
      - 4번) `@PostConstruct`, `@PreDestroy` 적용 // `결론은 이거 사용!` ⭐
    - 자세한 설명은 아래서 확인하자!

### 인터페이스 InitializingBean, DisposableBean

- 위 예제 코드 `2번)` 참고
- 설명
  - `InitializingBean`, `DisposableBean` 인터페이스를 구현하여 사용한다.
    - `InitializingBean`은 `afterPropertiesSet()` 메서드로 초기화를 지원한다.
    - `DisposableBean`은 `destroy()` 메서드로 소멸을 지원한다.
  - 단점
    - 스프링 전용 인터페이스다. 해당 코드가 `스프링 코드에 의존한다.`
    - 초기화, 소멸 `메서드의 이름`을 변경할 수 없다.
    - 내가 코드를 고칠 수 없는 `외부 라이브러리`에 적용할 수 없다.
  - 지금은 이 방식을  거의 사용하지 않는다.

### 빈 등록 초기화, 소멸 메서드 지정

- 위 예제 코드 `3번)` 참고
- 설명
  - 설정 정보에 `@Bean(initMethod = "init", destroyMethod = "close")` 처럼 초기화, 소멸 메서드를 지정할 수 있다.
  - 장점
    - 스프링 빈이 `스프링 코드에 의존하지 않는다.`
    - `메서드 이름`을 자유롭게 줄 수 있다.
    - 코드가 아니라 설정 정보를 사용하기 때문에, 코드를 고칠 수 없는 `외부 라이브러리`에도 초기화, 종료 메서드를 적용할 수 있다.
  - 종료 메서드 추론
    - `@Bean`의 `destroyMethod` 속성에는 아주 특별한 기능이 있다.
    - 라이브러리는 대부분 `close`, `shutdown` 이라는 이름의 종료 메서드를 사용한다.
    - `@Bean`의 `destroyMethod`는 기본값이 `(inferred)`(추론)으로 등록되어 있다.
      - 이 추론 기능은 `close`, `shutdown`라는 이름의 메서드를 자동으로 호출해준다. 
      - 이름 그대로 종료 메서드를 추론해서 호출해준다.
    - 따라서 직접 스프링 빈으로 등록하면 종료 메서드는 따로 적어주지 않아도 잘 동작한다.
    - 추론 기능을 사용하기 싫으면 `destroyMethod=""` 처럼 빈 공백을 지정하면 된다.

### 애노테이션 @PostConstruct, @PreDestroy

- 위 예제 코드 `4번)` 참고
- 특징
  - `최신 스프링`에서 가장 권장하는 방법이다.
  - 애노테이션 하나만 붙이면 되므로 매우 편리하다.
  - 스프링이 아닌 다른 컨테이너에서도 동작한다.
    - 패키지가 `javax.annotation.PostConstruct`이다. (지금은 `javax`가 아닌 `jakarta`임)
    - 스프링에 종속적인 기술이 아니라 JSR-250 라는 자바 표준이다. 
  - 컴포넌트 스캔과 잘 어울린다.
  - 유일한 단점: `외부 라이브러리`에는 적용하지 못한다.
    - 외부 라이브러리를 초기화, 종료 해야 하면 `@Bean`의 기능을 사용하자. (예제 `3번)` 참고) 

## 10. 빈 스코프

### 빈 스코프란?

- 지금까지 `스프링 빈`이 `스프링 컨테이너`의 시작과 함께 생성되어서 `스프링 컨테이너`가 종료될 때 까지 유지된다고 학습했다. 
  - 이것은 `스프링 빈`이 기본적으로 `싱글톤 스코프`로 생성되기 때문이다. 
- `스코프`는 `빈`이 존재할 수 있는 범위를 뜻한다. ✅

- `스프링`은 다음과 같은 다양한 `스코프`를 지원한다.
  - `싱글톤`: 기본 스코프. 스프링 컨테이너의 `시작과 종료까지` 유지되는 가장 넓은 범위의 스코프이다.
  - `프로토타입`: 스프링 컨테이너는 프로토타입 `빈의 생성과 의존관계 주입까지만` 관여하고, 더는 관리하지 않는 매우 짧은 범위의 스코프이다.
  - `웹` 관련 스코프
    - `request`: 웹 요청이 들어오고 나갈때 까지 유지되는 스코프이다.
    - `session`: 웹 세션이 생성되고 종료될 때 까지 유지되는 스코프이다.
    - `application`: 웹의 서블릿 컨텍스트와 같은 범위로 유지되는 스코프이다.

- `빈 스코프`는 다음과 같이 지정할 수 있다.
    ```java
    @Scope("prototype") //빈 스코프 지정
    @Component
    public class HelloBean {} 
    ```
  - 수동 등록

    ```java
    @Scope("prototype") //빈 스코프 지정
    @Bean
    PrototypeBean HelloBean() {
        return new HelloBean();
    }
    ```

### 프로토타입 스코프

- `싱글톤 스코프` vs `프로토타입 스코프`
  - `싱글톤 스코프`의 빈을 조회하면, 스프링 컨테이너는 `항상 같은 인스턴스`의 스프링 빈을 반환한다.
  - 반면에 `프로토타입 스코프`를 스프링 컨테이너에 조회하면, 스프링 컨테이너는 `항상 새로운 인스턴스`를 생성해서 반환한다.

- 싱글톤 빈 요청

    ![싱글톤 빈 요청](https://github.com/user-attachments/assets/b7048cf1-678f-4da5-8de9-df8422e70581)

- 프로토타입 빈 요청

  ![프로토타입 빈 요청1](https://github.com/user-attachments/assets/477bf49b-edf0-4eb2-b298-70c36589267b)

  ![프로토타입 빈 요청2](https://github.com/user-attachments/assets/daa4e2b9-58ca-46ac-8179-05dca5f6ce7a)

- 정리
  - 여기서 핵심은 `스프링 컨테이너`는 `프로토타입` `빈을 생성`하고, `의존관계 주입`, `초기화`까지만 처리한다는 것이다.
    - 클라이언트에 빈을 반환하고, 이후 `스프링 컨테이너`는 생성된 프로토타입 빈을 `관리하지 않는다.`
    - 프로토타입 빈을 관리할 책임은 프로토타입 빈을 받은 클라이언트에 있다.
    - 그래서 `@PreDestroy` 같은 종료 메서드가 호출되지 않는다.

- `싱글톤 스코프` 빈 테스트
  - 소스 코드 (비공개 레포지토리): `SingletonTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonTest.java
      - 같은 인스턴스의 스프링 빈을 반환했다.

- `프로토타입 스코프` 빈 테스트
  - 소스 코드 (비공개 레포지토리): `PrototypeTest`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/PrototypeTest.java
      - `@Scope("prototype")` 사용
      - 다른 스프링 빈이 생성됐고, 초기화도 2번 실행되었다.

- 차이점
  - 생성시점
    - `싱글톤 빈`은 `스프링 컨테이너` `생성` 시점에 초기화 메서드가 실행 되지만, 
    - `프로토타입 스코프의 빈`은 `스프링 컨테이너`에서 빈을 `조회`할 때 생성되고, 초기화 메서드도 실행된다.
  - 종료시점
    - `싱글톤 빈`은 `스프링 컨테이너`가 관리하기 때문에, `스프링 컨테이너`가 종료될 때 빈의 `종료 메서드가 실행되지만`,
    - `프로토타입 빈`은 `스프링 컨테이너`가 생성과 의존관계 주입 그리고 초기화 까지만 관여하고, 더는 관리하지 않는다. 
      - 따라서 `프로토타입 빈`은 `스프링 컨테이너`가 종료될 때 `@PreDestroy` 같은 `종료 메서드가 전혀 실행되지 않는다`.


### 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 문제점

- 서론
  - `스프링 컨테이너`에 `프로토타입 스코프의 빈`을 요청하면 `항상 새로운 객체 인스턴스`를 생성해서 반환한다. 
  - 하지만 `싱글톤 빈`과 함께 사용할 때는 의도한 대로 잘 동작하지 않으므로 `주의`해야 한다.
- `프로토타입 빈` 직접 요청
    - `스프링 컨테이너`에 `프로토타입 빈`을 요청하면 `항상 새로운 객체 인스턴스`를 생성해서 반환한다. 
    
      ![스프링 컨테이너에 프로토타입 빈 직접 요청2](https://github.com/user-attachments/assets/ae1a5408-402d-4384-8b64-9e66de1cf063)

      - 클라이언트 A,B의 카운트가 각각 1이다. 
    - 소스 코드 (비공개 레포지토리): `SingletonWithPrototypeTest1` - `prototypeFind()` 참고
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonWithPrototypeTest1.java

- `싱글톤 빈`에서 `프로토타입 빈` 사용 ⭐
  - `1. 싱글톤과 프로토타입을 같이 쓰면, 프로토타입이 싱글톤처럼 사용되어버린다.` 
    - (싱글톤이 같은 프로토타입을 계속 가지고 있어서)
    - 클라이언트 A,B의 카운트가 모두 2가 된다. (카운트를 공유한다.)

    ![싱글톤에서 프로토타입 빈 사용1](https://github.com/user-attachments/assets/3b51d3d4-c382-46fc-aa7c-8f9220506bff)
    
    ![싱글톤에서 프로토타입 빈 사용2](https://github.com/user-attachments/assets/7a049e1b-8c08-4a33-a82c-ea3fd0a3b2be)

    ![싱글톤에서 프로토타입 빈 사용3](https://github.com/user-attachments/assets/4966222a-2e7a-4b69-b89b-2c690ed63e65)

    - `clientBean`이 내부에 가지고 있는 `프로토타입 빈`은 이미 과거에 주입이 끝난 빈이다. 
    - 주입 시점에 스프링 컨테이너에 요청해서 `프로토타입 빈`이 새로 생성이 된 것이지, 사용 할 때마다 새로 생성되는 것이 아니다!

  - 소스 코드 (비공개 레포지토리): `SingletonWithPrototypeTest1`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonWithPrototypeTest1.java
        - `// 1. 싱글톤과 프로토타입을 같이 쓰면, 프로토타입이 싱글톤처럼 사용되어버린다.` 참고

- 문제점
  - 스프링은 일반적으로 `싱글톤 빈`을 사용하므로, `싱글톤 빈`이 `프로토타입 빈`을 사용하게 된다. 
  - 그런데 `싱글톤 빈`은 생성 시점에만 의존관계 주입을 받기 때문에, `프로토타입 빈`이 새로 생성되기는 하지만, `싱글톤 빈`과 함께 계속 유지되는 것이 문제다.
  - 아마 원하는 것이 이런 것은 아닐 것이다. 
    - `프로토타입 빈`을 주입 시점에만 새로 생성하는게 아니라, 사용할 때 마다 새로 생성해서 사용하는 것을 원할 것이다.

### 프로토타입 스코프 - 싱글톤 빈과 함께 사용시 Provider로 문제 해결

- `싱글톤 빈`과 `프로토타입 빈`을 함께 사용할 때, 어떻게 하면 사용할 때 마다 항상 새로운 `프로토타입 빈`을 생성할 수 있을까?

- 가장 간단한 방법은 `싱글톤 빈`이 `프로토타입`을 사용할 때 마다 `스프링 컨테이너`에 새로 요청하는 것이다.
  - 소스 코드 (비공개 레포지토리): `SingletonWithPrototypeTest1`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonWithPrototypeTest1.java
      - `// 2. 단순하고 무식(?)한 해결방법: 싱글톤 빈이 프로토타입을 사용할 때 마다 스프링 컨테이너에 새로 요청.` 참고
        - `ac.getBean()`을 통해서 항상 새로운 프로토타입 빈이 생성된다.
        - 의존관계를 외부에서 주입(DI) 받는게 아니라, 이렇게 `직접 필요한 의존관계를 찾는 것`을 `Dependency Lookup(DL)` `의존관계 조회(탐색)`이라 한다.
      - 문제점 
        - 그런데 이렇게 스프링의 애플리케이션 컨텍스트 전체를 주입받게 되면, 스프링 컨테이너에 종속적인 코드가 되고, 단위 테스트도 어려워진다.
        - 지금 필요한 기능은 지정한 `프로토타입 빈`을 컨테이너에서 대신 찾아주는 딱! `DL` 정도의 기능만 제공하는 무언가가 있으면 된다.
          - `스프링`에는 이미 모든게 준비되어 있다.

- `ObjectFactory`, `ObjectProvider`
  - 지정한 빈을 컨테이너에서 대신 찾아주는 `DL` 서비스를 제공하는 것이 바로 `ObjectProvider`이다. 
    - 참고로, 과거에는 `ObjectFactory`가 있었는데, 여기에 편의 기능을 추가해서 `ObjectProvider`가 만들어졌다.
  - 소스 코드 (비공개 레포지토리): `SingletonWithPrototypeTest1`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonWithPrototypeTest1.java
      - `// 3. ObjectProvider 사용.` 참고
        - `prototypeBeanProvider.getObject()`을 통해서 항상 새로운 `프로토타입 빈`이 생성된다.
        - `ObjectProvider`의 `getObject()`를 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환 한다. (`DL`)
        - 스프링이 제공하는 기능을 사용하지만, 기능이 단순하므로 단위테스트를 만들거나 mock 코드를 만들기는 훨씬 쉬워진다.
        - `ObjectProvider`는 지금 딱 필요한 `DL` 정도의 기능만 제공한다.

  - 특징
    - `ObjectFactory`: 기능이 단순, 별도의 라이브러리 필요 없음, 스프링에 의존
    - `ObjectProvider`: `ObjectFactory` 상속, 옵션, 스트림 처리등 편의 기능이 많고, 별도의 라이브러리 필요 없음, 스프링에 의존
    
- `JSR-330 Provider`
  - 마지막 방법은 `javax.inject.Provider` 라는 `JSR-330 자바 표준`을 사용하는 방법이다.
    - `스프링 부트 3.0`은 `jakarta.inject.Provider`를 사용한다.
    - 이 방법을 사용하려면, `라이브러리`를 `gradle`에 추가해야 한다.
      - `jakarta.inject:jakarta.inject-api:2.0.1`
      - 소스 코드 (비공개 레포지토리): `build.gradle`
        - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/build.gradle
  - 소스 코드 (비공개 레포지토리): `SingletonWithPrototypeTest1`
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/test/java/hello/core/scope/SingletonWithPrototypeTest1.java
      - `// 4. JSR-330 Provider 적용` 참고
        - `provider.get()`을 통해서 항상 새로운 `프로토타입 빈`이 생성된다.
        - `provider`의 `get()`을 호출하면 내부에서는 스프링 컨테이너를 통해 해당 빈을 찾아서 반환한다. (DL)
        - `자바 표준`이고, 기능이 단순하므로 단위테스트를 만들거나 mock 코드를 만들기는 훨씬 쉬워진다.
        - `Provider`는 지금 딱 필요한 `DL` 정도의 기능만 제공한다.
  - 특징
    - `get()` 메서드 하나로 기능이 매우 단순하다.
    - 별도의 라이브러리가 필요하다.
    - 자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용할 수 있다.

- 정리
  - 그러면 `프로토타입 빈`을 언제 사용할까?
    - 매번 사용할 때 마다 의존관계 주입이 완료된 새로운 객체가 필요하면 사용하면 된다. 
  - 그런데 `실무`에서 `웹 애플리케이션`을 개발해보면, `싱글톤 빈`으로 대부분의 문제를 해결할 수 있기 때문에 `프로토타입 빈`을 직접적으로 사용하는 일은 매우 드물다. ✅
  - `ObjectProvider`, `JSR330 Provider` 등은 `프로토타입` 뿐만 아니라 `DL`이 필요한 경우는 언제든지 사용할 수 있다.

- 참고
  - 스프링이 제공하는 메서드에 `@Lookup` 애노테이션을 사용하는 방법도 있지만, 이전 방법들로 충분하고, 고려해야할 내용도 많아서 생략하겠다.
  - 실무에서 자바 표준인 `JSR-330 Provider`를 사용할 것인지, 아니면 스프링이 제공하는 `ObjectProvider`를 사용할 것인지 고민이 될 것이다. 
    - `ObjectProvider`는 `DL`을 위한 편의 기능을 많이 제공해주고 스프링 외에 별도의 의존관계 추가가 필요 없기 때문에 편리하다. 
    - 만약(정말 그럴일은 거의 없겠지만) 코드를 스프링이 아닌 `다른 컨테이너`에서도 사용할 수 있어야 한다면 `JSR-330 Provider`를 사용해야한다.
  - 스프링을 사용하다 보면 이 기능 뿐만 아니라 다른 기능들도 `자바 표준`과 `스프링`이 제공하는 기능이 겹칠때가 많이 있다. 
    - 대부분 `스프링`이 더 다양하고 편리한 기능을 제공해주기 때문에, 특별히 다른 컨테이너를 사용할 일이 없다면, `스프링`이 제공하는 기능을 사용하면 된다.

### 웹 스코프

- `웹 스코프`의 특징
  - `웹 스코프`는 `웹 환경`에서만 동작한다.
  - `웹 스코프`는 `프로토타입`과 다르게 `스프링`이 해당 스코프의 종료시점까지 관리한다.
    - 따라서 `종료 메서드`가 호출된다.

- `웹 스코프` 종류
  - `request`: `HTTP 요청` 하나가 들어오고 나갈 때 까지 유지되는 스코프. 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고, 관리된다.
  - `session`: `HTTP Session`과 동일한 생명주기를 가지는 스코프
  - `application`: `서블릿 컨텍스트(ServletContext)`와 동일한 생명주기를 가지는 스코프
  - `websocket`: `웹 소켓`과 동일한 생명주기를 가지는 스코프

- 여기서는 `request` 스코프를 예제로 설명한다. 나머지도 범위만 다르지 동작 방식은 비슷하다.

- HTTP request 요청 당 각각 할당되는 `request 스코프`

    ![request 스코프](https://github.com/user-attachments/assets/5bdfd502-b9ca-483a-87ac-18f5729051f8)

### `request 스코프` 예제 만들기

- `웹 환경` 추가
  - `웹 스코프`는 `웹 환경`에서만 동작하므로 `web 환경`이 동작하도록 `라이브러리`를 추가하자.
  - `build.gradle`에 추가
    - 소스 코드 (비공개 레포지토리): `build.gradle`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/build.gradle
        - `implementation 'org.springframework.boot:spring-boot-starter-web'`
  - `hello.core.CoreApplication`의 `main 메서드`를 실행하면 `웹 애플리케이션`이 실행된다.
    - 소스 코드 (비공개 레포지토리): `CoreApplication`
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/CoreApplication.java
    - 실행결과 (콘솔)
      - `Tomcat started on port(s): 8080 (http) with context path ''`
    - 참고
      - `spring-boot-starter-web` 라이브러리를 추가하면, `스프링 부트`는 `내장 톰켓 서버`를 활용해서 `웹 서버`와 `스프링`을 함께 실행시킨다.
      - `스프링 부트`는 `웹 라이브러리`가 없으면, 지금까지 학습한 `AnnotationConfigApplicationContext`을 기반으로 애플리케이션을 구동한다. 
      - `웹 라이브러리`가 추가되면, 웹과 관련된 추가 설정과 환경들이 필요하므로 `AnnotationConfigServletWebServerApplicationContext`를 기반으로 애플리케이션을 구동한다.
      - 만약 기본 포트인 8080 포트를 다른곳에서 사용중이어서 오류가 발생하면 포트를 변경해야 한다. 
        - 9090 포트로 변경하려면 다음 설정을 추가하자.
          - `main/resources/application.properties`
            - `server.port=9090`
        - 나는 그냥 사용중인 8080을 닫고 다시 실행하였다.

- `request 스코프` 예제 개발

  - 동시에 여러 `HTTP 요청`이 오면 정확히 어떤 요청이 남긴 로그인지 구분하기 어렵다. 
    - 이럴때 사용하기 딱 좋은것이 바로 `request 스코프`이다.

  - `MyLogger`
    - 소스 코드 (비공개 레포지토리): 
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/common/MyLogger.java
        - 로그를 출력하기 위한 `MyLogger` 클래스이다.
        - `@Scope(value = "request")`를 사용해서 `request 스코프`로 지정했다.
        - 이제 이 빈은 `HTTP 요청` 당 하나씩 생성되고, `HTTP 요청`이 끝나는 시점에 소멸된다.
        - 이 빈이 생성되는 시점에 자동으로 `@PostConstruct` 초기화 메서드를 사용해서 `uuid`를 생성해서 저장해둔다.
        - 이 빈은 `HTTP 요청` 당 하나씩 생성되므로, `uuid`를 저장해두면 다른 `HTTP 요청`과 구분할 수 있다.
        - 이 빈이 소멸되는 시점에 `@PreDestroy`를 사용해서 종료 메시지를 남긴다.
        - `requestURL`은 이 빈이 생성되는 시점에는 알 수 없으므로, 외부에서 `setter`로 입력 받는다.
  - `LogDemoController`
    - 소스 코드 (비공개 레포지토리): `// 1. 초기 코드 (오류남... provider 적용 전)` 참고
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/web/LogDemoController.java
        - `로거`가 잘 작동하는지 확인하는 테스트용 `컨트롤러`다.
        - 여기서 `HttpServletRequest`를 통해서 요청 URL을 받았다.
          - `requestURL` 값:  `http://localhost:8080/log-demo`
        - 이렇게 받은 `requestURL` 값을 `myLogger`에 저장해둔다.
          - `myLogger`는 `HTTP 요청` 당 각각 구분되므로 다른 `HTTP 요청` 때문에 값이 섞이는 걱정은 하지 않아도 된다.
        - 참고: 
          - `requestURL`을 `MyLogger`에 저장하는 부분은 `컨트롤러` 보다는 공통 처리가 가능한 `스프링 인터셉터`나 `서블릿 필터` 같은 곳을 활용하는 것이 좋다.
          - 지금은 예제를 단순화하게 하기 위해서 `컨트롤러`에서 함.
  - `LogDemoService`
    - 소스 코드 (비공개 레포지토리): `// 1. 초기 코드 (오류남... provider 적용 전)` 참고
      - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/web/LogDemoService.java
- 중요
  - 문제점
    - `request scope`를 사용하지 않고, `파라미터`로 이 모든 정보를 `서비스 계층`에 넘긴다면, `파라미터`가 많아서 지저분해진다.
    - 더 문제는 `requestURL` 같은 웹과 관련된 정보가 웹과 관련없는 `서비스 계층`까지 넘어가게 된다.
      - 웹과 관련된 부분은 `컨트롤러`까지만 사용해야 한다. 
      - `서비스 계층`은 웹 기술에 종속되지 않고, 가급적 순수하게 유지하는 것이 유지보수 관점에서 좋다.
  - 문제점 해결
    - `request scope`의 `MyLogger` 덕분에 이런 부분을 `파라미터`로 넘기지 않고, `MyLogger`의 `멤버변수`에 저장해서 코드와 계층을 깔끔하게 유지할 수 있다.

- 실행
  - 에러가 난다...
    - `Error creating bean with name 'myLogger': Scope 'request' is not active for the current thread; consider defining a scoped proxy for this bean if you intend to refer to it from a singleton;`
  - 왜?
    - `스프링 애플리케이션`을 실행하는 시점에 `싱글톤 빈`은 생성해서 주입이 가능하지만, `request 스코프 빈`은 아직 생성되지 않는다.
    - `request 스코프 빈`은 실제 고객의 요청이 와야 생성할 수 있다!

### 스코프와 Provider

- 첫번째 해결방안은 앞서 배운 `Provider`를 사용하는 것이다.
  - 간단히 `ObjectProvider`를 사용해보자.

- 소스 코드 (비공개 레포지토리):  `LogDemoController`, `LogDemoService` - `// 2. ObjectProvider 적용` 참고
  - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/web

- 실행
  - `main() 메서드`로 스프링을 실행하고, 웹 브라우저에 `http://localhost:8080/log-demo` 를 입력하자.

- 실행결과
  - 웹 화면
  
    ![web화면](https://github.com/user-attachments/assets/4a3eb051-a96f-4057-9c5a-0eb9fffbaa31)

  - 콘솔
    - 새로고침 천천히 순차적으로 할 때:
      - 같은 요청끼리 순차적으로 출력된다. 

        ![순차실행](https://github.com/user-attachments/assets/88a0b4fd-521d-4c7c-972e-33cd90613f07)

    - 새로고침 빠르게 여러번 할 때: 
      - 여러 요청이 섞여서 출력된다. (`uuid`를 통해서 구분 할 수 있다.)
      
      ![연속실행](https://github.com/user-attachments/assets/b9f0f9fa-d59d-40c0-9738-dd5ff17925b3)

- 설명
  - `ObjectProvider` 덕분에 `ObjectProvider.getObject()`를 호출하는 시점까지 `request scope 빈`의 생성을 지연할 수 있다.
  - `ObjectProvider.getObject()`를 호출하시는 시점에는 `HTTP 요청`이 진행중이므로 `request scope 빈`의 생성이 정상 처리된다.
  - `ObjectProvider.getObject()`를 `LogDemoController`, `LogDemoService` 에서 각각 한번씩 따로 호출해도 같은 `HTTP 요청`이면 같은 `스프링 빈`이 반환된다!

- 이 정도에서 끝내도 될 것 같지만… 
  - 개발자들의 코드 몇자를 더 줄이려는 욕심은 끝이 없다.

### 스코프와 프록시

- 이번에는 `프록시` 방식을 사용해보자.
  - 소스 코드 (비공개 레포지토리): `MyLogger` - `// 3. 프록시 사용` 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/blob/master/src/main/java/hello/core/common/MyLogger.java
      - `@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)`
        - `proxyMode = ScopedProxyMode.TARGET_CLASS`을 추가했다.
          - `ScopedProxyMode`
            - 적용 대상이 `클래스`면 `TARGET_CLASS`를 선택
            - 적용 대상이 `인터페이스`면 `INTERFACES`를 선택
  - 이렇게 하면 `MyLogger`의 `가짜 프록시 클래스`를 만들어두고, `HTTP request`와 상관 없이 `가짜 프록시 클래스`를 다른 빈에 미리 주입해 둘 수 있다.

- 이제 나머지 코드를 `Provider`사용 이전으로 돌려두자.
  - 소스 코드 (비공개 레포지토리): `LogDemoController`, `LogDemoService` - `// 3. 프록시 사용` 참고
    - https://github.com/JohnKim0911/kyh_spring_basic/tree/master/src/main/java/hello/core/web

- `웹 스코프`와 `프록시` 동작 원리
  - `LogDemoController`에서 `myLogger.getClass()`를 출력해본 결과:
    - `class hello.core.common.MyLogger$$SpringCGLIB$$0`
      - 순수한 `MyLogger`가 아니라, `MyLogger$$SpringCGLIB$$0`를 사용하고 있다.
  - `CGLIB`라는 `라이브러리`로 내 클래스를 상속 받은 `가짜 프록시 객체`를 만들어서 주입한다.
    - `MyLogger`에서 `@Scope`의 `proxyMode = ScopedProxyMode.TARGET_CLASS`를 설정하면, `스프링 컨테이너`는 `CGLIB`라는 바이트코드를 조작하는 `라이브러리`를 사용해서, `MyLogger`를 상속받은 `가짜 프록시 객체`를 생성한다.
    - 의존관계 주입도 이 `가짜 프록시 객체`가 주입된다.
  
  ![가짜 프록시](https://github.com/user-attachments/assets/a0f29088-48c4-43c8-86ab-93cf45fe3c45)

  - `가짜 프록시 객체`는 요청이 오면 그때 내부에서 `진짜 빈`에게 요청한다.
    - `가짜 프록시 객체`는 내부에 `진짜 myLogger`를 찾는 방법을 알고 있다.
    - `클라이언트`가 `myLogger.log()`을 호출하면 사실은 `가짜 프록시 객체`의 메서드를 호출한 것이다.
    - `가짜 프록시 객체`는 `request 스코프`의 `진짜 myLogger.log()`를 호출한다.
    - `가짜 프록시 객체`는 원본 클래스를 상속 받아서 만들어졌기 때문에, 이 객체를 사용하는 `클라이언트` 입장에서는 사실 원본인지 아닌지도 모르게, 동일하게 사용할 수 있다 (`다형성`)
  - `가짜 프록시 객체`는 실제 `request scope`와는 관계가 없다. 
    - 그냥 가짜이고, 내부에 단순한 위임 로직만 있고, `싱글톤` 처럼 동작한다.
  - 특징 정리
    - `프록시 객체` 덕분에 `클라이언트`는 마치 `싱글톤 빈`을 사용하듯이 편리하게 `request scope`를 사용할 수 있다.
    - 사실 `Provider`를 사용하든, `프록시`를 사용하든, `핵심` 아이디어는 진짜 객체 조회를 꼭 필요한 시점까지 `지연처리` 한다는 점이다.
    - 단지 애노테이션 설정 변경만으로 원본 객체를 `프록시 객체`로 대체할 수 있다. 
      - 이것이 바로 `다형성`과 `DI 컨테이너`가 가진 큰 강점이다.
    - 꼭 `웹 스코프`가 아니어도 `프록시`는 사용할 수 있다.
  - 주의점
    - 마치 `싱글톤`을 사용하는 것 같지만, 다르게 동작하기 때문에 결국 `주의`해서 사용해야 한다.
    - 이런 `특별한 scope`는 꼭 필요한 곳에만 `최소화`해서 사용하자.
      - 무분별하게 사용하면 유지보수하기 어려워진다.

## 11. 다음으로