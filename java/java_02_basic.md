# (복습) 김영한의 실전 자바 - 기본편

|    | 제목                | 복습일        |
|----|-------------------|------------|
| 1  | 강의소개와 자료          | 2024-11-17 |
| 2  | 클래스와 데이터          | 2024-11-17 |
| 3  | 기본형과 참조형          | 2024-11-18 |
| 4  | 객체 지향 프로그래밍       | 2024-11-18 |
| 5  | 생성자               | 2024-11-19 |
| 6  | 패키지               | 2024-11-19 |
| 7  | 접근 제어자            | 2024-11-19 |
| 8  | 자바 메모리 구조와 static | 2024-11-20 |
| 9  | final             | 2024-11-20 |
| 10 | 상속                | 2024-11-   |
| 11 | 다형성1              | 2024-11-   |
| 12 | 다형성2              | 2024-11-   |
| 13 | 다형성과 설계           | 2024-11-   |
| 14 | 다음으로              | 2024-11-   |

---

## 1. 강의 소개와 자료

---

## 2. 클래스와 데이터

### 프로젝트 환경 구성

### 클래스가 필요한 이유
- 문제: 학생 정보 출력 프로그램 만들기
- 배열 사용의 한계
    - 학생의 `이름`, `나이`, `성적`을 각각의 배열에 따로 보관하니 관리가 어렵다.
        - 정확히 인덱스를 맞추지 않으면 잘못 수정하거나 하는 일들이 발생하기 쉽다.
            - 즉, 사람이 관리하기 좋지 방식이 아니다.
            - 사람이 관리하기 좋은 방식은,
                - 학생이라는 개념을 하나로 묶는 것이다.

### 클래스 도입

```java
public class Student {
    String name;
    int age;
    int grade;
}
```

- 클래스에 정의한 변수들을 `멤버 변수`, 또는 `필드`라 한다.
    - `멤버 변수 (Member Variable)`
        - 이 변수들은 특정 클래스에 소속된 멤버이기 때문에 이렇게 부른다.
    - `필드 (Field)`
        - 데이터 항목을 가리키는 전통적인 용어이다.
            - 데이터베이스, 엑셀 등에서 데이터 각각의 항목을 필드라 한다.
    - 자바에서 `멤버 변수`, `필드`는 같은 뜻이다. 클래스에 소속된 변수를 뜻한다.
- 클래스는 관례상 `대문자로 시작`하고 `낙타 표기법`을 사용한다.
- `클래스`와 `사용자 정의 타입`
    - `int` 라고 하면 `정수` 타입, `String` 이라고 하면 `문자` 타입이다.
        - `학생( Student )`이라는 타입을 만들면 되지 않을까? => `클래스`
    - 사용자가 직접 정의하는 `사용자 정의 타입`을 만들려면 설계도가 필요하다. 이 `설계도`가 바로 `클래스`이다.
    - 설계도인 `클래스`를 사용해서 `실제 메모리에 만들어진 실체`를 `객체` 또는 `인스턴스`라 한다.

- `참조값`을 변수에 보관
    1. `Student student1 = new Student();` //1. Student 객체 생성
    2. `Student student1 = x001;` //2. new Student()의 결과로 x001 참조값 반환
    3. `student1 = x001;` //3. 최종 결과

### 객체 사용

- 클래스를 통해 생성한 `객체`를 사용하려면, 먼저 `메모리`에 존재하는 객체에 접근해야 한다.
    - 객체에 접근하려면 `.` (점, dot)을 사용하면 된다.

      ```java
      //객체 값 대입
      student1.name = "학생1";
      student1.age = 15;
      student1.grade = 90;
      
      //객체 값 사용
      System.out.println("이름:" + student1.name + " 나이:" + student1.age + " 성적:" + student1.grade);
      ```

### 클래스, 객체, 인스턴스 정리

- `클래스` - `Class`
    - 객체를 생성하기 위한 '`틀`' 또는 '`설계도`'
    - 예)
        - 붕어빵 틀
        - 자동차 설계도
- `객체` - `Object`
    - 클래스에서 정의한 속성과 기능을 가진 `실체`
- `인스턴스` - `Instance`
    - 주로 객체가 어떤 클래스에 속해 있는지 강조할 때 사용한다.
        - `student1` 객체는 `Student` 클래스의 `인스턴스`다.

### 배열 도입 - 시작


- 자바에서 대입은 항상 변수에 들어 있는 값을 복사한다.
- 배열에 참조값 대입
- 배열에 들어있는 객체 사용

![배열에 참조값을 대입한 이후 최종 그림.png](../../java-basic/src/class1/img/배열에%20참조값을%20대입한%20이후%20최종%20그림.png)

```java
public class ClassStart4 {
    public static void main(String[] args) {
        Student student1 = new Student();
        student1.name = "학생1";
        student1.age = 15;
        student1.grade = 90;

        Student student2 = new Student();
        student2.name = "학생2";
        student2.age = 16;
        student2.grade = 80;

        Student[] students = new Student[2];

        students[0] = student1;
        students[1] = student2;

        System.out.println("이름:" + students[0].name + " 나이:" + students[0].age + " 성적:" + students[0].grade);
        System.out.println("이름:" + students[1].name + " 나이:" + students[1].age + " 성적:" + students[1].grade);
    }
}
```

### 배열 도입 - 리펙토링

- 배열 선언 최적화
    - `Student[] students = {student1, student2};`
- for문 최적화

    ```java
    for (Student s : students) {
        System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
    }
    ```

---

## 3. 기본형과 참조형

### 기본형 vs 참조형1 - 시작
- `기본형` vs `참조형`
    - 기본형
        - `int` , `long` , `double` , `boolean`
    - 참조형
        - 클래스.
            - ex) `Student`

### 기본형 vs 참조형2 - 변수 대입
- 대원칙: `자바는 항상 변수의 값을 복사해서 대입한다.`
- `기본형`과 `변수 대입`
    - a를 바꾼다고, b가 바뀌지 않는다.

      ```java
      int a = 10;
      int b = a;
      System.out.println("a = " + a); //10
      System.out.println("b = " + b); //10
      
      a = 20;
      System.out.println("a = " + a); //20
      System.out.println("b = " + b); //10 -> b 안바뀜
      ```

- `참조형`과 `변수 대입`
    - a를 바꾸면, b도 바뀐다. (같은 주소값을 가지고 있기 때문)
      ```java
      Data dataA = new Data();
      dataA.value = 10;
      Data dataB = dataA;
      
      System.out.println("dataA.value = " + dataA.value); //10
      System.out.println("dataB.value = " + dataB.value); //10
      
      dataA.value = 20;
      System.out.println("dataA.value = " + dataA.value); //20
      System.out.println("dataB.value = " + dataB.value); //20 -> b도 바뀜!!
      ```

