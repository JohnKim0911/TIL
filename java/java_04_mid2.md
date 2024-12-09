# (복습) 김영한의 실전 자바 - 중급2편

|    | 제목                                                               | 복습일             |
|----|------------------------------------------------------------------|-----------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)                                        | 2024-12-03      |
| 2  | [제네릭 - Generic1](#2-제네릭---generic1)                              | 2024-12-03      |
| 3  | [제네릭 - Generic2](#3-제네릭---generic2)                              | 2024-12-04      |
| 4  | [컬렉션 프레임워크 - ArrayList](#4-컬렉션-프레임워크---arraylist)                | 2024-12-04 ~ 05 |
| 5  | [컬렉션 프레임워크 - LinkedList](#5-컬렉션-프레임워크---linkedlist)              | 2024-12-06      |
| 6  | [컬렉션 프레임워크 - List](#6-컬렉션-프레임워크---list)                          | 2024-12-07 ~ 09 |
| 7  | [컬렉션 프레임워크 - 해시(Hash)](#7-컬렉션-프레임워크---해시hash)                    | 2024-12-09      |
| 8  | [컬렉션 프레임워크 - HashSet](#8-컬렉션-프레임워크---hashset)                    | 2024-12-10      |
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

### 리스트 추상화1 - 인터페이스 도입

- 개요
  - 위 강의에서 작성했던 `MyArrayListV4`, `MyLinkedListV3`를 복사해서
  - 새로운 `MyArrayList`, `MyLinkedList`를 만들고, `MyList` 인터페이스를 구현하도록 함.

- 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/list
  - `MyList`, `MyArrayList`, `MyLinkedList` 참고

### 리스트 추상화2 - 의존관계 주입

- `MyArrayList`에서 데이터를 리스트 앞 부분에 추가 할 때 더 효율적인`MyLinkedList`로 변경하고자 함.
  - 구체적인 리스트에 의존하는 것을 추상적인 리스트에 의존하도록 변경
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/list
    - `BatchProcessor`, `BatchProcessorMain` 참고
  - 변경 전:
    - 구체적인 `MyArrayList`, `MyLinkedList`에 의존하는 `BatchProcessor` 예시
      - 구체적인 클래스에 직접 의존하면 `MyArrayList`를 `MyLinkedList`로 변경할 때 마다 여기에 의존하는 `BatchProcessor`의 코드도 함께 수정해야 한다.
  - 변경 후:
    - 추상적인 `MyList`에 의존하는 `BatchProcessor` 예시
      - `BatchProcessor`가 추상적인 `MyList` 인터페이스에 의존하는 방법
      - `BatchProcessor`를 생성하는 시점에 생성자를 통해 원하는 리스트 전략(알고리즘)을 선택해서 전달하면 된다.

      - `MyList`를 사용하는 클라이언트 코드인 `BatchProcessor`를 전혀 변경하지 않고, 원하는 리스트 전략을 런타임에 지정할 수 있다.
  - 정리
    - 다형성과 추상화를 활용하면 `BatchProcessor` 코드를 전혀 변경하지 않고 리스트 전략(알고리즘)을
      `MyArrayList`에서 `MyLinkedList` 로 변경할 수 있다.
    - 의존관계 주입 (Dependency Injection, DI)
      - 의존성 주입이라고도 부른다.
      - `BatchProcessor`의 외부에서 의존관계가 결정되어서 `BatchProcessor` 인스턴스에 들어오는 것 같다. 
      - 마치 의존관계가 외부에서 주입되는 것 같다고 해서 이것을 `의존관계 주입`이라 한다.
      - 생성자를 통해서 의존관계를 주입했기 때문에 `생성자 의존관계 주입`이라 한다.
    - `MyLinkedList`를 사용한 덕분에 `O(n)` -> `O(1)`로 훨씬 더 성능이 개선 되었다.

### 리스트 추상화3 - 컴파일 타임, 런타임 의존관계

- `컴파일 타임 의존관계` vs `런타임 의존관계`
  - `컴파일 타임 의존관계`
    - 자바 컴파일러가 보는 의존관계
    - 클래스에 바로 보이는 의존관계
    - 실행하지 않은 소스 코드에 정적으로 나타나는 의존관계
  - `런타임 의존관계`
    - 실제 프로그램이 작동할 때 보이는 의존관계
    - 주로 생성된 인스턴스와 그것을 참조하는 의존관계
    - 프로그램이 실행될 때 인스턴스 간에 의존관계
    - 런타임 의존관계는 프로그램 실행 중에 계속 변할 수 있다.

- 위 예제 다시 한번 설명
  - `BatchProcessor` 클래스는 구체적인 `MyArrayList`나 `MyLinkedList` 에 의존하는 것이 아니라 추상적인 `MyList` 에 의존한다.
    - 따라서 런타임에 `MyList` 의 구현체를 얼마든지 선택할 수 있다.
    - 클라이언트 코드의 변경 없이, 구현 알고리즘인 `MyList` 인터페이스의 구현을 자유롭게 확장할 수 있다.
    - 생성자를 통해 `런타임 의존관계`를 주입하는 것을 `생성자 의존관계 주입` 또는 줄여서 `생성자 주입`이라 한다.
  - `전략 패턴`(Strategy Pattern)
    - 디자인 패턴 중에 가장 중요한 패턴을 하나 뽑으라고 하면 `전략 패턴`을 뽑을 수 있다.
    - `전략 패턴`은 알고리즘을 클라이언트 코드의 변경 없이 쉽게 교체할 수 있다.
    - 방금 설명한 코드가 바로 `전략 패턴`을 사용한 코드이다.
      - `MyList` 인터페이스가 바로 전략을 정의하는 인터페이스가 되고,
      - 각각의 구현체인 `MyArrayList`, `MyLinkedList`가 전략의 구체적인 구현이 된다.
      - 그리고 전략을 클라이언트 코드(`BatchProcessor`)의 변경 없이 손쉽게 교체할 수 있다

### 직접 구현한 리스트의 성능 비교

- 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/list/MyListPerformanceTest.java

  - 직접 구현한 리스트의 성능 비교 표
    
    | 기능        | 배열 리스트          | 연결 리스트          |
    |-----------|-----------------|-----------------|
    | 앞에 추가(삭제) | O(n) - 1369ms   | `O(1)` - 2ms    |
    | 평균 추가(삭제) | O(n) - 651ms    | O(n) - 1112ms   |
    | 뒤에 추가(삭제) | `O(1)` - 2ms    | O(n) - 2195ms   |
    | 인덱스 조회    | `O(1)` - 1ms    | O(n) - 평균 438ms |
    | 검색        | O(n) - 평균 115ms | O(n) - 평균 492ms |

- 시간 복잡도와 실제 성능
  - 이론적으로 `MyLinkedList`의 평균 추가(중간 삽입) 연산은 `MyArrayList` 보다 빠를 수 있다고 생각 할 수 있지만, 실제 성능은 그렇지 않다.
  - 실제 성능은 요소의 순차적 접근 속도, 메모리 할당 및 해제 비용, CPU 캐시 활용도 등 다양한 요소에 의해 영향을 받는다.
    - `MyArrayList`는 요소들이 메모리 상에서 연속적으로 위치하여 CPU 캐시 효율이 좋고, 메모리 접근 속도가 빠르다.
    - 반면, `MyLinkedList`는 각 요소가 별도의 객체로 존재하고 다음 요소의 참조를 저장하기 때문에 CPU 캐시 효율이 떨어지고, 메모리 접근 속도가 상대적으로 느릴 수 있다.

### 자바 리스트

- 리스트와 관련된 컬렉션 프레임워크는 다음 구조를 가진다.
  - `Collection` 인터페이스는 `java.util` 패키지의 컬렉션 프레임워크의 핵심 인터페이스 중 하나이다.

![컬렉션 프레임워크 - 리스트](https://github.com/user-attachments/assets/03f383af-cdda-49e6-b49d-b2c090cafe2c)

- `List` 인터페이스의 주요 메서드
  - `add(E e)` ⭐: 리스트의 끝에 지정된 요소를 추가한다.
  - `add(int index, E element)` ⭐: 리스트의 지정된 위치에 요소를 삽입한다.
  - `addAll(Collection<? extends E> c)` ⭐: 지정된 컬렉션의 모든 요소를 리스트의 끝에 추가한다.
  - `addAll(int index, Collection<? extends E> c)` : 지정된 컬렉션의 모든 요소를 리스트의 지정된 위치에 추가한다.
  - `get(int index)` ⭐: 리스트에서 지정된 위치의 요소를 반환한다.
  - `set(int index, E element)` : 지정한 위치의 요소를 변경하고, 이전 요소를 반환한다.
  - `remove(int index)` : 리스트에서 지정된 위치의 요소를 제거하고 그 요소를 반환한다.
  - `remove(Object o)` : 리스트에서 지정된 첫 번째 요소를 제거한다.
  - `clear()` ⭐: 리스트에서 모든 요소를 제거한다.
  - `indexOf(Object o)`: 리스트에서 지정된 요소의 첫 번째 인덱스를 반환한다.
  - `lastIndexOf(Object o)` : 리스트에서 지정된 요소의 마지막 인덱스를 반환한다.
  - `contains(Object o)` ⭐: 리스트가 지정된 요소를 포함하고 있는지 여부를 반환한다.
  - `sort(Comparator<? super E> c)` : 리스트의 요소를 지정된 비교자에 따라 정렬한다.
  - `subList(int fromIndex, int toIndex)` : 리스트의 일부분의 뷰를 반환한다.
  - `size()` ⭐: 리스트의 요소 수를 반환한다.
  - `isEmpty()` ⭐: 리스트가 비어있는지 여부를 반환한다.
  - `iterator()` : 리스트의 요소에 대한 반복자를 반환한다.
  - `toArray()` : 리스트의 모든 요소를 배열로 반환한다.
  - `toArray(T[] a)` : 리스트의 모든 요소를 지정된 배열로 반환한다.

- 자바 `ArrayList`
  - `java.util.ArrayList` 
  - 자바가 제공하는 `ArrayList`는 우리가 직접 만든 `MyArrayList`와 거의 비슷하다.
  - 자바 `ArrayList`의 특징
    - 배열을 사용해서 데이터를 관리한다.
    - 기본 `CAPACITY`는 10이다.
      - `CAPACITY`를 넘어가면 배열을 50% 증가한다.
    - 메모리 고속 복사 연산을 사용한다.
      - 모든 요소를 한 칸씩 이동 해야할 때 사용.
      - 내부적으로 `System.arraycopy()`를 사용

- 자바 `LinkedList`
  - `java.util.LinkedList`
  - 자바가 제공하는 `LinkedList`는 우리가 직접 만든 `MyLinkedList`와 거의 비슷하다.
  - 자바의 `LinkedList` 특징
    - 이중 연결 리스트 구조
    - 첫 번째 노드와 마지막 노드 둘다 참조
    - 이전 노드로 이동할 수 있기 때문에, 마지막 노드부터 앞으로 조회할 수 있다.
    - 인덱스 조회 성능을 최적화 할 수 있다.
      - 인덱스로 조회하는 경우
        - 인덱스가 사이즈의 절반 이하라면 처음부터 찾아서 올라가고,
        - 인덱스가 사이즈의 절반을 넘으면 마지막 노드 부터 역방향으로 조회해서 성능을 최적화 할 수 있다.

    ![이중 연결 리스트](https://github.com/user-attachments/assets/775094ec-9b75-40d7-bb7f-5d87ed119cc4)

### 자바 리스트의 성능 비교

- 기존에 만들었던 `MyListPerformanceTest`를 복사해서 자바의 리스트를 사용하도록 일부 수정하였다.
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/list/JavaListPerformanceTest.java

- 성능 비교 표 (직접 구현한 리스트 vs 자바 리스트)
  - 직접 구현한 리스트

    | 기능        | 배열 리스트          | 연결 리스트          |
    |-----------|-----------------|-----------------|
    | 앞에 추가(삭제) | O(n) - 1369ms   | `O(1)` - 2ms    |
    | 평균 추가(삭제) | O(n) - 651ms    | O(n) - 1112ms   |
    | 뒤에 추가(삭제) | `O(1)` - 2ms    | O(n) - 2195ms   |
    | 인덱스 조회    | `O(1)` - 1ms    | O(n) - 평균 438ms |
    | 검색        | O(n) - 평균 115ms | O(n) - 평균 492ms |

  - 자바 리스트
  
    | 기능        | 배열 리스트           | 연결 리스트          |
    |-----------|------------------|-----------------|
    | 앞에 추가(삭제) | O(n) - 106ms ✔️  | `O(1)` - 2ms    |
    | 평균 추가(삭제) | O(n) - 49ms ✔️️️ | O(n) - 1116ms   |
    | 뒤에 추가(삭제) | `O(1)` - 1ms     | `O(1)` - 2ms ✔️ |
    | 인덱스 조회    | `O(1)` - 1ms     | O(n) - 평균 439ms |
    | 검색        | O(n) - 평균 104ms  | O(n) - 평균 473ms |

  - 데이터를 추가할 때 자바 `ArrayList`가 직접 구현한 `MyArrayList`보다 빠른 이유
    - 자바의 배열 리스트는 이때 메모리 고속 복사를 사용하기 때문에 성능이 최적화된다.
  - 자바 연결 리스트는 마지막 노드 정보도 가지고 있어서, 뒤에 추가(삭제) 성능이 좋다. 

- `배열 리스트` vs `연결 리스트`
    - 대부분의 경우 `배열 리스트`가 성능상 유리하다.
        - 이런 이유로 실무에서는 주로 `배열 리스트`를 기본으로 사용한다.
    - 만약 데이터를 앞쪽에서 자주 추가하거나 삭제할 일이 있다면 `연결 리스트`를 고려하자.

### 문제와 풀이1

- 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/list/test/ex1
- 문제1 - 배열을 리스트로 변경하기 : `ArrayEx1`를 참고하여 -> `ListEx1`를 새로 작성
- 문제2 - 리스트의 입력과 출력 : `ListEx2`
- 문제3 - 합계와 평균: `ListEx3`

### 문제와 풀이2

- 문제 - 리스트를 사용한 쇼핑 카트
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/list/test/ex2
  - `Item`, `ShoppingCartMain`를 참고하여 -> `ShoppingCart`를 새로 작성
  - 단순 배열 사용시와 리스트 사용시 코드 비교 분석: 교재 p.40 참고
    - 리스트의 이점
      - 배열처럼 입력 가능한 크기를 미리 정하지 않아도 된다.
      - 배열에 몇개의 데이터가 추가 되었는지 추척하는 변수를 제거할 수 있다.

---

## 7. 컬렉션 프레임워크 - 해시(Hash)

### 리스트(List) vs 세트(Set)


![리스트](https://github.com/user-attachments/assets/16e8c906-9f9e-4914-8536-c7ec77ed53db)

- List (리스트)
  - 특징
    - 순서 유지
    - 중복 허용
    - 인덱스 접근
  - 용도
    - 순서가 중요하거나, 중복된 요소를 허용해야 하는 경우 사용
  - 사용 예시
    - 장바구니 목록
    - 순서가 중요한 일련의 이벤트 목록

![셋](https://github.com/user-attachments/assets/0d4aeb73-f30e-4b8c-8716-907ed1ac2cd7)

- Set (세트, 셋)
  - 특징
    - 유일성
      - 요소를 추가할 때, 이미 존재하는 요소면 무시된다.
    - 순서 미보장
    - 빠른 검색
  - 용도
    - 중복을 허용하지 않고, 요소의 유무만 중요한 경우에 사용
  - 사용 예시
    - 회원 ID 집합
    - 고유한 항목의 집합

### 직접 구현하는 Set0 - 시작

- `Set` 직접 구현하기
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `MyHashSetV0`, `MyHashSetV0Main` 참고
      - 우선 배열에 데이터를 저장하도록 하였다.
      - 데이터 추가, 검색 모두 `O(n)`으로 성능이 좋지 않다.
        - 데이터를 추가할 때 셋에 중복 데이터가 있는지 전체 데이터를 항상 확인해야 한다.
  
  - 중복 데이터를 찾는 부분이 성능의 발목을 잡는다. 어떻게 개선할 수 있을까?
    - 해시로 해결 가능!

### 해시 알고리즘1 - 시작

- 해시(`hash`) 알고리즘을 사용하면, 데이터를 찾는 검색 성능을 평균 `O(1)`로 끌어올릴 수 있다.
- 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
  - `HashStart1` 참고
    - 하나의 배열에 값들을 저장하고, 반복문으로 일일히 값을 비교하여 일치하는 값을 찾는다.
      - 배열에서 특정 데이터를 찾는 성능은 `O(n)`으로 느리다.

### 해시 알고리즘2 - index 사용

- 배열은 인덱스의 위치를 사용해서 데이터를 찾을 때 `O(1)`로 매우 빠른 특징을 가지고 있다.
  - 데이터를 검색할 때도 인덱스를 활용해서 데이터를 한 번에 찾을 수 있다면?
    - `O(n)` -> `O(1)`로 검색 성능을 끌어올릴 수 있다.

- 어떻게?
  - 데이터의 값 자체를 배열의 인덱스와 맞추어 저장!

    ![데이터의 값과 배열의 인덱스를 맞추어 입력](https://github.com/user-attachments/assets/c77e53d5-3fb5-41f0-be60-b182dd8c30c2)

  - 이제 데이터가 인덱스 번호가 된다. 따라서 배열의 인덱스를 활용해서 단번에 필요한 데이터를 찾을 수 있다.

- 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `HashStart2` 참고
- 정리
  - 검색 성능을 `O(1)`로 획기적으로 개선할 수 있었다.
- 문제점
  - 배열에 낭비되는 공간이 많이 발생한다.

### 해시 알고리즘3 - 메모리 낭비

- 입력 값의 범위를 0~99로 넓혀보자.
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `HashStart3` 참고
      - 배열의 크기를 얼마 필요?
        - 0~99 까지 범위 입력
          - 사이즈 100의 배열필요: 4byte * 100 (단순히 값의 크기로만 계산)
        - `int` 범위 입력
          - `int` 범위: -2,147,483,648 ~ 2,147,483,647 (약 -21억 ~ 21억)
          - 약 42억 사이즈의 배열 필요 (+- 모두 포함)
          - 4byte * 42억 = **약 17GB** 필요 (단순히 값의 크기로만 계산)
- 입력할 수 있는 값의 범위가 `int` 라면, 한번의 연산에 최신 컴퓨터의 메모리가 거의 다 소모되어 버린다.
  - 뿐만 아니라 처음 배열을 생성하기 위해 메모리를 할당하는데도 너무 오랜 시간이 소모된다.

- 정리
  - 데이터의 값을 인덱스로 사용하는 방법은 매우 빠른 성능을 보장하지만, 
  - 입력 값의 범위가 조금만 커져도 메모리 낭비가 너무 심하다.
  - 따라서 그대로 사용하기에는 문제가 있다.

### 해시 알고리즘4 - 나머지 연산

- 나머지 연산을 사용하면 공간도 절약하면서, 넓은 범위의 값을 사용할 수 있다.
  - 예시)
      - 저장할 수 있는 배열의 크기(`CAPACITY`)를 10이라고 가정하자.
      - 그 크기에 맞추어 나머지 연산을 사용하면 된다.
        - 1 `%` 10 = 1 
        - 2 `%` 10 = 2 
        - 5 `%` 10 = 5 
        - 8 `%` 10 = 8 
        - 14 `%` 10 = 4 
        - 99 `%` 10 = 9
      - 나머지 연산의 결과는 절대로 배열의 크기를 넘지 않는다.
        - 결과는 0~9 까지만 나온다. 절대로 10이 되거나 10을 넘지 않는다.

- 해시 인덱스 (`hashIndex`)
  - 배열의 인덱스로 사용할 수 있도록 원래의 값을 계산한 인덱스
  - 예시)
    - 14의 해시 인덱스는 4
    - 99의 해시 인덱스는 9

- 해시 인덱스와 데이터 저장
  - 1, 2, 5, 8, 14 ,99의 값을 크기가 10인 배열에 저장해보자.

    ![해시 인덱스와 데이터 저장](https://github.com/user-attachments/assets/9f6ddf66-1341-4548-8c2e-5ca3d8d230ba)
    
    - 저장할 값에 나머지 연산자를 사용해서 해시 인덱스를 구한다.
      - 1 % 10 = 1
      - 2 % 10 = 2
      - 5 % 10 = 5
      - ...
    - 해시 인덱스를 배열의 인덱스로 사용해서 데이터를 저장한다.
      - 예시) `inputArray[hashIndex] = value`
    
- 해시 인덱스와 데이터 조회
  - 값 2, 14, 99 찾기

    ![해시 인덱스와 데이터 조회](https://github.com/user-attachments/assets/d0805cce-eec6-4ef7-bb2a-8daca4c0a90c)

    - 조회할 값에 나머지 연산자를 사용해서 해시 인덱스를 구한다.
      - 2 % 10 = 2 
      - 14 % 10 = 4 
      - 99 % 10 = 9
    - 해시 인덱스를 배열의 인덱스로 사용해서 데이터를 조회한다.
      - 예시) `int value = inputArray[hashIndex]`

- 코드로 구현
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `HashStart4` 참고

- 정리
  - 해시 인덱스를 사용해서 `O(1)`의 성능으로 데이터를 저장하고, 조회할 수 있게 되었다.

- 문제점
  - 해시 충돌
    - 같은 해시 인덱스가 존재 할 수 있다.
    - 예시)
      - 1 `%` 10 = 1 
      - 11 `%` 10 = 1
      - 9 `%` 10 = 9
      - 99 `%` 10 = 9

### 해시 알고리즘5 - 해시 충돌 설명

- 해시 충돌이 발생하면 어떤 문제?
  - 같은 해시 인덱스를 가진 값이 덮여쓰이게 된다.
    - 99 `%` 10 = 9
    - 9 `%` 10 = 9
    - 인덱스 9에 99가 저장되었다가, 9가 덮여 쓰이게됨.

  ![해시 충돌](https://github.com/user-attachments/assets/b63edf07-f6a6-4cc3-a8fb-ab2f2b61f6b5)

- 해시 충돌 해결
  - 해시 충돌이 일어났을 때, 같은 인덱스에 함께 저장한다. 대신에 배열 안에 배열을 만든다.

  ![해시 충돌과 저장](https://github.com/user-attachments/assets/70c54a8f-49ec-47aa-a8d3-7fb3f2f9f5bc)

- 최악의 경우

  ![최악의 경우](https://github.com/user-attachments/assets/a2a6d42e-88c5-4b0b-bb37-ebef5292ee87)

- 정리
  - 해시 인덱스를 사용하는 방식은 최악의 경우 `O(n)`의 성능을 보인다.
  - 하지만 평균으로 보면 대부분 `O(1)`의 성능을 제공한다.
  - 해시 충돌이 가끔 발생해도 내부에서 값을 몇 번만 비교하는 수준이기 때문에, 대부분의 경우 매우 빠르게 값을 찾을 수 있다.

### 해시 알고리즘6 - 해시 충돌 구현

- 해시 충돌 상황까지 고려해서 코드를 구현해보자.
  - 소스코드 (비공개 레포지토리) : https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `HashStart5` 참고
      - `LinkedList`는 하나의 바구니이다. 이런 바구니를 여러개 모아서 배열(`buckets`)을 선언했다. 
      - 바구니(`LinkedList`) 안에 실제 데이터가 들어가있다.

- 해시 인덱스 충돌 확률
  - 해시 충돌은 가급적 발생하지 않도록 해야 한다.
    - 발생하면 데이터를 추가하거나 조회할 때, 연결 리스트 내부에서 `O(n)`의 추가 연산을 해야 하므로 성능이 떨어진다.
  - 해시 충돌이 발생할 확률은 입력하는 데이터의 수와 배열의 크기와 관련이 있다.
    - 크기가 클 수록 충돌 확률은 낮아진다.
      - (구현한 코드에서 배열의 크기를 변경하면서 확인해봄.)
  - 통계적으로 입력한 데이터의 수가 배열의 크기를 `75%` 넘지 않으면 해시 인덱스는 자주 충돌하지 않는다.
    - 보통 `75%`를 기준으로 잡는 것이 효과적이다.
      - 예) 값이 75개면 길이가 100인 배열 준비.

- 정리
  - 해시 인덱스를 사용하는 경우
    - 데이터 저장
      - 평균: `O(1)`
      - 최악: `O(n)` //거의 발생하지 않는다.
    - 데이터 조회
      - 평균: `O(1)`
      - 최악: `O(n)` //거의 발생하지 않는다.
    - 배열의 크기만 적절하게 잡아주면, 대부분 `O(1)`에 가까운 매우 빠른 성능을 보여준다.

---

## 8. 컬렉션 프레임워크 - HashSet

### 직접 구현하는 Set1 - MyHashSetV1

- 성능이 느린 `MyHashSetV0`를 해시 알고리즘을 사용해서 평균 `O(1)`로 개선해보자.
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `MyHashSetV1`, `MyHashSetV1Main` 참고
- 남은 문제
  - 지금까지는 숫자 데이터를 저장할 때, 해당 숫자를 해시 인덱스로 사용하였다.
  - 그렇다면 문자 데이터를 기반으로 숫자 해시 인덱스를 구하려면 어떻게 해야 할까?

### 문자열 해시 코드

- 문자를 숫자로 변경하는 방법
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/set/StringHashMain.java
    - `StringHashMain` 참고
  - 모든 문자는 본인만의 고유한 숫자로 표현할 수 있다.
    - 예시) 
      - `'A'`; `65`
      - `'B'`: `66`
      - `"AB"` : 65 + 66 = `131`
  - ASCII 코드 표
    - 컴퓨터는 문자를 직접 이해하지는 못한다. 대신에 각 문자에 고유한 숫자를 할당해서 인식한다.
    - 모든 문자가 고유한 숫자를 가지고 있다.

- 해시 코드와 해시 인덱스
  - `hashCode()`라는 메서드를 통해서 문자를 기반으로 고유한 숫자(해시 코드)를 만들었다.

  ![해시 코드와 해시 인덱스](https://github.com/user-attachments/assets/008f6ea2-9e8b-42e2-a237-8f38e38d3feb)

- 용어 정리
  - `해시 함수`: 해시 코드를 생성하는 함수
  - `해시 코드`: 데이터를 대표하는 값
  - `해시 인덱스`: 해시 코드를 사용해서 데이터의 저장 위치를 결정하는 값

- 정리
  - 문자의 경우에도 해시 인덱스를 통해 빠르게 저장하고 조회할 수 있다.
    - 해시 함수를 사용해서 정수 기반의 해시 코드로 변환한 덕분.

- 세상의 어떤 객체든지 정수로 만든 해시 코드만 정의할 수 있다면 해시 인덱스를 사용할 수 있다.
  - 문자 뿐만 아니라 내가 직접 만든 `Member`, `User`와 같은 객체는 어떻게 해시 코드를 정의할 수 있을까?
  - 자바의 `hashCode()` 메서드에 대해 알아보자.

### 자바의 hashCode()

- `Object.hashCode()`
  - 자바는 모든 객체가 자신만의 해시 코드를 표현할 수 있는 기능을 제공한다.
  - 이 메서드를 그대로 사용하기 보다는 보통 재정의(오버라이딩)해서 사용한다.
    - 오버라이딩 하지 않으면, 객체의 참조값을 기반으로 해시 코드를 생성한다.
      - 즉, 객체의 인스턴스가 다르면 해시 코드도 다르다.

- 코드로 구현
  - 소스코드 (비공개 레포지토리): 
    - `Member`: https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/set/member/Member.java
    - `JavaHashCodeMain`: https://github.com/JohnKim0911/kyh-java-mid2/blob/master/src/collection/set/JavaHashCodeMain.java

- `Object`의 해시 코드 비교
  - `Object`가 기본으로 제공하는 `hashCode()`는 객체의 참조값을 해시 코드로 사용한다.
    - 따라서 각각의 인스턴스마다 서로 다른 값을 반환한다.

- 자바의 기본 클래스의 해시 코드
  - `Integer`, `String` 같은 자바의 기본 클래스들은 대부분 내부 값을 기반으로 해시 코드를 구할 수 있도록 `hashCode()` 메서드를 재정의해 두었다.
    - 따라서 데이터의 값이 같으면 같은 해시 코드를 반환한다.
  - 해시 코드의 경우 정수를 반환하기 때문에 마이너스 값이 나올 수 있다.

- 동일성과 동등성 복습
  - 동일성(Identity): `==` 연산자 사용. 두 객체의 참조가 동일한 객체를 가리키고 있는지 확인
  - 동등성(Equality): `equals()` 메서드 사용. 두 객체가 논리적으로 동등한지 확인

- 직접 구현하는 해시 코드
  - `Member`의 경우 회원의 `id`가 같으면 논리적으로 같은 회원으로 표현할 수 있다.
    - 따라서 회원 `id`를 기반으로 동등성을 비교하도록 `equals`를 재정의해야 한다.
    - 따라서 회원 `id`를 기반으로 해시 코드를 생성해야 한다.

- 정리
  - 자바가 기본으로 제공하는 클래스 대부분은 `hashCode()`를 재정의해두었다.
  - 객체를 직접 만들어야 하는 경우에 `hashCode()`를 재정의하면 된다.

### 직접 구현하는 Set2 - MyHashSetV2

- `MyHashSetV1`은 `Integer` 숫자만 저장할 수 있었다. 모든 타입을 저장할 수 있는 `Set`을 만들어보자.
  - 기존 제네릭을 `Integer`에서 `Object`로 변경.
  - 소스코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh-java-mid2/tree/master/src/collection/set
    - `MyHashSetV2`, `MyHashSetV2Main1` 참고

---

## 9. 컬렉션 프레임워크 - Set

---

## 10. 컬렉션 프레임워크 - Map, Stack, Queue

---

## 11. 컬렉션 프레임워크 - 순회, 정렬, 전체 정리

---

## 12. 다음으로

---
