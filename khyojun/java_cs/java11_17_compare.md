## Java 11 vs Java 17

![images.jpg](images.jpg)


항상 고민을 하곤 한다. Java 11을 쓸 지 Java 17을 사용할 지 왜냐하면 기본적으로 17이 더 최신으로 나오기도 하였고 LTS라고도 하기도 하고 하지만 결국엔 나중에 프로젝트를 대부분 시작하려고 하면 Spring 2.x 대에서는 거의 다 Java11을 사용하면서 하게 된다.

그래서 이번 사이드 프로젝트를 현재 진행하고 있는데 Spring 3.x 버전으로 넘어가보면서 Java17을 사용해야 사용할 수 있었기에 Java17을 사용했다.

#### 그렇기에 왜 이 버전을 사용하는지 정립할 필요가 있다.


### Java 11에서 Java 17로의 마이그레이션

왜 넘어가야했을까? 너무 당연한 말들이 있겠지만 여러 기능들에 대한 개선도 있을 것이고 했을 것이다. 우선 새롭게 생겨난 몇 가지는 다음과 같다.


### compact한 문자열
> Java 9는 String 개체 의 메모리 소비를 최적화하기 위해 성능이 향상된 Compact String을 도입했습니다 .
간단히 말해서 String 객체는 내부적으로 char[] 대신 byte[] 로 표시됩니다 .
### 텍스트블록
> Java 15 이전에는 여러 줄 코드 스니펫을 포함하려면 명시적인 줄 종결자, 문자열 연결 및 구분 기호가 필요합니다. 이 문제를 해결하기 위해 Java 15는 코드 스니펫과 텍스트 시퀀스를 거의 그대로 포함할 수 있는 텍스트 블록을 도입했습니다 . 이는 HTML, JSON 및 SQL과 같은 리터럴 조각을 처리할 때 특히 유용합니다.
텍스트 블록은 일반적인 큰따옴표 문자열 리터럴을 사용할 수 있는 모든 곳에서 사용할 수 있는 대체 형식의 문자열 표현입니다 . 예를 들어 여러 줄 문자열 리터럴은 줄 종결자와 문자열 연결을 명시적으로 사용하지 않고 표현할 수 있습니다.
```java
// 텍스트 블록을 사용했을 때
String value = """
Multi-line
Text
""";

// 기존 방식으로 표현하였을때
    String value = "Multi-line"
    + "\n" // line separator
    "Text"
    + "\n";
    String str = "Multi-line\nText\n";

```
### 새로운 문자열 메서드
>String 객체를 다룰 때 일반적인 String 작업 을 위해 Apache Commons와 같은 타사 라이브러리를 사용하는 경향이 있습니다 . 특히 공백/비어 있는 값과 반복, 들여쓰기 등과 같은 기타 문자열 작업 을 확인하는 유틸리티 함수의 경우입니다.
그 후 Java 11 및 Java 12는 이러한 일반 문자열 작업에 내장된 함수( isBlank(), repeat(), indent(), lines(), strip() 및 transform()) 에 의존할 수 있도록 편리한 함수를 많이 도입했습니다. .


### Record 
데이터 전송 개체(DTO)는 개체 간에 데이터를 전달할 때 유용하다. 그러나 DTO를 만들려면 필드, 생성자, getter/setter, equals() , hashcode() 및 toString() 메서드 와 같은 많은 상용구 코드가 필요하다.
 
그렇지만 코드로 따져보면 다음과 같을거다.

```java
public class StudentDTO {
    
    private int rollNo;
    private String name;
    
    // constructors
    // getters & setters
    // equals(), hashcode() & toString() methods
}
```

```java
//Record를 사용하면 다음과 같다. 

public record Student(int rollNo, String name) {
}

```

위의 코드를 보다가 밑의 코드를 보면 뭔가 자동으로 다 처리해주는 `Lombok`처럼 보일 수 있다. 정말 기능만 따지면 비슷하다. 이렇게 Record를 사용하면 컴파일러는 public 생성자, private 및 final 필드 외에 equals() ,  hashCode() 및  toString() 메서드를 생성한다.



### 유용한 NPE(NullPointException)

NPE( NullPointerExceptions )는 모든 개발자가 직면하는 매우 일반적인 예외이다. 

대부분의 경우 컴파일러에서 발생하는 오류 메시지는 null 인 것을 확인하기 쉽지가 않다...  

또한 코드를 명시적이고 압축적으로 작성하기 위한 함수형 프로그래밍 및 메서드 체인에 대한 최근 추세로 인해 NPE를 디버그하기가 더 어려워졌다고 한다.

예시를 들면 이러한 예시이다.
> student.getAddress().getCity().toLowerCase();

이렇게 하면 어디가 null인지 개발자가 눈으로 보고 바로 직관적으로 확인하기가 너무 어렵다. 

그래서 vm인수를 사용하여 컴파일러에게 지시하여 유용한 NPE 메시지를 가져올 수 있다. 
```java
- XX:+ShowCodeDetailsInExceptionMessages
```

```
Cannot invoke "String.toLowerCase()" because the return value of "com.baeldung.java8to17.Address.getCity()" is null
```

이렇게 하면 더 쉽게 오류 메시지를 확인할 수 있다.

### 향상된 instanceOf 연산

기존의 방식보다 더 향상된 방식이다. 코드로 보는 것이 더 빠를거 같다.