### 기본형 vs 참조형3 - 메서드 호출
- `변수 대입`과 동일한 원리.
    - `기본형`과 `메서드 호출`
    - `참조형`과 `메서드 호출`

### 참조형과 메서드 호출 - 활용
- 참조형을 활용해서 기존코드 리팩토링. =>  메서드로 추출함.
    ```java
    public static void main(String[] args) {
        Student student1 = createStudent("학생1", 15, 90);
    }
    
    static Student createStudent(String name, int age, int grade) {
        Student student = new Student();
        student.name = name;
        student.age = age;
        student.grade = grade;
        return student;
    }
    ```

### 변수와 초기화
- 변수의 종류
    - `멤버 변수` (`필드`)
        - `클래스`에 선언
            - 아래에서 `name` , `age` , `grade`는 멤버 변수이다
              ```java
              public class Student {
                  String name;
                  int age;
                  int grade;
              }
              ```
    - `지역 변수`
        - `메서드`에 선언. `매개변수`도 지역 변수의 한 종류이다.
            - 아래에서 `a`, `x`(매개변수)는 지역 변수이다
                ```java
                public class MethodChange1 {
                  public static void main(String[] args) {
                      int a = 10;
                      changePrimitive(a);
                  }
                  
                  public static void changePrimitive(int x) {
                      x = 20;
                  }
                }
                ```

- 변수의 값 초기화
    - `멤버 변수`: `자동` 초기화
        - 인스턴스의 멤버 변수는 인스턴스를 생성할 때 자동으로 초기화된다.
            - 숫자(`int`)= `0`
            - `boolean` = `false`
            - 참조형 = `null`
        - 개발자가 초기값을 직접 지정할 수 있다.
    - `지역 변수`: `수동` 초기화
        - 지역 변수는 항상 직접 초기화해야 한다.

### null
- null 값 할당
    - 참조형 변수에 아직 가리키는 대상이 없거나, 가리키는 대상을 나중에 입력하고 싶을때 사용
- `GC` (가비지 컬렉션)
    - 아무도 참조하지 않는 인스턴스가 있으면 JVM의 GC가 자동으로 메모리에서 제거해준다.

### NullPointerException
- `null` 값에 `.`(dot)을 찍으면 발생
```java
data.value = 10 // null.value
```

---

## 4. 객체 지향 프로그래밍

### 절차 지향 프로그래밍1 - 시작
- 프로그래밍 방식은 크게 2가지로 나눌 수 있다.
    - `절차 지향 프로그래밍`
        - 절차를 지향한다. == 실행순서를 중요시 한다.
        - "어떻게" 중심
        - (중요한 차이) `데이터와 해당 데이터에 대한 처리 방식이 분리되어있음.`
    - `객체 지향 프로그래밍`
        - 객체를 지향한다.
        - 실제 세계의 사물이나 사건을 객체로 보고, 이러한 객체들 간의 상호작용을 중심으로 프로그래밍하는 방식
        - "무엇"을 중심
        - (중요한 차이) `데이터와 그 데이터에 대한 행동(메서드)가 하나의 '객체'안에 포함되어있음.`
- 지금까지 우리가 작성한 모든 프로그램은 절차 지향 프로그램
- 예시)
    - 절차 지향 음악 플레이어1
        - 메인 메서드에 모든 코드 작성

### 절차 지향 프로그래밍2 - 데이터 묶음
- 예시)
    - 절차 지향 음악 플레이어2
        - 데이터를 보관하는 클래스를 통하여 인스턴스 생성해서 사용

### 절차 지향 프로그래밍3 - 메서드 추출
- 예시)
    - 절차 지향 음악 플레이어3
        - 메인 메서드 안에 있던 기능 관련 코드를 메소드로 추출함.
            - (여전히 메인 클래스와 같은 자바 파일안에서 있음. 즉, 클래스와는 다른 파일에서 관리)

  ```java
  public class MusicPlayerData {
      int volume = 0;
      boolean isOn = false;
  }
  ```

  ```java
  public class MusicPlayerMain3 {
  
      public static void main(String[] args) {
          MusicPlayerData data = new MusicPlayerData();
          on(data);
          volumeUp(data);
          volumeUp(data);
          volumeDown(data);
          showStatus(data);
          off(data);
      }
      
      static void on(MusicPlayerData data) {
          data.isOn = true;
          System.out.println("음악 플레이어를 시작합니다");
      }
      
      static void off(MusicPlayerData data) {
          data.isOn = false;
          System.out.println("음악 플레이어를 종료합니다");
      }
      
      static void volumeUp(MusicPlayerData data) {
          data.volume++;
          System.out.println("음악 플레이어 볼륨:" + data.volume);
      }
      
      static void volumeDown(MusicPlayerData data) {
          data.volume--;
          System.out.println("음악 플레이어 볼륨:" + data.volume);
      }
      
      static void showStatus(MusicPlayerData data) {
          System.out.println("음악 플레이어 상태 확인");
          if (data.isOn) {
              System.out.println("음악 플레이어 ON, 볼륨:" + data.volume);
          } else {
              System.out.println("음악 플레이어 OFF");
          }
      }
    
  }
  ```

- 절차 지향 프로그래밍의 한계
    - `데이터`와 `기능`이 `분리`되어 있다.
        - 한쪽이 바뀌면 다른쪽에도 코드를 수정해줘야한다.
            - 관리 포인트가 늘어난다.
    - 객체 지향 프로그래밍을 사용하면, 한 곳에서 관리 할 수 있다.

### 클래스와 메서드
- 클래스는 `데이터`인 `멤버 변수` 뿐 아니라 `기능` 역할을 하는 `메서드`도 포함할 수 있다.
- 참고) 여기서 만드는 메서드에는 `static` 키워드를 사용하지 않는다.
    - `static`이 붙으면 객체를 생성하지 않고도 메서드를 호출할 수 있다.

### 객체 지향 프로그래밍
- 예시)
    - 객체 지향 음악 플레이어

