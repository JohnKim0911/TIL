# (복습) 김영한의 실전 자바 - 중급 1편

|    | 제목                                   | 복습일             |
|----|--------------------------------------|-----------------|
| 1  | [강의 소개와 자료](#1-강의-소개와-자료)            | 2024-11-24      |
| 2  | [Object 클래스](#2-object-클래스)          | 2024-11-24      |
| 3  | [불변 객체](#3-불변-객체)                    | 2024-11-25      |
| 4  | [String 클래스](#4-string-클래스)          | 2024-11-25      |
| 5  | [래퍼, Class 클래스](#5-래퍼-class-클래스)     | 2024-11-26      |
| 6  | [열거형 - ENUM](#6-열거형---enum)          | 2024-11-26      |
| 7  | [날짜와 시간](#7-날짜와-시간)                  | 2024-11-28 ~ 30 |
| 8  | [중첩 클래스, 내부 클래스1](#8-중첩-클래스-내부-클래스1) | 2024-12-01      |
| 9  | [중첩 클래스, 내부 클래스2](#9-중첩-클래스-내부-클래스2) | 2024-12-02      |
| 10 | [예외 처리1 - 이론](#10-예외-처리1---이론)       | 2024-12-02      |
| 11 | [예외 처리2 - 실습](#11-예외-처리2---실습)       | 2024-12-03      |
| 12 | [다음으로](#12-다음으로)                     | 2024-12-03      |

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

### String 클래스 - 기본

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

### 래퍼 클래스 - 기본형의 한계

- 기본형의 한계
    - 객체가 아님
        - 기본형은 객체가 아니므로 메서드를 제공할 수 없다.
        - 아래는 나중에 설명
            - 객체 참조가 필요한 컬렉션 프레임워크를 사용할 수 없다.
            - 제네릭도 사용할 수 없다.
    - `null` 값을 가질 수 없음
        - 기본형은 항상 값을 가진다.
        - `없음`이라는 상태를 표현 할 수 없다.

- 직접 만든 래퍼 클래스
    - 특정 기본형을 감싸서(Wrap) 만드는 클래스를 래퍼 클래스(Wrapper class)라 한다.
    - 래퍼클래스를 사용하면 기본형의 한계를 극복 할 수 있다.

```java
package lang.wrapper;

public class MyInteger { //직접 만든 래퍼 클래스

    private final int value;

    public MyInteger(int value) {
        this.value = value;
    }

    public int getValue() {
        return value;
    }

    public int compareTo(int target) {
        if (value < target) {
            return -1;
        } else if (value > target) {
            return 1;
        } else {
            return 0;
        }
    }

    @Override
    public String toString() {
        return String.valueOf(value); //숫자를 문자로 변경
    }
}
```

```java
package lang.wrapper;

public class MyIntegerNullMain1 {

    public static void main(String[] args) {
        MyInteger[] intArr = {new MyInteger(-1), new MyInteger(0), new MyInteger(1)};
        System.out.println(findValue(intArr, -1)); //-1
        System.out.println(findValue(intArr, 0)); //0
        System.out.println(findValue(intArr, 1)); //1
        System.out.println(findValue(intArr, 100)); //null
    }

    //배열에 해당 값이 있으면 그 값을 반환하고, 값이 없으면 null 반환
    private static MyInteger findValue(MyInteger[] intArr, int target) {
        for (MyInteger myInteger : intArr) {
            if (myInteger.getValue() == target) {
                return myInteger;
            }
        }
        return null;
    }
}
```

### 래퍼 클래스 - 자바 래퍼 클래스

- 자바는 기본형에 대응하는 래퍼 클래스를 기본으로 제공한다.
    - 래퍼 클래스는 기본형의 객체 버전이다.
    - 기본적으로 앞글자가 대문자로 바뀐다.
        - `Integer`와 `Character`는 예외

| 기본형     | 래퍼클래스     | 참고      |
|---------|-----------|---------|
| byte    | Byte      |         |
| short   | Short     |         |
| int     | Integer   | * 글자 다름 |
| long    | Long      |         |
| float   | Float     |         |
| double  | Double    |         |
| char    | Character | * 글자 다름 |
| boolean | Boolean   |         |

- 래퍼 클래스 특징
    - 불변이다.
    - `equals`로 비교해야 한다.
        - 래퍼 클래스는 객체이기 때문에 `==` 비교를 하면 인스턴스의 참조값을 비교한다.
            - 래퍼 클래스는 내부의 값을 비교하도록 `equals()` 를 재정의 해두었다.


- 래퍼 클래스 사용법
    - **래퍼 클래스 생성 - 박싱(Boxing)**
        - 기본형을 래퍼 클래스로 변경하는 것을 **박싱(Boxing)** 이라 한다.
            - `Integer integerObj = Integer.valueOf(10);`
                - 성능 최적화 기능
                    - 일반적으로 자주 사용하는 `-128` ~ `127` 범위의 `Integer` 클래스를 미리 생성해둔다.
                - 불변이다.
                - 내부에서 `new Integer(10)`을 사용해서 객체를 생성하고 반환한다.
            - `Integer newInteger = new Integer(10);` // 사용을 권장하지 않는다.
                - 미래에 삭제 예정. 위의 `valueOf()` 사용하자
        - 다른 타입도 동일하게 사용한다.
            - `Long longObj = Long.valueOf(100);`
            - `Double doubleObj = Double.valueOf(10.5);`
    - **intValue() - 언박싱(Unboxing)**
        - 래퍼 클래스에 들어있는 기본형 값을 다시 꺼내는 메서드이다.
            - `int intValue = integerObj.intValue();`
            - `long longValue = longObj.longValue();`
    - 래퍼 클래스는 객체를 그대로 출력해도 내부에 있는 값을 문자로 출력하도록 `toString()`을 재정의했다.

### 래퍼 클래스 - 오토 박싱

- 기본형을 래퍼 클래스로 변환하거나(`valueOf()`),  래퍼 클래스를 기본형으로 변환하는 일(`intValue()`)이 자주 있는데, 그 과정이 번거롭다.
    - 자바 1.5부터 오토 박싱(Auto-boxing), 오토 언박싱(Auto-Unboxing)을 지원한다.
        - 컴파일러가 자동으로 `valueOf()`, `intValue()`를  추가해준다.

```java
Integer boxedValue = 10; //오토 박싱(Auto-boxing)
//Integer boxedValue = Integer.valueOf(10); //컴파일 단계에서 추가

int unboxedValue = boxedValue; //오토 언박싱(Auto-Unboxing)
//int unboxedValue = boxedValue.intValue(); //컴파일 단계에서 추가
```

### 래퍼 클래스 - 주요 메서드와 성능

- 래퍼 클래스 - 주요 메서드
    - `valueOf()` : 래퍼 타입을 반환한다. 숫자, 문자열을 모두 지원한다. **(숫자 or 문자열 --> 래퍼)**
        - 예시) `Integer i1 = Integer.valueOf(10);` //숫자, 래퍼 객체 반환
        - 예시) `Integer i2 = Integer.valueOf("10");` //문자열, 래퍼 객체 반환
    - `parseInt()` : 문자열을 기본형으로 변환한다. **(문자열 --> 기본형)**
        - 예시) `int intValue = Integer.parseInt("10");` //문자열 전용, 기본형 반환
        - `Long.parseLong()` 처럼 각 타입에 `parseXxx()`가 존재한다.
    - `compareTo()` : 내 값과 인수로 넘어온 값을 비교한다. 내 값이 크면 `1` , 같으면 `0` , 내 값이 작으면 `-1` 을 반환한다.
        - 예시) `int compareResult = i1.compareTo(20);` // 10.compareTo(20) --> 10이 20보다 작으므로 -1 반환
    - `Integer.sum()` , `Integer.min()` , `Integer.max()` : static 메서드이다. 간단한 덧셈, 작은 값, 큰 값 연산을 수행한다
        - 예시) `Integer.sum(10, 20);` //30
        - 예시) `Integer.min(10, 20)` //10
        - 예시) `Integer.max(10, 20)` //20

- 래퍼 클래스와 성능
    - `1` ~ `1_000_000_000`(10억) 까지 숫자를 더하는 반복문 수행시간 비교
        - 기본형 vs 래퍼 클래스
            - 기본형 : `387ms`
            - 래퍼 클래스 : `4031ms`
            - 실행 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/wrapper/WrapperVsPrimitive.java
    - 기본형이 래퍼 클래스보다 훨씬 빠르다...
        - 기본형은 메모리에서 단순히 그 크기만큼의 공간을 차지한다.
            - 예) `int`는 보통 4바이트의 메모리를 사용한다.
        - 래퍼 클래스의 인스턴스는 내부에 필드로 가지고 있는 기본형의 값 뿐만 아니라, 자바에서 객체 자체를 다루는데 필요한 객체 메타데이터를 포함하므로 더 많은 메모리를 사용한다.
            - 자바 버전과 시스템마다 다르지만 대략 8~16 바이트의 메모리를 추가로 사용한다.
        - 위 연산은 10억번 수행했을 때 결과이다. 일반적인 경우에는 별 차이가 없다.
            - 0.3초 나누기 10억 vs 1.5초 나누기 10억이다

    - 기본형, 래퍼 클래스 어떤 것을 사용?
        - 일반적으론 유지보수하기 더 나은것을 선택.
            - 성능 테스트를 하다가 문제가 되는 부분이 있으면 기본형을 고려하자.
                - (수만~ 수십만 이상 연속해서 연산을 수행해야 하는 경우)
        - 일반적인 애플리케이션을 만드는 관점에서 보면 이런 부분을 최적화해도 사막의 모래알 하나 정도의 차이가 날 뿐 이다.

- 유지보수 vs 최적화
    - 유지보수가 우선!
    - 최적화를 한다고 했지만 전체 애플리케이션의 성능 관점에서 보면 불필요한 최적화를 할 가능성이 있다.
        - 최신 컴퓨터는 매우 빠르기 때문에 메모리 상에서 발생하는 연산을 몇 번 줄인다고해도 실질적인 도움이 되지 않는 경우가 많다.
        - 성능 최적화는 대부분 복잡함을 요구하고, 더 많은 코드들을 추가로 만들어야 한다.
        - 특히 웹 애플리케이션의 경우, 메모리 안에서 발생하는 연산 하나보다 네트워크 호출 한 번이 많게는 수십만배 더 오래 걸린다.
            - 자바 메모리 내부에서 발생하는 연산을 수천번에서 한 번으로 줄이는 것 보다, 네트워크 호출 한 번 을 더 줄이는 것이 더 효과적인 경우가 많다.

### Class 클래스

- 클래스의 정보(메타데이터)를 다루는데 사용된다.

- 지금은 `Class`가 뭔지, 그리고 대략 어떤 기능들을 제공하는지만 알아두면 충분하다.
    - 이걸 몰라도 당장 개발하는데 문제 없다. 이것보다 중요한 기본기가 많다...

- `Class` 클래스의 주요 기능
    - 타입 정보 얻기
        - 클래스의 이름, 슈퍼클래스, 인터페이스, 접근 제한자 등과 같은 정보를 조회할 수 있다.
    - 리플렉션
        - 클래스에 정의된 메서드, 필드, 생성자 등을 조회하고, 이들을 통해 객체 인스턴스를 생성하거나 메서드를 호출하는 등의 작업을 할 수 있다.
    - 동적 로딩과 생성
        - `Class.forName()` 메서드를 사용하여 클래스를 동적으로 로드하고, `newInstance()` 메서드를 통해 새로운 인스턴스를 생성할 수 있다
    - 애노테이션 처리
        - 클래스에 적용된 애노테이션(annotation)을 조회하고 처리하는 기능을 제공한다.

- 예제코드
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/clazz/ClassMetaMain.java
    - `Class` 클래스는 다음과 같이 3가지 방법으로 조회할 수 있다.
        - `Class clazz = String.class;` // 1.클래스에서 조회
        - `Class clazz = new String().getClass();` // 2.인스턴스에서 조회
        - `Class clazz = Class.forName("java.lang.String");` // 3.문자열로 조회
    - `Class` 클래스의 주요 기능
        - `getDeclaredFields()`: 클래스의 모든 필드를 조회한다.
        - `getDeclaredMethods()`: 클래스의 모든 메서드를 조회한다.
        - `getSuperclass()`: 클래스의 부모 클래스를 조회한다.
        - `getInterfaces()`: 클래스의 인터페이스들을 조회한다.
    - `class`는 자바의 예약어다. 따라서 패키지명, 변수명으로 사용할 수 없다.
        - 대신 `clazz` 라는 이름을 관행으로 사용한다.

- 클래스 생성하기
    - Class 클래스에는 클래스의 모든 정보가 들어있다.
    - 이 정보를 기반으로 인스턴스를 생성하거나, 메서드를 호출하고, 필드의 값도 변경할 수 있다.
        - 예제코드 (비공개 레포지토리)
            - hello() 클래스: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/clazz/Hello.java
            - main 클래스: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/clazz/ClassCreateMain.java
- `class` 클래스는 대략 보고, 넘어가자. 나중에 다시 다룬다.

### System 클래스

- `System` 클래스는 시스템과 관련된 기본 기능들을 제공한다.
    - 표준 입력, 출력, 오류 스트림
        - `System.in` : 표준 입력 스트림
        - `System.out` : 표준 출력 스트림
        - `System.err` : 표준 오류 스트림. (잘 사용하지 않는다.)
    - 시간 측정
        - `System.currentTimeMillis()` : 현재 시간(밀리초)
        - `System.nanoTime()` : 현재 시간(나노초)
    - 환경 변수
        -  `System.getenv()` : OS에서 설정한 환경 변수의 값
    - 시스템 속성
        - 자바에서 사용하는 설정 값
        - `System.getProperties()` : 현재 시스템 속성
        - `System.getProperty(String key)` : 특정 속성
    - 시스템 종료
        - `System.exit(int status)` : 프로그램을 종료하고, OS에 프로그램 종료의 상태 코드를 전달한다.
            - 상태 코드 0 : 정상 종료
            - 상태 코드 0 이 아님: 오류나 예외적인 종료
    - 배열 고속 복사
        - `System.arraycopy()`: 시스템 레벨에서 최적화된 메모리 복사 연산을 사용한다.
            - 직접 반복문을 사용해서 배열을 복사할 때 보다 수 배 이상 빠른 성능을 제공한다.

- 예제 코드
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/system/SystemMain.java

### Math, Random 클래스

- Math 클래스
    - 수학 문제를 해결해주는 클래스
        - 이런게 있구나 보고, 나중에 필요할 때 찾아보자.
    - 주요 메서드
        - 기본 연산
            - `abs(x)` : 절대값
            - `max(a, b)` : 최대값
            - `min(a, b)` : 최소값
        - 지수 및 로그 연산
            - `exp(x)` : e^x 계산
            - `log(x)` : 자연 로그
            - `log10(x)` : 로그 10
            - `pow(a, b)` : a의 b 제곱
        - 반올림 및 정밀도
            - `ceil(x)` : 올림
            - `floor(x)` : 내림
            - `rint(x)` : 가장 가까운 정수로 반올림
            - `round(x)` : 반올림
        - 삼각 함수
            - `sin(x)` : 사인
            - `cos(x)` : 코사인
            - `tan(x)` : 탄젠트
        - 기타
            - `sqrt(x)` : 제곱근
            - `cbrt(x)` : 세제곱근
            - `random()` : 0.0과 1.0 사이의 무작위 값 생성
                - 이거말고, `Random` 클래스 사용을 권장한다.
                - `Math.random()` 도 내부에서는 `Random` 클래스를 사용한다.
    - 예제 코드:
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/math/MathMain.java
    - 아주 정밀한 숫자와 반올림 계산이 필요하다면 `BigDecimal`을 검색해보자. (정산 시스템 등에 사용)

- Random 클래스
    - `Random random = new Random();` : 인스턴스를 생성해서 사용한다.
        - `random.nextInt();` //-435493522
        - `random.nextDouble();` //0.0d ~ 1.0d //0.35895881763641546
        - `random.nextBoolean();` //false
        - `random.nextInt(10);` //0 ~ 9까지 출력
            - `random.nextInt(10) + 1;` //1 ~ 10까지 출력
    - `Random random = new Random(1);` : seed가 같으면 Random의 결과가 같다.
        - 테스트 시에 사용하면 유용하다.
    - 예제 코드:
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/lang/math/RandomMain.java

### 문제와 풀이

- 로또 번호 자동 생성기
    - 조건
        - 로또 번호는 1~45 사이의 숫자를 6개 뽑아야 한다.
        - 각 숫자는 중복되면 안된다.
        - 실행할 때 마다 결과가 달라야 한다.
    - 실제 코드:
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/lang/math/test

---

## 6. 열거형 - ENUM

### 문자열과 타입 안전성

- 열거형이 생겨난 이유를 예제를 통해 알아보자.

- 예제 0번
    - **단순히 문자열을 입력하는 방식**
    - 예제 코드
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/enumeration/ex0
            - 공통 코드 :  `DiscountService.java`
            - 정상 작동 : `StringGradeEx0_1.java`
            - 문제 발생 : `StringGradeEx0_2.java`
    - 예제에서는 다음과 같은 문제가 발생했다.
        - 존재하지 않는 `VIP`라는 등급을 입력했다.
        - 오타: `DIAMOND` 마지막에 `D`가 하나 추가되었다.
        - 소문자 입력: 등급은 모두 대문자인데, 소문자를 입력했다.
    - 이런 문제를 해결하려면 특정 범위로 값을 제한해야 한다.
        - 예를 들어 `BASIC`, `GOLD`, `DIAMOND`라는 정확한 문자만 `discount()` 메서드에 전달되어야 한다.
        - 하지만 `String`은 어떤 문자열이든 받을 수 있기 때문에 자바 문법 관점에서는 아무런 문제가 없다.
        - 결국 `String` 타입을 사용해서는 문제를 해결할 수 없다.

- 예제 1번
    - **문자열 상수 사용**
        - 미리 정의한 변수명을 사용하기 때문에 문자열보다 안전하다.
    - 예제 코드
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/enumeration/ex1
            - 공통 코드 :  `DiscountService.java`, `StringGrade.java`
            - 정상 작동 : `StringGradeEx1_1.java`,
            - 문제 발생 : `StringGradeEx1_2.java`
    - 더 나아진 점
        - 상수의 이름을 잘못 입력하면 컴파일 시점에 오류가 발생한다. 오류를 쉽고 빠르게 찾을 수 있다.
    - 문제점
        - `StringGrade`에 있는 문자열 상수를 사용하지 않고, 직접 문자열을 사용해도 막을 수 있는 방법이 없다.

### 타입 안전 열거형 패턴

- `타입 안전 열거형 패턴` (Type-Safe Enum Pattern)
    - `Enum`
        - `enumeration`의 줄임말.
        - `열거`라는 뜻. 어떤 항목을 나열하는 것을 뜻한다.
        - 예시)
            - 회원 등급인 `BASIC` , `GOLD` , `DIAMOND`를 나열하는 것.
    - `타입 안전 열거형 패턴`을 사용하면 미리 나열한 항목만 사용할 수 있다.
        - 아무런 문자열이나 다 사용할 수 있는 것이 아니라,
        - 우리가 나열한 항목인 `BASIC`, `GOLD`, `DIAMOND`만 안전하게 사용할 수 있다.

- 직접 구현

```java
package enumeration.ex2;

//회원 등급을 다루는 클래스를 만들고, 각각의 회원 등급별로 상수를 선언한다.
public class ClassGrade {
    public static final ClassGrade BASIC = new ClassGrade(); //x001
    public static final ClassGrade GOLD = new ClassGrade(); //x002
    public static final ClassGrade DIAMOND = new ClassGrade(); //x003
    //각각의 상수마다 별도의 인스턴스를 생성하고, 생성한 인스턴스를 대입한다.
    //- static을 사용해서 상수를 메서드 영역에 선언한다.
    //- final을 사용해서 인스턴스(참조값)를 변경할 수 없게 한다.

    //private 생성자 추가: 외부에서 임의로 인스턴스를 생성할 수 있다는 문제를 차단한다.
    private ClassGrade() {}
}
```

- 위 코드 설명
    - `static` 이므로 애플리케이션 로딩 시점에 3개의 `ClassGrade` 인스턴스가 생성된다.
        - `getClass()`의 결과는 모두 `ClassGrade`이다.
    - 각각의 상수는 서로 다른 인스턴스의 참조값을 가진다.
    - 관련 코드:
        - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/enumeration/ex2
    - 메모리 구조:

![타입안전열거형패턴_직접구현](https://github.com/user-attachments/assets/978f8314-6cbf-45a4-8ad9-0bd410a1f2b4)

- `타입 안전 열거형 패턴`의 장단점
    - 장점
        - 타입 안정성 향상
            - 정해진 객체만 사용할 수 있기 때문에, 잘못된 값을 입력하는 문제를 컴파일 시점에 방지할 수 있다.
        - 데이터 일관성 보장
            - 정해진 객체만 사용하므로, 데이터의 일관성이 보장된다.
    - 단점
        - 이 패턴을 구현하려면 많은 코드를 작성해야 한다.
        - `private` 생성자를 넣어야 하는데, 잊어버릴 수 있다.

### 열거형 - Enum Type

- 자바는 `타입 안전 열거형 패턴`을 매우 편리하게 사용할 수 있는 `열거형`(Enum Type)을 제공한다.

```java
package enumeration.ex3;

public enum Grade { //열거형을 정의할 때는 class 대신에 enum을 사용한다.
    BASIC, GOLD, DIAMOND
    //원하는 상수의 이름을 나열하면 된다.
    //뒤에 ;를 안붙여도 된다.
}
```

위 코드는 아래 코드와 같다.

```java
public class Grade extends Enum {
    public static final Grade BASIC = new Grade();
    public static final Grade GOLD = new Grade();
    public static final Grade DIAMOND = new Grade();
    
    private Grade() {}
}
```

- 사용 예시

```java
package enumeration.ex3;

public class DiscountService {

    public int discount(Grade grade, int price) {
        int discountPercent = 0;

        if (grade == Grade.BASIC) {
            discountPercent = 10;
        } else if (grade == Grade.GOLD) {
            discountPercent = 20;
        } else if (grade == Grade.DIAMOND) {
            discountPercent = 30;
        } else {
            System.out.println("할인X");
        }

        return price * discountPercent / 100;
    }
}
```

```java
package enumeration.ex3;


public class ClassGradeEx3_1 {

    public static void main(String[] args) {
        int price = 10000;

        DiscountService discountService = new DiscountService();
        int basic = discountService.discount(Grade.BASIC, price);
        int gold = discountService.discount(Grade.GOLD, price);
        int diamond = discountService.discount(Grade.DIAMOND, price);

        System.out.println("BASIC 등급의 할인 금액: " + basic); //1000
        System.out.println("GOLD 등급의 할인 금액: " + gold); //2000
        System.out.println("DIAMOND 등급의 할인 금액: " + diamond); //3000
    }
}
```

- 열거형
  - 열거형도 클래스이다.
      - 열거형을 제공하기 위해 제약이 추가된 클래스라 생각하면 된다.
  - 열거형은 자동(강제)으로 `java.lang.Enum`을 상속 받는다.
    - 따라서 해당 클래스가 제공하는 기능들을 사용할 수 있다.
  - 외부에서 임의로 생성할 수 없다. (`private` 생성자 역할)
  - 장점
    - 타입 안정성 향상
      - 열거형은 사전에 정의된 상수들로만 구성되므로, 유효하지 않은 값이 입력될 가능성이 없다.
      - 이런 경우 컴파일 오류가 발생한다.
    - 간결성 및 일관성
      - 열거형을 사용하면 코드가 더 간결하고 명확해지며, 데이터의 일관성이 보장된다.
    - 확장성
      - 새로운 회원 등급을 타입을 추가하고 싶을 때, ENUM에 새로운 상수를 추가하기만 하면 된다.
  - `static import`를 사용하면 더 읽기 좋은 코드를 만들 수 있다.
  - 열거형은 인터페이스를 구현할 수 있다. 
  - 열거형에 추상 메서드를 선언하고, 구현할 수 있다.
    - 이 경우 익명 클래스와 같은 방식을 사용한다. 익명 클래스는 뒤에서 다룬다.

### 열거형 - 주요 메서드

- ENUM - 주요 메서드
  - `values()`: 모든 ENUM 상수를 포함하는 배열을 반환한다. 
  - `valueOf(String name)`: 주어진 이름과 일치하는 ENUM 상수를 반환한다. 
  - `name()`: ENUM 상수의 이름을 문자열로 반환한다.
  - `ordinal()`: ENUM 상수의 선언 순서(0부터 시작)를 반환한다.
    - 가급적 사용하지 않는 것이 좋다.
      - 전설적인 에러를 야기할 수 있다...
      - 이 값을 사용하다가 중간에 상수를 선언하는 위치가 변경되면 전체 상수의 위치가 모두 변경될 수 있다.
  - `toString()`: ENUM 상수의 이름을 문자열로 반환한다.
    - `name()` 메서드와 유사하지만, `toString()`은 직접 오버라이딩 할 수 있다.

- `Arrays.toString()`: 배열 내부의 값을 출력할 때 사용한다.

```java
package enumeration.ex3;

import java.util.Arrays;

public class EnumMethodMain {

    public static void main(String[] args) {

        //모든 ENUM 반환
        Grade[] values = Grade.values();
        System.out.println("values = " + Arrays.toString(values));
        
        for (Grade value : values) {
            System.out.println("name = " + value.name() + ", ordinal=" + value.ordinal());
        }

        //String -> ENUM 변환, 잘못된 문자면 IllegalArgumentException 발생
        String input = "GOLD";
        Grade gold = Grade.valueOf(input);
        System.out.println("gold = " + gold); //toString() 오버라이딩 가능
    }
}

/*
values = [BASIC, GOLD, DIAMOND]

name = BASIC, ordinal=0
name = GOLD, ordinal=1
name = DIAMOND, ordinal=2

gold = GOLD
*/
```

### 열거형 - 리팩토링

- 주요 리펙토링 내용
  - 회원 등급 클래스가 할인율(`discountPercent`)을 가지고 관리하도록 변경.
    - 객체지향 캡슐화 적용
  - `DiscountService` 제거
    - `Grade`가 스스로 할인율을 계산하면서 `DiscountService` 클래스가 더는 필요하지 않다.
  - 새로운 등급이 추가되더라도 `main()` 코드의 변경없도록 변경
  - 출력 부분의 중복 제거.

```java
package enumeration.ref3;

public enum Grade {
    BASIC(10), GOLD(20), DIAMOND(30);

    private final int discountPercent;

    Grade(int discountPercent) { //private이 생략되어있음
        this.discountPercent = discountPercent;
    }

    public int getDiscountPercent() {
        return discountPercent;
    }

    public int discount(int price) {
        return price * discountPercent / 100;
    }
}
```

```java
package enumeration.ref3;

public class EnumRefMain3_4 {

    public static void main(String[] args) {
        int price = 10000;
        
        //새로운 등급이 추가되더라도 main() 코드의 변경없도록 변경
        Grade[] grades = Grade.values();
        for (Grade grade : grades) {
            printDiscount(grade, price);
        }
    }

    private static void printDiscount(Grade grade, int price) { //출력 부분의 중복 제거
        System.out.println(grade.name() + " 등급의 할인 금액: " + grade.discount(price));
    }
}

/*
BASIC 등급의 할인 금액: 1000
GOLD 등급의 할인 금액: 2000
DIAMOND 등급의 할인 금액: 3000
*/
```

### 문제와 풀이

- 인증 등급따라 볼 수 있는 페이지 출력
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/enumeration/test

    ```
    당신의 등급을 입력하세요[GUEST, LOGIN, ADMIN]: LOGIN
    당신의 등급은 로그인 회원입니다.
    ==메뉴 목록==
    - 메인 화면
    - 이메일 관리 화면 
    ```

- 입력된 HTTP code의 상태코드, 상태메시지 성공여부 출력
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/enumeration/test/http

       ```
       HTTP CODE: 400
       400 Bad Request
       isSuccess = false
       ```

---

## 7. 날짜와 시간

### 날짜와 시간 라이브러리가 필요한 이유

- 직접 계산하기 복잡하고 어렵다. 자바 시간 라이브러리를 사용하자.
  - 왜 어렵나?
    - 날짜
      - 어떤달은 28일, 30일, 31일...
    - 윤년
      - 4년마다 하루(2월 29일)를 추가하는 윤년 + 윤년 관련 다른 규칙들...
    - 일광 절약 시간 (Daylight Saving Time, `DST`)
      - 썸머타임... 해 뜨는 시간따라 시간이 바뀐다. 한국은 해당없음.
    - 타임존
      - 세계는 다양한 타임존으로 나눠져 있고, 각 타임존은 `UTC`(협정 세계시)로부터의 시간 차이로 정의된다.
      - 일광 절약 시간이 적용되는 경우, 타임존 차이가 변할 수 있다.

- 용어
  - 역사적으로 `GMT`가 국제적인 시간 표준으로 사용되었고, `UTC`가 나중에 이를 대체하기 위해 도입되었다.
    - `UTC`(협정 세계시, Universal Time Coordinated)
      - **원자 시계**를 사용하여 측정한 국제적으로 합의된 시간 체계.
      - 지구의 자전 속도가 변화하는 것을 고려하여 윤초를 추가하거나 빼는 방식으로 시간을 조정함으로써, **보다 정확한 시간**을 유지한다.
    - `GMT` (그리니치 평균시, Greenwich Mean Time)
    - 둘 다 경도 0°에 위치한 영국의 그리니치 천문대를 기준으로 하며, 이로 인해 실질적으로 같은 시간대를 나타낸다.
    - `GMT`와 `UTC`는 거의 차이가 없으나, 정밀한 시간 측정과 국제적인 표준에 관해서는 `UTC`가 선호된다.

- 자바 날짜와 시간 라이브러리의 역사
  1. 자바 표준 라이브러리는 사용성이 너무 떨어지고, 문제가 많았다.
     - JDK 1.0 (java.util.Date) 
     - JDK 1.1 (java.util.Calendar)
  2. `Joda-Time`이라는 오픈소스 라이브러리가 등장한다. 편리함과 사용성 덕분에 크게 대중화 되었다.
  3. 자바는 `Joda-Time`을 만든 개발자를 데려와서, 새로운 자바 표준 날짜와 시간 라이브러리를 정의한다.
     - JDK 8(1.8) (java.time 패키지)
  - 자세한 내용은 교재 참고 (p.4)

### 자바 날짜와 시간 라이브러리 소개

![날짜와시간 라이브러리 표](https://github.com/user-attachments/assets/e25c440f-d0af-4af6-8e06-225b43aeda72)

- `LocalDate`, `LocalTime`, `LocalDateTime` ⭐⭐
  - 특정 지역의 날짜와 시간만 고려할 때 사용한다.
    - 세계 시간대를 고려하지 않는다.
    - 국내 서비스만 할때 사용.
      - 가장 많이 사용하게 될 타입이다.
  - `LocalDate`
    - 날짜만 표현할 때 사용 (년, 월, 일)
    - 예시) `2013-11-21`
  - `LocalTime`
    - 시간만 표현할 때 사용 (시, 분, 초)
    - 예시) `08:20:30.213`
      - 초는 밀리초, 나노초 단위도 포함할 수 있다.
  - `LocalDateTime`
    - `LocalDate`와 `LocalTime`을 합한 개념
    - 예시) `2013-11-21T08:20:30.213`

- `ZonedDateTime`, `OffsetDateTime`
  - 세계 시간대를 고려 할 때 사용한다.
  - `ZonedDateTime` ⭐
    - 타임존이 포함된다.
        - 이 타임존을 알면 오프셋과 일광 절약 시간제에 대한 정보를 알 수 있다
    - 예시) `2013-11-21T08:20:30.213+9:00[Asia/Seoul]`
      - `+9:00` 은 `UTC`(협정 세계시)로 부터의 시간대 차이이다. 오프셋이라 한다.
      - `Asia/Seoul`은 타임존이라 한다.
  - `OffsetDateTime` : 잘안쓴다...
    - 타임존은 없고, `UTC`로 부터의 시간대 차이인 고정된 오프셋만 포함한다.
    - 예시) `2013-11-21T08:20:30.213+9:00`
    - 일광 절약 시간제가 적용되지 않는다.

