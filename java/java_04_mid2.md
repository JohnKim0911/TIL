# (복습) 김영한의 실전 자바 - 중급2편

|    | 제목                                                               | 복습일             |
|----|------------------------------------------------------------------|-----------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)                                        | 2024-12-03      |
| 2  | [제네릭 - Generic1](#2-제네릭---generic1)                              | 2024-12-03      |
| 3  | [제네릭 - Generic2](#3-제네릭---generic2)                              | 2024-12-04      |
| 4  | [컬렉션 프레임워크 - ArrayList](#4-컬렉션-프레임워크---arraylist)                | 2024-12-04 ~ 05 |
| 5  | [컬렉션 프레임워크 - LinkedList](#5-컬렉션-프레임워크---linkedlist)              | 2024-12-06      |
| 6  | [컬렉션 프레임워크 - List](#6-컬렉션-프레임워크---list)                          |                 |
| 7  | [컬렉션 프레임워크 - 해시(Hash)](#7-컬렉션-프레임워크---해시hash)                    |                 |
| 8  | [컬렉션 프레임워크 - HashSet](#8-컬렉션-프레임워크---hashset)                    |                 |
| 9  | [컬렉션 프레임워크 - Set](#9-컬렉션-프레임워크---set)                            |                 |
| 10 | [컬렉션 프레임워크 - Map, Stack, Queue](#10-컬렉션-프레임워크---map-stack-queue) |                 |
| 11 | [컬렉션 프레임워크 - 순회, 정렬, 전체 정리](#11-컬렉션-프레임워크---순회-정렬-전체-정리)         |                 |
| 12 | [다음으로](#12-다음으로)                                                 |                 |

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

### 타입 매개변수 제한1 - 시작

- 예제 1) 동물병원 만들기
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex3
        - `DogHospital`, `CatHospital`, `AnimalHospitalMainV0` 참고
    - 문제점
        - 코드 재사용 X:
            - 개 병원과 고양이 병원은 중복이 많이 보인다.
                - `DogHospital`, `CatHospital`를 따로 작성해서 중복되는 코드가 많다.
        - 타입 안전성 O:
            - 타입 안전성이 명확하게 지켜진다.
                - 개 병원은 개만 받을 수 있고, 고양이 병원은 고양이만 받을 수 있다.

### 타입 매개변수 제한2 - 다형성 시도

- 예제 2) 동물병원 만들기 - 리팩토링
    - `Dog`, `Cat`은 `Animal`이라는 부모타입이 있다. 다형성을 사용해서 중복을 제거해보자.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex3
        - `AnimalHospitalV1`, `AnimalHospitalMainV1` 참고
    - 문제점
        - 코드 재사용 O:
            - 다형성을 통해 `AnimalHospitalV1` 하나로 개와 고양이를 모두 처리한다.
                - 기존 `DogHospital`, `CatHospital`로 따로 작성했던 것을 `AnimalHospitalV1` 하나로 처리 할 수 있다.
        - 타입 안전성 X:
            - 개 병원에 고양이를 전달하는 문제가 발생한다.
            - `Animal` 타입을 반환하기 때문에 다운 캐스팅을 해야 한다.
            - 실수로 고양이를 입력했는데, 개를 반환하는 상황이라면 캐스팅 예외가 발생한다.

### 타입 매개변수 제한3 - 제네릭 도입과 실패

- 예제 3) 동물병원 만들기 - 리팩토링
    - 제네릭을 도입해서 코드 재사용은 늘리고, 타입 안전성 문제도 해결해보자.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex3
        - `AnimalHospitalV2`, `AnimalHospitalMainV2` 참고
    - 문제점
        - 컴파일시, 자바 컴파일러는 타입 매개변수에 어떤 타입이 들어올 지 알 수 없기 때문에 모든 객체의 최종 부모인 `Object` 타입으로 가정한다.
        - 따라서 `AnimalHospitalV2`에서는 `Object`가 제공하는 메서드만 호출할 수 있다.
        - 동물 병원에 `Integer`, `Object` 같은 동물과 전혀 관계 없는 타입을 타입 인자로 전달 할 수 있다.

### 타입 매개변수 제한4 - 타입 매개변수 제한

- 예제 4) 동물병원 만들기 - 리팩토링
    - 타입 매개변수를 특정 타입으로 제한할 수 있다.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex3
        - `AnimalHospitalV3`, `AnimalHospitalMainV3` 참고

      ```java
      public class AnimalHospitalV3<T extends Animal> { ... } // extends를 사용하여 Animal 타입만 사용할 수 있도록 제한.
      ```

    - 정리
        - 제네릭에 `타입 매개변수 상한`을 사용해서 타입 안전성을 지키면서 상위 타입의 원하는 기능까지 사용할 수 있었다.
        - 덕분에 코드 재사용과 타입 안전성이라는 두 마리 토끼를 동시에 잡을 수 있었다.

### 제네릭 메서드

- 제네릭 메서드는 클래스 전체가 아니라, 특정 메서드 단위로 제네릭을 도입할 때 사용한다.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex4
        - `GenericMethod`, `MethodMain1` 참고

- 제네릭 타입 vs 제네릭 메서드
    - 제네릭 타입
        - 타입 인자 전달: 객체를 생성하는 시점
      ```java
      public class AnimalHospitalV3<T extends Animal> { //제네릭 타입
          private T animal;
      
          public void set(T animal) {
            // 생략
          }
      }
      ```
    - 제네릭 메서드
        - 타입 인자 전달: 메서드를 호출하는 시점
      ```java
      public class GenericMethod {
          public static <T extends Number> T numberMethod(T t) { //제네릭 메서드
              // 생략
              return t;
          }
      }
      ```

- 참고
    - 제네릭 메서드는 인스턴스 메서드와 static 메서드에 모두 적용할 수 있다.
      ```java
      class Box<T> { //제네릭 타입
          static <V> V staticMethod2(V t) {} //static 메서드에 제네릭 메서드 도입 가능
          <Z> Z instanceMethod2(Z z) {} //인스턴스 메서드에 제네릭 메서드 도입 가능
      }
      ```
    - 제네릭 타입은 static 메서드에 타입 매개변수를 사용할 수 없다.
        - 제네릭 타입은 객체를 생성하는 시점에 타입이 정해진다.
        - 그런데 static 메서드는 인스턴스 단위가 아니라 클래스 단위로 작동하기 때문에 제네릭 타입과는 무관하다.
        - 따라서 static 메서드에 제네릭을 도입하려면 제네릭 메서드를 사용해야 한다.
      ```java
      class Box<T> {
          T instanceMethod(T t) {} //가능
          static T staticMethod1(T t) {} //제네릭 타입의 T 사용 불가능
      }
      ```

- 제네릭 메서드 타입 매개변수 제한
    - 제네릭 타입과 마찬가지로 타입 매개변수를 제한할 수 있다.
        - 예시) `public static <T extends Number> T numberMethod(T t) {...}`
            - `extends`로 `Number` 타입만 받을 수 있도록 제한한다.

- 제네릭 메서드 타입 추론
    - 제네릭 메서드를 호출할 때 이 타입 인자를 계속 전달하는 것은 매우 불편하다.
        - 예시) `Integer result = GenericMethod.<Integer>genericMethod(10);` //<Integer> 넣어주는 것 불편
    - 자바 컴파일러가 타입 인자를 추론하여 자동으로 해당 타입 인자를 넣어준다.
        - 개발자는 타입 인자를 생략하고 다음과 같이 사용하면 된다.
        - 예시) `Integer result2 = GenericMethod.genericMethod(10);` //<Integer> 생략 가능!

### 제네릭 메서드 활용

- 앞서 제네릭 타입으로 만들었던 `AnimalHospitalV3`의 주요 기능을 **제네릭 메서드**로 다시 만들어보자.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex4
        - `AnimalMethod`, `MethodMain2` 참고

- 제네릭 타입과 제네릭 메서드의 우선순위
    - 제네릭 타입과 제네릭 메서드의 타입 매개변수를 같은 이름으로 사용하면 어떻게 될까?
        - 결론: 제네릭 타입보다 제네릭 메서드가 높은 우선순위를 가진다.
        - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex4
            - `ComplexBox`, `MethodMain3` 참고
    - 프로그래밍에서 이렇게 모호한 것은 좋지 않다.
        - 이름이 겹치면 둘 중 하나를 다른 이름으로 바꾸자.

### 와일드카드1

- 와일드카드는 제네릭 타입이나, 제네릭 메서드를 선언하는 것이 아니다.
    - 와일드카드는 이미 만들어진 제네릭 타입을 활용할 때 사용한다.
- 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex5
    - `Box`, `WildcardEx`, `WildcardMain1` 참고
        - `WildcardEx`를 자세히 보자.
            - 제네릭 메서드와 와일드 카드를 비교하였다.
            - 와일드카드는 `?` 를 사용해서 정의한다.

```java
package generic.ex5;

import generic.animal.Animal;

public class WildcardEx {

    static <T> void printGenericV1(Box<T> box) { //제네릭 메서드
        System.out.println("T = " + box.get());
    }

    static void printWildcardV1(Box<?> box) { //일반 메서드 + 비제한 와일드카드
        System.out.println("? = " + box.get());
    }

    static <T extends Animal> void printGenericV2(Box<T> box) { //제네릭 메서드 + 타입 매개변수 제한
        T t = box.get();
        System.out.println("이름 = " + t.getName());
    }

    static  void printWildcardV2(Box<? extends Animal> box) { //일반 메서드 + 상한 와일드카드
        Animal animal = box.get();
        System.out.println("이름 = " + animal.getName());
    }

    //생략
}
```

- 비제한 와일드카드
    - `?` 만 사용해서 제한 없이 모든 타입을 다 받을 수 있는 와일드카드

- 제네릭 메서드 vs 와일드카드
    - 꼭 필요한 상황이 아니라면, 더 단순한 와일드카드 사용을 권장한다.
    - 제네릭 메서드
        - 제네릭 메서드에는 타입 매개변수가 존재한다.
        - 그리고 특정 시점에 타입 매개변수에 타입 인자를 전달해서 타입을 결정해야 한다.
        - 이런 과정은 매우 복잡하다.
    - 와일드 카드
        - 제네릭 메서드처럼 타입을 결정하거나 복잡하게 작동하지 않는다.
        - 단순히 일반 메서드에 제네릭 타입을 받을 수 있는 매개변수가 하나 있는 것 뿐이다.

### 와일드카드2

- 상한 와일드카드
    - "와일드카드1"의 예시 참고.
    - 예시) `static void printWildcardV2(Box<? extends Animal> box) {...}`
        - 와일드카드(`?`)뒤에 `extends`로 `Animal`과 그 하위 타입만 받을 수 있도록 상한 제한을 두었다.

- 타입 매개변수가 꼭 필요한 경우

```java
package generic.ex5;

import generic.animal.Animal;

public class WildcardEx {
    //생략

    static <T extends Animal> T printAndReturnGeneric(Box<T> box) { //제네릭 메서드
        T t = box.get(); //타입 매개변수를 사용하면 전달한 타입을 그대로 받을 수 있다.
        System.out.println("이름 = " + t.getName());
        return t;
    }

    static Animal printAndReturnWildcard(Box<? extends Animal> box) { //일반 메서드 + 상한 와일드카드
        Animal animal = box.get(); //와일드카드를 사용하면 전달한 타입을 그대로 받을 수 없다. 상한 걸어둔 타입으로 받게된다.
        System.out.println("이름 = " + animal.getName());
        return animal;
    }
}
```

- 하한 와일드 카드
    - 와일드카드는 상한 뿐만 아니라 하한도 지정할 수 있다.
    - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/ex5
        - `WildcardMain2` 참고
            - `static void writeBox(Box<? super Animal> box) { ... }` // `super`로 하한을 지정한다.
                - `?` 가 `Animal` 타입을 포함한 상위 타입만 입력 받을 수 있다는 뜻.

### 타입 이레이저

- 이레이저(eraser): 지우개
- 제네릭은 자바 컴파일 단계에서만 사용되고, 컴파일 이후에는 제네릭 정보가 지워진다. --> 타입 이레이저
    - 컴파일 전인 `.java` 에는 제네릭의 타입 매개변수가 존재하지만,
    - 컴파일 이후인 자바 바이트코드 `.class` 에는 타입 매개변수가 존재하지 않는다.
    - 예시) 100% 정확한 코드는 아니고 대략 이런 방식으로 작동한다고 이해하면 충분하다.
        - 컴파일 전
          ```java
          public class GenericBox<T> { //타입 매개변수 존재
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
          void main() {
              GenericBox<Integer> box = new GenericBox<Integer>();
              box.set(10);
              Integer result = box.get();
          }
          ```      
        - 컴파일 후
          ```java
          public class GenericBox { //타입 매개변수 삭제
              private Object value;
            
              public void set(Object value) {
                  this.value = value;
              }
            
              public Object get() {
                  return value;
              }
          }
          ```
          ```java
          void main() {
              GenericBox box = new GenericBox();
              box.set(10);
              Integer result = (Integer) box.get(); //자바 컴파일러는 제네릭에서 타입 인자로 지정한 타입(Integer)으로 캐스팅하는 코드를 추가해준다.
          }
          ```

- 타입 매개변수 제한의 경우
    - 타입 매개변수를 제한하면 제한한 타입으로 코드를 변경한다.
    - 예시)
        - 컴파일 전
          ```java
          public class AnimalHospitalV3<T extends Animal> { //Animal로 타입 매개변수 제한
              private T animal;
              //생략
          }
          ```
        - 컴파일 후
          ```java
          public class AnimalHospitalV3 {
              private Animal animal; //제한한 타입으로 코드를 변경 (T -> Animal)
              //생략
          }
          ```

- 타입 이레이저 방식의 한계
    - 런타임에는 제네릭으로 지정한 타입 정보가 모두 제거된다.
    - 따라서, 런타임에 타입을 활용하는 다음과 같은 코드는 작성할 수 없다.
        ```java
        class EraserBox<T> {
            public boolean instanceCheck(Object param) {
                return param instanceof T; //오류 //컴파일후에는 T가 Object로 변경된다. 항상 true가 되기때문에 사용할 수 없다.
            }
            public void create() {
                return new T(); //오류 //컴파일후에는 new Object()로 변경된다. 개발자가 의도한것과는 다르게 된다.
            }
        }
        ```
    - 위 주석과 같은 이유로 자바는 타입 매개변수에 `instanceof` 혹은 `new`를 허용하지 않는다.

### 문제와 풀이

- 스타크래프트 유닛 만들기
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/generic/test/ex3
    - 공통 소스 생성: `unit` 패키지 참고 (`BioUnit`, `Marine`, `Zealot`, `Zergling`)
    - 문제와 풀이1 - 제네릭 메서드와 상한 (`UnitUtilTest`, `UnitUtil`)
    - 문제와 풀이2 - 제네릭 타입과 상한 (`ShuttleTest`, `Shuttle`)
    - 문제와 풀이3 - 제네릭 메서드와 와일드카드 (`UnitPrinterTest`, `UnitPrinter`)

### 정리

- 실무에서 직접 제네릭을 사용해서 무언가를 설계하거나 만드는 일은 드물다.
  - 그것보다는 대부분 이미 제네릭을 통해 만들어진 프레임워크나 라이브러리들을 가져다 사용하는 경우가 훨씬 많다.
  - 그래서 이미 만들어진 코드의 제네릭을 읽고 이해하는 정도면 충분하다.
  - 실무에서 직접 제네릭을 사용하더라도 어렵고 복잡하게 사용하기 보다는 보통 단순하게 사용한다.
  - 지금까지 학습한 정도면 실무에 필요한 제네릭은 충분히 이해했다고 볼 수 있다.

- 제네릭은 지금까지 설명한 내용보다 더 복잡하고 어려운 개념들도 있다.
  - 예) 공변(covariant), 반공변(contravariant)
  - 이런 부분은 실무에서 많은 경험을 쌓고, 본인이 필요하다고 느껴질 때 따로 공부하는 것을 권장한다.