```java
public class MusicPlayer {

    int volume = 0;
    boolean isOn = false;

    void on() {
        isOn = true;
        System.out.println("음악 플레이어를 시작합니다");
    }

    void off() {
        isOn = false;
        System.out.println("음악 플레이어를 종료합니다");
    }

    void volumeUp() {
        volume++;
        System.out.println("음악 플레이어 볼륨:" + volume);
    }

    void volumeDown() {
        volume--;
        System.out.println("음악 플레이어 볼륨:" + volume);
    }

    void showStatus() {
        System.out.println("음악 플레이어 상태 확인");
        if (isOn) {
            System.out.println("음악 플레이어 ON, 볼륨:" + volume);
        } else {
            System.out.println("음악 플레이어 OFF");
        }
    }
}
```

```java
public class MusicPlayerMain4 {

    public static void main(String[] args) {
        MusicPlayer player = new MusicPlayer();
        player.on();
        player.volumeUp();
        player.volumeUp();
        player.volumeDown();
        player.showStatus();
        player.off();
    }

}
```

- 캡슐화
    - `속성`과 `기능`을 하나로 묶어서 필요한 기능을 메서드를 통해 외부에 제공하는 것을 `캡슐화`라 한다.

- 정리
    - `객체 지향 프로그래밍`과 `절차 지향 프로그래밍`은 서로 대치되는 개념이 아니다.
        -  다만 어디에 더 초점을 맞추는가에 둘의 차이가 있다.
    - `객체`란?
        - 세상의 모든 사물을 단순하게 추상화해보면 `속성`(데이터)과 `기능` 딱 2가지로 설명할 수 있다.
        - 예시)
            - 자동차
                - 속성:
                    - 차량 색상
                    - 현재속도
                - 기능:
                    - 엑셀
                    - 브레이크
                    - 문열기
                    - 문닫기
    - `객체 지향 프로그래밍`은 모든 사물을 `속성`과 `기능`을 가진 `객체`로 생각하는 것이다.
    - 객체 지향의 특징
        - `속성`과 `기능`을 하나로 묶는 것 뿐만 아니라,
        - `캡슐화`, `상속`, `다형성`, `추상화`, 메시지 전달 같은 다양한 특징들이 있다.
        - 앞으로 이런 특징들을 하나씩 알아가보자.

---

## 5. 생성자

### 생성자 - 필요한 이유
- `생성자 없이` 코드 작성1
    - 초기값 설정 부분이 중복되므로 메서드로 추출함. (main 메서드와 같은 자바 파일내에서)

### this
- `생성자 없이` 코드 작성2
    - 클래스 내에 `속성`만 있었는데, `기능`(메서드)도 클래스 내부로 이동시킴.

```java
package construct;

public class MemberInit {
    String name;
    int age;
    int grade;

    //추가
    void initMember(String name, int age, int grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```

```java
package construct;

public class MethodInitMain3 {

    public static void main(String[] args) {
        MemberInit member1 = new MemberInit();
        member1.initMember("user1", 15, 90);

        MemberInit member2 = new MemberInit();
        member2.initMember("user2", 16, 80);

        MemberInit[] members = {member1, member2};

        for (MemberInit s : members) {
            System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
        }
    }

}
```

- this
    - `멤버 변수`와 메서드의 `매개변수`의 이름이 같으면 둘을 어떻게 구분?
        - 가장 가까운 범위가 우선순위를 가짐.
            - 즉, `매개변수`가 우선순위를 가짐.
        - `멤버 변수`에 접근하려면, `this`를 사용하면된다.
            - `this`는 인스턴스 자신의 참조값을 가리킴.
    - `this`의 생략
        - `멤버 변수`와 메서드의 `매개변수`의 이름이 같으면, `this`를 생략해도 된다.
    - `this`와 코딩 스타일
        - `멤버 변수`와 메서드의 `매개변수`의 이름이 같던, 다르던 항상 `this`를 사용하는 코딩 스타일도 있다.
        - 예전에는 구별이 어려웠으므로 `this`를 꼭 쓰는걸 권장했지만, 요즘은 `IDE`가 `색상`으로 구별해주기 때문에 안써도 된다. - 강사님 의견

### 생성자 - 도입

- 초기값 할당하는 경우가 많다. 매번 메서드를 만들기보다 `생성자`를 사용하면 된다.

```java
package construct;

public class MemberConstruct {
    String name;
    int age;
    int grade;

    //생성자
    MemberConstruct(String name, int age, int grade) {
        System.out.println("생성자 호출 name=" + name + ",age=" + age + ",grade=" + grade);
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}

```

```java
package construct;

public class ConstructMain1 {

    public static void main(String[] args) {
        MemberConstruct member1 = new MemberConstruct("user1", 15, 90);
        MemberConstruct member2 = new MemberConstruct("user2", 16, 80);

        MemberConstruct[] members = {member1, member2};

        for (MemberConstruct s : members) {
            System.out.println("이름:" + s.name + " 나이:" + s.age + " 성적:" + s.grade);
        }
    }

}
```

- 생성자
    - 생성자의 이름은 `클래스 이름과 같아야 한다`. 따라서 첫 글자도 대문자로 시작한다.
    - 생성자는 `반환 타입이 없다.` 비워두어야 한다.
    - 생성자 장점
        - 객체 생성하면서 동시에 초기값을 할당하는 작업을 한번에 처리 할 수 있다.
        - 생성자 호출을 강제한다. (제약)
            - 실수로 초기값 넣는 것을 누락하지 않도록 한다.
                - 값이 없어도 프로그램은 작동한다. 유령 데이터가 생기게 되는데, 이를 방지 할 수 있다.

### 기본 생성자

```java
package construct;

public class MemberDefault {
    String name;

    //기본 생성자
    MemberDefault() {
        System.out.println("생성자 호출");
    }
}
```

```java
package construct;

public class MemberDefaultMain {

    public static void main(String[] args) {
        MemberDefault memberDefault = new MemberDefault();
    }

}
```

- 기본 생성자
    - 매개변수가 없는 생성자를 `기본 생성자`라 한다.
    - 클래스에 생성자가 하나도 없으면 `자바 컴파일러`는 `기본 생성자`를 자동으로 만들어준다.
        - `생성자가 하나라도 있으면 자바는 기본 생성자를 만들지 않는다.`
        - 기본 생성자를 왜 자동으로 만들어줄까?
            - 생성자 기능이 필요하지 않은 경우에도 모든 클래스에 개발자가 직접 기본 생성자를 정의해야 한다.

### 생성자 - 오버로딩과 this()

- 생성자도 메서드 `오버로딩`처럼 매개변수만 다르게 해서 여러 생성자를 제공할 수 있다.