- `Year`, `Month`, `YearMonth`, `MonthDay` : 잘안쓴다...
  - 년, 월, 년월, 달일을 각각 다룰 때 사용한다.

- `Instant`: 특이한 경우에만 쓰인다.
  - 1970년 1월 1일 0시 0분 0초(`UTC`)를 기준으로 경과한 시간으로 계산된다.
  - 초 데이터만 들어있다. 계산에 사용할 때는 적합하지 않다.

- `Period`, `Duration` ⭐⭐
  - **시간의 양(amount of time)** 을 표현하는데 사용된다.
    - `Period`
      - 두 날짜 사이의 간격
      - 년, 월, 일 단위
      - 예시) "이 프로젝트는 3개월 남았어."
    - `Duration`
      - 두 시간 사이의 간격
      - 시, 분, 초(나노초) 단위
      - 예시) "라면은 3분 동안 끓어야 해."
- 모든 날짜 클래스는 불변이다. ⭐⭐
  - 따라서 변경이 발생하는 경우 새로운 객체를 생성해서 반환하므로 **반환값**을 꼭 받아야 한다.

### 기본 날짜와 시간 - LocalDateTime

- `LocalDate`, `LocalTime`
  - 관련 메서드
    - `now()`: 현재 시간을 기준으로 생성
    - `of(...)`: 특정 날짜를 기준으로 생성
    - `plusDays()`: 특정 일을 더한다.
      - 다양한 `plusXxx()` 메서드가 존재한다.