- 제네릭은 컬렉션 프레임워크에서 가장 많이 사용된다.
  - 따라서 컬렉션 프레임워크를 통해서 제네릭이 어떻게 활용되는지 자연스럽게 학습할 수 있다.

---

## 4. 컬렉션 프레임워크 - ArrayList

### 배열의 특징1 - 배열과 인덱스

- 자료 구조
  - 여러 데이터(자료)를 구조화해서 다루는 것을 자료 구조라 한다. 예) 배열
  - 자바는 컬렉션 프레임워크라는 이름으로 다양한 자료 구조를 제공한다.
  - 먼저 자료 구조의 가장 기본이 되는 배열의 특징을 알아보자.

- 배열의 특징
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/array/ArrayMain1.java
  - 배열에서 인덱스를 사용하는 경우 데이터가 아무리 많아도 한 번의 연산으로 필요한 위치를 찾을 수 있다.
    - 공식: 배열의 시작 참조 + (자료의 크기 * 인덱스 위치)
      - arr[0]: x100 + (4byte * 0): x100
      - arr[1]: x100 + (4byte * 1): x104
      - arr[2]: x100 + (4byte * 2): x108
    
    ![배열 index 사용 예시](https://github.com/user-attachments/assets/17dc941b-4088-431d-88f9-6b1f44d75f4b)

- 배열의 검색
  - 데이터를 검색할 때는 배열에 들어있는 데이터를 하나하나 비교해야 한다.
  - 배열의 순차 검색은 배열에 들어있는 데이터의 크기 만큼 연산이 필요하다.
    - 배열의 크기가 n이면 연산도 n만큼 필요하다.

### 빅오(O) 표기법

- 빅오(O) 표기법
  - 알고리즘의 성능을 분석할 때 사용하는 수학적 표현 방식이다.
  - 큰 데이터를 입력한다고 가정하고, 데이터 양 증가에 따른 성능의 변화 추세를 비교하는데 사용한다.
  - 정확한 성능을 측정하는 것이 아니라 대략적인 추세를 비교를 하는 것이 목적이다.
    - 상수는 크게 의미가 없기때문에 제거한다. 
      - 예를 들어 `O(n + 2)`, `O(n/2)`도 모두 `O(n)`으로 표시한다.
  - 빅오 표기법은 보통 최악의 상황을 가정해서 표기한다.
  
![빅오(O) 표기법](https://github.com/user-attachments/assets/b3f594e8-c570-4d48-bc69-56b0b377cae8)

- 빅오 표기법의 예시
  - `O(1)` - `상수 시간`: 입력 데이터의 크기에 관계없이 알고리즘의 실행 시간이 일정하다.
    - 예) 배열에서 인덱스를 사용하는 경우
  - `O(n)` - `선형 시간`: 알고리즘의 실행 시간이 입력 데이터의 크기에 비례하여 증가한다.
    - 예) 배열의 검색, 배열의 모든 요소를 순회하는 경우
  - `O(n²)` - `제곱 시간`: 알고리즘의 실행 시간이 입력 데이터의 크기의 제곱에 비례하여 증가한다.
    - 예) 보통 이중 루프를 사용하는 알고리즘에서 나타남
  - `O(log n)` - `로그 시간`: 알고리즘의 실행 시간이 데이터 크기의 로그에 비례하여 증가한다.
    - 예) 이진 탐색
  - `O(n log n)` - `선형 로그 시간`:
    - 예) 많은 효율적인 정렬 알고리즘들

