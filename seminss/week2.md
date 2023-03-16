[//]: # (- SOLID 좋은 객체 지향 설계)
[//]: # (- Spring이 나오게 된 이유)


## DI, IOC, Spring Bean

### DI : Dependency Injection (의존성 주입)

- 외부에서 두 객체 간의 관계를 결정해주는 디자인 패턴이다.
- 인터페이스를 사이에 둠으로써, 클래스 레벨에서는 의존관계가 고정되지 않도록 하여, 런타임 시에 관계를 동적으로 주입한다.

`public Store() { this.pencil = new Pencil() }`을 보면, Store 클래스와 Pencil 클래스가 강하게 결합되어 있다.

Pencil, Food 등 여러 제품을 하나로 표현하기 위한 Product라는 인터페이스 및,
해당 인터페이스의 구현체 Pencil을 선언해보자. 

`public interface Product { }`
`public class Pencil implements Product { }`

그럼 다음과 같은 코드 작성이 가능해진다.

``` 
public class Store {

    private Product product;

    public Store(Product product) {
        this.product = product;
    }

} 
```
위 코드를 보면 외부에서 상품을 "주입" 받고 있다. Store이 구체 클래스를 의존하지 않기 위함이다.

이러한 이유로 Spring이라는 DI 컨테이너를 필요로 한다.

Store에서 Product 객체를 주입하기 위해서는 어플리케이션 실행 시점에 
필요한 객체(빈) 을 생성해야 하며, 의존성이 있는 두 객체를 연결하기 위해 한 객체를 다른 객체로 주입시켜야 한다.

- 두 객체의 관계라는 관심사 분리
- 두 객체 간의 결합도를 낮춤
- 객체의 유연성을 높임
- 테스트 작성을 용이하게 함

<br>

### IOC : Inversion of Control (제어의 역전)

-  프로그램의 흐름을 개발자가 관리하는 것이 아닌, 외부에 맡긴다는 뜻이다.



출처 : https://mangkyu.tistory.com/150

<br>

### 스프링 빈과 빈 컨테이너
스프링은 실행시 빈 컨테이너(Bean Factory 또는 ApplicationContext)를 만든다.
이때 componentScan 같은 과정을 거쳐서 자바의 객체들을 빈으로 등록하게 된다.

그럼, 빈으로 등록하는 이유는 무엇일까? 

DI, IOC 개념과 연결된다.

런타임 시 빈컨테이너에 빈(자바 객체)들이 등록되어 있고,
프로그래머가 작성한 코드에서 특정 객체를 필요로 한다면, 스프링 프레임워크가 해당 객체(빈)을 알아서 주입해준다!

개발자는 직접 new classB() 같은 것들을 호출할 필요가 없어지는 것이다.

빈을 주입하는 방식은 생성자 주입, Setter 주입, 필드 주입 등 다양하지만, 스프링에서는 생성자 주입을 권장한다!

- 스프링 빈으로 등록된 객체는 applicationContext(main에 붙어있음)라는 빈 컨테이너에 등록되어, 런타임시 필요로 하는 곳에 의존성을 주입해준다.
- 더불어, 런타임시 필요로 하는 곳에 자바 객체를 주입해 준다.


---
## RestControllerAdvice

---
## @Transactional 어노테이션

---
## JPA

---
## REST API

---
## 컨트롤러에서 사용자가 보낸 HTTP 내 값 받기


---
## 엔티티와 DTO