```java
package time;

import java.time.LocalDate;

public class LocalDataMain {
    
    public static void main(String[] args) {
        LocalDate nowDate = LocalDate.now();
        LocalDate ofDate = LocalDate.of(2013, 11, 21);
        System.out.println("오늘 날짜= " + nowDate); //2024-11-28
        System.out.println("지정 날짜= " + ofDate); //2013-11-21

        //계산(불변)
        LocalDate plusDays = ofDate.plusDays(10);
        System.out.println("지정 날짜+10d= " + plusDays); //2013-12-01
    }
}
```

```java
package time;

import java.time.LocalTime;

public class LocalTimeMain {
    
    public static void main(String[] args) {
        LocalTime nowTime = LocalTime.now();
        LocalTime ofTime = LocalTime.of(9, 10, 30);

        System.out.println("현재 시간 = " + nowTime); //14:34:30.819218100
        System.out.println("지정 시간 = " + ofTime); //09:10:30

        //계산(불변)
        LocalTime ofTimePlus = ofTime.plusSeconds(30);
        System.out.println("지정 시간+30s = " + ofTimePlus); //09:11
    }
}
```

- `LocalDateTime`
  - `LocalDateTime`은 `LocalDate`와 `LocalTime`을 내부에 가진다.
      ```java
      public class LocalDateTime {
          private final LocalDate date;
          private final LocalTime time;
          ...
      }
      ```
  - 관련 메서드
    - `now()`: 현재 날짜와 시간을 기준으로 생성
    - `of(...)`: 특정 날짜와 시간을 기준으로 생성
    - `toXxx()`: `LocalDate`, `LocalTime`로 분리
    - `LocalDateTime.of(localDate, localTime)`: 합체
    - `plusXxx()`: 특정 날짜와 시간을 더한다.
    - `isBefore()`, `isAfter()`, `isEqual()`: 비교하여 `true`/`false` 반환
  - `isEqual()` vs `equals()` 비교
    - `isEqual()`: 시간을 계산해서 시간으로만 둘을 비교한다.
      - 예시) 서울의 9시와 UTC의 0시는 시간적으로 같다. `true`를 반환한다.
    - `equals()`: 객체의 타입, 타임존 등등 내부 데이터의 모든 구성요소가 같아야 `true`를 반환한다.
      - 예시) 서울의 9시와 UTC의 0시는 시간적으로 같지만, 타임존의 데이터가 다르기 때문에 `false`를 반환한다.