- 배열 정리 
  - 배열의 인덱스 사용: `O(1)`
  - 배열의 순차 검색: `O(n)`
  - 인덱스를 사용할 수 있다면 최대한 활용하는 것이 좋다.

### 배열의 특징2 - 데이터 추가

- 배열의 특정 위치에 데이터를 추가해보자.
  - 기존 데이터를 유지하면서 새로운 데이터를 입력하는 것을 뜻한다.

- 배열의 데이터 추가 예시
  - 배열의 첫번째 위치에 추가 (`O(n)`)
    - 기존 데이터들을 모두 오른쪽으로 한 칸씩 밀어서 추가할 위치를 확보해야 한다.
    - 이때 배열의 마지막 부분 부터 오른쪽으로 밀어야 데이터를 유지할 수 있다.
  - 배열의 중간 위치에 추가 (`O(n)`)
    - `index`부터 시작해서 데이터들을 오른쪽으로 한 칸씩 밀어야 한다.
  - 배열의 마지막 위치에 추가 (`O(1)`)
    - 기존 데이터를 이동하지 않아도 된다. 단순하게 값만 입력하면 된다.
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/array/ArrayMain2.java

- 배열의 한계
  - 배열의 크기를 배열을 생성하는 시점에 미리 정해야 한다.
    - 처음부터 너무 적은 배열을 확보하면 배열을 초과하는 문제가 발생 할 수 있다.
    - 처음부터 너무 많은 배열을 확보하면 메모리가 많이 낭비된다.

