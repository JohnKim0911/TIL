# (복습) 스프링 핵심 원리 - 기본편

- 김영한의 스프링 완전 정복 로드맵
    - 2편) 스프링 핵심 원리 - 기본편

|    | 제목                                                            | 강의 분량     | 교재 분량 (페이지) | 복습일        |
|----|---------------------------------------------------------------|-----------|-------------|------------|
| 1  | [강의 소개](#1-강의-소개)                                             | 4분        | 3           | 2024.12.16 |
| 2  | [객체 지향 설계와 스프링](#2-객체-지향-설계와-스프링)                             | 1시간 16분   | 65          | 2024.12.17 |
| 3  | [스프링 핵심 원리 이해1 - 예제 만들기](#3-스프링-핵심-원리-이해1---예제-만들기)           | 1시간 1분    | 20          | 2024.12.17 |
| 4  | [스프링 핵심 원리 이해2 - 객체 지향 원리 적용](#4-스프링-핵심-원리-이해2---객체-지향-원리-적용) | 1시간 38분   | 30          | 2024.12.17 |
| 5  | [스프링 컨테이너와 스프링 빈](#5-스프링-컨테이너와-스프링-빈)                         | 1시간 19분   |             |            |
| 6  | [싱글톤 컨테이너](#6-싱글톤-컨테이너)                                       | 1시간 15분   |             |            |
| 7  | [컴포넌트 스캔](#7-컴포넌트-스캔)                                         | 51분       |             |            |
| 8  | [의존관계 자동 주입](#8-의존관계-자동-주입)                                   | 1시간 53분   |             |            |
| 9  | [빈 생명주기 콜백](#9-빈-생명주기-콜백)                                     | 35분       |             |            |
| 10 | [빈 스코프](#10-빈-스코프)                                            | 1시간 44분   |             |            |
| 11 | [다음으로](#11-다음으로)                                              | 25분       |             |            |
|    |                                                               | 총 12시간 5분 |             |            |

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

## 6. 싱글톤 컨테이너

## 7. 컴포넌트 스캔

## 8. 의존관계 자동 주입

## 9. 빈 생명주기 콜백

## 10. 빈 스코프

## 11. 다음으로