```java
package time;

import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;

public class LocalDateTimeMain {

    public static void main(String[] args) {
        LocalDateTime nowDt = LocalDateTime.now();
        LocalDateTime ofDt = LocalDateTime.of(2016, 8, 16, 8, 10, 1);
        System.out.println("현재 날짜시간 = " + nowDt); //2024-11-28T14:37:49.404287900
        System.out.println("지정 날짜시간 = " + ofDt); //2016-08-16T08:10:01

        //날짜와 시간 분리
        LocalDate localDate = ofDt.toLocalDate();
        LocalTime localTime = ofDt.toLocalTime();
        System.out.println("localDate = " + localDate); //2016-08-16
        System.out.println("localTime = " + localTime); //08:10:01

        //날짜와 시간 합체
        LocalDateTime localDateTime = LocalDateTime.of(localDate, localTime);
        System.out.println("localDateTime = " + localDateTime); //2016-08-16T08:10:01

        //계산(불변)
        LocalDateTime ofDtPlus = ofDt.plusDays(1000);
        System.out.println("지정 날짜시간+1000d = " + ofDtPlus); //2019-05-13T08:10:01
        LocalDateTime ofDtPlus1Year = ofDt.plusYears(1);
        System.out.println("지정 날짜시간+1년 = " + ofDtPlus1Year); //2017-08-16T08:10:01

        //비교
        System.out.println("현재 날짜시간이 지정 날짜시간보다 이전인가? " + nowDt.isBefore(ofDt)); //false
        System.out.println("현재 날짜시간이 지정 날짜시간보다 이후인가? " + nowDt.isAfter(ofDt)); //true
        System.out.println("현재 날짜시간이 지정 날짜시간과 같은가? " + nowDt.isEqual(ofDt)); //false
    }
}
```

### 타임존 - ZonedDateTime
- 글로벌 서비스를 하지 않으면 잘 사용하지 않는다.
  - 너무 깊이있게 파기 보다는 대략 이런 것이 있다 정도로만 알아두면 된다.
  - 나중에 필요할때 깊이있게 학습하면 된다.

- `ZoneId`
  - 자바는 타임존을 `ZoneId` 클래스로 제공한다.
  - `ZoneId.getAvailableZoneIds()`: 사용가능한 `ZoneId`들을 문자열 형태로 반환한다.
  - `ZoneId.systemDefault()`: 시스템이 사용하는 기본 `ZoneId`를 반환한다.
  - `ZoneId.of()` : 타임존을 직접 제공해서 `ZoneId` 인스턴스를 반환한다.
  - 예시 코드:
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/ZoneIdMain.java

- `ZonedDateTime`
  - `LocalDateTime`에 시간대 정보인 `ZoneId`가 합쳐진 것이다.
      ```java
      public class ZonedDateTime {
          private final LocalDateTime dateTime;
          private final ZoneOffset offset;
          private final ZoneId zone;
      }
      ```
  - 관련 메서드
    - `now()`: 현재 날짜와 시간을 기준으로 생성한다.
    - `of(...)` : 특정 날짜와 시간을 기준으로 생성한다. `ZoneId`를 추가해야 한다.
      - `LocalDateTime`에 `ZoneId`를 추가해서 생성할 수 있다.
    - `withZoneSameInstant(ZoneId)` : 타임존을 변경한다. 타임존에 맞추어 시간도 함께 변경된다.
      - 지금 다른 나라는 몇 시 인지 확인일 수 있다.
    - 사용 예시:
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/ZonedDateTimeMain.java

- `OffsetDateTime`
  - `LocalDateTime`에 UTC 오프셋 정보인 `ZoneOffset`이 합쳐진 것이다.
    ```java
    public class OffsetDateTime {
        private final LocalDateTime dateTime;
        private final ZoneOffset offset;
    }
    ```
  - 사용 예시:
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/OffsetDateTimeMain.java

### 기계 중심의 시간 - Instant

- `Instant` 내부에는 초 데이터만 들어있다. (나노초 포함)
    ```java
    public class Instant {
        private final long seconds;
        private final int nanos;
        ...
    }
    ```
  - 예시) UTC 기준 1970년 1월 1일,
      - 0시 0분 0초라면 `seconds`에 `0`이 들어간다.
      - 0시 0분 10초라면 `seconds` 에 `10`이 들어간다.
      - 0시 1분 0초라면 `seconds` 에 `60`이 들어간다.

- Epoch 시간 (에포크 시간)
  - Epoch time, 또는 Unix timestamp는 컴퓨터 시스템에서 시간을 나타내는 방법 중 하나이다.
  - 1970년 1월 1일 00:00:00 UTC부터 현재까지 경과된 시간을 초 단위로 표현한 것이다.
  - 시간대에 영향을 받지 않는 절대적인 시간 표현 방식이다. 
    - 전 세계 어디서나 동일한 시점을 가리키는데 유용하다.
      - 예시) 항상 UTC 기준이므로 전세계 모든 서버 시간을 똑같이 맞출 수 있음.
        - 한국에 있는 `Instant`, 미국에 있는 `Instant`의 시간이 똑같음.
  - Epoch의 뜻: 어떤 중요한 사건이 발생한 시점을 기준으로 삼는 시작점.
  - `Instant`는 바로 이 Epoch 시간을 다루는 클래스이다.

- `Instant` 사용 예시
  - 전 세계적으로 일관된 시점을 표현할 때.
    - 예시) 로그 기록, 트랜잭션 타임스탬프, 서버 간의 시간 동기화 등
  - 시간대의 변화 없이 순수하게 시간의 흐름만을 다루고 싶을 때.
    - 예시) 지속 시간 계산
  - 데이터베이스에 날짜와 시간 정보를 저장하거나, 다른 시스템과 날짜와 시간 정보를 교환할 때.
    - 모든 시스템에서 동일한 기준점(UTC)을 사용하게 되므로 데이터의 일관성을 유지하기 쉽다.

- 관련 메서드
  - `now()` : UTC를 기준 현재 시간의 `Instant`를 생성한다. 
  - `from()` : 다른 타입의 날짜와 시간을 기준으로 `Instant`를 생성한다.
    - 참고로 `Instant`는 UTC를 기준으로 하기 때문에 시간대 정보가 필요하다. 따라서 `LocalDateTime`은 사용할 수 없다.
  - `ofEpochSecond()` : 에포크 시간을 기준으로 `Instant`를 생성한다.
    - 0초를 선택하면 에포크 시간인 1970년 1월 1일 0시 0분 0초로 생성된다.
  - `plusSeconds()` : 초를 더한다.
    - 초, 밀리초, 나노초 정도만 더하는 간단한 메서드가 제공된다.
  - `getEpochSecond()`: 에포크 시간를 기준으로 흐른 초를 반환한다.
    - UTC 1970년 1월 1일 0시 0분 0초부터 얼마나 시간이 흘렀는지.
  - 예시 코드:
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/InstantMain.java

### 기간, 시간의 간격 - Duration, Period

- 시간의 개념은 크게 2가지로 표현할 수 있다.
  - 특정 시점의 시간(시각)
    - 예) "이 프로젝트는 2013년 8월 16일 까지 완료해야해."
  - 시간의 간격(기간)
    - 예) "이 프로젝트는 3개월 남았어."
    - `Period`, `Duration`은 시간의 간격(기간)을 표현하는데 사용된다.
      - `Period`: 날짜 (년, 월, 일)
      - `Duration`: 시간 (시간, 분, 초, 나노초)

- `Period`
    - 년, 월, 일 포함.
    ```java
    public class Period {
        private final int years;
        private final int months;
        private final int days;
    }
    ```
    - 관련 메서드
      - `of()` : 특정 기간을 지정해서 `Period`를 생성한다.
        - `of(년, 월, 일)`
        - `ofDays()`
        - `ofMonths()`
        - `ofYears()`
      - 계산에 사용
        - 예시) `Period`를 사용하여 특정 날짜에 10일이라는 기간을 더 할 수 있다.
      - `Period.between(startDate, endDate)`: 특정 날짜의 차이를 `Period`로 반환한다.
      - `getYears()`, `getMonths()`, `getDays()`

```java
package time;

import java.time.LocalDate;
import java.time.Period;

public class PeriodMain {

    public static void main(String[] args) {
        //생성
        Period period = Period.ofDays(10);
        System.out.println("period = " + period); //P10D

        //계산에 사용
        LocalDate currentDate = LocalDate.of(2030, 1, 1);
        LocalDate plusDate = currentDate.plus(period);
        System.out.println("currentDate = " + currentDate); //2030-01-01
        System.out.println("plusDate = " + plusDate); //2030-01-11

        //기간 차이
        LocalDate startDate = LocalDate.of(2023, 1, 1);
        LocalDate endDate = LocalDate.of(2023, 4, 2);
        Period between = Period.between(startDate, endDate);
        System.out.println("between = " + between); //P3M1D
        System.out.println("기간: " + between.getMonths() + "개월 " + between.getDays() + "일"); //3개월 1일
    }

}
```

- `Duration`
    - 시, 분, 초 포함.
    ```java
    public class Duration {
        private final long seconds;
        private final int nanos;
    }
    ```
    - 관련 메서드
      - `of()` : 특정 시간을 지정해서 `Duration`를 생성한다. 
        - `of(지정)`
        - `ofSeconds()`
        - `ofMinutes()`
        - `ofHours()`
      - 계산에 사용
        - `Duration`를 사용하여 특정 시간에 30분이라는 시간(시간의 간격)을 더할 수 있다.
      - `Duration.between(start, end)`: 특정 시간의 차이를 `Duration`으로 반환한다.
      - `getSeconds()`, `getNano()`와 `toHours()`, `toMinutes()`
        - `Duration`은 내부에서 초를 기반으로 계산해서 사용한다. 
          - 그래서 시, 분에 대한 메서드명이 특이함!
    - 참고
      - 1분 = 60초
      - 1시간 = 3600초 (60분 x 60초)

```java
package time;

import java.time.Duration;
import java.time.LocalTime;

public class DurationMain {

    public static void main(String[] args) {
        Duration duration = Duration.ofMinutes(30);
        System.out.println("duration = " + duration); //PT30M

        LocalTime lt = LocalTime.of(1, 0);
        System.out.println("lt = " + lt); //01:00

        //계산에 사용
        LocalTime plusTime = lt.plus(duration);
        System.out.println("더한 시간: " + plusTime); //01:30

        //시간 차이
        LocalTime start = LocalTime.of(9, 0);
        LocalTime end = LocalTime.of(10, 0);
        Duration between = Duration.between(start, end);
        System.out.println("차이: " + between.getSeconds() + "초"); //3600초
        System.out.println("근무 시간: " + between.toHours() + "시간" + between.toMinutesPart() + "분"); //1시간0분
    }
}
```

### 날짜와 시간의 핵심 인터페이스

![날짜와 시간의 핵심 인터페이스](https://github.com/user-attachments/assets/20def9e5-e794-4e5e-a63a-04cf97d1c173)

- 날짜와 시간은 2가지로 나눌 수 있다.
  - 특정 시점의 시간 (시각)
    - `Temporal` (`TemporalAccessor`포함) 인터페이스를 구현한다.
      - `TemporalAccessor` : 조회용 기능 제공
      - `Temporal` : 조회 & 조작용 기능 제공
    - 구현: `LocalDateTime`, `LocalDate`, `LocalTime`, `ZonedDateTime` , `OffsetDateTime`, `Instant` 등
    - 참고) 인터페이스끼리는 상속관계이다.
  - 시간의 간격 (기간)
    - `TemporalAmount` 인터페이스를 구현한다.
      - 시간의 양을 나타내고, 특정 날짜에 일정 기간을 더하거나 빼는 데 사용된다.
    - 구현: `Period`, `Duration`