### 직접 구현하는 배열 리스트1 - 시작

- 배열의 불편한 점
  - 배열의 길이를 동적으로 변경할 수 없다.
  - 데이터를 추가하기 불편하다.
    - 데이터를 추가하는 경우, 직접 오른쪽으로 한 칸씩 데이터를 밀어야 한다.
- `List`(리스트) 자료구조
  - 배열의 불편함을 해소하고, 동적으로 데이터를 추가할 수 있는 자료 구조.
  - 순서가 있고, 중복을 허용한다.

- `MyArrayListV1` 구현
  - 배열을 활용해서 리스트 자료 구조를 직접 만들어보자.
  - 보통 배열을 사용한 리스트라고 해서 `ArrayList`라고 부른다. 여기서는 `MyArrayList`라는 이름을 사용.
  - 먼저 정적인 배열을 그대로 사용해서 구현.
    - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/array
      - `MyArrayListV1`, `MyArrayListV1Main` 참고
      - 리스트의 마지막에 데이터를 추가하기 때문에 배열에 들어있는 기존 데이터는 이동하지 않는다.
      - 데이터를 추가하다가 배열 크기를 초과하게되면 에러가 발생한다.

### 직접 구현하는 배열 리스트2 - 동적 배열

- 배열의 크기를 넘어가야 하는 상황이라면 더 큰 배열을 만들어서 문제를 해결해보자.
- 배열의 크기를 넘어갈때는 기존 배열을 복사한 새로운 배열을 만들고 배열의 크기를 2배로 늘려준다.
  - 예제를 단순화 하기 위해 여기서는 2배씩 증가했지만, 보통 50% 정도 증가하는 방법을 사용한다.
  - 배열을 새로 복사해서 만드는 연산은 배열을 새로 만들고 또 기존 데이터를 복사하는 시간이 걸리므로 가능한 줄이는 것이 좋다.
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/array
    - `MyArrayListV2`, `MyArrayListV2Main` 참고
      - `Arrays.copyOf(기존배열, 새로운길이)` : 새로운 길이로 배열을 생성하고, 기존 배열의 값을 새로운 배열에 복사한다.