```java
package construct;

public class MemberConstruct {
    String name;
    int age;
    int grade;

    MemberConstruct(String name, int age) {
        this(name, age, 50); //아래 생성자를 호출한다.
    }

    MemberConstruct(String name, int age, int grade) {
        System.out.println("생성자 호출 name=" + name + ",age=" + age + ",grade=" + grade);
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
}
```

- `this()`
    - `this()`를 사용하면 생성자 내부에서 자신의 생성자를 호출할 수 있다. => 중복을 줄일 수 있다.
    - `this()`는 생성자 코드의 `첫줄`에만 작성할 수 있다.

---

## 6. 패키지

### 패키지 - 시작

- 패키지
    - 관련 있는 기능들을 분류해서 관리하고 싶다 -> `패키지`
    - 컴퓨터에서 `폴더`와 같은 개념 => 자바에서는 `패키지`

```
* user //패키지
    * User //클래스
    * UserManager
    * UserHistory
* product //패키지
    * Product
    * ProductCatalog
    * ProductImage
* order
    * Order
    * OrderService
    * OrderHistory
* cart
    * ShoppingCart
    * CartItem
* payment
    * Payment
    * PaymentHistory
* shipping
    * Shipment
    * ShipmentTracker
```

- 패키지 사용
    - 항상 코드 `첫줄`에 `패키지` 이름을 적어주어야 한다. (IDE가 보통 자동으로 해줌)
    - 생성자에 `public`을 사용했다.
        - 다른 패키지에서 이 클래스의 생성자를 호출하려면 `public`을 사용해야 한다.

```java
package pack; //패키지 이름

public class Data {
    public Data() {
        System.out.println("패키지 pack Data 생성");
    }
}
```

```java
package pack.a;

public class User {
    public User() {
        System.out.println("패키지 pack.a 회원 생성");
    }
}
```

```java
package pack;

public class PackageMain1 {
    public static void main(String[] args) {
        Data data = new Data(); //같은 패키지에 있는 경우, 패키지 경로 생략가능.
        pack.a.User user = new pack.a.User(); //다른 패키지에 있는 경우, 패키지 전체 경로 포함해야함.
    }
}
```

### 패키지 - import
- 패키지 경로 적어주는 것 불편 => `import`를 사용하자.
```java
package pack;
import pack.a.User;

public class PackageMain2 {
    public static void main(String[] args) {
        Data data = new Data();
        User user = new User(); //import 사용으로 패키지 명 생략 가능
    }
}
```

- 특정 패키지에 포함된 모든 클래스를 포함해서 사용하고 싶으면 `*`(별) 을 사용하면 된다.
```java
package pack;
import pack.a.*; //pack.a의 모든 클래스를 패키지 명을 생략하고 사용할 수 있다.

public class PackageMain2 {
    public static void main(String[] args) {
        Data data = new Data();
        User user = new User();
    }
}
```

- 클래스 이름 중복
    - 패키지 덕분에 클래스 이름이 같아도 사용할 수 있다.
        - 예시)
            - `pack.a.User`
            - `pack.b.User`
    - `import`는 둘중 하나만 선택할 수 있다.
        - 자주 사용하는 클래스를 import 하고, 나머지를 패키지를 포함한 전체 경로를 적어주면 된다.

```java
package pack;
import pack.a.User;

public class PackageMain3 {
    public static void main(String[] args) {
        User userA = new User();
        pack.b.User userB = new pack.b.User();
    }
}
```

### 패키지 규칙

- 패키지 규칙
    - 패키지의 `이름`과 `위치`는 폴더(디렉토리) 위치와 같아야 한다. (필수)
    - 패키지 이름은 모두 `소문자`를 사용한다. (관례)
    - 패키지 이름의 앞 부분에는 일반적으로 회사의 도메인 이름을 거꾸로 사용한다. (관례)
        - 예시) `com.company.myapp`

- 패키지와 계층 구조
    - 예시)
        - a
            - b
            - c
    - 위 예시처럼 하면 총 3개 패키지가 존재한다.
        - `a`
        - `a.b`
        - `a.c`
    - 서로 완전히 다른 패키지이다.
        - 다른 패키지의 클래스가 필요하면 `import`해서 사용해야 한다.

### 패키지 활용

- 전체 구조도 (예시)
    - `com.helloshop` //패키지
        - `user` //패키지
            - `User` //클래스
            - `UserService` //클래스
        - `product`
            - `Product`
            - `ProductService`
        - `order`
            - `Order`
            - `OrderService`
            - `OrderHistory`

---

## 7. 접근 제어자

### 접근 제어자 이해1
- 접근 제어자
    - `public`, `private` 등등.
    - 해당 클래스 외부에서 특정 필드나 메서드에 접근하는 것을 허용하거나 제한할 수 있다.
    - 필요한 이유
        - 예시) `음량이 100이 넘어가면 폭발하는 스피커` 1
            - 메서드에는 100이 넘어가지 않도록 조건이 걸려있긴한데,
                - 필드에 바로 접근해서 값을 바꾸어버리면 100이 넘어가도록 수정가능.
                    - 즉, 폭발해버림...
            - 음량에 직접 접근 할 수 없도록 막아야 함.

### 접근 제어자 이해2

- 예시) `음량이 100이 넘어가면 폭발하는 스피커` 2
    - 음량에 `private` 접근제어자로 직접 접근 할 수 없도록 함.

```java
package access;

public class Speaker {
    private int volume; //private 접근제어자 추가

    Speaker(int volume) {
        this.volume = volume;
    }

    void volumeUp() {
        if (volume >= 100) {
            System.out.println("음량을 증가할 수 없습니다. 최대 음량입니다.");
        }else {
            volume += 10;
            System.out.println("음량을 10 증가합니다.");
        }
    }

    void volumeDown() {
        volume -= 10;
        System.out.println("volumnDown 호출");
    }

    void showVolume() {
        System.out.println("현재 음량: " + volume);
    }
}
```

```java
package access;

public class SpeakerMain {
    public static void main(String[] args) {
        Speaker speaker = new Speaker(90);
        speaker.showVolume(); //현재 음량: 90

        speaker.volumeUp(); //음량을 10 증가합니다
        speaker.showVolume(); //현재 음량: 100

        speaker.volumeUp(); //음량을 증가할 수 없습니다. 최대 음량입니다.
        speaker.showVolume(); //현재 음량: 100

        //필드에 직접 접근
        System.out.println("volume 필드 직접 접근 수정");
        //speaker.volume = 200; // 접근제어자 private 적용 후 => private 접근 오류
        speaker.showVolume(); //현재 음량: 200 (스피커 폭발...) => 접근제어자 private 적용 => 현재 음량: 100
    }
}
```