![시간의 단위와 시간 필드](https://github.com/user-attachments/assets/9af9fbcc-2d56-4e19-84fa-e9937020ba74)

- 시간의 단위(`TemporalUnit`, `ChronoUnit`)와 시간 필드(`TemporalField`, `ChronoField`)
  - ✅ 단독으로 사용하기 보다는 주로 날짜와 시간을 조회하거나 조작할 때 사용한다.
  - ✅ 차이점
    - 시간의 단위(`TemporalUnit`, `ChronoUnit`)
      - 단순히 날짜나 시간을 나타낸다.
    - 시간 필드(`TemporalField`, `ChronoField`)
      - ⭐ 날짜나 시간의 특정 필드를 나타낸다.
  - ✅ 시간의 단위 - `TemporalUnit`, `ChronoUnit`
    - `TemporalUnit` 인터페이스는 날짜와 시간을 측정하는 단위를 나타내며,
    - 주로 사용되는 구현체는 `java.time.temporal.ChronoUnit` 열거형으로 구현되어 있다.
    - `ChronoUnit`은 다양한 시간 단위를 제공한다.
      - 시간 단위
        - `ChronoUnit.NANOS`: 나노초
        - `ChronoUnit.MICROS`: 마이크로초
        - `ChronoUnit.MILLIS`: 밀리초
        - `ChronoUnit.SECONDS`: 초 ✔️
        - `ChronoUnit.MINUTES`: 분 ✔️
        - `ChronoUnit.HOURS`: 시간 ✔️
      - 날짜 단위
        - `ChronoUnit.DAYS`: 일 ✔️
        - `ChronoUnit.WEEKS`: 주 ✔️
        - `ChronoUnit.MONTHS`: 월 ✔️
        - `ChronoUnit.YEARS`: 년 ✔️
        - `ChronoUnit.DECADES`: 10년
        - `ChronoUnit.CENTURIES`: 세기
        - `ChronoUnit.MILLENNIA`: 천년
      - 기타 단위
        - `ERAS`: 시대
        - `FOREVER`: 무한대
    - `ChronoUnit` 주요 메서드
      - `between(Temporal, Temporal)`: 두 `Temporal` 객체 사이의 시간을 현재 `ChronoUnit` 단위로 측정하여 반환한다.
      - `isDateBased()`: 현재 `ChronoUnit`이 날짜 기반 단위인지 (예: 일, 주, 월, 년) 여부를 반환한다.
      - `isTimeBased()`: 현재 `ChronoUnit`이 시간 기반 단위인지 (예: 시, 분, 초) 여부를 반환한다.
      - `isSupportedBy(Temporal)`: 주어진 `Temporal` 객체가 현재 `ChronoUnit` 단위를 지원하는지 여부를 반환한다.
      - `getDuration()`: 현재 `ChronoUnit`의 기간을 `Duration` 객체로 반환한다.
    - 예제코드:
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/ChronoUnitMain.java
  - ✅ 시간 필드 - `TemporalField`, `ChronoField`
    - `TemporalField` 인터페이스는 날짜와 시간을 나타내는데 사용된다.
    - 주로 사용되는 구현체는 `java.time.temporal.ChronoField` 열거형으로 구현되어 있다.
      - ⭐ `ChronoField`는 다양한 필드를 통해 날짜와 시간의 특정 부분을 나타낸다. 
          - 여기서 필드(`Field`)라는 뜻이 날짜와 시간 중에 있는 특정 필드들을 뜻한다.
          - 예시) 2024년 8월 16일이라고 하면 각각의 필드는 다음과 같다.
            - `YEAR`: 2024
            - `MONTH_OF_YEAR`: 8
            - `DAY_OF_MONTH`: 16
          - 단순히 시간의 단위 하나하나를 뜻하는 `ChronoUnit`과는 다른 것을 알 수 있다.
            - `ChronoField`를 사용해야 날짜와 시간의 각 필드 중에 원하는 데이터를 조회할 수 있다.
    - `ChronoField`의 필드
      - 연도 관련 필드
        - `ERA`: 연대, 예를 들어 서기(AD) 또는 기원전(BC)
        - `YEAR_OF_ERA`: 연대 내의 연도
        - `YEAR`: 연도
        - `EPOCH_DAY`: 1970-01-01부터의 일 수
      - 월 관련 필드
        - `MONTH_OF_YEAR`: 월 (1월 = 1) ✔️
        - `PROLEPTIC_MONTH`: 연도를 월로 확장한 값
      - 주 및 일 관련 필드
        - `DAY_OF_WEEK`: 요일 (월요일 = 1)
        - `ALIGNED_DAY_OF_WEEK_IN_MONTH`: 월의 첫 번째 요일을 기준으로 정렬된 요일
        - `ALIGNED_DAY_OF_WEEK_IN_YEAR`: 연의 첫 번째 요일을 기준으로 정렬된 요일
        - `DAY_OF_MONTH`: 월의 일 (1일 = 1) ✔️
        - `DAY_OF_YEAR`: 연의 일 (1월 1일 = 1)
        - `EPOCH_DAY`: 유닉스 에폭(1970-01-01)부터의 일 수
      - 시간 관련 필드
        - `HOUR_OF_DAY`: 시간 (0-23)
        - `CLOCK_HOUR_OF_DAY`: 시계 시간 (1-24)
        - `HOUR_OF_AMPM`: 오전/오후 시간 (0-11)
        - `CLOCK_HOUR_OF_AMPM`: 오전/오후 시계 시간 (1-12)
        - `MINUTE_OF_HOUR `: 분 (0-59)
        - `SECOND_OF_MINUTE`: 초 (0-59)
        - `NANO_OF_SECOND`: 초의 나노초 (0-999,999,999)
        - `MICRO_OF_SECOND`: 초의 마이크로초 (0-999,999)
        - `MILLI_OF_SECOND`: 초의 밀리초 (0-999)
      - 기타 필드
        - `AMPM_OF_DAY`: 하루의 AM/PM 부분
        - `INSTANT_SECONDS`: 초를 기준으로 한 시간
        - `OFFSET_SECONDS`: UTC/GMT에서의 시간 오프셋 초
    - `ChronoField`의 주요 메서드
      - `getBaseUnit()`: 필드의 기본 단위를 반환한다.
        - 예) 분 필드의 기본 단위는 `ChronoUnit.MINUTES`이다.
      - `getRangeUnit()`: 필드의 범위 단위를 반환한다.
        - 예) `MONTH_OF_YEAR`의 범위 단위는 `ChronoUnit.YEARS`이다.
      - `isDateBased()`: 필드가 주로 날짜를 기반으로 하는지 여부를 나타낸다.
        - 예) `YEAR`와 같은 날짜 기반 필드는 `true`를 반환한다.
      - `isTimeBased()`: 필드가 주로 시간을 기반으로 하는지 여부를 나타낸다.
        - 예) `HOUR_OF_DAY`와 같은 시간 기반 필드는 `true`를 반환한다.
      - `range()`: 필드가 가질 수 있는 값의 유효 범위를 `ValueRange` 객체로 반환한다. ✔️
        - 객체는 최소값과 최대값을 제공한다.
    - 예제코드:
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/ChronoFieldMain.java
    
### 날짜와 시간 조회하고 조작하기1

- 날짜와 시간 조회하기
  - 날짜와 시간을 조회하려면, 날짜와 시간 항목중에 어떤 필드를 조회할 지 선택해야 한다.
    - 이때 날짜와 시간의 필드를 뜻 하는 `ChronoField`가 사용된다.
  - 편의 메서드를 사용 하면 편하다.
      - 예) `dt.get(ChronoField.DAY_OF_MONTH))` --> `dt.getDayOfMonth()`
    - 자주 사용하지 않는 기능은 편의 메서드를 제공하지 않는다.

```java
package time;

import java.time.LocalDateTime;
import java.time.temporal.ChronoField;

public class GetTimeMain {

    public static void main(String[] args) {
        LocalDateTime dt = LocalDateTime.of(2030, 1, 1, 13, 30, 59);
        
        System.out.println("YEAR = " + dt.get(ChronoField.YEAR)); //2030
        System.out.println("MONTH_OF_YEAR = " + dt.get(ChronoField.MONTH_OF_YEAR)); //1
        System.out.println("DAY_OF_MONTH = " + dt.get(ChronoField.DAY_OF_MONTH)); //1
        System.out.println("HOUR_OF_DAY = " + dt.get(ChronoField.HOUR_OF_DAY)); //13
        System.out.println("MINUTE_OF_HOUR = " + dt.get(ChronoField.MINUTE_OF_HOUR)); //30
        System.out.println("SECOND_OF_MINUTE = " + dt.get(ChronoField.SECOND_OF_MINUTE)); //59

        System.out.println("편의 메서드 제공");
        System.out.println("YEAR = " + dt.getYear()); //2030
        System.out.println("MONTH_OF_YEAR = " + dt.getMonthValue()); //1
        System.out.println("DAY_OF_MONTH = " + dt.getDayOfMonth()); //1
        System.out.println("HOUR_OF_DAY = " + dt.getHour()); //13
        System.out.println("MINUTE_OF_HOUR = " + dt.getMinute()); //30
        System.out.println("SECOND_OF_MINUTE = " + dt.getSecond()); //59

        System.out.println("편의 메서드에 없음");
        System.out.println("MINUTE_OF_DAY = " + dt.get(ChronoField.MINUTE_OF_DAY)); //810
        System.out.println("SECOND_OF_DAY = " + dt.get(ChronoField.SECOND_OF_DAY)); //48659
    }
}
```

- 날짜와 시간 조작하기
  - 날짜와 시간을 조작하려면, 어떤 시간 단위(Unit)를 변경할 지 선택해야 한다.
    - 이때 날짜와 시간의 단위를 뜻하는 `ChronoUnit`이 사용된다.
  - 편의 메서드를 사용 하면 편하다.
    - `dt.plus(10, ChronoUnit.YEARS)` --> `dt.plusYears(10)`
  - 참고로 `minus()`도 존재한다.

```java
package time;

import java.time.LocalDateTime;
import java.time.Period;
import java.time.temporal.ChronoUnit;

public class ChangeTimePlusMain {

    public static void main(String[] args) {
        LocalDateTime dt = LocalDateTime.of(2018, 1, 1, 13, 30, 59);
        System.out.println("dt = " + dt); //2018-01-01T13:30:59

        LocalDateTime plusDt1 = dt.plus(10, ChronoUnit.YEARS);
        System.out.println("plusDt1 = " + plusDt1); //2028-01-01T13:30:59

        LocalDateTime plusDt2 = dt.plusYears(10);
        System.out.println("plusDt2 = " + plusDt2); //2028-01-01T13:30:59

        Period period = Period.ofYears(10);
        LocalDateTime plusDt3 = dt.plus(period);
        System.out.println("plusDt3 = " + plusDt3); //2028-01-01T13:30:59
    }
}
```

- 정리
  - 특정 구현 클래스와 무관하게 아주 일관성 있는 시간 조회, 조작 기능을 제공한다.
    - `TemporalAccessor.get()`, `Temporal.plus()`와 같은 인터페이스 덕분.
  - 하지만 모든 시간 필드를 다 조회할 수 있는 것은 아니다.
    - 예시) `LocalDate`는 날짜 정보만 가지고 있는데, 분에 접근 하는 경우.
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/IsSupportedMain1.java
  - 이런 문제를 예방하기 위해 인터페이스는 현재 타입에서 특정 시간 단위나 필드를 사용할 수 있는지 확인할 수 있는 메서드를 제공한다.
    - `TemporalAccessor` 인터페이스
      - `boolean isSupported(TemporalField field);`
    - `Temporal` 인터페이스
      - `boolean isSupported(TemporalUnit unit);`
    - 예시)
      - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/IsSupportedMain2.java