```java
//이전
if (obj instanceof Address) {
    Address address = (Address) obj; 
    city = address.getCity();
}
//이후
if (obj instanceof Address address) {
    city = address.getCity();
}

```

더 가독성이 좋아진 것을 직관적으로 볼 수 있다. 

### switch 표현식

```java
double circumference = switch(shape) {
    case Rectangle r -> 2 * r.length() + 2 * r.width();
    case Circle c -> 2 * c.radius() * Math.PI;
    default -> throw new IllegalArgumentException("Unknown shape");
};
```

기존과 좀 다른 것이 있는거 같다. 어디일까?

바로 break 구분이 없어졌다. 그리고 case 뒤에 :도 없어졌다. 그리고 표현 방식도 -> 를 사용하여 바로 표현을 할 수 있도록 하였다. 이건 람다를 지원하는 것임으로 더 효율성있게 사용할 수 있을 것 같다. 

### 봉인된 클래스

Java 17 에서 추가된 Sealed Class/Interface 는 상속하거나(extends), 구현(implements) 할 클래스를 지정해두고, 해당 클래스들만 상속/구현이 가능하도록 제한하는 기능이다.
이를 통해 개발자는 어떤 클래스가 해당클래스를 상속받는지를 쉽게 알수 있고 제한할 수 있다.

```java
// Character.java
public sealed class Character permits Hero, Monster {}
...

// Hero.java
// permits 로 선언된 class 들 (Link , Mario) 만이 Hero class 를 상속할 수 있다.
public sealed class Hero extends Character permits Link, Mario {}
...

// Monster.java
// non-sealed 로 선언된 Monster 는 어떤 class 든지 상 속 할 수 있다.
public non-sealed class Monster extends Character {}
```

뭐 이렇게 있다고 하면 

```java
// Hero 를 상속 받을 수 있는 클래스는 Link, Mario 뿐이다.
public final class Link extends Hero {}
public final class Maro extends Hero {}
// Link 와 Mario 는 final 로 선언된 class 들이기 때문에,
// 어떠한 class 도 이 둘을 상속 할 수 없다.


public class Troll extends Hero {} // 상속 불가능, 에러
public class Troll extends Link {} // 상속 불가능, 에러
//
public class Troll extends Monster {} // 상속 가능
```

즉, 더 직관적으로 어떤 클래스들이 상속 받을수 있고 없는지에 대한 것을 알 수 있을 것이다. 더 객체지향의 특징들을 잘 살릴 수 있을 것이다.



### Spring 3.x부터 Java 17을 사용해야 하는 이유

1. Spring Framework 6이 JDK 11을 건너뛰고 JDK 17을 선택한 이유는 JDK 11이 commercial support 기간이 JDK 8보다 짧고 이미 2023년 말에 단계적으로 중단되며 반면 JDK 17은 최소한 2026년까지 support 기간이 있기 때문에 JDK 11을 과도기 relese로 보기 때문이라고 한다.

2. Java EE는 Servlet, JSP, JSF, JMS, JPA, JTA, EJB, Java Mail, JDBC, JNDI 등의 수많은 기능을 포함하고 있는데 오라클이 이를 포기하면서 이클립스 재단으로 넘어갔고 Jakarta EE로 명칭이 변경되었다.

> 스프링 공식 블로그 추신 : JDK 11이 LTS 세대인지 궁금하신 분은 JDK 11의 상용 지원 기간이 JDK 8보다 짧고 JDK 11 LTS가 이미 2023년 말에 단계적으로 중단된다는 점에 유의하세요. 차세대 LTS인 JDK 17은 적어도 2026년까지 지원 기간을 제공할 것입니다. 우리는 JDK 8이 생태계에서 고유한 역할을 한다고 생각합니다. 이에 비해 JDK 11은 과도기적 릴리스입니다. 또한 JDK 17은 누적된 최신 언어, API 및 JVM 향상 기능을 제공하여 더욱 매력적인 업그레이드가 되었습니다. 마지막으로 중요한 것은 동일한 Spring Framework 6.x 세대 내에서 29 LTS(2027년)까지 JDK 릴리스가 계속 지원되어 결국 지원 범위가 다소 광범위한 JDK 17-29로 바뀔 것입니다.

요약하면 JDK 11은 슬슬 2023년 말부터 단계적으로 지원이 중단되기 때문에 더 최신 버전이고 발전하고 있는 JDK 17로 넘어가자! 이 말이다.

### 결론

당연한 말이겠지만 계속해서 이전 버전보다 버전업이 되면 더 좋아지는 부분이 많아지고 개선되는 부분들이 많아질 것이다.
여러 위에서 말한 이유들에 의해서 결국엔 우린 Java 11에서 Java 17로 넘어갈 준비를 해야하고 결국엔 넘어가야 하니 어떤 차이가 있어서 넘어가는지에 대한 건 어느정도는 알고 있어야 겠다.  


### 출처

- https://spring.io/blog/2021/09/02/a-java-17-and-jakarta-ee-9-baseline-for-spring-framework-6
- https://www.baeldung.com/java-migrate-8-to-17
- https://velog.io/@wwe221/Java-17-Sealed-Class
- https://luvstudy.tistory.com/165
- https://mydeveloperplanet.com/2021/09/28/whats-new-between-java-11-and-java-17/