### 접근 제어자 종류

- 접근 제어자 종류
    - `private`
        - 모든 외부 호출을 막는다.
    - `default` (`package-private`)
        - 같은 패키지안에서 호출은 허용한다.
        - 접근 제어자를 명시하지 않으면 `default` 접근 제어자가 적용된다.
    - `protected`
        - 같은 패키지안에서 호출은 허용한다.
        - 패키지가 달라도 상속 관계의 호출은 허용한다.
    - `public`
        - 모든 외부 호출을 허용한다.
- 접근 제어 강도
    - `private` -> `default` -> `protected` -> `public`
        - `private`이 가장 많이 차단
        - `public`이 가장 많이 허용
- 접근 제어자 사용 위치
    - `필드`
    - `메서드`
    - `생성자`
    - `클래스 레벨`에도 일부 접근 제어자를 사용할 수 있다.
- 접근 제어자의 핵심은 `속성`과 `기능`을 외부로부터 숨기는 것이다.

### 접근 제어자 사용 - 필드, 메서드

- 예시) 같은 패키지, 다른 패키지 접근 제어자 사용 예시
    - `private`, `default`, `public` 접근 제어자

### 접근 제어자 사용 - 클래스 레벨
- `클래스 레벨`의 접근 제어자 규칙
    - `public`, `default`만 사용할 수 있다.
        - `private`, `protected` 는 사용할 수 없다.
    - `public` 클래스는 반드시 파일명과 이름이 같아야 한다.
        - 하나의 자바 파일에 `public` 클래스는 하나만 등장할 수 있다.
        - 하나의 자바 파일에 `default` 접근 제어자를 사용하는 클래스는 무한정 만들 수 있다.

`PublicClass.java` 파일
```java
package access.a;

//하나의 자바 파일에 public 클래스는 하나만 등장할 수 있다.
public class PublicClass { //public 클래스는 반드시 파일명과 이름이 같아야 한다.
    public static void main(String[] args) {
        PublicClass publicClass = new PublicClass();
        DefaultClass1 class1 = new DefaultClass1();
        DefaultClass2 class2 = new DefaultClass2();
    }
}

class DefaultClass1 { //default 접근 제어자를 사용하는 클래스는 무한정 만들 수 있다.
}

class DefaultClass2 {
}
```

### 캡슐화

- `캡슐화` (Encapsulation)
    - `객체 지향 프로그래밍`의 중요한 개념 중 하나.
    - `속성`과 `기능`을 하나로 묶고, `외부에 꼭 필요한 기능만 노출하고 나머지는 모두 내부로 숨기는 것`.
    - `접근 제어자`: `캡슐화`를 안전하게 완성할 수 있게 해주는 장치

- 어떤 것을 숨기고 어떤 것을 노출해야 할까?
    - `데이터`는 모두 숨기고, `기능`은 꼭 필요한 기능만 노출하는 것이 좋은 `캡슐화`이다.
        1. `데이터`
            - 예시) 자동차
                - 자동차 속도계 직접 조절하지 못하게.
                - 자동차가 제공하는 엑셀 기능만 사용 할 수 있게.
                    - 나머지는 자동차가 알아서 하는 것.
            - 객체의 `데이터`는 객체가 제공하는 `메서드`를 통해서 접근해야 한다.
        2. `기능`
            - 예시) 자동차
                - 자동차의 복잡한 내부 기능(내부 엔진 조절기능, 배기 기능)까지 다 알 필요없다.
                    - 엑셀, 핸들 정도만 알면 충분하다.
                - 불필요한 기능은 감추고, 꼭 필요한 기능만 노출하자.

- 잘 캡슐화된 예제

```java
package access;

public class BankAccount {

    private int balance;

    public BankAccount() {
        this.balance = 0; //사실 없어도됨. 자동으로 0으로 초기화됨. 여기선 public을 사용해보기 위해서 넣음.
    }

    // public 메서드: deposit
    public void deposit(int amount) {
        if (isAmountValid(amount)) {
            balance += amount;
        } else {
            System.out.println("유효하지 않은 금액입니다.");
        }
    }

    // public 메서드: withdraw
    public void withdraw(int amount) {
        if (isAmountValid(amount) && balance - amount >= 0) {
            balance -= amount;
        } else {
            System.out.println("유효하지 않은 금액이거나 잔액이 부족합니다.");
        }
    }

    // public 메서드: getBalance
    public int getBalance() {
        return balance;
    }

    // private 메서드: isAmountValid
    private boolean isAmountValid(int amount) {
        // 금액이 0보다 커야함
        return amount > 0;
    }
}
```

```java
package access;

public class BankAccountMain {

    public static void main(String[] args) {
        BankAccount account = new BankAccount();
        account.deposit(10000);
        account.withdraw(3000);
        System.out.println("balance = " + account.getBalance());
    }
}
```

---

## 8. 자바 메모리 구조와 static

### 자바 메모리 구조

![자바 메모리 구조 - 비유](../../java-basic/src/static1/img/자바%20메모리%20구조_비유.png)

- 자바 메모리 구조
    - `메서드 영역`
        - 클래스 정보(붕어빵틀)를 보관한다.
    - `스택 영역`
        - 실제 프로그램이 실행되는 영역
        - 메서드를 실행할 때 마다 하나씩 쌓인다.
    - `힙 영역`
        - 객체(인스턴스)가 생성되는 영역
        - new 명령어를 사용하면 이 영역을 사용한다.
        - 붕어빵 틀로부터 생성된 붕어빵이 존재하는 공간.
        - 배열도 이 영역에 생성된다.


![자바 메모리 구조 - 실제](../../java-basic/src/static1/img/자바%20메모리%20구조_실제.png)

- 자바 메모리 구조
    - `메서드 영역`
        - 개요
            - 프로그램을 실행하는데 필요한 공통 데이터를 관리한다.
            - 이 영역은 프로그램의 모든 영역에서 공유한다.
        - 클래스 정보
        - static 영역
        - 런타임 상수 풀
            - 프로그램을 실행하는데 필요한 공통 리터럴 상수 보관
    - `스택 영역`
        - 자바 실행 시, 하나의 실행 스택이 생성된다.
        - 각 스택 프레임은 지역 변수, 중간 연산 결과, 메서드 호출 정보 등을 포함한다.
            - 스택 프레임:
                - 스택 영역에 쌓이는 네모 박스가 하나의 스택 프레임.
                - 메소드를 호출할 때 마다 하나의 스택 프레임이 쌓이고, 메서드가 종료되면 해당 스택 프레임이 제거된다.
        - 스택 영역은 더 정확히는 각 쓰레드별로 하나의 실행 스택이 생성된다.
    - `힙 영역`
        - 객체(인스턴스)와 배열이 생성되는 영역
        - 가비지 컬렉션(GC)이 이루어지는 주요 영역.
            - 더 이상 참조되지 않는 객체는 GC에 의해 제거된다.