### 날짜와 시간 조회하고 조작하기2

- 날짜와 시간을 조작하는 `with()` 메서드
  - `Temporal.with()`를 사용하면 날짜와 시간의 특정 필드의 값만 변경할 수 있다.
  - 자주 사용하는 메서드는 편의 메서드가 제공된다.
    - `dt.with(ChronoField.YEAR, 2020)` --> `dt.withYear(2020)`
    - `with()` 는 아주 단순한 날짜만 변경할 수 있다.
  - 복잡한 날짜는 `TemporalAdjuster`를 사용하면 된다.
    - 예시) 다음 금요일, 이번 달의 마지막 일요일
    - 자바는 이미 필요한 구현체들을 `TemporalAdjusters`에 다 만들어두었다.
      - 우리는 단순히 구현체들을 모아둔 `TemporalAdjusters`를 사용하면 된다.

```java
package time;

import java.time.DayOfWeek;
import java.time.LocalDateTime;
import java.time.temporal.ChronoField;
import java.time.temporal.TemporalAdjusters;

public class ChangeTimeWithMain {

    public static void main(String[] args) {
        LocalDateTime dt = LocalDateTime.of(2018, 1, 1, 13, 30, 59);
        System.out.println("dt = " + dt); //2018-01-01T13:30:59

        LocalDateTime changedDt1 = dt.with(ChronoField.YEAR, 2020);
        System.out.println("changedDt1 = " + changedDt1); //2020-01-01T13:30:59

        LocalDateTime changedDt2 = dt.withYear(2020);
        System.out.println("changedDt2 = " + changedDt2); //2020-01-01T13:30:59

        //TemporalAdjuster 사용
        //다음주 금요일
        LocalDateTime with1 = dt.with(TemporalAdjusters.next(DayOfWeek.FRIDAY));
        System.out.println("기준 날짜: " + dt); //2018-01-01T13:30:59
        System.out.println("다음 금요일: " + with1); //2018-01-05T13:30:59

        //이번 달의 마지막 일요일
        LocalDateTime with2 = dt.with(TemporalAdjusters.lastInMonth(DayOfWeek.SUNDAY));
        System.out.println("같은 달의 마지막 일요일 = " + with2); //2018-01-28T13:30:59
    }
}
```

- `DayOfWeek`
  - 월, 화, 수, 목, 금, 토, 일을 나타내는 열거형.

- `TemporalAdjusters` 클래스가 제공하는 주요 기능
  - `dayOfWeekInMonth`: 주어진 요일이 몇 번째인지에 따라 날짜를 조정한다.
  - `firstDayOfMonth`: 해당 월의 첫째 날로 조정한다.
  - `firstDayOfNextMonth`: 다음 달의 첫째 날로 조정한다.
  - `firstDayOfNextYear`: 다음 해의 첫째 날로 조정한다.
  - `firstDayOfYear`: 해당 해의 첫째 날로 조정한다.
  - `firstInMonth`: 주어진 요일 중 해당 월의 첫 번째 요일로 조정한다.
  - `lastDayOfMonth`: 해당 월의 마지막 날로 조정한다.
  - `lastDayOfNextMonth`: 다음 달의 마지막 날로 조정한다.
  - `lastDayOfNextYear`: 다음 해의 마지막 날로 조정한다.
  - `lastDayOfYear`: 해당 해의 마지막 날로 조정한다.
  - `lastInMonth`: 주어진 요일 중 해당 월의 마지막 요일로 조정한다. ✔️
  - `next`: 주어진 요일 이후의 가장 가까운 요일로 조정한다. ✔️
  - `nextOrSame`: 주어진 요일 이후의 가장 가까운 요일로 조정하되, 현재 날짜가 주어진 요일인 경우 현재 날짜를 반환한다. ✔️
  - `previous`: 주어진 요일 이전의 가장 가까운 요일로 조정한다.
  - `previousOrSame`: 주어진 요일 이전의 가장 가까운 요일로 조정하되, 현재 날짜가 주어진 요일인 경우 현재 날짜를 반환한다.

### 날짜와 시간 문자열 파싱과 포맷팅

- 정의
  - 포맷팅: `Date` --> `String`로 변경하는 것
  - 파싱: `String` --> `Date`로 변경하는 것

- 예시1) 날짜만.

```java
package time;

import java.time.LocalDate;
import java.time.format.DateTimeFormatter;

public class FormattingMain1 {

    public static void main(String[] args) {
        // 포맷팅: 날짜를 문자로
        LocalDate date = LocalDate.of(2024, 12, 31);
        System.out.println("date = " + date); //2024-12-31
        DateTimeFormatter formatter = DateTimeFormatter.ofPattern("yyyy년 MM월 dd일");
        String formattedDate = date.format(formatter);
        System.out.println("날짜와 시간 포맷팅 = " + formattedDate); //2024년 12월 31일

        // 파싱: 문자를 날짜로
        String input = "2030년 01월 01일";
        LocalDate parsedDate = LocalDate.parse(input, formatter);
        System.out.println("문자열 파싱 날짜와 시간: " + parsedDate); //2030-01-01
    }
}
```

- 예시2) 시간 포함.
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/FormattingMain2.java

- `DateTimeFormatter` 패턴
  - 교재 참고 (p.41)
  - or 공식사이트
    - https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#patterns

### 문제와 풀이

- 문제1 - 날짜 더하기
  - 2024년 1월 1일 0시 0분 0초에 1년 2개월 3일 4시간 후의 시각을 찾아라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestPlus.java
- 문제2 - 날짜 간격 반복 출력하기
  - 2024년 1월 1일 부터 2주 간격으로 5번 반복하여 날짜를 출력해라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestLoopPlus.java
- 문제3 - 디데이 구하기
  - 시작 날짜와 목표 날짜를 입력해서 남은 기간과 디데이를 구해라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestBetween.java
- 문제4 - 시작 요일, 마지막 요일 구하기
  - 입력 받은 월의 첫날 요일과 마지막날 요일을 구해라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestAdjusters.java
- 문제5 - 국제 회의 시간
  - 서울의 회의 시간은 2024년 1월 1일 오전 9시다. 이때 런던, 뉴욕의 회의 시간을 구해라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestZone.java
- 문제6 - 달력 출력하기 ⭐
  - 입력한 년 & 월에 맞춰 달력을 출력해라.
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/time/test/TestCalendarPrinterAnswer.java

---

## 8. 중첩 클래스, 내부 클래스1

### 중첩 클래스, 내부 클래스란?

- 중첩 클래스?
  - 클래스 안에 클래스를 정의하는 것

    ```java
    class Outer {
        ...
        
        class Nested { //중첩 클래스
            ...
        }
    }
    ```

- 중첩 클래스 종류
  - 크게 2가지로 분류한다.
    - `정적 중첩 클래스`
      - 바깥 클래스의 안에 있지만, 바깥 클래스와 관계 없는 전혀 다른 클래스다.
    - `내부 클래스`
      - 바깥 클래스의 인스턴스 내부에서 구성 요소로 사용된다.
  - 세부적으론 4가지로 분류한다.
    - `정적 중첩 클래스`
    - `내부 클래스`
    - `지역 클래스` 
    - `익명 클래스`
  - 클래스를 정의하는 위치에 따라 분류한다.