### 직접 구현하는 배열 리스트3 - 기능 추가

- `MyArrayList`에 다음 기능을 추가한다.
  - `add(index, 데이터)` : index 위치에 데이터를 추가한다.
  - `remove(index)` : index 위치의 데이터를 삭제한다.

- 데이터 추가 삭제 예시
  - 데이터 추가
    - 마지막에 추가 
      - 기존 데이터를 이동하지 않는다. `O(1)`
    - 앞에 추가
      - 입력한 위치를 기준으로 데이터를 오른쪽으로 한 칸씩 이동해야 한다. `O(n)`
  - 데이터 삭제
    - 마지막에 삭제
      - 기존 데이터를 이동할 필요가 없다. `O(1)`
    - 앞에 삭제
      - 삭제할 데이터의 위치를 기준으로 데이터를 한 칸씩 왼쪽으로 이동해야 한다. `O(n)`
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/array
    - `MyArrayListV3`, `MyArrayListV3Main`

- 지금까지 만든 자료 구조를 배열 리스트(`ArrayList`)라 한다.

### 직접 구현하는 배열 리스트4 - 제네릭1

- 기존 코드 문제점
  - 앞서 만든 `MyArrayList`들은 `Object`를 입력받기 때문에 아무 데이터나 입력할 수 있고, 또 결과로 `Object`를 반환한다. 
    - 따라서 필요한 경우 다운 캐스팅을 해야하고, 또 타입 안전성이 떨어지는 단점이 있다.
  - 참고로, 하나의 자료 구조에 서로 관계없는 여러 데이터 타입을 섞어서 보관하는 일은 거의 없다.
    - 일반적으로 같은 데이터 타입을 보관하고 관리한다.
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/array/MyArrayListV3BadMain.java