- `메서드` 코드는 `메서드 영역`에.
    - 인스턴스는 내부에 `변수`와 `메서드`를 가진다.
    - 같은 클래스로 부터 생성된 객체라도, 인스턴스 내부의 `변수` 값은 서로 다를 수 있지만, `메서드`는 공통된 코드를 공유한다.
    - 인스턴스 `변수`에는 메모리가 할당되지만, `메서드`에 대한 새로운 메모리 할당은 없다.
    - `메서드`는 `메서드 영역`에서 공통으로 관리되고 실행된다.
    - 인스턴스의 `메서드`를 호출하면 실제로는 `메서드 영역`에 있는 코드를 불러서 수행한다.

![메서드 코드는 메서드 영역에](../../java-basic/src/static1/img/메서드%20코드는%20메서드%20영역에.png)

### 스택과 큐 자료 구조

- `스택`
    - `후입 선출`(`LIFO`, Last In First Out)
        - 나중에 넣은 것이 가장 먼저 나오는 것
        - `1`(넣기) ➡️ `2`(넣기) ➡️ `3`(넣기) ➡️ `3`(빼기) ➡️ `2`(빼기) ➡️ `1`(빼기)
        - 예시) 냉장고에 콜라 넣기.
            - 가장 나중에 넣은 콜라가 가장 먼저 나옴.

![스택구조1](../../java-basic/src/static1/img/스택구조1.png)
![스택구조2](../../java-basic/src/static1/img/스택구조2.png)

- `큐`(Queue)
    - `선입 선출`(`FIFO`, First In First Out)
        - 가장 먼저 넣은 것이 가장 먼저 나오는 것
        - `1`(넣기) ➡️ `2`(넣기) ➡️ `3`(넣기) ➡️ `1`(빼기) ➡️ `2`(빼기) ➡️ `3`(빼기)
        - 예시) 선착순 이벤트
            - 가장 먼저 온 사람이 먼저 당첨되도록.

![queue](../../java-basic/src/static1/img/queue.png)

### 스택 영역

- 정리
    - 자바는 `스택 영역`을 사용해서 `메서드 호출`과 `지역 변수(매개변수 포함)`를 관리한다.
    - `메서드`를 계속 호출하면 `스택 프레임`이 계속 쌓인다.
    - `스택 프레임`이 종료되면 `지역 변수`도 함께 제거된다.
    - `스택 프레임`이 모두 제거되면 `프로그램`도 종료된다.

### 스택 영역과 힙 영역

![스택 영역 and 힙 영역](../../java-basic/src/static1/img/스택%20영역%20and%20힙%20영역.png)

- `x001` 참조값을 가진 `Data` 인스턴스를 참조하는 곳이 없다.
    - 참조하는 곳이 없으므로 사용되는 곳도 없다.
    - `GC(가비지 컬렉션)`이 사용되지 않는 인스턴스를 찾아서 메모리에서 제거한다.
- `지역 변수`는 `스택 영역`에, `객체(인스턴스)`는 `힙 영역`에 관리된다.
- `메서드 영역`이 관리하는 변수도 있다.
    - 이걸 이해하려면 먼저 `static` 키워드를 알아야 한다.

### static 변수1

- `static` 키워드가 왜 필요?
    - 예시) 특정 클래스를 통해 생성된 객체의 수 세기.
        - `static` 키워드 없이 할 경우.
            - `인스턴스 내부` 변수에 카운트 저장 ️ ➡️ 카운트가 안올라감.
            - `외부 인스턴스`에 카운트 저장 ➡️ 카운트가 올라가긴 하나 불편한 점이 있음.
                - `Data2` 클래스와 관련된 일인데, `Counter`라는 별도의 클래스를 추가로 사용해야 한다.
                - 생성자의 매개변수도 추가되고, 생성자가 복잡해진다. 생성자를 호출하는 부분도 복잡해진다.

- 외부 인스턴스에 카운트 저장 (코드)

```java
package static1;

public class Counter {
    public int count;
}

```

```java
package static1;

public class Data2 {
    public String name;

    public Data2(String name, Counter counter) {
        this.name = name;
        counter.count++;
    }
}
```

```java
package static1;

public class DataCountMain2 {

    public static void main(String[] args) {
        Counter counter = new Counter();
        Data2 data1 = new Data2("A", counter);
        System.out.println("A count=" + counter.count);

        Data2 data2 = new Data2("B", counter);
        System.out.println("B count=" + counter.count);

        Data2 data3 = new Data2("C", counter);
        System.out.println("C count=" + counter.count);
    }
}
```

### static 변수2

- `static` 키워드를 사용하면 `공용으로 함께 사용하는 변수`를 만들 수 있다.
- `static`이 붙으면 `static변수`, `정적변수` 또는 `클래스 변수`라 한다.

```java
package static1;

public class Data3 {
    public String name;
    public static int count; //static 키워드 추가

    public Data3(String name) {
        this.name = name;
        count++; //Data3.count++와 동일. 같은 클래스이기 때문에 Data3를 생략가능.
    }
}
```

```java
package static1;

public class DataCountMain3 {

    public static void main(String[] args) {
        Data3 data1 = new Data3("A");
        System.out.println("A count=" + Data3.count); //1

        Data3 data2 = new Data3("B");
        System.out.println("B count=" + Data3.count); //2

        Data3 data3 = new Data3("C");
        System.out.println("C count=" + Data3.count); //3
    }
}
```

- 정적 변수에 접근하는 방법
    - `Data3.count`와 같이 `클래스명`에 `.`(dot)을 사용 한다.
    - 마치 클래스에 직접 접근하는 것 처럼 느껴진다.

![static 변수](../../java-basic/src/static1/img/static%20변수.png)

- `static`이 붙은 멤버 변수는 `메서드 영역`에서 관리한다.
    - `static`이 붙은 멤버 변수 `count`는 `인스턴스 영역`에 생성되지 않는다. 대신에 `메서드 영역`에서 이 변수를 관리한다.

