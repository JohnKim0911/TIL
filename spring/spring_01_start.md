# (복습) 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

- 김영한의 스프링 완전 정복 로드맵
  - 1편) 스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술

|   | 제목                                            | 강의 분량     | 교재 분량 | 복습일        |
|---|-----------------------------------------------|-----------|-------|------------|
| 1 | [강의 소개](#1-강의-소개)                             | 5분        | 3     | 2024.12.13 |
| 2 | [프로젝트 환경설정](#2-프로젝트-환경설정)                     | 47분       | 10    | 2024.12.13 |
| 3 | [스프링 웹 개발 기초](#3-스프링-웹-개발-기초)                 | 33분       | 5     | 2024.12.14 |
| 4 | [회원 관리 예제 - 백엔드 개발](#4-회원-관리-예제---백엔드-개발)     | 55분       |       |            |
| 5 | [스프링 빈과 의존관계](#5-스프링-빈과-의존관계)                 | 27분       |       |            |
| 6 | [회원 관리 예제 - 웹 MVC 개발](#6-회원-관리-예제---웹-mvc-개발) | 17분       |       |            |
| 7 | [스프링 DB 접근 기술](#7-스프링-db-접근-기술)               | 1시간 33분   |       |            |
| 8 | [AOP](#8-aop)                                 | 22분       |       |            |
| 9 | [다음으로](#9-다음으로)                               | 18분       |       |            |
|   |                                               | 총 5시간 21분 |       |            |

## 1. 강의 소개

- 강의 소개 페이지: https://inf.run/hivx6

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
        - 제 기억을 살리기 위한 용도이다보니, 아래 글만으로는 이해가 어려울 수 있습니다.
            - 필요하시다면, 위 강의를 직접 수강하시는 것을 추천드립니다.
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

## 5. 스프링 빈과 의존관계

## 6. 회원 관리 예제 - 웹 MVC 개발

## 7. 스프링 DB 접근 기술

## 8. AOP

## 9. 다음으로