- 제네릭을 도입하면 이런 문제를 한번에 해결할 수 있다.
  - 소스 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/array
    - `MyArrayListV4`, `MyArrayListV4Main` 참고
    - 제네릭의 도움으로 타입 안전성이 높은 자료 구조를 만들 수 있었다.

### 직접 구현하는 배열 리스트5 - 제네릭2

- `Object` 배열을 사용한 이유
  - 제네릭은 런타임에 타입 이레이저에 의해 타입 정보가 사라진다. 따라서 런타임에 타입 정보가 필요한 생성자에 사용할 수 없다.
  - 즉, 생성자에는 제네릭의 타입 매개변수를 사용할 수 없다. (제네릭의 한계)
    - `new E[DEFAULT_CAPACITY]` : 사용 불가 (컴파일 오류 발생)
    - `new Object[DEFAULT_CAPACITY]` : 이걸로 대신 사용

- 이렇게 `Object[]`을 생성해서 사용해도 해도 문제가 없는지?
  - 문제 없다. 
  - 제네릭이 리스트의 데이터를 입력 받고 반환하는 곳의 타입을 고정해준다.
  - 따라서 고정된 타입으로 `Object` 배열에 데이터를 보관하고, 또 데이터를 꺼낼 때도 같은 고정된 타입으로 안전하게 다운 캐스팅 할 수 있다.