- 정리
    - `static 변수`는 클래스인 `붕어빵 틀`이 특별히 관리하는 변수이다.
        - `붕어빵 틀`은 1개이므로 `클래스 변수`도 `하나`만 존재한다.
        - 반면에 `인스턴스 변수`는 `붕어빵`인 `인스턴스의 수` 만큼 존재한다.

### static 변수3

- 용어 정리

```java
public class Data3 {
    public String name; //멤버 변수, 인스턴스 변수
    public static int count; //멤버 변수, 클래스 변수 == 정적 변수 == static 변수
}
```

- `멤버 변수`(필드)의 종류
    - `인스턴스 변수`
        - `static`이 붙지 않은 멤버 변수
        - `인스턴스`를 생성해야 사용할 수 있고, `인스턴스`에 소속되어있다.
        - `인스턴스`를 만들 때 마다 새로 만들어진다.
    - `클래스 변수`
        - `static`이 붙은 멤버 변수
        - `클래스 변수`, `정적 변수`, `static 변수`등으로 부른다.
        - `인스턴스`와 무관하게 `클래스`에 바로 접근해서 사용할 수 있고, `클래스` 자체에 소속되어있다.
        - `클래스 변수`는 자바 프로그램을 시작할 때 딱 1개가 만들어진다.
            - `인스턴스`와는 다르게 보통 여러곳에서 공유하는 목적으로 사용된다.

- 변수와 생명주기
    - `지역 변수`(`매개변수` 포함)
        - 지역 변수는 `스택 영역`에 있는 스택 프레임 안에 보관된다.
        - 메서드가 종료되면 스택 프레임도 제거 되는데, 이때 해당 스택 프레임에 포함된 지역 변수도 함께 제거된다.
        - 따라서 지역 변수는 생존 주기가 짧다.
    - `인스턴스 변수`
        - 인스턴스에 있는 멤버 변수를 인스턴스 변수라 한다.
        - 인스턴스 변수는 `힙 영역`을 사용한다.
        - 힙 영역은 GC(가비지 컬렉션)가 발생하기 전까지는 생존하기 때문에 보통 지역 변수보다 생존 주기가 길다.
    - `클래스 변수`
        - 클래스 변수는 `메서드 영역`의 static 영역에 보관되는 변수이다.
        - 메서드 영역은 프로그램 전체에서 사용하는 공용 공간이다.
        - 클래스 변수는 해당 클래스가 JVM에 로딩 되는 순간 생성된다. 그리고 JVM이 종료될때 까지 생명주기가 이어진다.
        - 따라서 가장 긴 생명주기를 가진다.
    - 생명주기 정리
        - `지역 변수`(짧다) < `인스턴스 변수` < `클래스 변수` (길다)
    - `static`이 `정적`이라는 이유
        - 힙 영역에 생성되는 `인스턴스 변수`는 `동적`으로 생성되고, 제거된다.
        - 반면에 `static`인 `정적 변수`는 거의 프로그램 실행 시점에 딱 만들어지고, 프로그램 종료 시점에 제거된다.
            - `정적 변수`는 이름 그대로 정적이다.

- `정적 변수` 접근 법
    - `클래스`를 통해 바로 접근할 수도 있고,
    - `인스턴스`를 통해서도 접근할 수 있다. (`권장하지 않음`)
        - 코드를 읽을 때 마치 인스턴스 변수에 접근하는 것 처럼 오해할 수 있기 때문.

```java
package static1;

public class DataCountMain3 {

    public static void main(String[] args) {
        Data3 data1 = new Data3("A");
        System.out.println("A count=" + Data3.count); //1

        Data3 data2 = new Data3("B");
        System.out.println("B count=" + Data3.count); //2

        Data3 data3 = new Data3("C");
        System.out.println("C count=" + Data3.count); //3

        //추가
        //인스턴스를 통한 접근 (권장하지 않음)
        Data3 data4 = new Data3("D");
        System.out.println(data4.count); //4

        //클래스를 통한 접근
        System.out.println(Data3.count); //4
    }
}
```

### static 메서드1

- 인스턴스 메서드
    - 단점:
        - `deco()` 메서드를 호출하기 위해서는 `DecoUtil1`의 인스턴스를 먼저 생성해야 한다.
```java
package static2;

public class DecoUtil1 {
    public String deco(String str) {
        return "*" + str + "*";
    }
}
```

```java
package static2;

public class DecoMain1 {
    public static void main(String[] args) {
        String s = "hello java";
        DecoUtil1 utils = new DecoUtil1(); //인스턴스 생성
        String deco = utils.deco(s);

        System.out.println("before: " + s);
        System.out.println("after: " + deco);
    }
}
```

- static 메서드
    - 장점:
        - 인스턴스 생성 없이 클래스 명을 통해서 바로 호출할 수 있다.

```java
package static2;

public class DecoUtil2 {
    public static String deco(String str) { //static 추가
        return "*" + str + "*";
    }
}
```

```java
package static2;

public class DecoMain2 {
    public static void main(String[] args) {
        String s = "hello java";
        String deco = DecoUtil2.deco(s); //인스턴스 생성없이 클래스명을 통해서 바로 호출

        System.out.println("before: " + s);
        System.out.println("after: " + deco);
    }
}
```

- `클래스 메서드`
    - `static`이 붙은 메서드
    - `정적 메서드`, `클래스 메서드`라고도 한다.
- `인스턴스 메서드`
    - `static`이 붙지않은 메서드
    - 인스턴스를 생성해야 호출 할 수 있다.

### static 메서드2

- `정적 메서드`는 언제나 사용할 수 있는 것이 아니다.
    - `static 메서드`는 `static`만 사용할 수 있다.
        - 클래스 내부의 기능을 사용할 때, `정적 메서드`는 `static`이 붙은 `정적 메서드`나 `정적 변수`만 사용할 수 있다.
        - 클래스 내부의 기능을 사용할 때, `정적 메서드`는 `인스턴스 변수`나, `인스턴스 메서드`를 사용할 수 없다.
    - 반대로 모든 곳에서 `static`을 호출할 수 있다.

- `정적 메서드`가 `인스턴스`의 기능을 사용할 수 없는 이유
    - 특정 인스턴스의 기능을 사용하려면 참조값을 알아야 하는데, 정적 메서드는 참조값 없이 호출한다.

### static 메서드3

- 정적 메서드 활용
    - 객체 생성 없이 메서드의 호출만으로 필요한 기능을 수행할 때 주로 사용한다.
        - 간단한 메서드로 끝나는 유틸리티성 메서드에 자주 사용한다.