![중첩 클래스 종류](https://github.com/user-attachments/assets/1fd34553-d814-4324-97c6-20842efd3f46)

- 중첩 클래스는 언제 사용?
    - 특정 클래스가 하나의 클래스 안에서만 사용되거나, 둘이 아주 긴밀하게 연결되어 있는 특별한 경우에만 사용해야 한다.

- 중첩 클래스를 사용하는 이유?
  - 논리적 그룹화
    - 특정 클래스가 다른 하나의 클래스 안에서만 사용되는 경우 해당 클래스 안에 포함하는 것이 논리적으로 더 그룹화 된다.
    - 패키지를 열었을 때, 다른 곳에서 사용될 필요가 없는 중첩 클래스가 외부에 노출되지 않는다.
  - 캡슐화
    - 불필요한 `public` 메서드를 제거할 수 있다.
      - 중첩 클래스는 바깥 클래스의 `private` 멤버에 접근할 수 있기 때문.

### 정적 중첩 클래스

```java
package nested.nested;

public class NestedOuter { // 바깥 클래스

    private static int outClassValue = 3;
    private int outInstanceValue = 2;

    static class Nested { // 정적 중첩 클래스 ⭐
        private int nestedInstanceValue = 1;

        public void print() {
            // 자신의 멤버에 접근
            System.out.println(nestedInstanceValue); //1

            // 바깥 클래스의 인스턴스 멤버에 접근에는 접근할 수 없다.
            //System.out.println(outInstanceValue);

            // 바깥 클래스의 클래스 멤버에는 접근할 수 있다. private도 접근 가능
            System.out.println(NestedOuter.outClassValue); //NestedOuter 없이 써도 됨. //3
        }
    }
}
```

- 정적 중첩 클래스
  - 앞에 `static`이 붙는다.
  - 바깥 클래스의 인스턴스 멤버에는 접근할 수 없다.
   
    ![바깥 클래스의 멤버에 접근](https://github.com/user-attachments/assets/c5fb9e22-a87f-4dca-a6b5-3929133238af)
  
  - 바깥 클래스 생성없이, 정적 중첩 클래스의 인스턴스만 따로 생성해도 된다.

```java
package nested.nested;

public class NestedOuterMain {

    public static void main(String[] args) {
        //NestedOuter outer = new NestedOuter(); //바깥 클래스 생성 안해도 됨.
        NestedOuter.Nested nested = new NestedOuter.Nested(); //정적 중첩 클래스의 인스턴스 생성
        nested.print();

        System.out.println("nestedClass = " + nested.getClass()); //class nested.nested.NestedOuter$Nested
        //중첩 클래스의 이름은 "바깥 클래스 이름" + "$" + "중첩 클래스 이름" 으로 구성된다. --> NestedOuter$Nested
    }
}
```

### 정적 중첩 클래스의 활용

![정적 중첩 클래스 리팩토링](https://github.com/user-attachments/assets/e6207441-27e6-4445-b843-6f63a4829dff)

- `ex1`를 `ex2`처럼 리팩토링 했다.
  - `ex1`을 열어본 개발자는 `Network`와 `NetworkMessage`를 둘다 사용해야하나 의문이 든다.
    - 코드를 다 읽어보아야 한다.
    - 실제로는 `NetworkMessage`가 `Network`에서만 쓰인다.
  - `ex2`에서는 `NetworkMessage`를 `Network`안에 넣었다.
    - 개발자는 한눈에 `Network`만 사용하면 된다는 걸 `ex2`를 열자마자 인지할 수 있다.
  - 실제 코드:
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/nested/ex2/Network.java

### 내부 클래스

```java
package nested.inner;

public class InnerOuter { // 바깥 클래스

    private static int outClassValue = 3;
    private int outInstanceValue = 2;

    class Inner { // 내부 클래스 ⭐
        private int innerInstanceValue = 1;

        public void print() {
            // 자기 자신에 접근
            System.out.println(innerInstanceValue); //1

            // 외부 클래스의 인스턴스 멤버에 접근 가능, private도 접근 가능
            System.out.println(outInstanceValue); //2

            // 외부 클래스의 클래스 멤버에 접근 가능, private도 접근 가능
            System.out.println(outClassValue); //3
        }
    }
}
```

```java
package nested.inner;

public class InnerOuterMain {

    public static void main(String[] args) {
        InnerOuter outer = new InnerOuter(); 
        InnerOuter.Inner inner = outer.new Inner(); //내부 클래스를 생성할 때, 바깥 클래스의 인스턴스 참조가 필요하다.
        inner.print();

        System.out.println("innerClass = " + inner.getClass()); //class nested.inner.InnerOuter$Inner
    }
}
```

- 내부 클래스
  - 내부 클래스는 바깥 클래스의 인스턴스에 소속된다.
    - 내부 클래스를 생성할 때, 바깥 클래스의 인스턴스 참조가 필요하다.

- 내부 클래스 메모리 구조
  - `개념`상 인스턴스 안에 생성된다고 이해하면 충분하지만,
  - `실제`로 내부 인스턴스가 바깥 인스턴스 안에 생성되는 것은 아니다.

| 개념                                                                                                | 실제                                                                                                |
|---------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| ![내부 클래스의 생성_개념](https://github.com/user-attachments/assets/d65de71e-6b0b-45ba-bb6b-6c20649af586) | ![내부 클래스의 생성_실제](https://github.com/user-attachments/assets/1d52c93b-b3ca-44f6-9a9f-4b07431ef85b) |

### 내부 클래스의 활용

![내부 클래스 리팩토링](https://github.com/user-attachments/assets/f7a8b8fc-03a8-4bfa-9220-86b68a25538c)

- `ex1`를 `ex2`처럼 리팩토링 했다.
  - `ex1`에서 `Engine`과 `Car`가 분리되어 있어서, 어쩔수 없이 `public`으로 노출해야하는 메서드가 있었는데,
  - `ex2`에서 `Engine`을 `Car`에 내부클래스로 넣어서, 꼭 필요한 메서드만 외부에 노출시키게 하였다. 
    - 캡슐화를 높임!
  - 실제 코드:
    - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/inner/ex2/Car.java

### 같은 이름의 바깥 변수 접근

- 바깥 클래스와 내부 클래스의 변수 이름이 같으면?
  - 가까운 범위가 우선순위를 갖는다.
    - 지역변수 > 내부 클래스의 인스턴스 변수 > 바깥 클래스의 인스턴스 변수
    - 이렇게 다른 변수들을 가려서 보이지 않게 하는 것을 `섀도잉(Shadowing)`이라 한다.
  - 처음부터 이름을 서로 다르게 지어서 명확하게 구분하는 것이 더 나은 방법이다.
- 관련 코드:
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/ShadowingMain.java

---

## 9. 중첩 클래스, 내부 클래스2

### 지역 클래스 - 시작

- 지역 클래스(Local class)는 내부 클래스의 특별한 종류의 하나이다.
  - 따라서 내부 클래스의 특징을 그대로 가진다.

```java
package nested.local;

public class LocalOuterV2 { //바깥 클래스

    private int outInstanceVar = 3; //바깥 클래스의 인스턴스 멤버

    public void process(int paramVar) { //자신이 속한 코드 블럭의 매개변수. //매개변수도 지역 변수의 한 종류이다.
        int localVar = 1; //자신이 속한 코드 블럭의 지역 변수

        class LocalPrinter implements Printer { //지역 클래스⭐ //인터페이스를 구현할 수 있다.

            int value = 0; //자신의 인스턴스 변수

            @Override
            public void print() {
                System.out.println("value = " + value); //0
                System.out.println("localVar = " + localVar); //1
                System.out.println("paramVar = " + paramVar); //2
                System.out.println("outInstanceVar = " + outInstanceVar); //3
            }
        }

        LocalPrinter printer = new LocalPrinter();
        printer.print();
    }

    public static void main(String[] args) {
        LocalOuterV2 localOuter = new LocalOuterV2();
        localOuter.process(2);
    }
}
```

```java
package nested.local;

public interface Printer {
    void print();
}
```

### 지역 클래스 - 지역 변수 캡처

- 지역 변수 캡처
  - 너무 깊이있게 이해하지 않아도 된다.
  - `지역 클래스가 접근하는 지역 변수의 값은 변경하면 안된다` 정도로 이해하면 충분하다.
- 예제 코드:
  - 비공개 레포지토리: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/local/LocalOuterV3.java
  - 문제점: 제거된 지역변수(`paramVar`, `localVar`)에 접근할 수 없어야 하는데, 왜 잘 실행되나?...
  
    ![지역 변수 캡쳐](https://github.com/user-attachments/assets/883ff0f0-770e-4421-b82c-e3c7c6dc6b2d)

  - 실제: 캡처한 지역변수를 사용한다.

    ![지역 변수 캡쳐_실제](https://github.com/user-attachments/assets/dc675392-4165-4737-97e6-8de4cd6475e8)

  - 캡처 변수의 값을 변경하지 못하는 이유
    - 캡처 변수의 값을 변경하면 여러 문제들이 파생될 수 있다.
    - 자바는 캡처한 지역 변수의 값을 변하지 못하게 막아서 이런 복잡한 문제들을 근본적으로 차단한다.
    - 자세한 내용은 교재 참고 (p.14) 

- 정리
  - 지역 클래스는 인스턴스를 생성할 때, 필요한 지역 변수를 먼저 캡처해서 인스턴스에 보관한다.
  - 지역 변수에 접근하면, 실제로는 지역 변수에 접근하는 것이 아니라 인스턴스에 있는 캡처한 캡처 변수에 접근한다.
  
### 익명 클래스 - 시작

- 익명 클래스(anonymous class)
  - 이름이 없는 지역 클래스이다.
  - 클래스의 선언과 생성을 한번에 처리할 수 있다. 코드가 간결해진다.
  - 복잡하거나 재사용이 필요한 경우에는 익명 클래스가 아닌, 별도의 클래스를 정의하는 것이 좋다.
  - 익명 클래스는 부모 클래스를 상속 받거나, 또는 인터페이스를 구현해야 한다.

```java
package nested.anonymous;

import nested.local.Printer;

public class AnonymousOuter { //바깥 클래스

    private int outInstanceVar = 3;

    public void process(int paramVar) {

        int localVar = 1;

        Printer printer = new Printer() { //익명클래스
            // 인터페이스를 생성하는 것이 아니고, 인터페이스를 구현한 익명 클래스를 생성하는 것이다.
            
            int value = 0;

            @Override
            public void print() {
                System.out.println("value = " + value); //0
                System.out.println("localVar = " + localVar); //1
                System.out.println("paramVar = " + paramVar); //2
                System.out.println("outInstanceVar = " + outInstanceVar); //3
            }
        };

        printer.print();
        System.out.println("printer.class=" + printer.getClass()); //class nested.anonymous.AnonymousOuter$1
        //바깥 클래스 이름 + $ + 숫자로 정의된다. (AnonymousOuter$1)
    }

    public static void main(String[] args) {
        AnonymousOuter localOuter = new AnonymousOuter();
        localOuter.process(2);
    }
}
```

### 익명 클래스 활용

- 공통 메서드를 만들어 중복을 제거.
  - 변하지 않는 부분은 공통메서드에 넣고, 변하는 부분만 외부로 부터 메서드의 인수로 받아서 처리한다.
    - 예제 1) 인자가 문자열인 경우
      - 비공개 레포지토리:
        - 리팩토링 전: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex0Main.java
        - 리팩토링 후: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex0RefMain.java
    - 예제 2) 인자가 코드 조각인 경우
      - 메서드를 바로 전달 할 수 없다.
        - 대신에 인스턴스를 전달하고, 인스턴스에 있는 메서드를 호출하면 된다.
      - 비공개 레포지토리:
        - 리팩토링 전: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1Main.java
        - 리팩토링 후
          - 1번) 중첩 클래스 사용: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1RefMainV1.java
          - 2번) 지역 클래스 사용: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1RefMainV2.java
          - 3번) 익명 클래스 사용1: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1RefMainV3.java
          - 4번) 익명 클래스 사용2: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1RefMainV4.java
            - 익명 클래스의 참조값을 변수에 담아둘 필요 없이, 인수로 바로 전달할 수 있다.
          - 5번) 람다(Lambda) 사용: https://github.com/JohnKim0911/kyh_java-mid1/blob/master/src/nested/anonymous/ex/Ex1RefMainV5.java
            - 클래스나 인스턴스를 정의하지 않고, 메서드(더 정확히는 함수)의 코드 블럭을 직접 전달할 수 있다.
            - 람다에 대한 자세한 내용은 나중에 별도로 다룬다.

### 문제와 풀이

- 도서 관리 시스템
  - 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/nested/nested/test/ex1

---

## 10. 예외 처리1 - 이론

### 예외 처리가 필요한 이유

- 예제를 통해 알아본다.
  - 사용자의 입력을 받고, 입력 받은 문자를 외부 서버에 전송하는 프로그램
    
![예외 처리가 필요한 이유_예제](https://github.com/user-attachments/assets/3c9d3b92-bf87-45de-947e-b952db889c67)

- 실제 코드 (비공개 레포지토리):
  - 한 가지의 예제를 점진적으로 바꾸어본다.
    - 참고) 이 코드는 하나하나 다시 안읽어봐도 된다. 
      - 예외를 왜 써야하는지 빌드업을 위한 코드임!
    - 제일 처음 코드:
      - https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex0
    - `NetworkService`을 `V1_1` --> `V1_2` --> `V1_3` 으로 리팩토링:
      - https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex1
- 결론
  - 정상 흐름과 예외 흐름이 섞여 있어서 코드를 한눈에 이해하기 어렵다.
      - 반환 값을 사용해서 예외 상황을 처리하는 방식으로는 해결 할 수 없다.
  - 자바가 제공하는 **예외 처리** 메커리즘을 사용하자.

### 자바 예외 처리1 - 예외 계층

- 예외 처리 키워드
  - `try`, `catch`, `finally`, `throw`, `throws`

- 예외 처리용 객체
  - `Object`: 예외도 객체이다. 예외의 최상위 부모도 `Object`이다.
  - `Throwable` : 최상위 예외이다.
    - 하지만, 여기서 예외를 잡으면 안된다. (`Error`도 같이 잡히기 때문.)
  - `Error` : 메모리 부족이나 심각한 시스템 오류와 같이 애플리케이션에서 복구가 불가능한 시스템 예외이다.
    - 애플리케이션 개발자는 이 예외를 잡으려고 해서는 안된다.
  - `Exception` ⭐: 체크 예외 
    - 애플리케이션 로직에서 사용할 수 있는 **실질적인 최상위 예외**이다.
    - `Exception`과 그 하위 예외는 모두 컴파일러가 체크하는 체크 예외이다. (`RuntimeException`은 예외)
  - `RuntimeException` ⭐: 언체크 예외, 런타임 예외 
    - 컴파일러가 체크 하지 않는 언체크 예외이다.

![예외 계층 그림](https://github.com/user-attachments/assets/ea62045a-d5dd-446c-8c1b-a63bc20b0fd1)

- 체크 예외 vs 언체크 예외(런타임 예외)
  - 체크 예외
    - 개발자가 발생한 예외를 명시적으로 처리해야 한다.
    - 안하면 컴파일 오류 발생
  - 언체크 예외
    - 개발자가 발생한 예외를 명시적으로 처리하지 않아도 된다.
    - 컴파일러가 예외를 체크하지 않는다.
  
### 자바 예외 처리2 - 예외 기본 규칙

- 예외는 잡아서 처리하거나 밖으로 던져야 한다.
- 예외를 잡거나 던질 때 지정한 예외뿐만 아니라 그 예외의 자식들도 함께 처리할 수 있다. (다형성 적용)

### 자바 예외 처리3 - 체크 예외

- 예제코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/basic/checked
  - 예외 클래스를 만들려면 예외를 상속 받으면 된다. (`MyCheckedException.java`)
    - `Exception`을 상속받으면 체크 예외가 된다.
  - `throw new 예외명` 라고 하면 새로운 예외를 발생시킬 수 있다. (`Client.java`)
    - 예외도 객체이기 때문에 객체를 먼저 `new`로 생성하고 예외를 발생시켜야 한다.
  - `try` & `catch` 로 예외를 잡아서 처리하거나, `throws`로 예외를 던질 수 있다. (`Service.java`)
  - 예외가 `main()` 밖으로 던져지면, 예외 정보와 스택 트레이스(Stack Trace)를 출력하고 프로그램이 종료된다.

- 체크 예외의 장단점
  - 장점
    - 개발자가 실수로 예외를 누락하지 않도록 컴파일러를 통해 문제를 잡아준다.
  - 단점
    - 개발자가 모든 체크 예외를 반드시 잡거나 던지도록 처리해야 하기 때문에 번거롭다.
    - 크게 신경쓰고 싶지 않은 예외까지 모두 챙겨야 한다.

### 자바 예외 처리4 - 언체크 예외

- 체크 예외 VS 언체크 예외
  - 기본적으로 동일하다.
  - 차이점: 예외를 처리할 수 없을 때 예외를 밖으로 던지는 부분에 있다.
    - 체크 예외: `throws` 예외를 필수로 선언해야 된다.
    - 언체크 예외: `throws` 예외를 선언하지 않아도 된다.

- 예제코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/basic/unchecked
  - `RuntimeException`을 상속받은 예외는 언체크 예외가 된다. (`MyUncheckedException.java`)
  - 언체크 예외는 체크 예외와 다르게 `throws` 예외를 선언하지 않아도 된다. (`Service.java`, `Client.java`)
    - 참고) 언체크 예외는 주로 생략하지만, 중요한 예외의 경우 넣기도 한다.
      - 해당 코드를 호출하는 개발자가 이런 예외가 발생한다는 점을 인지할 수 있다.