- `MyArrayList`의 단점
  - 정확한 크기를 미리 알지 못하면 메모리가 낭비된다. 배열을 사용하므로 배열 뒷 부분에 사용되지 않고, 낭비되는 메모리가 있다.
  - 데이터를 중간에 추가하거나 삭제할 때 비효율적이다.

- ArrayList(배열 리스트)의 빅오
    - 데이터 추가
        - 마지막에 추가: `O(1)`
        - 앞, 중간에 추가: `O(n)`
    - 데이터 삭제
        - 마지막에 삭제: `O(1)`
        - 앞, 중간에 삭제: `O(n)`
    - 인덱스 조회: `O(1)`
    - 데이터 검색: `O(n)`

- 정리
  - 배열 리스트는 순서대로 마지막에 데이터를 추가하거나 삭제할 때는 성능이 좋지만, 앞이나 중간에 데이터를 추가하거나 삭제할 때는 성능이 좋지 않다
  - 이런 단점을 해결한 자료 구조인 링크드 리스트(`LinkedList`)에 대해 알아보자.

---

## 5. 컬렉션 프레임워크 - LinkedList

### 노드와 연결1

- 배열 리스트의 단점
  - 사용하지 않는 공간 낭비
    - 배열은 필요한 배열의 크기를 미리 확보해야 한다. 데이터가 얼마나 추가될지 예측할 수 없는 경우 나머지는 공간은 사용되지 않고 낭비된다.
  - 배열의 중간에 데이터 추가
    - 앞이나 중간에 데이터를 추가하거나 삭제하는 경우 많은 데이터를 이동해야 하기 때문에 성능이 좋지 않다.

- 노드와 연결
  - 개요
    - 낭비되는 메모리 없이 딱 필요한 만큼만 메모리를 확보해서 사용하고,
    - 앞이나 중간에 데이터를 추가하거나 삭제할 때도 효율적인 자료 구조.
    - 노드를 만들고 각 노드를 서로 연결하는 방식.
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/link
    - `Node`, `NodeMain1` 참고
    - 노드 추가: 끝에 하나씩 추가
    - 노드 탐색: 반복문으로 일일히 탐색

### 노드와 연결2

- `toString()`
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/link
    - `Node`, `NodeMain2` 참고 
    - `Node`에 `toString()`을 IDE로 오버라이딩 했다가, 직접 구현함. (좀 더 가독성있게 출력하기 위해서.)

### 노드와 연결3

- 다양한 기능을 만들어보자.
  - 추가 기능
    - 모든 노드 탐색하기
    - 마지막 노드 조회하기
    - 특정 index의 노드 조회하기
    - 노드에 데이터 추가하기
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/link/NodeMain3.java
    - `NodeMain3` 참고

### 직접 구현하는 연결 리스트1 - 시작

- 연결 리스트(`LinkedList`)
  - 노드와 연결 구조를 이용한 리스트
  - 자료구조
  - 링크드 리스트, 연결 리스트라는 용어를 둘다 사용한다.

- 리스트 자료 구조
  - 배열 리스트도, 연결 리스트도 모두 같은 리스트이다.
  - 리스트의 내부에서 배열을 사용하는가 아니면 노드와 연결 구조를 사용하는가의 차이가 있을 뿐이다.
  - 리스트를 사용하는 개발자 입장에서는 거의 비슷하게 느껴져야 한다.

