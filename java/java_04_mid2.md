# (복습) 김영한의 실전 자바 - 중급2편

|    | 제목                                                               | 복습일        |
|----|------------------------------------------------------------------|------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)                                        | 2024-12-03 |
| 2  | [제네릭 - Generic1](#2-제네릭---generic1)                              | 2024-12-03 |
| 3  | [제네릭 - Generic2](#3-제네릭---generic2)                              |            |
| 4  | [컬렉션 프레임워크 - ArrayList](#4-컬렉션-프레임워크---arraylist)                |            |
| 5  | [컬렉션 프레임워크 - LinkedList](#5-컬렉션-프레임워크---linkedlist)              |            |
| 6  | [컬렉션 프레임워크 - List](#6-컬렉션-프레임워크---list)                          |            |
| 7  | [컬렉션 프레임워크 - 해시(Hash)](#7-컬렉션-프레임워크---해시hash)                    |            |
| 8  | [컬렉션 프레임워크 - HashSet](#8-컬렉션-프레임워크---hashset)                    |            |
| 9  | [컬렉션 프레임워크 - Set](#9-컬렉션-프레임워크---set)                            |            |
| 10 | [컬렉션 프레임워크 - Map, Stack, Queue](#10-컬렉션-프레임워크---map-stack-queue) |            |
| 11 | [컬렉션 프레임워크 - 순회, 정렬, 전체 정리](#11-컬렉션-프레임워크---순회-정렬-전체-정리)         |            |
| 12 | [다음으로](#12-다음으로)                                                 |            |

---

## 1. 강의 소개와 자료

- 실제 강의:
    - https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-2

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
      - 제 기억을 살리기 위한 용도이다보니, 아래 글만으로는 이해가 어려울 수 있습니다.
        - 필요하시다면, 위 강의를 직접 수강하시는 것을 추천드립니다.
      - 방식:
        - 강의를 들으면서 코드를 직접 치고, 
        - 강의가 끝나면 다시 교재를 보면서 중요 내용 위주로 정리하였습니다.
    - 유료 강의이므로, 실제 작성한 전체 코드는 비공개 합니다. (저작권...)
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh-java-mid2
            - 링크가 있긴하지만, 저만 볼 수 있습니다. (404 error 뜨는게 정상)

- 강의 구성

  ![중급 2편 강의내용](https://github.com/user-attachments/assets/a13273ec-4bbf-4006-8f9e-be15b4548b11)

---

## 2. 제네릭 - Generic1

### 프로젝트 환경 구성

- 교제 참고...

### 제네릭이 필요한 이유

- 예제를 통해 알아본다.

- 예제 1 (`BoxMain1.java`)
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex1
  - `IntegerBox.java`: 숫자를 보관하고 꺼낼 수 있는 단순한 기능을 제공한다.
  - `StringBox.java`: 문자열을 보관하고 꺼낼 수 있는 단순한 기능을 제공한다.
  - 문제점
    - 이후에 `Double`, `Boolean`을 포함한 다양한 타입을 담는 박스가 필요하다면, 각각의 타입별로 `DoubleBox`, `BooleanBox`와 같이 클래스를 새로 만들어야 한다.
    - 담는 타입이 수십개라면, 수십개의 `XxxBox` 클래스를 만들어야 한다.

### 다형성을 통한 중복 해결 시도

- `Object`는 모든 타입의 부모이다. 다형성(다형적 참조)를 사용해서 중복을 해결하도록 시도해본다.
- 예제 2 (`BoxMain2`)
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex1
  - `ObjectBox.java`
    - `Object`는 모든 타입의 부모이다. 다형성(다형적 참조)를 사용해서 모든 타입을 `ObjectBox`에 보관할 수 있다.
  - 문제점
    - 반환 타입이 맞지 않는 문제
      - `Object`를 반환하므로 다운 캐스팅을 해줘야 한다.
    - 잘못된 타입의 인수 전달 문제
      - 아무 타입이나 전달되어도 컴파일러가 잡아주지 못한다.
      - 잘못된 타입의 값을 전달하면, 값을 꺼낼 때 에러가 발생한다.
        - 예시) `Integer result = (Integer) "문자100";` // 캐스팅 에러발생
- 결과적으로 이 방식은 타입 안전성이 떨어진다.    

### 제네릭 적용

- 제네릭을 사용하면 `코드 재사용`과 `타입 안전성`이라는 두 마리 토끼를 한 번에 잡을 수 있다.

```java
package generic.ex1;

public class GenericBox<T> { //<>: 다이아몬드, T: 타입 매개변수

    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}
```

```java
package generic.ex1;

public class BoxMain3 {

    public static void main(String[] args) {

        GenericBox<Integer> integerBox = new GenericBox<Integer>(); //생성 시점에 T의 타입 결정
        integerBox.set(10);
        //integerBox.set("문자100"); //Integer 타입만 허용, 컴파일 오류
        Integer integer = integerBox.get(); //Integer 타입 변환(캐스팅X)
        System.out.println("integer = " + integer); //10

        //... 생략
        
        //타입 추론: 생성하는 제네릭 타입 생략 가능
        GenericBox<Integer> integerBox2 = new GenericBox<>();
    }
}
```

- 전체 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex1
  - `GenericBox.java`, `BoxMain3.java` 참고

### 제네릭 용어와 관례

- 메서드의 매개변수와 인자 

    ```java
    void method(String param); //매개변수
    
    void main() {
        String arg = "hello";
        method(arg); //인수 전달
    }
    ```

  - 매개변수(`Parameter`): String param 
  - 인자, 인수(`Argument`): arg

- 메서드 vs 제네릭 클래스
  - 메서드는 `매개변수`에 `인자`를 전달해서 사용할 값을 결정한다.
  - 제네릭 클래스는 `타입 매개변수`에 `타입 인자`를 전달해서 사용할 타입을 결정한다.

- 용어 정리
  - 제네릭 (Generic) 단어
    - 영어단어 뜻: 일반적인, 범용적인
    - 특정 타입에 속한 것이 아니라 일반적으로, 범용적으로 사용할 수 있다는 뜻
  - 제네릭 타입  (Generic Type)
    - 클래스나 인터페이스를 정의할 때 타입 매개변수를 사용하는 것을 말한다.
    - 제네릭 클래스, 제네릭 인터페이스를 모두 합쳐서 제네릭 타입이라 한다.
    - 예시) `GenericBox<T>`
  - 타입 매개변수 (Type Parameter)
    - 예시) `GenericBox<T>`에서 `T` //제네릭 타입이나 메서드에서 사용되는 변수
  - 타입 인자 (Type Argument)
    - 예시) `GenericBox<Integer>`에서 `Integer` //제네릭 타입을 사용할 때 제공되는 실제 타입.

- 제네릭 명명 관례
  - 여러 글자나, 소문자를 사용해도 상관은 없다.
  - 하지만 대부분 관례를 따른다.
    - 관례 - 일반적으로 대문자를 사용하고, 용도에 맞는 단어의 첫글자를 사용
    - 주로 사용하는 키워드
      - `E`: Element 
      - `K`: Key 
      - `N`: Number 
      - `T`: Type 
      - `V`: Value 
      - `S`,`U`,`V` etc.: 2nd, 3rd, 4th types

- 한번에 여러 타입 매개변수를 선언할 수 있다.
  - 예) `class Data<K, V> { ... }`

- 제네릭의 타입 인자로 기본형(`int`, `double`, ...)은 사용 불가
  - 래퍼 클래스(`Integer`, `Double`)를 사용하기!

- 로 타입 (raw type)
  - `GenericBox integerBox = new GenericBox();` // 로 타입 (raw type) 혹은 원시타입이라 한다.
    - 실제론 이와 같이 작동한다: `GenericBox<Object> integerBox = new GenericBox<>();`
  - 로 타입은 하위 호환을 위해 남겨둔 것. 사용하지 말자.

### 제네릭 활용 예제

- 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic
  - `animal`, `ex2` 패키지 참조
    - `animal` 패키지
      - `Dog`, `Cat`은 `Animal`을 상속받는다. 
    - `ex2` 패키지
      - `AnimalMain1.java`: 
        - 제네릭으로 `Box`클래스 만들고 (`Box.java`),
        - 타입 매개변수에 `Animal`, `Dog`, `Cat` 넣어서 `animalBox`, `dogBox`, `catBox`를 만든다.
      - `AnimalMain2.java`:
        - `set(Animal value)`이므로 `set()`에 `Animal`의 하위 타입인 `Dog`, `Cat`도 전달할 수 있다.

### 문제와 풀이

- 문제1 - 제네릭 기본1
  - `ContainerTest.java`를 참고해서`Container.java`를 만들어라. (제네릭 사용)
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/test/ex1
- 문제2 - 제네릭 기본2
  - `PairTest.java`를 참고해서`Pair.java`를 만들어라. (제네릭 사용)
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/test/ex2

---

## 3. 제네릭 - Generic2

---

## 4. 컬렉션 프레임워크 - ArrayList

---

## 5. 컬렉션 프레임워크 - LinkedList

---

## 6. 컬렉션 프레임워크 - List

---

## 7. 컬렉션 프레임워크 - 해시(Hash)

---

## 8. 컬렉션 프레임워크 - HashSet

---

## 9. 컬렉션 프레임워크 - Set

---

## 10. 컬렉션 프레임워크 - Map, Stack, Queue

---

## 11. 컬렉션 프레임워크 - 순회, 정렬, 전체 정리

---

## 12. 다음으로

---
