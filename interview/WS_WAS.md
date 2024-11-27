# `Web Server` vs `Web Application Server` 차이점

![WS, WAS](https://github.com/user-attachments/assets/cef6dfc2-98ac-4235-b031-8e1e30d43a05)

## 용어

- `Web Server` (`WS`)
  - 웹 서버
- `Web Application Server` (`WAS`)
  - 애플리케이션 서버
  - '와스'라고 발음한다.


## 차이점

- `Web Server`
  - 정적 컨텐츠 제공
    - 이미지나 `html` 같은 정적인 리소스를 전달
    - 예시) `Apache`
- `WAS`
  - 동적 데이터 처리
    - 비즈니스 로직, 데이터 처리
    - 예시) `Tomcat`

## WS, WAS 왜 나누나?

- `Web Server`가 하는 일을 `WAS`로도 전부 가능한데, 왜 나누나?
  - 단순한 정적 콘텐츠를 `Web Server`에게 맡기면, `WAS`의 부하를 줄일 수 있음.
    - `WAS`는 DB 연동 및 비즈니스 로직을 처리하는데 집중 할 수 있음.
  - 장애 극복에 유리
    - 기존에 여러 `WAS`가 있는데, 어느 한 `WAS`에서 문제가 생긴다면...
      - `Web Server`에서 해당 `WAS`를 사용하지 막아도 됨.
      - `Web Server`에서 화면은 계속 보여주고, 비즈니스 로직은 다른 `WAS`를 통해 계속 진행함.
        - 사용자 입장에선 문제가 발생했는지 느끼지 못함. 장애를 자연스럽게 극복 가능.

- 규모가 커질수록 웹 서버와 웹앱 서버를 분리함.

## 웹 서비스 구조
아래 처럼 다양한 구조를 가질 수 있다.

1. `Client` → `Web Server` → `DB`
2. `Client` → `WAS` → `DB`
3. `Client` → `Web Server` → `WAS` → `DB`

## 참고한 곳

https://yozm.wishket.com/magazine/detail/1780/