- 연결 리스트 직접 구현
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/link
    - `MyLinkedListV1`, `MyLinkedListV1Main` 참고

- 연결 리스트와 빅오
  - 특정 위치에 있는 데이터를 반환한다. `O(n)`
  - 마지막에 데이터를 추가한다. `O(n)`
  - 특정 위치에 있는 데이터를 찾아서 변경한다. 그리고 기존 값을 반환한다. `O(n)`
  - 데이터를 검색하고, 검색된 위치를 반환한다. `O(n)`

### 직접 구현하는 연결 리스트2 - 추가와 삭제1

- 특정 위치에 있는 데이터를 추가하고, 삭제하는 기능을 만들어보자.
  - 우선 설명만! 코드 작성은 그 밑에서!
  - 내용
    - 첫 번째 위치에 데이터 추가 / 삭제
    - 중간 위치에 데이터 추가 / 삭제

- 첫 번째 위치에 데이터 추가

  ![노드_첫 번째 위치에 데이터 추가](https://github.com/user-attachments/assets/7d0adb2f-87be-430a-bb98-e9d63bc85256)

  - 배열의 경우 첫 번째 항목에 데이터가 추가되면 모든 데이터를 오른쪽으로 하나씩 밀어야 하지만,
  - 연결 리스트는 새로 생성한 노드의 참조만 변경하면 된다. 
    - 나머지 노드는 어떤 일이 일어난지도 모른다.

- 첫 번째 위치의 데이터 삭제

  ![노드_첫 번째 위치의 데이터 삭제](https://github.com/user-attachments/assets/f94347fd-beba-4dc8-8989-f25e1b710b09)

- 중간 위치에 데이터 추가

  ![노드_중간 위치에 데이터 추가](https://github.com/user-attachments/assets/f7c16038-f431-475a-9d0e-33e0f931b376)

- 중간 위치의 데이터 삭제

    ![노드_중간 위치의 데이터 삭제](https://github.com/user-attachments/assets/d43f7818-e51b-4015-a5ca-ace4053f107a)

### 직접 구현하는 연결 리스트3 - 추가와 삭제2

- 바로 위에서 설명한 내용을 실제 코드로 구현함.
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/link
    - `MyLinkedListV2`, `MyLinkedListV2Main`

- 정리
  - 직접 만든 배열 리스트와 연결 리스트의 성능 비교 표

      | 기능        | 배열 리스트 | 연결 리스트 |
      |-----------|--------|--------|
      | 인덱스 조회    | `O(1)` | O(n)   |
      | 검색        | O(n)   | O(n)   |
      | 앞에 추가(삭제) | O(n)   | `O(1)` |
      | 뒤에 추가(삭제) | `O(1)` | O(n)   |
      | 평균 추가(삭제) | O(n)   | O(n)   |
  
  - `배열 리스트` vs `연결 리스트` 사용
    - 데이터를 조회할 일이 많고, 뒷 부분에 데이터를 추가한다면 `배열 리스트`가 보통 더 좋은 성능을 제공한다.
    - 앞쪽의 데이터를 추가하거나 삭제할 일이 많다면 `연결 리스트`를 사용하는 것이 보통 더 좋은 성능을 제공한다.

  - 참고 - `단일 연결 리스트`, `이중 연결 리스트`
    - 우리가 구현한 연결 리스트는 한 방향으로만 이동하는 `단일 연결 리스트`다.
    - 자바가 제공하는 연결 리스트는 `이중 연결 리스트`다.
      - 마지막 노드를 참조하는 변수를 가지고 있어서, 뒤에 추가하거나 삭제하는 삭제하는 경우에도 `O(1)`의 성능을 제공한다.

### 직접 구현하는 연결 리스트4 - 제네릭 도입

- 목표
  - 제네릭을 도입해서 타입 안전성을 높여보자.
  - `Node`를 중첩 클래스로 만들자.
    - 외부에서 사용되는 것이 아니라 연결 리스트 내부에서만 사용된다.
- ⭐ 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/link
  - `MyLinkedListV3`, `MyLinkedListV3Main` 참고

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
