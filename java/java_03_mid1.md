# (복습) 김영한의 실전 자바 - 중급 1편

|    | 제목                                   | 복습일        |
|----|--------------------------------------|------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)            | 2024-11-24 |
| 2  | [Object 클래스](#2-object-클래스)          | 2024-11-24 |
| 3  | [불변 객체](#3-불변-객체)                    |            |
| 4  | [String 클래스](#4-string-클래스)          |            |
| 5  | [래퍼, Class 클래스](#5-래퍼-class-클래스)     |            |
| 6  | [열거형 - ENUM](#6-열거형---enum)          |            |
| 7  | [날짜와 시간](#7-날짜와-시간)                  |            |
| 8  | [중첩 클래스, 내부 클래스1](#8-중첩-클래스-내부-클래스1) |            |
| 9  | [중첩 클래스, 내부 클래스2](#9-중첩-클래스-내부-클래스2) |            |
| 10 | [예외 처리1 - 이론](#10-예외-처리1---이론)       |            |
| 11 | [예외 처리2 - 실습](#11-예외-처리2---실습)       |            |
| 12 | [다음으로](#12-다음으로)                     |            |

---

## 1. 강의 소개와 자료

![강의소개](https://github.com/user-attachments/assets/9c5f142f-03be-4d03-b94d-95d9745eb9f4)

- 실제 강의:
    - https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-1

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
    - 유료 강의이므로, 실제 작성한 전체 코드는 비공개 합니다. (저작권...)

- 비공개 레포지토리:
    - https://github.com/JohnKim0911/kyh_java-mid1
        - 링크가 있긴하지만, 저만 볼 수 있습니다.
        - (강의 들으면서 직접 작성한 코드를 보관)

---

## 2. Object 클래스

### java.lang 패키지 소개
- 자바가 기본으로 제공하는 라이브러리 중에 가장 기본이 되는 패키지.
  - 라이브러리: 클래스 모음
  - `lang`: Language

- `java.lang` 패키지의 대표적인 클래스들
  - `Object` : 모든 자바 객체의 부모 클래스
  - `String` : 문자열
  - `Integer`, `Long`, `Double` : 래퍼 타입, 기본형 데이터 타입을 객체로 만든 것
  - `Class` : 클래스 메타 정보
  - `System` : 시스템과 관련된 기본 기능들을 제공
  - 여기 나열한 클래스들은 자바 언어의 기본을 이루기 때문에 반드시 잘 알아두어야 한다.

- `import` 생략 가능
  - `java.lang` 패키지는 모든 자바 애플리케이션에 자동으로 임포트(`import`)된다.
    - 예시) `System.out.println()`는 `import java.lang.System;`가 필요하지만, 안해줘도 자동으로 된다.

### Object 클래스

- 자바에서 모든 클래스의 최상위 부모 클래스는 항상 `Object` 클래스이다.
  - 클래스에 상속 받을 부모 클래스가 없으면, 묵시적으로 `Object` 클래스를 상속 받는다.
    - 자바가 `extends Object` 코드를 넣어준다. 따라서 생략을 권장한다.
  - 묵시적(Implicit) vs 명시적(Explicit)
      - 묵시적: 개발자가 코드에 직접 기술하지 않아도 시스템 또는 컴파일러에 의해 자동으로 수행되는 것
      - 명시적: 개발자가 코드에 직접 기술하는 것

![Object 클래스](https://github.com/user-attachments/assets/e6c17df7-a22f-4027-86ac-f1c949975518)

![Object 클래스_메모리구조](https://github.com/user-attachments/assets/6671cc77-bc8f-4041-ad1f-51da37291c75)

- 모든 클래스가 `Object` 클래스를 상속 받는 이유
  - **공통 기능 제공**
    - 객체의 정보를 제공하고, 이 객체가 다른 객체와 같은지 비교하고, 객체가 어떤 클래스로 만들어졌는지 확인하는 기능은 모든 객체에게 필요한 기본 기능이다.
      - 이런 기능을 객체를 만들 때 마다 항상 새로운 메서드를 정의해서 만들어야 한다면 상당히 번거로울 것이다.
      - 막상 만든다고 해도 개발자마다 서로 다른 이름의 메서드를 만들어서 일관성이 없을 것이다.
    - `Object`는 모든 객체에 필요한 공통 기능을 제공한다.
      -  `Object`는 최상위 부모 클래스이기 때문에 모든 객체는 공통 기능을 편리하게 제공(상속) 받을 수 있다.
      - `Object`가 제공하는 기능
        - 객체의 정보를 제공하는 `toString()`
        - 객체의 같음을 비교하는 `equals()`
        - 객체의 클래스 정보를 제공하는 `getClass()`
        - 기타 여러가지 기능
  - **다형성의 기본 구현**
    - 부모는 자식을 담을 수 있다. `Object`는 모든 클래스의 부모 클래스이다.
    - `Object`는 모든 객체를 다 담을 수 있다. 타입이 다른 객체들을 `Object`에 보관할 수 있다.

### Object 다형성

- `Dog` 와 `Car`와 같이, 서로 아무런 관련이 없는 클래스를 한 곳에 담으려면?
  - 둘다 부모가 없으므로 `Object`를 자동으로 상속 받는다. `Object`를 활용하자.

![Object 다형성](https://github.com/user-attachments/assets/2b3e9f7e-9ef3-4740-b3a1-f11883866957)

```java
package lang.object.poly;

public class Dog {
    public void sound() {
        System.out.println("멍멍");
    }
}
```

```java
package lang.object.poly;

public class Car {
    public void move() {
        System.out.println("자동차 이동");
    }
}
```

```java
package lang.object.poly;

public class ObjectPolyExample1 {

    public static void main(String[] args) {
        Dog dog = new Dog();
        Car car = new Car();

        action(dog);
        action(car);
    }

    private static void action(Object obj) {
        //obj.sound(); //컴파일 오류, Object는 sound()가 없다.
        //obj.move(); //컴파일 오류, Object는 move()가 없다.

        //객체에 맞는 다운캐스팅 필요
        if (obj instanceof Dog dog) {
            dog.sound();
        } else if (obj instanceof Car car) {
            car.move();
        }
    }
}
```

- Object 다형성의 한계
    - `Object`를 통해 전달 받은 객체를 호출하려면 각 객체에 맞는 다운캐스팅 과정이 필요하다.

![다형성의 한계](https://github.com/user-attachments/assets/db67e7de-d6f6-4706-811b-be9c9928f298)

![다형성의 한계2](https://github.com/user-attachments/assets/7602453b-9c5c-4a79-9945-14d320299d15)

### Object 배열

- `Object`타입을 사용하면 세상의 모든 객체를 담을 수 있는 배열을 만들 수 있다. (`Object[]`)

```java
package lang.object.poly;

public class ObjectPolyExample2 {

    public static void main(String[] args) {
        Dog dog = new Dog();
        Car car = new Car();
        Object object = new Object(); //Object 인스턴스도 만들 수 있다.

        Object[] objects = {dog, car, object};

        size(objects);
    }

    private static void size(Object[] objects) {
        System.out.println("전달된 객체의 수는: " + objects.length);
    }
}
```

![Object 배열](https://github.com/user-attachments/assets/931ccda1-bd7d-4a7c-b307-d8fc145afdfe)

### toString()

- `Object.toString()` 메서드는 객체의 정보를 문자열 형태로 제공한다.
  - 디버깅과 로깅에 유용하게 사용된다.
  - Object 클래스에 정의되므로 모든 클래스에서 상속받아 사용할 수 있다.
- `System.out.println()` 메서드는 내부에서 `toString()`을 호출한다.
- `toString()` 오버라이딩
  - `Object.toString()` 메서드가 클래스 정보와 참조값을 제공하지만, 이 정보만으로는 객체의 상태를 적절히 나타내지 못한다. 
  - 보통 `toString()` 을 재정의(오버라이딩)해서 보다 유용한 정보를 제공하는 것이 일반적이다.

```java
package lang.object.tostring;

public class Dog {

    private String dogName;
    private int age;

    public Dog(String dogName, int age) {
        this.dogName = dogName;
        this.age = age;
    }

    @Override
    public String toString() { //IDE의 도움을 받아서 작성하는 것이 매우 편리하다.
        return "Dog{" +
                "dogName='" + dogName + '\'' +
                ", age=" + age +
                '}';
    }
}
```

### Object와 OCP

```java
public class ObjectPrinter {
    public static void print(Object obj) {
        String string = "객체 정보 출력: " + obj.toString();
        System.out.println(string);
    }
}
```

- `ObjectPrinter`는 구체적인 `Car`, `Dog`에 의존하는 것이 아니라, 추상적인 `Object`에 의존하면서 OCP 원칙을 지킬 수 있다.
- OCP 원칙
  - **Open** (확장에 열려있다): 
    - 새로운 클래스를 추가하고, `toString()`을 오버라이딩해서 기능을 확장할 수 있다.
  - **Closed** (기존코드 변경에 닫혀있다): 
    - 새로운 클래스를 추가해도 `Object`와 `toString()`을 사용하는 클라이언트 코드인 `ObjectPrinter`는 변경하지 않아도 된다.

![ObjectPrinter](https://github.com/user-attachments/assets/3179c41a-fc6b-4a56-8f8d-fb9d5d149053)

- System.out.println()
  - `ObjectPrinter.print()`는 사실 `System.out.println()`의 작동 방식을 설명하기 위해 만든 것이다.

![sout](https://github.com/user-attachments/assets/f6236b44-0b7f-479e-91f2-9016e9029c6a)

- 자바 언어는 객체지향 언어 답게 언어 스스로도 객체지향의 특징을 매우 잘 활용한다.
- 참고) 정적 의존관계 vs 동적 의존관계
  - 정적 의존관계
    - **컴파일** 시간에 결정되며, 주로 클래스 간의 관계를 의미한다.
    - 앞서 보여준 클래스 의존 관계 그림이 바로 정적 의존관계이다.
    - 프로그램을 실행하지 않고, 클래스 내에서 사용하는 타입들만 보면 쉽게 의존관계를 파악할 수 있다.
  - 동적 의존관계
    - 프로그램을 실행하는 **런타임**에 확인할 수 있는 의존관계이다.
    - 앞서 `ObjectPrinter.print(Object obj)`에 인자로 어떤 객체가 전달 될 지는 프로그램을 실행해봐야 알 수 있다.
      - 어떤 경우에는 `Car` 인스턴스가 넘어오고, 어떤 경우에는 `Dog` 인스턴스가 넘어온다.
      - 이렇게 런타임에 어떤 인스턴스를 사용하는지를 나타내는 것이 동적 의존관계이다.

### equals()

- `Object`는 동등성 비교를 위한 `equals()` 메서드를 제공한다.
- 자바는 두 객체가 같다라는 표현을 2가지로 분리해서 제공한다.
  - 동일성 (Identity)
    - **물리적**으로 같은 메모리에 있는 객체 인스턴스인지 참조값을 확인하는 것
    - `==` 연산자를 사용
  - 동등성 (Equality)
    - **논리적**으로 같은지 확인하는 것
    - `equals()` 메서드를 사용
  - 예시)
    - `User a = new User("id-100")` //참조 x001
    - `User b = new User("id-100")` //참조 x002
      - id 값은 같지만, 실제 인스턴스는 다른 참조값을 가르키고 있는 경우 
        - 물리적으로 다른 메모리에 있는 다른 객체
        - 회원 번호를 기준으로 생각해보면 논리적으로는 같은 회원 (주민등록번호가 같다고 가정해도 된다.)
- `Object`가 기본으로 제공하는 `equals()`는 내부적으로 `==`으로 비교를 한다.
    - 논리적으로 같은지 비교 하고 싶으면, `equals()` 메서드를 재정의해서 사용해야 한다.

```java
package lang.object.equals;

import java.util.Objects;

public class UserV2 {

    private String id;

    public UserV2(String id) {
        this.id = id;
    }

/*
    // 이해를 돕기 위해 간단히 작성한 버전.
    @Override
    public boolean equals(Object obj) {
        UserV2 user = (UserV2) obj;
        return id.equals(user.id);
    }
*/

    // 더 정확한 equals() 메서드. IDE를 통해 생성하자.
    @Override
    public boolean equals(Object object) {
        if (object == null || getClass() != object.getClass()) return false;

        UserV2 userV2 = (UserV2) object;
        return id.equals(userV2.id);
    }

}
```

```java
package lang.object.equals;

public class EqualsMainV2 {

    public static void main(String[] args) {
        UserV2 user1 = new UserV2("id-100");
        UserV2 user2 = new UserV2("id-100");

        System.out.println("identity = " + (user1 == user2)); //false
        System.out.println("equality = " + (user1.equals(user2))); //true
    }
}
```

- `equals()` 메서드를 구현할 때 지켜야 하는 규칙
  - 외우기 보다는 대략 이렇구나 정도로 한번 읽어보고 넘어가면 충분하다. (필요하면 실제 교제 참고!)
  - 실무에서는 대부분 IDE가 만들어주는 `equals()`를 사용한다.

### 문제와 풀이

- Rectangle 클래스를 만들어라.
  - 넓이, 높이가 같으면 동등성 비교에 성공해야 한다.
  - (소스 코드는 비공개. 저작권 문제!)

### 정리

- Object의 나머지 메서드
  - `clone()` :  객체를 복사할 때 사용한다. 잘 사용하지 않으므로 다루지 않는다.
  - `hashCode()` : 뒤에 컬렉션 프레임워크에서 설명한다. `equals()`와 `hashCode()`는 보통 함께 사용된다.
  - `getClass()` : 뒤에 `Class`에서 설명한다
  - `notify()`, `notifyAll()`, `wait()` : 멀티쓰레드용 메서드이다. 멀티쓰레드에서 다룬다.

---

## 3. 불변 객체

---

## 4. String 클래스

---

## 5. 래퍼, Class 클래스

---

## 6. 열거형 - ENUM

---

## 7. 날짜와 시간

---

## 8. 중첩 클래스, 내부 클래스1

---

## 9. 중첩 클래스, 내부 클래스2

---

## 10. 예외 처리1 - 이론

---

## 11. 예외 처리2 - 실습

---

## 12. 다음으로

---