- 정적 메서드 접근법
    - static 변수와 동일.
        - `클래스`로 접근하거나,
            - 예시) `DecoData.staticCall()`
        - `인스턴스`를 통해서 접근가능 (`권장하지않음.`)
            - 예시) `data3.staticCall()`

- static import
  - 해당 메서드를 다음과 같이 자주 호출해야 한다면 `static import`를 사용하자.

```
// import static 적용 전
DecoData.staticCall();
DecoData.staticCall();
DecoData.staticCall();
```

```
// import static 적용 후
staticCall();
staticCall();
staticCall();
```


```java
package static2;

//import static static2.DecoData.staticCall; //특정 클래스의 정적 메서드 하나만 적용
import static static2.DecoData.*; //특정 클래스의 모든 정적 메서드에 적용

public class DecoDataMain {
    public static void main(String[] args) {
        System.out.println("1.정적 호출");
        staticCall(); //클래스 명 생략 가능
        
        //생략
    }
}
```

- `main()` 메서드는 정적 메서드
  - 인스턴스 생성 없이 실행하는 가장 대표적인 메서드
  - 객체를 생성하지 않아도 `main()` 메서드가 작동했다. 이것은 `main()` 메서드가 `static`이기 때문이다.
  - 정적 메서드는 정적 메서드만 호출할 수 있다.
    - 정적 메서드인 `main()`이 호출하는 메서드에는 정적 메서드를 사용했다.

```java
public class ValueDataMain {
    public static void main(String[] args) { //정적 메서드
        ValueData valueData = new ValueData();
        add(valueData);
    }
    
    static void add(ValueData valueData) { //정적 메서드
        valueData.value++;
        System.out.println("숫자 증가 value=" + valueData.value);
    }
}
```

---

## 9. final

### final 변수와 상수1

- 변수에 `final` 키워드가 붙으면 더는 값을 변경 할 수 없다.
- 예시
  - final - 지역 변수
  - final - 필드(멤버 변수)


- final - 필드(멤버 변수)

```java
package final1;

//final 필드 - 생성자 초기화
public class ConstructInit {
    final int value; //생성자를 통해서 한번만 초기화 될 수 있다
    
    public ConstructInit(int value) {
        this.value = value;
    }
}
```

```java
package final1;

//final 필드 - 필드 초기화
public class FieldInit {
    static final int CONST_VALUE = 10; //상수
    final int value = 10; //필드에서 초기화 하는 경우, 모든 인스턴스가 같은 값을 가진다.
}
```

```java
package final1;

public class FinalFieldMain {

    public static void main(String[] args) {
        //final 필드 - 생성자 초기화
        System.out.println("생성자 초기화");
        ConstructInit constructInit1 = new ConstructInit(10);
        ConstructInit constructInit2 = new ConstructInit(20);
        System.out.println(constructInit1.value); //10
        System.out.println(constructInit2.value); //20

        //final 필드 - 필드 초기화
        System.out.println("필드 초기화");
        FieldInit fieldInit1 = new FieldInit();
        FieldInit fieldInit2 = new FieldInit();
        FieldInit fieldInit3 = new FieldInit();
        System.out.println(fieldInit1.value); //10 //모든 인스턴스가 같은 값을 사용하기 때문에 결과적으로 메모리를 낭비하게 된다.
        System.out.println(fieldInit2.value); //10 //중복코드...
        System.out.println(fieldInit3.value); //10 //이럴 때 사용하면 좋은 것이 바로 '상수'이다.

        //상수
        System.out.println("상수");
        System.out.println(FieldInit.CONST_VALUE); //10
    }
}
```

### final 변수와 상수2

- `상수`(Constant)
  - 단 하나만 존재하는 변하지 않는 고정된 값
  - `static final` 키워드 사용
  - `대문자`를 사용하고 구분은 `_` (언더스코어)로 한다. (관례)
  - 필드를 직접 접근해서 사용한다.
    - 상수는 값을 변경할 수 없다. 따라서 필드에 직접 접근해도 데이터가 변하는 문제가 발생하지 않는다.

```java
package final1;

//상수
public class Constant {
    //수학 상수
    public static final double PI = 3.14;
    //시간 상수
    public static final int HOURS_IN_DAY = 24;
    public static final int MINUTES_IN_HOUR = 60;
    public static final int SECONDS_IN_MINUTE = 60;
    //애플리케이션 설정 상수
    public static final int MAX_USERS = 1000;
}
```
- 보통 상수들은 애플리케이션 전반에서 사용되기 때문에 `public`를 자주 사용한다.
  - 특정 위치에서만 사용된다면 다른 접근 제어자를 사용하면 된다
- 상수는 중앙에서 값을 하나로 관리할 수 있다는 장점도 있다.
- 상수는 런타임에 변경할 수 없다.
  - 변경하려면 프로그램을 종료하고, 변경 후 다시 실행해야한다.
- 매직넘버 대신 사용할 수 있다.
  - 매직넘버: 아무 설명없이 덜렁 숫자만 있는경우, 무슨 의미로 쓰인건지 알아보기 어려움.

      ```java
      package final1;
    
      public class ConstantMain2 {
    
          public static void main(String[] args) {
              System.out.println("프로그램 최대 참여자 수 " + Constant.MAX_USERS); // 숫자 1000이 아닌 상수(MAX_USERS) 사용 => 매직넘버 해결.
              int currentUserCount = 999;
              process(currentUserCount++);
              process(currentUserCount++);
              process(currentUserCount++);
          }
    
          private static void process(int currentUserCount) {
              System.out.println("참여자 수:" + currentUserCount);
              if (currentUserCount > Constant.MAX_USERS) { // 숫자 1000이 아닌 상수(MAX_USERS) 사용 => 매직넘버 해결.
                  System.out.println("대기자로 등록합니다.");
              }else {
                  System.out.println("게임에 참여합니다.");
              }
          }
      }
      ```

### final 변수와 참조

- `기본형 변수`가 `final`인 경우
  - 값 변경 불가
- `참조형 변수`가 `final`인 경우
  - 참조값 변경 불가
  - 참조하는 대상의 값은 변경 가능

```java
package final1;

public class FinalRefMain {
    public static void main(String[] args) {
        final Data data = new Data();
        //data = new Data(); //final 변경 불가. 컴파일 오류

        //참조 대상의 값은 변경 가능
        data.value = 10;
        System.out.println(data.value); //10
        data.value = 20;
        System.out.println(data.value); //20
    }
}
```

---

## 10. 상속

---

## 11. 다형성1

---

## 12. 다형성2

---

## 13. 다형성과 설계

---

## 14. 다음으로

---
