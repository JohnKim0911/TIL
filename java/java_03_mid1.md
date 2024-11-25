# (복습) 김영한의 실전 자바 - 중급 1편

|    | 제목                                   | 복습일        |
|----|--------------------------------------|------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)            | 2024-11-24 |
| 2  | [Object 클래스](#2-object-클래스)          | 2024-11-24 |
| 3  | [불변 객체](#3-불변-객체)                    | 2024-11-25 |
| 4  | [String 클래스](#4-string-클래스)          | 2024-11-25 |
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

- 실제 강의:
    - https://www.inflearn.com/course/%EA%B9%80%EC%98%81%ED%95%9C%EC%9D%98-%EC%8B%A4%EC%A0%84-%EC%9E%90%EB%B0%94-%EC%A4%91%EA%B8%89-1

- 아래 내용은...
    - 강의 내용을 개인적으로 복습하고자 정리하였습니다.
    - 유료 강의이므로, 실제 작성한 전체 코드는 비공개 합니다. (저작권...)
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1
        - 링크가 있긴하지만, 저만 볼 수 있습니다. (404 error 뜨는게 정상)

- 강의 구성

![강의소개](https://github.com/user-attachments/assets/9c5f142f-03be-4d03-b94d-95d9745eb9f4)


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

### 기본형과 참조형의 공유

- 자바 데이터 타입
    - 기본형(Primitive Type)
        - 하나의 값을 여러 변수에서 절대로 공유하지 않는다.
        - a를 바꾸면, a만 바뀐다. b는 바뀌지 않는다.
    - 참조형(Reference Type)
        - 하나의 객체를 참조값을 통해 여러 변수에서 공유할 수 있다.
        - a를 바꾸면, b도 바뀐다.

- 공유 참조와 사이드 이펙트
    - a만 바꾸려고 했는데, 원치 않았던 b도 바뀌어 버림.
        - 해결 방안
            - 처음부터 다른 인스턴스를 선언하면 된다.
    - 참조값의 공유를 막을 수 있는 방법이 없다.
       ```java
       Address a = new Address("서울");
       Address b = a; //참조값 대입을 막을 수 있는 방법이 없다.
       ```
    - 문제의 직접적인 원인은 공유된 객체의 값을 변경한 것에 있다.
        - `b.setValue("부산");` //b의 값을 부산으로 변경
        - 만약 `Address`객체의 값을 변경하지 못하게 설계했다면 이런 사이드 이펙트 자체가 발생하지 않을 것이다.
            - **불변**이라는 단순한 제약을 사용해서 사이드 이펙트라는 큰 문제를 막을 수 있다.


### 불변 객체

- 불변 객체 (Immutable Object)
    - 객체의 상태(객체 내부의 값, 필드, 멤버 변수)가 변하지 않는 객체
    - 불변 클래스를 만드는 방법
        - 어떻게든 필드 값을 변경할 수 없게 클래스를 설계하면 된다.
            - 내부 값이 변경되면 안된다. 따라서 `value`의 필드를 `final`로 선언했다.
            - 값을 변경할 수 있는 `setValue()`를 제거했다.

```java
package lang.immutable.address;

public class ImmutableAddress {

    private final String value; //final로 선언!

    public ImmutableAddress(String value) {
        this.value = value;
    }

    public String getValue() {
        return value;
    }

    //setValue(); 삭제!

    @Override
    public String toString() {
        return "Address{" +
                "value='" + value + '\'' +
                '}';
    }
}
```

```java
package lang.immutable.address;

public class RefMain2 {

    public static void main(String[] args) {
        ImmutableAddress a = new ImmutableAddress("서울");
        ImmutableAddress b = a; //참조값 대입을 막을 수 있는 방법이 없다.
        System.out.println("a = " + a); //서울
        System.out.println("b = " + b); //서울

        //b의 값을 부산으로 변경
        //b.setValue("부산"); //컴파일 오류 발생
        b = new ImmutableAddress("부산"); //개발자가 값을 변경할 수 없음을 알게되고, 새로운 인스턴스를 생성함.
        System.out.println("부산 -> b");
        System.out.println("a = " + a); //서울
        System.out.println("b = " + b); //부산
    }
}
```

![불변객체 예제_1](https://github.com/user-attachments/assets/0d4da1e9-7243-4343-931f-daa9c687add4)

![불변객체 예제_2](https://github.com/user-attachments/assets/ad7cea4a-a50b-4605-af32-621917c46bd8)


### 불변 객체 - 값 변경

- 불변 객체를 사용하지만 그래도 값을 변경해야 하는 메서드가 필요하다면?
    - 기존 값은 변경하지 않고, 대신에 계산 결과를 바탕으로 새로운 객체를 만들어서 반환한다.
    - 이렇게 하면 불변도 유지하면서 새로운 결과도 만들 수 있다.

```java
package lang.immutable.change;

public class ImmutableObj {

    private final int value;

    public ImmutableObj(int value) {
        this.value = value;
    }

    public ImmutableObj add(int addValue) { //기존 값은 변경하지 않고, 계산 결과를 바탕으로 새로운 객체를 만들어서 반환한다.
        int result = value + addValue;
        return new ImmutableObj(result);
    }

    public int getValue() {
        return value;
    }
}
```

```java
package lang.immutable.change;

public class ImmutableMain1 {

    public static void main(String[] args) {
        ImmutableObj obj1 = new ImmutableObj(10);
        ImmutableObj obj2 = obj1.add(20);

        //계산 이후에도 기존값과 신규값 모두 확인 가능
        System.out.println("obj1 = " + obj1.getValue()); //10
        System.out.println("obj2 = " + obj2.getValue()); //30
    }
}
```

![불변객체_값 변경](https://github.com/user-attachments/assets/1f4486ee-fcdd-4820-9ea8-3cc3767056bd)

- 불변 객체에서 변경과 관련된 메서드들은 보통 객체를 새로 만들어서 반환하기 때문에 꼭! 반환 값을 받아야 한다.
    - 새로 생성된 반환 값을 사용하지 않으면, 아무것도 처리되지 않은 것 처럼 보인다.

### 문제와 풀이

- 가변 클래스를 불변 클래스로 만드는 문제
    - 불변 객체에서 값을 변경하는 경우 `withYear()` 처럼 "`with`"로 시작하는 경우가 많다.
    - `setYear()`, `setMonth()`, `setDay()`로 원하는 날짜만 바꾸는 가변 클래스
        - 불변 클래스에서는 `setXXX()`가 아닌, `withXXX()`를 사용 (관례)

```java
package lang.immutable.test;

public class ImmutableMyDate {

    private final int year;
    private final int month;
    private final int day;

    public ImmutableMyDate(int year, int month, int day) {
        this.year = year;
        this.month = month;
        this.day = day;
    }

    public ImmutableMyDate withYear(int newYear) { //withXXX()
        return new ImmutableMyDate(newYear, month, day);
    }
    
    // 일부 생략
}
```

### 정리

- 불변 객체 예시
  - String 클래스
  - Integer, LocalDate 등
- **모든 클래스를 불변으로 만드는 것은 아니다.**
  - 가변 클래스가 더 일반적이고, 불변 클래스는 값을 변경하면 안되는 특별한 경우에 만들어서 사용한다고 생각하면 된다.
- 클래스를 불변으로 설계하는 이유는 더 많다.
  - 캐시 안정성
  - 멀티 쓰레드 안정성
  - 엔티티의 값 타입
  - 지금은 불변 클래스의 원리만 이해해도 충분하다. 이런건 나중에 배운다.

---

## 4. String 클래스

## String 클래스 - 기본

- 자바에서 문자를 다루는 타입은 `char`, `String`.
  - `char`를 사용해서 여러 문자를 나열하려면 `char[]`을 사용해야 한다.
  - `char[]`을 직접 다루는 방법은 매우 불편하다.
  - 자바는 문자열을 매우 편리하게 다룰 수 있는 `String` 클래스를 제공한다.

- `String` 클래스를 통해 문자열을 생성하는 방법은 2가지가 있다.
  - `String str1 = "hello";`
    - 문자열은 매우 자주 사용된다. 그래서 편의상 `str1`과 같이 입력하면, 자바에서 `str2`처럼 변경해준다.
      - 이 경우 실제로는 성능 최적화를 위해 문자열 풀을 사용하는데, 이 부분은 뒤에서 설명한다.
  - `String str2 = new String("hello");`

- `String` 클래스 구조
  - 다루기 불편한 `char[]`을 내부에 감추고,
  - 문자열을 다룰 수 있도록 다양한 기능을 제공한다.

```java
public final class String {
    
    //문자열 보관
    //private final char[] value;// 자바 9 이전
    private final byte[] value;// 자바 9 이후
    
    //여러 메서드
    public String concat(String str) {...}
    public int length() {...}
    
    //생략
}
```

- 참고: 자바 9 이후 `String` 클래스 변경 사항
  - 자바에서 문자 하나를 표현하는 `char`는 `2byte`를 차지한다.
  - `String` 클래스 변경 사항
    - 자바 9 이전
      - `char[]` 사용
      - 모든 문자에 `2byte` 사용
    - 자바 9 이후
      - `byte[]` 사용
      - 단순 영어, 숫자로만 표현된 경우 `1byte`를 사용하고
      - 그렇지 않은 경우, `2byte`를 사용한다.

- String 클래스와 참조형
    - `String`은 클래스이고, 참조형이다.
      - 원칙적으로 `+` 같은 연산을 사용할 수 없다.
      - 하지만 문자열은 너무 자주 다루어지기 때문에 자바 언어에서 편의상 특별히 `+` 연산을 제공한다.

### String 클래스 - 비교

- `String` 클래스 비교할 때는 `==` 비교가 아니라 항상 `equals()` 비교를 해야한다.


```java
package lang.string.equals;

public class StringEqualsMain1 {

    public static void main(String[] args) {
        String str1 = new String("hello"); //x001
        String str2 = new String("hello"); //x002
        System.out.println("new String() == 비교: " + (str1 == str2)); //false
        System.out.println("new String() equals 비교: " + (str1.equals(str2))); //true

        String str3 = "hello"; //x003 //문자열 리터럴 -> 문자열 풀 사용
        String str4 = "hello"; //x003
        System.out.println("리터럴 == 비교: " + (str3 == str4)); //true
        System.out.println("리터럴 equals 비교: " + (str3.equals(str4))); //true
    }
}
```

![문자열 풀](https://github.com/user-attachments/assets/7fa09ce8-804d-4ce5-9216-98dcac5ebea4)

- 문자열 풀 (String Pool)
  - 문자열 리터럴을 사용하는 경우, 자바는 메모리 효율성과 성능 최적화를 위해 문자열 풀을 사용한다.
      - 자바가 실행되는 시점에 문자열 풀에 `String` 인스턴스를 미리 만들어둔다.
      - 같은 문자열이 이미 있으면 만들지 않는다.
    - 같은 문자를 사용하는 경우, 메모리 사용을 줄이고 문자를 만드는 시간도 줄어들기 때문에 성능도 최적화 할 수 있다.
  - 문자열 리터럴을 사용하는 경우, 같은 참조값을 가지므로 `==` 비교에 성공한다.
    - 하지만, `String` 인스턴스를 받는 쪽이 `new String()`으로 만들어진건지 문자열 리터럴로 만들어진것지 확인 할 수 있는 방법이 없다.
    - 따라서 항상 `equals()`를 사용해서 동등성 비교를 해야한다.

### String 클래스 - 불변 객체

- `String`은 불변 객체이다.
  - 생성 이후에 절대로 내부의 문자열 값을 변경할 수 없다.
  - `String.concat()`은 내부에서 새로운 `String` 객체를 만들어서 반환한다.

- `String`이 불변으로 설계된 이유
  - `String`은 자바 내부에서 문자열 풀을 통해 최적화를 한다.
    - 만약 `String` 내부의 값을 변경할 수 있다면, 기존에 문자열 풀에서 같은 문자를 참조하는 변수의 모든 문자가 함께 변경되어 버리는 문제가 발생한다.
    - `String` 클래스는 불변으로 설계되어서 이런 사이드 이펙트 문제가 발생하지 않는다.

### String 클래스 - 주요 메서드

- 외우지 말자. 이런게 있구나 대략 보고, 나중에 필요할때 찾아보자.

- 주요 메서드 목록
  - 아래 메서드들의 예제 코드들은 비공개. (저작권)
    - 비공개 레포지토리에서 나만 볼 수 있다...
  - 문자열 정보 조회
    - `length()` : 문자열의 길이를 반환한다. 
    - `isEmpty()` : 문자열이 비어 있는지 확인한다. (길이가 0)
    - `isBlank()` : 문자열이 비어 있는지 확인한다. (길이가 0이거나 공백(Whitespace)만 있는 경우), 자바 11 
    - `charAt(int index)` : 지정된 인덱스에 있는 문자를 반환한다.
    -  비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringInfoMain.java
  - 문자열 비교
    - `equals(Object anObject)` : 두 문자열이 동일한지 비교한다. 
    - `equalsIgnoreCase(String anotherString)` : 두 문자열을 대소문자 구분 없이 비교한다. 
    - `compareTo(String anotherString)` : 두 문자열을 사전 순으로 비교한다. 
    - `compareToIgnoreCase(String str)` : 두 문자열을 대소문자 구분 없이 사전적으로 비교한다. 
    - `startsWith(String prefix)` : 문자열이 특정 접두사로 시작하는지 확인한다. 
    - `endsWith(String suffix)` : 문자열이 특정 접미사로 끝나는지 확인한다.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringComparisonMain.java
  - 문자열 검색
    - `contains(CharSequence s)` : 문자열이 특정 문자열을 포함하고 있는지 확인한다. 
      - 참고: `CharSequence` 는 `String`, `StringBuilder` 의 상위 타입이다.
    - `indexOf(String ch)` / `indexOf(String ch, int fromIndex)` : 문자열이 처음 등장하는 위치를 반환한다. 
    - `lastIndexOf(String ch)` : 문자열이 마지막으로 등장하는 위치를 반환한다.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringSearchMain.java
  - 문자열 조작 및 변환
    - `substring(int beginIndex)` / `substring(int beginIndex, int endIndex)` : 문자열의 부분 문자열을 반환한다. 
    - `concat(String str)` : 문자열의 끝에 다른 문자열을 붙인다. 
    - `replace(CharSequence target, CharSequence replacement)` : 특정 문자열을 새 문자열로 대체한다. 
    - `replaceAll(String regex, String replacement)` : 문자열에서 정규 표현식과 일치하는 부분을 새 문자열로 대체한다. 
    - `replaceFirst(String regex, String replacement)` : 문자열에서 정규 표현식과 일치하는 첫 번째 부분을 새 문자열로 대체한다. 
    - 비공개 레포지토리1: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringUtilsMain1.java
    - `toLowerCase()` / `toUpperCase()` : 문자열을 소문자나 대문자로 변환한다. 
    - `trim()` : 문자열 양쪽 끝의 공백을 제거한다. 단순 Whitespace 만 제거할 수 있다. 
    - `strip()` : Whitespace 와 유니코드 공백을 포함해서 제거한다. 자바 11
    - 비공개 레포지토리2: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringUtilsMain2.java
  - 문자열 분할 및 조합
    - `split(String regex)` : 문자열을 정규 표현식을 기준으로 분할한다. 
    - `join(CharSequence delimiter, CharSequence... elements)` : 주어진 구분자로 여러 문자열을 결합한다.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringSplitJoinMain.java
  - 기타 유틸리티
    - `valueOf(Object obj)` : 다양한 타입을 문자열로 변환한다. 
    - `toCharArray()`: 문자열을 문자 배열로 변환한다. 
    - 비공개 레포지토리1: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringUtilsMain1.java
    - `format(String format, Object... args)` : 형식 문자열과 인자를 사용하여 새로운 문자열을 생성한다. 
    - `matches(String regex)` : 문자열이 주어진 정규 표현식과 일치하는지 확인한다.
    - 비공개 레포지토리2: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/method/StringUtilsMain2.java

### StringBuilder - 가변 String

- 불변인 `String` 클래스의 단점
    - 문자를 더하거나 변경할 때 마다 계속해서 **새로운 객체**를 생성해야 한다.
      - 문자를 자주 더하거나 변경해야 하는 상황이라면 더 많은 String 객체를 만들고, GC해야 한다.
      - 결과적으로 컴퓨터의 CPU, 메모리를 자원을 더 많이 사용하게 된다. 
        - 문자열의 크기가 클수록, 문자열을 더 자주 변경할수록 시스템의 자원을 더 많이 소모한다.
        
```java
String str = "A" + "B" + "C" + "D";
String str = String("A") + String("B") + String("C") + String("D");
String str = new String("AB") + String("C") + String("D");
String str = new String("ABC") + String("D");
String str = new String("ABCD");
```

- `StringBuilder`를 사용하면 위 문제들을 해결할 수 있다.

- `StringBuilder`
  - 가변 `String`이다.
    - 가변은 내부의 값을 바로 변경하면 되기 때문에 새로운 객체를 생성할 필요가 없다.
    - 따라서 성능과 메모리 사용면에서 불변보다 더 효율적이다.
- `StringBuilder` 메서드 목록
  - `append(String str)` : 메서드를 사용해 여러 문자열을 추가한다. 
  - `insert(int index, String str)` : 메서드로 특정 위치에 문자열을 삽입한다. 
  - `delete(int index1, int index2)` : 메서드로 특정 범위의 문자열을 삭제한다. 
  - `reverse()` : 메서드로 문자열을 뒤집는다.
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/builder/StringBuilderMain1_1.java

- `StringBuilder`는 보통 문자열을 변경하는 동안만 사용하다가 문자열 변경이 끝나면 안전한(불변) `String`으로 변환하는 것이 좋다.

### String 최적화

- 문자열 리터럴 최적화
  - 자바 컴파일러는 문자열 리터럴을 더하는 부분을 자동으로 합쳐준다.
      - 컴파일 전 : `String helloWorld = "Hello, " + "World!";`
      - 컴파일 후 : `String helloWorld = "Hello, World!";`
      - 런타임에 별도의 문자열 결합 연산을 수행하지 않기 때문에 성능이 향상된다.

- `String` 변수 최적화
  - 문자열 변수의 경우 그 안에 어떤 값이 들어있는지 컴파일 시점에는 알 수 없기 때문에 단순하게 합칠 수 없다.
    - `String result = str1 + str2;`
    - 이런 경우 다음과 같이 최적화를 수행한다.
      - `String result = new StringBuilder().append(str1).append(str2).toString();`
  - 이렇듯 자바가 최적화를 처리해주기 때문에 지금처럼 간단한 경우에는 `StringBuilder`를 사용하지 않아도 된다.
  - 대신에 문자열 더하기 연산(`+`)을 사용하면 충분하다.

- `String` 최적화가 어려운 경우
  - 반복문안에서 문자열을 더하는 경우에는 최적화가 이루어지지 않는다.
    - 반복 횟수만큼 객체를 생성해야 한다.
    - 반복문 내에서의 문자열 연결은, 런타임에 연결할 문자열의 개수와 내용이 결정된다.
      - 이런 경우, 컴파일러는 얼마나 많은 반복이 일어날지, 각 반복에서 문자열이 어떻게 변할지 예측할 수 없다.
  - 반복문 내 문자열 연산 비교. (`String` vs `StringBuilder`)
    - `String`
      - 11484ms == 11초
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/builder/LoopStringMain.java
    - `StringBuilder`
      - 9ms == 0.009초
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/string/builder/LoopStringBuilderMain.java
    - `StringBuilder`를 사용했을때 압도적으로 빠르다...

- `StringBuilder`를 직접 사용하는 것이 더 좋은 경우
  - **반복문**에서 반복해서 문자를 연결할 때 
    - 천번 이상...
  - **조건문**을 통해 동적으로 문자열을 조합할 때 
  - **복잡한** 문자열의 특정 부분을 변경해야 할 때 
  - **매우 긴** 대용량 문자열을 다룰 때

- 참고: `StringBuilder` vs `StringBuffer`
    - `StringBuilder`와 똑같은 기능을 수행하는 `StringBuffer` 클래스도 있다.
    - `StringBuffer`는 멀티 스레드 상황에서 사용한다. 지금은 몰라도 된다. 
    - 대부분의 경우 `StringBuilder`를 사용한다.

### 메서드 체인닝 - Method Chaining

- 메서드 체이닝 기법
  - 코드를 간결하고 읽기 쉽게 만들어준다.
  - 메서드 체이닝 기법을 사용하기 위해선 자기 자신(`this`)을 반환해야 한다.
      - 예) `StringBuilder` 에서 문자열을 변경하는 대부분의 메서드
        - `append()`, `insert()`, `delete()`, `reverse()` 등.

```java
public StringBuilder append(String str) {
    super.append(str);
    return this;
}
```

```java
package lang.string.builder;

public class StringBuilderMain1_2 {
    
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder();
        
        //메서드 체이닝 사용
        String string = sb.append("A").append("B").append("C").append("D")
                            .insert(4, "Java")
                            .delete(4, 8)
                            .reverse()
                            .toString();
        
        System.out.println("string = " + string);
    }
    
}
```

- "만드는 사람이 수고로우면 쓰는 사람이 편하고, 만드는 사람이 편하면 쓰는 사람이 수고롭다."
    - 메서드 체이닝은 구현하는 입장에서는 번거롭지만 사용하는 개발자는 편리해진다.
    - 자바의 라이브러리와 오픈 소스들은 메서드 체이닝 방식을 종종 사용한다.

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