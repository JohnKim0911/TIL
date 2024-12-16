# (복습) 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

- 김영한의 스프링 완전 정복 로드맵
  - 1편) 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

|   | 제목                                            | 강의 분량     | 교재 분량 (쪽) | 복습일        |
|---|-----------------------------------------------|-----------|-----------|------------|
| 1 | [강의 소개](#1-강의-소개)                             | 5분        | 3         | 2024.12.13 |
| 2 | [프로젝트 환경설정](#2-프로젝트-환경설정)                     | 47분       | 10        | 2024.12.13 |
| 3 | [스프링 웹 개발 기초](#3-스프링-웹-개발-기초)                 | 33분       | 5         | 2024.12.14 |
| 4 | [회원 관리 예제 - 백엔드 개발](#4-회원-관리-예제---백엔드-개발)     | 55분       | 9         | 2024.12.15 |
| 5 | [스프링 빈과 의존관계](#5-스프링-빈과-의존관계)                 | 27분       | 5         | 2024.12.15 |
| 6 | [회원 관리 예제 - 웹 MVC 개발](#6-회원-관리-예제---웹-mvc-개발) | 17분       | 5         | 2024.12.15 |
| 7 | [스프링 DB 접근 기술](#7-스프링-db-접근-기술)               | 1시간 33분   | 21        | 2024.12.16 |
| 8 | [AOP](#8-aop)                                 | 22분       |           |            |
| 9 | [다음으로](#9-다음으로)                               | 18분       |           |            |
|   |                                               | 총 5시간 21분 |           |            |

## 1. 강의 소개

- 강의 소개 페이지: https://inf.run/hivx6

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
        - 제 기억을 살리기 위한 용도이다보니, 아래 글만으로는 이해가 어려울 수 있습니다.
            - 필요하시다면, 위 강의를 직접 수강하시는 것을 추천드립니다. (무료)
        - 방식:
            - 강의를 들으면서 코드를 직접 치고,
            - 강의가 끝나면 다시 교재를 보면서 중요 내용 위주로 정리하였습니다.
    - 무료 강의이긴 하지만, 실제 작성한 전체 코드는 비공개 합니다. (저작권...)
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_hello-spring
            - 링크가 있긴하지만, 저만 볼 수 있습니다. (404 error 뜨는게 정상)

## 2. 프로젝트 환경설정

### 프로젝트 생성

- 사전 준비물
  - `Java 17` 이상 설치
    - 나는 `Java 23` 사용.
    - (인텔리제이를 사용하므로 자바를 별도로 설치하지 않아도 문제가 없었으나, 강의 마지막에 터미널로 빌드하고 `jar`파일 실행 할 때는 필요했다.)
  - IDE: `IntelliJ`

- 스프링 프로젝트 생성
  - 스프링 부트 스타터 사이트에서 생성: https://start.spring.io/
  - 프로젝트 설정
  
    ![spring boot](https://github.com/user-attachments/assets/bfce0f14-1830-4824-ae27-7ff91d61e0b5)

    - Project
      - `Gradle` : 버전 설정하고 라이브러리 땡겨옴.
        - 요즘은 `maven`은 잘 안쓴다.
    - Spring Boot
      - 나는 최신버전인 `3.4.0` 선택함.
      - `SNAPSHOT`은 아직 안정화 되지 않은 버전임.
    - Project Metadata
      - `Group`: 보통 기업 도메인명 입력
      - `Artifact`: 빌드되어 나온 결과물? 프로젝트명 같은 것.
    - Dependencies
      - `Spring Web`
      - `Thymeleaf` : 템플릿 엔진. 정적인 html을 자바 코드를 넣어 동적으로 만들어준다.
  
  - 설정 마치면 `GENERATE` 버튼을 누른다.
    - 압축파일이 다운로드 된다.
    - 압축을 풀고 해당 프로젝트 폴더를 원하는 위치에 놓는다.

- 프로젝트 열기
  - IntelliJ 실행.
  - 프로젝트 폴더내에 `build.gradle`를 선택하여 프로젝트를 연다.
    
    ![open project](https://github.com/user-attachments/assets/3a2e70a6-464b-4b77-9789-e82ac5418980)

  - 메인 메서드 실행하면 에러가 난다. 아래 Gradle 설정을 해줘야 한다.

- Gradle 설정

    ![gradle setting](https://github.com/user-attachments/assets/bad1bfa5-be16-49af-8341-e33d3b2b8423)

- 프로젝트 JDK 설정
  - 혹시 모르니 확인해보자.

  ![project structure](https://github.com/user-attachments/assets/01f48447-085c-4577-afad-76b41d37d932)

- 프로젝트 실행
  - `main` 메서드를 실행한다. (프로젝트 생성시 샘플로 생성된 코드)
    - 소스코드 (비공개 레포지토리) `HelloSpringApplication`:
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/HelloSpringApplication.java
  - 이미 해당 포트 번호가 사용 중 인 경우, 해당 작업 끝내기 (강의에 없는 내용)
    - 나의 경우, 8080 포트가 이미 사용중이라 에러가 떴었다. 이런 경우, 사용하고 있는 8080을 닫아줘야한다.
    - 방법
      - 관리자 권한으로 명령 프롬프트를 연다. (`ctrl` + `r` --> `cmd`)
      - `netstat-ano`을 입력하여, 해당 주소 8080을 사용하고 있는 `PID`를 확인한다.
      
        ![find pid](https://github.com/user-attachments/assets/4bb75c2a-4109-486f-a033-81e7393168c9)

      - `taskkill /pid 5988 /f`를 입력한다. (5988 대신 해당 `PID`를 입력)
 
        ![taskkill](https://github.com/user-attachments/assets/c2f6a121-a59b-454d-881f-7aaa2a2c7498)
      
      - 위와 같이 성공적으로 종료되었다.
  - 아래와 같이 정상 실행되면, 인터넷 브라우저에서 `localhost:8080`을 입력한다.
    ![console](https://github.com/user-attachments/assets/70775837-6ca4-4209-9f01-c53db6f76818)
  - 아래와 같이 에러 페이지가 뜨면 정상!

  ![localhost](https://github.com/user-attachments/assets/9ae86637-1b31-4e42-8c42-ff1b5dd50b9b)

### 라이브러리 살펴보기

- `Gradle`은 의존관계가 있는 라이브러리를 함께 다운로드 한다.
- `Gradle`을 다음과 같이 둘러 보았다.
  - 직접 써봐야 뭔지 이해할 수 있다. 지금은 이런게 있다 정도만 참고하자.

  ![gradle](https://github.com/user-attachments/assets/5d58dbd8-6768-44b2-b875-82da4d21bce2)

- 스프링 부트 라이브러리
  - `spring-boot-starter-web`
    - `spring-boot-starter-tomcat`: 톰캣 (웹서버)
    - `spring-webmvc`: 스프링 웹 MVC
  - `spring-boot-starter-thymeleaf`: 타임리프 템플릿 엔진(View)
  - `spring-boot-starter`(공통): 스프링 부트 + 스프링 코어 + 로깅
    - `spring-boot`
      - `spring-core`
  - `spring-boot-starter-logging`
    - `logback`, `slf4j`
    
- 테스트 라이브러리
  - `spring-boot-starter-test`
    - `junit`: 테스트 프레임워크
    - `mockito`: 목 라이브러리
    - `assertj`: 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    - `spring-test`: 스프링 통합 테스트 지원

### View 환경설정

- Welcome Page 만들기
  - 정적 페이지 만들기
    - `resources/static`에 `index.html`을 만든다.
      - 소스코드 (비공개 레포지토리):
        - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/static/index.html
    - 다시 서버를 돌려서 에러 페이지 대신 해당 `index.html`이 뜨는지 확인한다. (`localhost:8080`)

      ![8080](https://github.com/user-attachments/assets/b3f2b7e2-020a-4a52-9c81-432a66e4e905)    

  - 데이터 넘겨주기
    - `Controller` 작성
      - 소스코드 (비공개 레포지토리):
        - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/HelloController.java
       - `model.addAttribute("data", "hello!!");`로 `hello!!`를 넘긴다.
    - `resources/templates/hello.html` 작성
      - 소스코드 (비공개 레포지토리):
        - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/templates/hello.html
      - `thymeleaf` 템플릿 엔진을 사용한다.
        - `<html xmlns:th="http://www.thymeleaf.org">`
        - `<p th:text="'안녕하세요. ' + ${data}" >안녕하세요. 손님</p>` // th는 thymeleaf를 뜻한다.
    - `Controller`에서 `hello.html` 넘긴 `"hello!!"`가 `${data}` 자리에 제대로 전달되는지 확인한다. (`localhost:8080/hello`)
    
      ![8080 hello](https://github.com/user-attachments/assets/515b9853-9618-4392-970c-6771f51ebab0)

- thymeleaf 템플릿엔진 동작 확인

  ![동작 환경 그림](https://github.com/user-attachments/assets/5ad3ff7b-d263-44bf-966e-1bbed5e1c790)

  - `컨트롤러`에서 리턴 값으로 문자를 반환하면, `뷰 리졸버(viewResolver)`가 화면을 찾아서 처리한다.
    - `resources:templates/` + `{ViewName}` + `.html`

- 참고:
  - `spring-boot-devtools` 라이브러리를 추가하면, `html` 파일을 컴파일만 해주면 서버 재시작 없이 `View` 파일 변경이 가능하다.
    - 인텔리J 컴파일 방법: 메뉴 build ->  Recompile

### 빌드하고 실행하기

- 강사님은 `mac OS`에서 진행했지만, 나는 `Windows OS`에서 했다.

- `Window OS`에서 진행
  - `ctrl + r` -> `cmd`로 터미널을 연다.
  - 해당 프로젝트가 있는 폴더로 이동한다. (명령어 `cd`)
    - 나는 윈도우 폴더로 해당 프로젝트로 이동한 후, 해당 폴더의 경로를 복사해서 붙여넣었다.
    - 예시) `cd C:\Users\John\Desktop\study\hello-spring` // hello-spring 이 프로젝트 root 폴더
  - `gradlew build` 명령어를 입력하여 build 한다.
    - 참고)
      - 나는 처음에 인텔리제이 외에 java를 별도로 설치하지 않았어서 오류가 났었다.
      - java 23 설치
        - https://www.oracle.com/kr/java/technologies/downloads/#jdk23-windows

        ![java 설치](https://github.com/user-attachments/assets/b0c13331-616b-41ca-927e-aef0bc31af45)
      - 자바 설치 후, 다시 시도하면 잘 된다.
    - build 폴더에 파일들이 생성된다.
    - 참고로, 해당 현재 폴더의 파일들을 확인하고 싶으면 `dir` 명령어를 사용한다.
    
    ![gradlew build](https://github.com/user-attachments/assets/9dfa4802-86d9-42a6-be08-1edfba73cb9b)

  - `build\lib` 폴더로 이동한다.
  - `dir` 명령어로 파일 목록을 확인하면, `.jar` 파일이 생성된 것을 확인 할 수 있다. 해당 파일명을 복사한다.
  - 서버 실행
    - `java -jar` 명령어로 `.jar` 파일을 실행한다.

    ![java jar](https://github.com/user-attachments/assets/58276994-e0e8-4149-ad9c-7cfb494cb5bf)

  - 서버 종료
    - `ctrl + c`로 종료 할 수 있다.
    - 종료되면, `Graceful shutdown complete`이라는 메시지가 뜬다.

    ![ctrl c](https://github.com/user-attachments/assets/8db726cd-e7e7-4a3e-9708-69fd532f666d)

## 3. 스프링 웹 개발 기초

- 웹 개발 3가지 방법
  - 정적 컨텐츠
  - MVC와 템플릿 엔진
  - API

### 정적 컨텐츠

- 소스코드 (비공개 레포지토리): 
  - `resources/static/hello-static.html`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/static/hello-static.html
  - 컨트롤러 필요없음. `html` 파일만 생성

- 실행
  - `localhost` + `해당 파일명`으로 접근.
  - `http://localhost:8080/hello-static.html`
 
    ![static](https://github.com/user-attachments/assets/8dbadce8-182d-4a03-a7c4-4993e7ecc9b1)

- 정적 컨텐츠 이미지

  ![정적 컨텐츠 이미지](https://github.com/user-attachments/assets/0306ff43-f484-48c3-8055-3b7f5b423d66)

### MVC와 템플릿 엔진

- MVC: `Model`, `View`, `Controller`

- 소스코드 (비공개 레포지토리):
  - `HelloController`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/HelloController.java
      - `@GetMapping("hello-mvc")` 부분
  - `resources/templates/hello-template.html`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/templates/hello-template.html

- 실행
  - `localhost` + `url mapping` + `?key=value`
  - `http://localhost:8080/hello-mvc?name=spring`
    - `hello-mvc`라고 맵핑된 `Controller`가 실행되고,
    - `url`로 부터 `@RequestParam("name")`으로 `name`을 받고, `hello-template.html`에 넘겨준다.
    - Thymeleaf 템플릿을 통해 `html`을 변환하여 내려준다. (받은 `name`값을 `html`에 넣음)

- 결과

  ![hello-mvc](https://github.com/user-attachments/assets/421cf137-8ff5-4f0f-80a9-18228f9e4eb8)

  - 우클릭, 페이지 소스 보기:
    - html 태그들이 포함되어있다.
  
    ![hello-mvc_src](https://github.com/user-attachments/assets/68e2c6d3-5507-422a-9a66-f6b4cecddc90)

- MVC, 템플릿 엔진 이미지

  ![mvc 템플릿 엔진](https://github.com/user-attachments/assets/98aad78b-dc1b-49fc-82f3-7df7572ac64a)

### API

- 2가지로 나눠서 보았다.
  - `@ResponseBody` 문자 반환
  - `@ResponseBody` 객체 반환

- `@ResponseBody` 문자 반환
  - `@ResponseBody`를 사용하면 `뷰 리졸버(viewResolver)`를 사용하지 않음.
  - 대신에 HTTP의 BODY에 문자 내용을 직접 반환
    - (HTML BODY TAG를 말하는 것이 아님)

  - 소스코드 (비공개 레포지토리):
    - `HelloController`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/HelloController.java
        - `@GetMapping("hello-string")` 부분
        - `@ResponseBody`을 붙였다.
        - 컨트롤러의 `return`값에 문자열을 그대로 반환한다. (html 파일명이 아님)

  - 실행
    - `http://localhost:8080/hello-string?name=spring`

  - 결과
    - 화면에 보이는 것은 mvc와 동일하나, 페이지 소스를 보면 다르다.
  
    ![hello-string](https://github.com/user-attachments/assets/bd89d9ef-57f7-4f3d-8b9e-f62fa3d50106)

    - 우클릭, 페이지 소스 보기:
      - html 태그 없이 문자열만 있다.
      
      ![hello-string_src](https://github.com/user-attachments/assets/172ab67a-6e2f-4e4e-9e4f-95774ddb8f27)

- `@ResponseBody` 객체 반환

  - 소스코드 (비공개 레포지토리):
    - `HelloController`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/HelloController.java
        - `@GetMapping("hello-api")` 부분
        - 내부 클래스를 만들고 객체를 생성하였다. 생성한 객체를 `return` 한다.
  
  - 실행
    - `http://localhost:8080/hello-api?name=spring`
  
  - 결과
    - JSON 형태로 결과를 반환한다.
    
    ![hello-api](https://github.com/user-attachments/assets/6b9e9640-1adc-43d5-8e7a-5874af745d40)

- `@ResponseBody` 사용 원리

  ![ResponseBody 사용 원리](https://github.com/user-attachments/assets/db4e37dc-b388-4ec7-be4e-c5c34fc609f6)

  - HTTP의 BODY에 문자 내용을 직접 반환
  - `viewResolver` 대신에 `HttpMessageConverter`가 동작
    - 기본 문자처리: `StringHttpMessageConverter`
    - 기본 객체처리: `MappingJackson2HttpMessageConverter`
      - 객체를 `JSON`으로 바꿔주는 라이브러리에 `Jackson`과 `GSON` 등이 있다.
        - `GSON`은 `Google`에서 만든 라이브러리.
        - `Jackson`은 스프링이 기본으로 탑재하고 있는 라이브러리이다.
          - `Jackson` 뒤에 붙은 `2`는 버전을 나타냄.
    - 참고:
      - byte 처리 등등 기타 여러 `HttpMessageConverter`가 기본으로 등록되어 있음
      - 클라이언트의 `HTTP Accept 해더`와 서버의 `컨트롤러 반환 타입 정보` 둘을 조합해서 `HttpMessageConverter`가 선택된다.

## 4. 회원 관리 예제 - 백엔드 개발

### 비즈니스 요구사항 정리

- 요구사항
  - 데이터: 회원ID, 이름
  - 기능: 회원 등록, 조회

- 일반적인 웹 애플리케이션 계층 구조

  ![웹 앱 구조](https://github.com/user-attachments/assets/9f3efd26-4846-4a56-8234-9a16159e68cb)

  - `컨트롤러`: 웹 MVC의 컨트롤러 역할
  - `서비스`: 핵심 비즈니스 로직 구현
  - `리포지토리`: 데이터베이스에 접근
    - 도메인 객체를 DB에 저장하고 관리
  - `도메인`: 비즈니스 도메인 객체
    - 예) 회원, 주문, 쿠폰 등등 주로 데이터베이스에 저장하고 관리됨

- 클래스 의존관계

  ![클래스 의존관계](https://github.com/user-attachments/assets/fd598cb3-edba-4d94-8995-e690093d9061)

  - 아직 데이터 저장소가 선정되지 않아서, 우선 인터페이스로 구현 클래스를 변경할 수 있도록 설계

### 회원 도메인과 리포지토리 만들기

- 회원 객체 `Member`
  - 소스코드 (비공개 레포지토리):
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/domain/Member.java

- 회원 리포지토리
  - 소스코드 (비공개 레포지토리):
    - https://github.com/JohnKim0911/kyh_hello-spring/tree/master/src/main/java/hello/hello_spring/repository
      - 인터페이스: `MemberRepository`
      - 메모리 구현체: `MemoryMemberRepository`
        - (동시성 문제가 고려되어 있지 않음, 실무에서는 `ConcurrentHashMap`, `AtomicLong` 사용 고려)
      - 특이사항
        - `Optional` 처음 사용해봄.
          - `Optional`로 감싸면, 값이 `null` 일 경우 `optional`을 반환하게됨.
        - 람다 처음 사용해봄.

### 회원 리포지토리 테스트 케이스 작성

- 기존 테스트 방법의 단점
  - 기존 방법:
    - 자바의 `main` 메서드를 통해서 실행하거나,
    - 웹 애플리케이션의 `컨트롤러`를 통해서 해당 기능을 실행한다.
  - 단점
    - 이러한 방법은 준비하고 실행하는데 오래 걸리고,
    - 반복 실행하기 어렵고,
    - 여러 테스트를 한번에 실행하기 어렵다.
  - 해결방법:
    - 자바는 `JUnit`이라는 프레임워크로 테스트를 실행해서 이러한 문제를 해결한다.

- 회원 리포지토리 메모리 구현체 테스트
  - `src/test/java` 하위 폴더에 생성한다.
  - 소스 코드 (비공개 레포지토리): `MemoryMemberRepositoryTest`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/test/java/hello/hello_spring/repository/MemoryMemberRepositoryTest.java
      - 특이사항 
        - 테스트는 순서와 관계없이, 서로 의존관계 없이 설계가 되어야 한다.
          - 한번에 여러 테스트를 실행하면 각 테스트의 실행 순서가 랜덤이다.
        - `@AfterEach`
          - 각 테스트가 종료 될 때 마다 이 기능을 실행한다.
          - 한번에 여러 테스트를 실행하면 메모리 DB에 직전 테스트의 결과가 남을 수 있는데, 이전 데이터를 삭제 할 때 사용한다.
        - `get()`으로 `Optional`에서 값을 꺼낼 수 있다. (권장하는 방법은 아니다.)
        - `assertThat(member).isEqualTo(result);`
          - `import static org.assertj.core.api.Assertions.*;`
            - `assertj`를 사용한다.
            - `static import` 하면 편하게 사용 가능하다.
        - `TDD (Test-driven development, 테스트 주도 개발)`
          - 테스트를 먼저 짜고, 나중에 코드를 짜서 미리 작성한 테스트 코드로 제대로 작동하는지 확인하는 방식.
          - 여러명이 협업하거나, 코드가 많아지면, 테스트 코드 없이 개발하기 어렵다. 기회가 되면 제대로 공부해보자.

### 회원 서비스 개발

- 소스 코드 (비공개 레포지토리): `MemberService`
  - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/service/MemberService.java
    - `회원가입`, `전체 회원 조회`, `회원 아이디로 조회` 구현

### 회원 서비스 테스트

- `MemberService`의 `memberRepository`를 직접 생성해서 보관하지 않고, 외부에서 넣어주도록 수정함.
  - `DI` (`Dependency Injection`), `의존성 주입`이라 함.
  - 위 `MemberService` 참고.
  - 자세한 설명은 `MemberServiceTest`내 주석 참고.

- 회원 서비스 테스트
  - 소스 코드 (비공개 레포지토리): `MemberServiceTest`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/test/java/hello/hello_spring/service/MemberServiceTest.java
      - 특이사항
        - 테스트 파일 단축키로 생성
          - 해당 클래스에서 `ctrl` + `shift` + `t` 누르면 테스트 파일 자동 생성
          
            ![test 자동생성](https://github.com/user-attachments/assets/b1b95fbc-e553-4e69-9497-39f44b15671e)
            
            - 생성된 테스트 파일

              ![test 자동생성 결과](https://github.com/user-attachments/assets/15ff75fb-6d98-49f3-9244-b27e9c3b2435)
        
        - `@BeforeEach` 사용
          - 각 테스트 실행 전에 호출된다.
          - 테스트가 서로 영향이 없도록 항상 새로운 객체를 생성하고, 의존관계도 새로 맺어준다.
        - 테스트 메서드명은 `한글`로 작성해도 된다.
        - `given` - `when` - `then` 문법 사용하면 테스트 코드 작성이 명확해진다.
        - 테스트는 잘되는 것 뿐만 아니라, 잘 안되는 상황도 확인 해봐야함. (예상한 에러가 잘 뜨는지...)

## 5. 스프링 빈과 의존관계

### 컴포넌트 스캔과 자동 의존관계 설정

- `회원 컨트롤러`가 `회원서비스`와 `회원 리포지토리`를 사용할 수 있게 의존관계를 준비하자.

- `회원 컨트롤러`에 의존관계 추가
  - `MemberController`를 새로 작성함.
    - 클래스에 `@Controller`를 붙이고, 생성자에 `@Autowired`를 추가했다.
      - `@Controller`을 붙이면...
        - 스프링이 처음에 뜰 때, 스프링 컨테이너라는 스프링 통에,
        - `@Controller`이 붙은 `MemberController` 객체를 생성해서 스프링에 넣어둔다. (스프링 빈 등록)
        - 그리고 스프링이 관리한다.
          - "스프링 컨테이너에서 스프링 빈이 관리된다"고 표현한다.
      - 생성자에 `@Autowired`가 있으면, 스프링이 연관된 객체를 스프링 컨테이너에서 찾아서 넣어준다.
    - 소스 코드 (비공개 레포지토리): `MemberController`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberController.java
    - 실행해보니, 에러가 발생했다.
      - (생성자에 쓰인 `MemberService`가 스프링 빈으로 등록되어 있지 않아서...)

        ![cannot find_service](https://github.com/user-attachments/assets/ed37d5af-8425-4e40-b321-60a239fad42c)

- `회원 서비스` 스프링 빈 등록
  - `MemberService`도 `@Service`를 추가하고, 생성자에 `@Autowired`를 추가했다.
  - `MemberService`는 여러 인스턴스를 생성할 필요가 없다. 하나만 생성해서 공용으로 쓰면 된다.
    - 스프링 컨테이너에 등록하고 쓰면 여러 부가적인 효과를 볼 수 있다.
  - 소스코드 (비공개 레포지토리): `MemberService`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/service/MemberService.java

- `회원 리포지토리` 스프링 빈 등록
  - `MemoryMemberRepository`에도 `@Repository`를 추가했다.
    - 소스코드 (비공개 레포지토리): `MemoryMemberRepository`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/repository/MemoryMemberRepository.java

- 스프링 빈 등록 이미지

  ![spring bean container](https://github.com/user-attachments/assets/c9a75e6f-9079-4594-9326-8314d68b374e)

  - 참고
    - `스프링`은 `스프링 컨테이너`에 `스프링 빈`을 등록할 때, 기본으로 `싱글톤`으로 등록한다 (유일하게 하나만 등록해서 공유한다).
    - 따라서 같은 `스프링 빈`이면 모두 같은 `인스턴스`다.
    - 설정으로 `싱글톤`이 아니게 설정할 수 있지만, 특별한 경우를 제외하면 대부분 `싱글톤`을 사용한다.

- 컴포넌트 스캔 원리
  - `@Component` 애노테이션이 있으면, 스프링 빈으로 자동 등록된다.
  - `@Component`를 포함하는 다음 애노테이션도 스프링 빈으로 자동 등록된다.
    - `@Controller`
    - `@Service`
    - `@Repository`

- `스프링 빈`을 등록하는 2가지 방법
  - `컴포넌트 스캔과 자동 의존관계 설정`
    - 위에서 한 방법임.
      - 컴포넌트 스캔: `@Controller`, `@Service`, `@Repository`
      - 자동 의존관계 설정: `@Autowired`
  - `자바 코드로 직접 스프링 빈 등록하기`
  - 참고
    - 실무에서는 주로 정형화된 `컨트롤러`, `서비스`, `리포지토리` 같은 코드는 `컴포넌트 스캔`을 사용한다.
    - 정형화 되지 않거나, 상황에 따라 구현 클래스를 변경해야 하면 설정을 통해 스프링 빈으로 등록한다. (`직접 스프링 빈 등록`)
    - 2가지 방법 다 알아두어야 한다.

### 자바 코드로 직접 스프링 빈 등록하기

- `회원 서비스`와 `회원 리포지토리`의 `@Service`, `@Repository`, `@Autowired` 애노테이션을 제거하고 진행한다.
  - `회원 컨트롤러`의 `@Controller`, `@Autowired`는 그대로 둔다.

- 소스 코드 (비공개 레포지토리): `SpringConfig`
  - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/SpringConfig.java
    - `application`이 실행되는 `HelloSpringApplication`와 같은 위치에 `SpringConfig`를 새로 작성하였다.
    - `@Configuration`을 클래스에 추가
    - `MemberService`, `MemberRepository`을 `SpringConfig`에서 정의한다. (`@Bean`을 각각에 추가)

- 여기서는 향후 메모리 리포지토리를 다른 리포지토리로 변경할 예정이므로, `컴포넌트 스캔 방식` 대신에 `자바 코드로 스프링 빈을 설정`하였다.

- 참고
  - `XML`로 설정하는 방식도 있지만 최근에는 잘 사용하지 않으므로 생략한다.
  - `DI`에는 `필드 주입`, `setter 주입`, `생성자 주입` 이렇게 3가지 방법이 있다.
    - 의존관계가 실행중에 동적으로 변하는 경우는 거의 없으므로 `생성자 주입`을 권장한다.
    - 코드 비교 (비공개 레포지토리):
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberController.java

- 주의
  - `@Autowired`를 통한 `DI`는 `memberController`, `memberService` 등과 같이 스프링이 관리하는 객체에서만 동작한다.
    - 스프링 빈으로 등록하지 않고 내가 직접 생성한 객체에서는 동작하지 않는다.

## 6. 회원 관리 예제 - 웹 MVC 개발

### 회원 웹 기능 - 홈 화면 추가

- `홈 컨트롤러` 추가
  - 소스 코드 (비공개 레포지토리): `HomeController`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/HomeController.java
      - `@GetMapping("/")`

- 회원 관리용 `홈 HTML`
  - 소스 코드 (비공개 레포지토리): `home.html`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/templates/home.html

- 실행 결과

  ![home](https://github.com/user-attachments/assets/df64e46d-7d99-4283-a9f5-17204b0c04c8)

- 참고
  - `컨트롤러`가 `정적 파일`보다 우선순위가 높다.

### 회원 웹 기능 - 등록

- 회원 등록 폼 개발
  - `회원` 등록 폼 `컨트롤러`
    - 소스 코드 (비공개 레포지토리): `MemberController`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberController.java
        - `@GetMapping("/members/new")` 부분
          - `return "members/createMemberForm";` // 아래 회원 등록 폼 `HTML`을 화면에 띄운다.
  - 회원 등록 폼 `HTML`
    - 소스 코드 (비공개 레포지토리): `resources/templates/members/createMemberForm.html`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/templates/members/createMemberForm.html
        - `<form action="/members/new" method="post">` // post 방식
          - `<input type="text" id="name" name="name" placeholder="이름을 입력하세요">` // input의 name을 name으로 지정
  - 결과
    - 홈에서 회원 가입 클릭
    
      ![home_signup](https://github.com/user-attachments/assets/c115396f-20bd-42fe-8681-379b5609bb91)

    - 회원 가입 폼으로 이동.
    
      ![form](https://github.com/user-attachments/assets/b7bffd75-a7e7-4104-8eed-33be703237e4)

- 회원 등록 컨트롤러
  - 웹 등록 화면에서 데이터를 전달 받을 `폼 객체`
    - 소스 코드 (비공개 레포지토리): `MemberForm`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberForm.java

  - `회원 컨트롤러`에서 회원을 실제 등록하는 기능
    - 소스 코드 (비공개 레포지토리): `MemberController`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberController.java
        - `@PostMapping("/members/new")` 부분
          - 새로운 `member` 인스턴스를 생성하고, 
          - `MemberForm`을 사용하여 `html form`에 입력된 `name`값을 받아와서, 생성된 `member` 인스턴스에 넣어준다.
            - `createMemberForm.html`에 있는 `<input>`의 `name`과 `MemberForm`의 필드명이 매칭이 되고, 데이터가 `MemberForm`에 보관되어 전달된다.
              - 이때, `MemberForm`의 `setName()` 메서드가 사용된다.
          - `memberService.join(member);`을 통해서 회원등록한다.
          - 완료 후, 홈 페이지로 리다이렉트 한다. `return "redirect:/";`
        - 참고
          - `@GetMapping()`: 단순 조회시 (get 방식)
          - `@PostMapping()`: HTML form에 post mothod로 데이터 보낼시 사용 (post 방식)
  - 결과
    - 회원 가입 폼에서 이름에 `spring1`을 입력하고 등록을 누르면, 회원가입이 내부적으로 완료되고, 홈페이지로 리다이렉트 된다.
    - 다시 한번 회원 가입 폼으로 이동해서 `spring2`을 등록한다.

### 회원 웹 기능 - 조회

- `회원 컨트롤러`에서 조회 기능
  - 소스 코드 (비공개 레포지토리): `MemberController`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/controller/MemberController.java
      - `@GetMapping("/members")` 부분
        - `memberService.findMember();`를 통해 `List` 형태로 `members`를 받아온다.
        - `model`을 통해 화면에 값을 전달한다. `return "members/memberList";` // 바로 아래 `HTML`

- 회원 리스트 `HTML`
  - 소스 코드 (비공개 레포지토리): `resources/templates/members/memberList.html`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/templates/members/memberList.html
      - 전달받은 `members` 리스트를 `Thymeleaf` 템플릿 엔진을 통해 반복문을 돌면서 렌더링한다.
        - `<tr th:each="member : ${members}">`
          - `<td th:text="${member.id}"></td>` //Member의 getId()을 사용한다.
          - `<td th:text="${member.name}"></td>` //Member의 getName()을  사용한다.
        - `</tr>`

- 결과
  - 홈에서 회원 목록을 클릭한다.
  
    ![home_list](https://github.com/user-attachments/assets/8b5c52ef-f57b-4bb2-99d0-a64a46115318)

  - 회원 목록 페이지로 이동된다.
    - 위에서 추가했던 `spring1`, `spring2`가 화면에 표시된다.

      ![list](https://github.com/user-attachments/assets/5bdd558e-ff4e-4190-a821-a3aa5201cbd4)

- `DB` 없이 진행한거라 서버를 끄고, 다시 켜면 데이터가 날라간다...
  - 다음 강의서 `DB`에 대해서 다뤄보자.

## 7. 스프링 DB 접근 기술

### H2 데이터베이스 설치

- 개발이나 테스트 용도로 가볍고 편리한 DB, 웹 화면 제공

- 다운로드
  - https://www.h2database.com/ 에서 다운로드
  - 나는 `Windows Installer` 다운로드 함.
    - 일반 윈도우 프로그램 처럼 설치하면된다.
    
- 실행
  - 윈도우 버전은 그냥 아이콘 눌러서 실행하면 된다.
  - 맥처럼 설정하거나 command line으로 접근 할 필요 없다.
  - 실행되면 H2 console 웹 화면이 뜬다.
  
- 데이터베이스 파일 생성 방법
  - 제일 처음 실행시에는,
    - JDBC URL에 `jdbc:h2:~/test`를 입력하고, 실행(`Connect`)한다.
    
      ![최초 한번](https://github.com/user-attachments/assets/451fb034-5a17-477d-a390-b35980a49c52)

  - `/test.mv.db` 파일이 생성된다. (직접 쓸 일은 없고, 생성이 됐는지만 확인하면 된다.)

    ![test mv db](https://github.com/user-attachments/assets/fcebd545-acc3-43be-8dd2-b70bcc9e36f0)
    
  - DB를 끌때는 왼쪽 상단의 아이콘을 이용한다.

    ![quit db](https://github.com/user-attachments/assets/e2ef0f1b-bcac-4cd7-91bf-979da34268c8)

  - 이후부터는 JDBC URL에 `jdbc:h2:tcp://localhost/~/test`을 입력하고 실행한다. (한번만 하면 계속 그대로 남아있다.)

    ![이후부터](https://github.com/user-attachments/assets/00832043-5373-441c-9601-a7dcc9f40b04)

  - 왜 JDBC URL을 바꿨나?
    - 처음엔 한번 세팅 한 것 (파일로 접근하는 방식) : 동시에 `웹 콘솔`이랑 `어플리케이션`에서 동시 접근 안됨. 파일이 충돌남.
    - 두번째 부터는 파일에 직접 접근하는게 아니라, `소켓`을 통해서 접근 할 수 있도록 변경함.

- 테이블 생성하기
  - 프로젝트 루트에 `sql/ddl.sql` 생성
    - 소스코드 (비공개 레포지토리): 
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/sql/ddl.sql
    - `SQL`도 프로젝트에 넣어두면, 버전 관리나 참고할 때 용이하다.
  - `H2 데이터베이스`에 `member` 테이블 생성
    - 위 코드를 복사해서, 웹 `H2 콘솔`에 붙여놓고 실행한다.
  - 결과
    - `Member` 테이블이 생성이 되고, `select` 문을 통해 `table`의 내용을 확인 할 수 있다.
    
      ![create table result](https://github.com/user-attachments/assets/46101500-1efd-4af2-b929-269ef7c30f7c)

      - 지금은 아무것도 넣지 않아서 데이터가 없다.

- `H2 데이터베이스`가 정상 생성되지 않을 때
  - H2 데이터베이스를 종료하고, 다시 시작한다.
  - 웹 브라우저 주소창에 `:8082` 이전의 숫자들을 지우고, `localhost`로 바꾼다.
    - 나머지는 바꾸면 안된다. (특히 뒤에 세션 부분이 변경되면 안된다.)

    ![localhost](https://github.com/user-attachments/assets/1d7c9bb6-e22f-43fc-bca4-870aa19e7a47)

### 순수 Jdbc

- 환경 설정
  - `build.gradle` 파일에 `jdbc`, `h2 데이터베이스` 관련 라이브러리 추가
    - 소스 코드 (비공개 레포지토리): `build.gradle`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/build.gradle
        - `dependencies`에 아래 2줄 추가 
          - `implementation 'org.springframework.boot:spring-boot-starter-jdbc'`
          - `runtimeOnly 'com.h2database:h2'`
    - 라이브러리 추가 후, 코끼리 아이콘(?)을 눌러준다. (`sync gradle changes`)
    
      ![sync gradle changes](https://github.com/user-attachments/assets/12060077-2d88-4e34-b25d-d8db99b9a5f1)
      
  - `스프링 부트` 데이터베이스 연결 설정 추가
    - 소스 코드 (비공개 레포지토리): `resources/application.properties`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/application.properties
        - 아래 3줄 추가
          - `spring.datasource.url=jdbc:h2:tcp://localhost/~/test`
          - `spring.datasource.driver-class-name=org.h2.Driver`
          - `spring.datasource.username=sa` //이거 안넣으면 오류 난다. (`Wrong user name or password`)
            - 공백은 모두 제거해야 한다.

- `Jdbc` 리포지토리 구현
  - 이렇게 `JDBC API`로 직접 코딩하는 것은 20년 전 이야기이다. 
    - 고대 개발자들이 이렇게 고생하고 살았구나 생각하고, 정신건강을 위해 참고만 하고 넘어가자.

  - `Jdbc` 회원 리포지토리
    - 소스 코드 (비공개 레포지토리): `JdbcMemberRepository`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/repository/JdbcMemberRepository.java

  - 스프링 설정 변경
    - 소스 코드 (비공개 레포지토리): `SpringConfig`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/SpringConfig.java
        - `DataSource`는 데이터베이스 커넥션을 획득할 때 사용하는 객체다.
          - `스프링 부트`는 데이터베이스 커넥션 정보를 바탕으로 `DataSource`를 생성하고 `스프링 빈`으로 만들어둔다.
          - 그래서 `DI`를 받을 수 있다.
        - `MemoryMemberRepository`에서 `JdbcMemberRepository`을 사용하도록 변경하였다.
          - 다른곳에 코드 수정없이 `SpringConfig`에서만 수정하면 된다!
            - 스프링의 `DI (Dependencies Injection)`을 사용하면 기존 코드를 전혀 손대지 않고, 설정만으로 구현 클래스를 변경할 수 있다.

- 구현 클래스 추가 이미지

  ![구현 클래스 추가 이미지](https://github.com/user-attachments/assets/3ffce39a-9b5e-4e00-8bff-bfbbebfc2810)

- 스프링 설정 이미지

  ![스프링 설정 이미지](https://github.com/user-attachments/assets/6bd2d9a3-5fe8-4241-a568-cce95a2b060d)

- 실행
  - 웹 애플리케이션을 실행해서 데이터를 추가하고, 목록을 확인해본다.
  
    ![web result](https://github.com/user-attachments/assets/c8b5d65b-d905-4ff7-b74c-c7f0f3140b8c)

  - H2 콘솔에서도 확인해본다.
  
    ![H2 result](https://github.com/user-attachments/assets/f9faba70-09be-4bec-bb2c-0d2d169258fd)

- 데이터를 DB에 저장하므로, 스프링 서버를 다시 실행해도 데이터가 안전하게 저장된다.

### 스프링 통합 테스트

- `스프링 컨테이너`와 `DB`까지 연결한 `통합 테스트`를 진행해보자.

- 회원 서비스 스프링 통합 테스트 작성
  - 소스 코드 (비공개 레포지토리): `MemberServiceIntegrationTest`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/test/java/hello/hello_spring/service/MemberServiceIntegrationTest.java
      - `@SpringBootTest` : 스프링 컨테이너와 테스트를 함께 실행한다. 즉, 실제로 스프링이 띄어서 테스트한다.
      - `@Transactional` : 테스트 시작 전에 트랜잭션을 시작하고, 테스트 완료 후에 항상 롤백한다. 이렇게 하면 DB에 데이터가 남지 않으므로 다음 테스트에 영향을 주지 않는다.
        - 참고) `@Commit`을 붙이면, 테스트 한게 실제로 DB에 반영된다.
      - `@BeforeEach`, `@AfterEach` 삭제
      - `단위 테스트` vs `통합 테스트`
        - `단위 테스트`:
          - 순수하게 자바에서 모든 테스트를 끝내서 실행이 빠르다.
        - `통합 테스트`:
          - 스프링까지 띄우므로 실행이 느리다.
        - 되도록 단위 테스트로 잘게 쪼개서 테스트 하는게 테스트 설계가 잘되었다고 볼 수 있다.
      - 참고)
        - 실무에서 테스트는 실제 사용하는 DB가 아니라, 테스트용 DB를 별도로 두고 진행하게 된다.
        - 테스트 코드에는 굳이 생성자로 할 필요없이, 필드에 바로 `@Autowired`를 붙여서 아래와 같이 많이 함.
          - `@Autowired MemberService memberService;`

### 스프링 JdbcTemplate

- 서론
  - `순수 Jdbc`와 동일한 환경설정을 하면 된다.
  - `스프링 JdbcTemplate`과 `MyBatis` 같은 라이브러리는 `JDBC API`에서 본 반복 코드를 대부분 제거해준다. 
    - 하지만 `SQL`은 직접 작성해야 한다.
  - `JdbcTemplate`은 실무에서도 많이 쓰인다.

- `스프링 JdbcTemplate` 회원 리포지토리 작성
  - 소스 코드 (비공개 레포지토리): `JdbcTemplateMemberRepository`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/repository/JdbcTemplateMemberRepository.java

- `JdbcTemplate`을 사용하도록 스프링 설정 변경
  - 소스 코드 (비공개 레포지토리): `SpringConfig`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/SpringConfig.java

- 테스트
  - 직접 스프링 띄어서 테스트 할 필요없이, 위에서 작성했던 `MemberServiceIntegrationTest`를 다시 실행하면 된다!
    - 소스 코드 (비공개 레포지토리): `MemberServiceIntegrationTest`
      - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/test/java/hello/hello_spring/service/MemberServiceIntegrationTest.java

### JPA

- 서론
  - `JPA`를 사용하면 개발 생산성을 크게 높일 수 있다.
    - `JPA`는 기존의 반복 코드는 물론이고, 기본적인 `SQL`도 `JPA`가 직접 만들어서 실행해준다.
    - `JPA`를 사용하면, `SQL`과 데이터 중심의 설계에서 객체 중심의 설계로 패러다임을 전환을 할 수 있다.
  - `JPA` vs `Mybatis`
    - 참고
      - `구글 트렌드`에서 검색
      - `자바 퍼시스턴스 API` --> `JPA`
    - 한국 동향
      - 예전에는 `Mybatis`를 많이쓰다가, 최근엔 `JPA`를 더 많이 쓰는 추세다.

        ![jpa vs mabatis in korea](https://github.com/user-attachments/assets/78c0639f-6ee4-40d3-be9f-0bdcdd846cde)

    - 전세계 동향
      - 전세계적으로 `JPA`를 훨씬 더 많이 쓴다.
      
        ![jpa vs mabatis in the world](https://github.com/user-attachments/assets/459c8d48-6838-4f53-9960-73cf2d996a12)

        ![jpa vs mabatis map](https://github.com/user-attachments/assets/05104c97-a2e6-433f-a41a-7e0e633a342b)
      
         - 중국, 한국, 일본만 `Mybatis`를 많이 사용..

- `build.gradle` 파일에 `JPA`, `h2 데이터베이스` 관련 라이브러리 추가
  - 소스 코드 (비공개 레포지토리): `build.gradle`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/build.gradle
        - `implementation 'org.springframework.boot:spring-boot-starter-data-jpa'` 추가
          - 내부에 jdbc 관련 라이브러리를 포함한다. 따라서 jdbc는 제거해도 된다.

- 스프링 부트에 JPA 설정 추가
  - 소스 코드 (비공개 레포지토리): `resources/application.properties`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/resources/application.properties
      - 아래 2줄 추가함
        - `spring.jpa.show-sql=true` // JPA가 생성하는 SQL을 출력한다.
        - `spring.jpa.hibernate.ddl-auto=none`

- JPA 엔티티 매핑
  - 소스 코드 (비공개 레포지토리): `Member`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/domain/Member.java
      - `@Entity`, `@Id`, `@GeneratedValue()` 추가

- JPA 회원 리포지토리
  - 소스 코드 (비공개 레포지토리): `JpaMemberRepository`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/repository/JpaMemberRepository.java
      - JPA를 쓰려면 `EntityManager`를 주입 받아야 한다.
        - 스프링 부트가 자동으로 `EntityManager`를 생성해준다.

- 서비스 계층에 트랜잭션 추가
  - 소스 코드 (비공개 레포지토리): `MemberService`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/service/MemberService.java
      - `@Transactional` 추가함.
        - **JPA를 통한 모든 데이터 변경은 트랜잭션 안에서 실행해야 한다.**
        - 스프링은 해당 클래스의 메서드를 실행할 때 트랜잭션을 시작하고, 메서드가 정상 종료되면 트랜잭션을 커밋한다.
          - 만약 런타임 예외가 발생하면 롤백한다.

- JPA를 사용하도록 스프링 설정 변경
  - 소스 코드 (비공개 레포지토리): `SpringConfig`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/SpringConfig.java
      - JPA를 위해 `EntityManager` 추가함.

- 참고
  - JPA도 스프링 만큼 성숙한 기술이고, 학습해야 할 분량도 방대하다...

### 스프링 데이터 JPA

- 서론
  - `스프링 부트`와 `JPA`
    - `스프링 부트`와 `JPA`만 사용해도 개발 생산성이 정말 많이 증가하고, 개발해야할 코드도 확연히 줄어든다.
  - `스프링 데이터 JPA`
    - 여기에 `스프링 데이터 JPA`를 사용하면, 리포지토리에 `구현 클래스` 없이 `인터페이스` 만으로 개발을 완료할 수 있다.
    - 반복 개발해온 기본 `CRUD` 기능도 모두 제공한다.
    - 개발자는 핵심 비즈니스 로직을 개발하는데, 집중할 수 있다.
    - 실무에서 관계형 데이터베이스를 사용한다면, `스프링 데이터 JPA`는 이제 선택이 아니라 필수이다.
  - 주의
    - `스프링 데이터 JPA`는 `JPA`를 편리하게 사용하도록 도와주는 기술이다.
    - 따라서 `JPA`를 먼저 학습한 후에 `스프링 데이터 JPA`를 학습해야 한다.

- 스프링 데이터 JPA 회원 리포지토리
  - 소스 코드 (비공개 레포지토리): `SpringDataJpaMemberRepository` (`interface`)
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/repository/SpringDataJpaMemberRepository.java
      - 개발자가 `구현체`를 구현할 필요 없이 `인터페이스`만으로 기능을 구현한다!
        - 스프링 데이터 JPA가 자동으로 구현체를 만들고, 스프링빈을 자동으로 등록해준다.
      - 공통 기능들을 이미 인터페이스에 다 정의 되어있다. 
        - 공통화 하기 어려운 것들만 여기서 정의 해주면 된다.

- 스프링 데이터 JPA 회원 리포지토리를 사용하도록 스프링 설정 변경
  - 소스 코드 (비공개 레포지토리): `SpringConfig`
    - https://github.com/JohnKim0911/kyh_hello-spring/blob/master/src/main/java/hello/hello_spring/SpringConfig.java
      - 스프링 데이터 JPA가 `SpringDataJpaMemberRepository`를 스프링 빈으로 자동 등록해준다.

- 스프링 데이터 JPA 제공 클래스

  ![스프링 데이터 JPA 제공 클래스](https://github.com/user-attachments/assets/2b52269f-7e45-48e6-bf85-7eb5192cd642)

- 스프링 데이터 JPA 제공 기능
  - 인터페이스를 통한 기본적인 CRUD
  - `findByName()`, `findByEmail()`처럼 메서드 이름 만으로 조회 기능 제공
  - 페이징 기능 자동 제공

- 참고
  - 실무에서는 `JPA`와 `스프링 데이터 JPA`를 기본으로 사용하고, 복잡한 동적 쿼리는 `Querydsl`이라는 라이브러리를 사용하면 된다.
  - `Querydsl`을 사용하면 쿼리도 자바 코드로 안전하게 작성할 수 있고, 동적 쿼리도 편리하게 작성할 수 있다.
  - 이 조합으로 해결하기 어려운 쿼리는 `JPA`가 제공하는 `네이티브 쿼리`를 사용하거나, 앞서 학습한 `스프링 JdbcTemplate`를 사용하면 된다.

## 8. AOP

## 9. 다음으로