- 언체크 예외의 장단점
  - 장점
    - 신경쓰고 싶지 않은 언체크 예외를 무시할 수 있다.
  - 단점
    - 개발자가 실수로 예외를 누락할 수 있다.

- 참고) 요즘 개발에서는 체크예외가 아닌, 언체크 예외를 사용하는 추세이다.

---

## 11. 예외 처리2 - 실습

### 예외 처리 도입

- "예외 처리1" 강의에서 했던 예제를 점진적으로 리팩토링 해본다.
  - 예제코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex2
    - 예외 처리 도입1 - 시작 (`NetworkServiceV2_1`)
      - 기존의 코드와 대부분 같지만, 오류가 발생했을 때 오류 코드를 반환하는 것이 아니라 예외를 던진다.
    - 예외 처리 도입2 - 예외 복구 (`NetworkServiceV2_2`)
      - 예외를 잡아서 예외 흐름을 정상 흐름으로 복구한다.
    - 예외 처리 도입3 - 정상, 예외 흐름 분리 (`NetworkServiceV2_3`)
      - 정상 흐름은 `try` 블럭에, 예외 흐름은 `catch` 블럭으로 분리한다.
    - 예외 처리 도입4 - 리소스 반환 문제 (`NetworkServiceV2_4`)
      - `client.disconnect()`가 예외가 터져도 실행되도록 수정.
      - 하지만 예상치 못한 예외가 터지면 여전히 실행이 안된다.
    - 예외 처리 도입5 - `finally` (`NetworkServiceV2_5`)
      - `finally`로 위 문제를 해결한다.

- 정리
  - 자바 예외 처리는 `try ~ catch ~ finally` 구조를 사용해서 처리할 수 있다.
  - 이점
    - 정상 흐름과 예외 흐름을 분리해서, 코드를 읽기 쉽게 만든다.
    - 사용한 자원을 항상 반환할 수 있도록 보장해준다.

### 예외 계층1 - 시작

- 예외를 계층화해서 다양하게 만들면 더 세밀하게 예외를 처리할 수 있다.

    ![체크 예외 계층화](https://github.com/user-attachments/assets/3eba9098-aafd-45cc-b0cb-c8de9ffe1d46)

  - 예제 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex3
    - `NetworkServiceV3_1.java` 참고

### 예외 계층2 - 활용

- 모든 예외를 하나하나 다 잡아서 처리하는 것은 상당히 번거롭다.
  - 중요한 예외와 그렇지 않은 예외로 나누어서 처리해본다. (`NetworkServiceV3_2`)
- 예외가 발생했을 때 `catch`를 순서대로 실행하므로, 더 디테일한 자식을 먼저 잡아야 한다.
- 참고) 여러 예외를 한번에 잡는 기능
  - `|` 를 사용해서 여러 예외를 한번에 잡을 수 있다.

    ```java
    try {
        ...
    } catch (ConnectExceptionV3 | SendExceptionV3 e) {
        ... 
    } finally {
        ... 
    }
    ```

- 정리 
  - 예외를 계층화하고 다양하게 만들면 더 세밀한 동작들을 깔끔하게 처리할 수 있다. 
  - 그리고 특정 분류의 공통 예외들도 한번에 `catch`로 잡아서 처리할 수 있다.

### 실무 예외 처리 방안1 - 설명

- 처리할 수 없는 예외
  - 개발자가 처리할 수 없는 예외가 많다.
    - 예시)
      - 상대 네트워크 서버에 문제가 발생해서 통신 불가
      - 데이터베이스 서버에 문제가 발생해서 접속 불가
      - 애플리케이션에서 연결 오류 등
  - 이런 경우 고객에게는 "현재 시스템에 문제가 있습니다."라는 오류 메시지를 보여주고,
    - 만약 웹이라면 오류 페이지를 보여주면 된다.
  - 그리고 내부 개발자가 문제 상황을 빠르게 인지할 수 있도록, 오류에 대한 로그를 남겨두어야 한다.

- 체크 예외의 부담
  - 체크 예외를 예전에 많이 썼었으나, 
  - 처리할 수 없는 예외가 많아지고, 
  - 또 프로그램이 점점 복잡해지면서 (외부 라이브러리 사용등)
  - 체크 예외를 사용하는 것이 점점 더 부담스러워졌다. 

#### 체크 예외 사용 시나리오

- 체크 예외를 사용하게 되면 어떤 문제가 발생하는지?
  - 본인이 처리 할 수 없는 에러를 밖으로 던져야 한다. 
  - 근데, 밖에서도 처리를 할 수 없는 경우가 많아서 결국 예외 전달만 하게된다.
  - 중간에 코드가 많으면 그걸 일일히 다 전달해줘야 한다.
  - 예외 처리 지옥...

![예외 처리 지옥](https://github.com/user-attachments/assets/953a645f-2989-48f7-ae09-5b19d7abcaba)

- `throws Exception`의 문제
  - `Exception` 은 최상위 타입이므로 모든 체크 예외를 다 밖으로 던질 수 있다.
    - 그래서 에러를 일일히 전달하지 않고 한번만 전달하면 되므로, 예외 처리 지옥에서 벗어 날 수는 있다.
  - 하지만, 다른 체크 예외를 체크할 수 있는 기능이 무효화 되고, 중요한 체크 예외를 다 놓치게 된다.
    - 컴파일러가 `Exception`이 선언되어있기때문에 문제가 없다고 판단하고 오류를 발생시키지 않는다.
  - 이렇게 하면 모든 예외를 다 던지기 때문에 체크 예외를 의도한 대로 사용하는 것이 아니다.
  - 따라서 꼭 필요한 경우가 아니면 이렇게 `Exception` 자체를 밖으로 던지는 것은 좋지 않은 방법이다.

#### 언체크(런타임) 예외 사용 사나리오

- 언체크(런타임) 예외를 전달한다고 가정해보자.
  - 언체크 예외가 늘어도 본인이 필요한 예외만 잡으면 되고, `throws`를 늘리지 않아도 된다.

![언체크 예외 사용 사나리오](https://github.com/user-attachments/assets/2ca5ac72-498d-42e5-9caa-5b271e6e8c5c)

- 예외 공통 처리
  - 처리할 수 없는 예외들은 중간에 여러곳에서 나누어 처리하기 보다는 예외를 공통으로 처리할 수 있는 곳을 만들어서 한 곳에서 해결하면 된다.

### 실무 예외 처리 방안2 - 구현

- 지금까지 실습한 내용을 언체크 예외로 만들고, 또 해결할 수 없는 예외들을 공통으로 처리해보자.

![언체크 예외 계층화](https://github.com/user-attachments/assets/37f51be3-21e9-442b-a1af-80bff383e189)

- 예제 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex4
  - `V4` 코드 참고
  - 언체크 예외이므로 `throws`를 사용하지 않는다.
  - 해결할 수 없는 예외 보다는 본인 스스로의 코드에 더 집중할 수 있다. 코드가 깔끔해진다.
  - 공통 예외 처리 (`MainV4`의 `exceptionHandler()` 참고)
    - 예외도 객체이므로 필요하면 `instanceof`와 같이 예외 객체의 타입을 확인해서 별도의 추가 처리를 할 수 있다.
  - `e.printStackTrace()`
    - 예외 메시지와 스택 트레이스를 출력할 수 있다.
    - `e.printStackTrace(System.out)`: 표준 출력.
      - 콘솔에 `System.out.println()` 으로 출력하는 거랑 같다.
    - `e.printStackTrace()`: `System.err` 이라는 표준 오류에 결과를 출력한다.
      - 출력 결과를 빨간색으로 보여준다.
      - 스트림이 달라서, 출력 순서가 예상한 것과 다를 수 있다.
    - 실무에서는 콘솔에 출력하지 않는다. 하지만, 학습 단계에서는 콘솔을 적극 활용하자.
      - 실무에서는 주로 `Slf4J`, `logback` 같은 별도의 로그 라이브러리를 사용해서 콘솔과 특정 파일에 함께 결과를 출력한다.

### try-with-resources

- `try`가 끝나면 외부 자원을 반납하는 패턴이 반복되면서 자바에서는 `Try with resources`라는 편의 기능을 자바 7에서 도입했다.

- 이 기능을 사용하려면 `AutoCloseable` 인터페이스를 구현해야 한다.
  - 이 인터페이스를 구현하면, `try`가 끝나는 시점에 `close()`가 자동으로 호출된다.

    ```java
    package java.lang;
    
    public interface AutoCloseable { 
        void close() throws Exception;
    }
    ```

- ⭐ 예제 코드 (비공개 레포지토리): https://github.com/JohnKim0911/kyh_java-mid1/tree/master/src/exception/ex4
  - `V5` 코드 참고
    - `NetworkClientV5`
      - `implements AutoCloseable`을 통해 `AutoCloseable`을 구현한다.
      - `AutoCloseable`의 `close()`를 오버라이딩 한다.
        - 이 메서드는 `try`가 끝나면 자동으로 호출된다.
    - `NetworkServiceV5`
      - `try` 괄호 안에 사용할 자원을 명시한다.
        - `try (NetworkClientV5 client = new NetworkClientV5(address)) {...}`
    - 실행순서에 주목하자.
      - `try`가 끝나자마자 바로 `AutoCloseable`의 `close()`가 실행된다.
        - (`https://example.com 서버 연결 해제`문구가 `[예외 확인]~~~`문구보다 먼저 나온다.)

- `Try with resources` 장점
  - 리소스 누수 방지: 
    - 모든 리소스가 제대로 닫히도록 보장한다. 
    - 실수로 `finally` 블록을 적지 않거나, `finally` 블럭 안에서 자원 해제 코드를 누락하는 문제들을 예방할 수 있다.
  - 코드 간결성 및 가독성 향상: 
    - 명시적인` close()` 호출이 필요 없어 코드가 더 간결하고 읽기 쉬워진다.
  - 스코프 범위 한정: 
    - 예를 들어 리소스로 사용되는 `client` 변수의 스코프가 `try` 블럭 안으로 한정된다.
    - 따라서 코드 유지보수가 더 쉬워진다.
  - 조금 더 빠른 자원 해제: 
    - 기존에는 `try catch finally`로 `catch` 이후에 자원을 반납했다. 
    - `Try with resources` 구분은 `try` 블럭이 끝나면 즉시 `close()`를 호출한다.

### 정리

- 현대 개발에서는 체크 예외보다 언체크(런타임) 예외를 사용하는 추세다.
- 런타임 예외도 필요하면 잡을 수 있기 때문에 필요한 경우에는 잡아서 처리하고, 그렇지 않으면 자연스럽게 던지도록 둔다. 
- 그리고 처리할 수 없는 예외는 예외를 공통으로 처리하는 부분을 만들어서 해결하면 된다.
- 참고) 
  - 최근 라이브러리들은 대부분 런타임 예외를 기본으로 제공한다. - 예시) 스프링, JPA

---

## 12. 다음으로

김영한의 실전 자바 - 중급 2편

---