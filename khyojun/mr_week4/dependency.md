# 스프링 프레임워크의 핵심 기능

이 글은 스프링 프레임워크 첫 걸음을 보고 정리한 글입니다.

---

## 의존성


DI에 대해서 보기전에 우선 의존성이라는 단어에 대해서 생각해 볼 필요가 있다.

객체의 관점에서 보게 되면 A, B클래스가 있다고 할 때 A클래스에서 B클래스를 사용한다고 하면 다음과 같을거다.

```java

public class B{
    
   /* void method1(){

        System.out.println("hello");
        
    }*/
    
    void method2(){
        System.out.println("hello world");
    }
    
    
}
public class A{
    
    B b = new B();
    b.method1();
    
}
```


![dependency.webp](dependency.webp)


위 경우 처음엔 A 클래스는 B 클래스에 의존한다고 말을 한다. 왜냐하면 B클래스의 method1을 method2로 바꾸게 된다면 기존의 A 클래스에 있던 method1이라고 호출했던 부분까지 변경의 영향이 가게 된다. 이랬을때 `A 클래스는 B 클래스에 의존한다.` 라고 표현을 한다.

그리고 또 다른 말로 표현하면
> 한 클래스나 객체가 다른 클래스나 객체를 사용하거나 다른 클래스나 객체와 상호작용을 하는 것을 의존성이라고 표현한다.


**책에서는 의존하는 유형에는 2가지가 있다고 얘기를 한다.**

- 클래스 의존
- 인터페이스 의존


### 클래스 의존

```java

public class A{
    
    B b = new B();
    b.method1();
    
}

public class B{

void method1(){
    
}

}


public class C{

void method2(){
    
}

}
```

위에 있는 A에서 B의 method1을 사용하고 있었는데 만약 여기서 C 클래스의 method2를 사용하고 싶다면 어떻게 해야할까? B객체를 C객체로 바꾸고 호출하는 부분도 바꿔야한다. 그러니까 **즉, 말하자면 클래스에서의 의존성이라는 것은 한 클래스에서 변경이 일어날때 다른 클래스에서에 까지 영향이 계속 미치게 된다면 그것을 클래스간의 의존성이 생겼다고 말할 수 있는 것이다.**



### 인터페이스 의존

인터페이스를 사용을 한다.. 라는 말은 어떤 의미로 하면 완전 구현 클래스가 아닌 추상화를 시킨 클래스를 이용하는 것이다.



```java

public interface A{
    
    void methodX();
    
}

public class AA{
    
    // A a=new B();
    // a.methodX();
    
    A a= new C();
    a.methodX();
    
}



public class B implements I{
    @Override
    void methodX(){
        System.out.println("I'm B");
    }
    
    
}



public class C implements I{

    @Override
    void methodX(){
        System.out.println("I'm C");
    }
}
```

만약 이런 상황에서 C에 있는 methodX를 사용하고 싶다면 아까와는 다르게 `new B()` 를 `new C()` 로 바꾸기만 하면 된다.

![di.png](di.png)

**이렇게 봤을 때 클래스에서의 의존성과 인터페이스의 의존성을 봤을때 상대적으로 인터페이스의 의존성이 더 낮다는 것을 알 수 있다!**


위에 있는 모든 상황을 요약해보면 다음과 같다.

> 의존관계를 클래스가 아닌 인터페이스로 추상화하게 되면, 더 다양한 의존 관계를 맺을 수가 있고, 실제 구현 클래스와의 관계가 느슨해지고, 결합도가 낮아진다.

### DI 컨테이너

앞에서 계속 의존성이라는 것에 대해서 알아봤는데 DI 즉 의존성 주입은 그러면 말 뜻을 풀어보면 **의존하는 부분을 외부에서 주입한다.** 라고 말할 수 있다.

한 번 코드로 보자.


```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

    public BurgerChef() {
        burgerRecipe = new HamBurgerRecipe();
        //burgerRecipe = new CheeseBurgerRecipe();
        //burgerRecipe = new ChickenBurgerRecipe();
    }
}

interface BugerRecipe {
    newBurger();
    // 이외의 다양한 메소드
}

class HamBurgerRecipe implements BurgerRecipe {
    public Burger newBurger() {
        return new HamBerger();
    }
    // ...
}

```


이런 관계가 잇다고 했을때 BugerChef가 내부적으로 어떤 bugerRecipe를 만들지 결정하고 있다.

더 생각해봐서 이 상황에서 만약 어떤 레시피를 사용할 지 본인이 선택하지 않고 외부(사장)님이 결정하게 되는 것을 Dependency Injection이라고 흔히 불리는 것이다.

> DI: 의존관계를 외부에서 결정하고 주입하는 것
>
> 토비의 스프링에서는 다음 세 가지를 충족하는 작업을 DI라고 부르기로 했다.
> - 클래스 모델이나 코드에는 런타임 시점의 의존관계가 드러나지 않는다. 그러기 위해서는 인터페이스만 의존하고 있어야 한다.
> - 런타임 시점의 의존관계는 컨테이너나 팩토리 같은 제3의 존재가 결정한다.
> - 의존관계는 사용할 오브젝트에 대한 레퍼런스를 외부에서 제공(주입)해줌으로써 만들어진다.


> 컴파일 시점, 런타임 시점
> - 컴파일 시점 : 컴파일 과정을 하고 있는 때
    >   - compile error: syntax error 등등이 일어난다.
> - 런타임 시점 : 프로그램이 동작하는 때
    >   - runtime error: 문법적인 오류가 아닌 실행을 한 후에야 감지하는 에러인 것이다. -> 배열의 index 문제, NPE같은 문제


### 이런 시점이 있는데 중요한 것은 어느 시점에 의존성을 가지게 되냐가 중요!


> - 컴파일 타임 의존성 : 컴파일타임 의존성이란 코드를 컴파일하는 시점에 결정되는 의존성이며, 클래스 사이의 의존성에 해당한다. **일반적으로 추상화된 클래스나 인터페이스가 아닌 구체 클래스에 의존하면 컴파일타임 의존성을 갖게된다.**
> - 런타임 의존성 : 런타임 의존성이란 코드(애플리케이션)를 실행하는 시점에 결정되는 의존성이며, 객체 사이의 의존성에 해당한다. **일반적으로 추상화된 클래스나 인터페이스에 의존할 때 런타임 의존성을 갖게 된다.**



즉, 런타임에서 의존관계가 결정된다는 말은 다음 코드를 보면 된다.

```java
class BurgerChef {
    private BurgerRecipe burgerRecipe;

    public BurgerChef(BurgerRecipe burgerRecipe) {
        this.burgerRecipe = burgerRecipe;
    }
}

class BurgerRestaurantOwner {
    private BurgerChef burgerChef = new BurgerChef(new HamburgerRecipe());

    public void changeMenu() {
        burgerChef = new BurgerChef(new CheeseBurgerRecipe());
    }
}
```

위와 같은 코드를 봤을때 `BugerChef`의 입장에서 보면 `BugerRecipe`는 사장님이 결정을 해줘야지 어떤 버거를 만들지 알 수가 있다. 이처럼 외부에서 주입을 하는 것이다.




### 컴파일타임 의존성과 런타임 의존성 차이 및 비교 정리
- 컴파일타임 의존성
   - 코드를 컴파일하는 시점에 결정되는 의존성
   - 클래스 사이의 의존성
   - 결합도가 높으며 변경에 유연하지 못함
- 런타임 의존성
   - 코드(애플리케이션)를 실행하는 시점에 결정되는 의존성
   - 객체 사이의 의존성
   - 결합도가 낮으며 변경에 유연함

사실 의존성을 주입하는 방법으로는 크게 또 3가지가 있다.

1. 필드 주입
   - 개발자 입장에서는 너무 편한 방법이다.
   - 외부에서 변경이 불가능하여 테스트하기가 힘들다.
   - DI 프레임워크가 없다면 아예 주입할 수가 없다.
   - 그러니까 되도록 사용하지 말자.
      - 애플리케이션의 실제 코드와 관계 없는 테스트 코드에서는 사용
      - 스프링 설정 목적으로 하는 @Configuration 같은 곳에서만 특별히 사용
2. **생성자 주입**
   - 생성자 호출 시점때 단 1번만 호출하는 것이 보장
   - 불변, 필수 의존관계에 사용
   - 대부분 이 방식 사용
   - **final 키워드를 넣을 수 있어서 실수를 방지하게 도와준다.(잘못 사용할 경우 컴파일 오류를 발생시킴)**
3. setter 주입
   - 선택, 변경 가능성 있는 의존관계에 사용
   - 자바빈 프로퍼티 규약의 수정자 메서드 사용 방식
4. 일반 메서드 주입
   - 생성자 주입이랑 별로 다를게 없는 방식




### 그래서 그럼 보통 어떻게 하는데?

대부분 보면 알겠지만 `생성자 주입`을 거의 다 사용한다. 위의 특징을 적어놨었는데 생성자 주입을 주로 사용하는 이유는 다음과 같다.

1. 불변
   - setter와 같은 경우에는 외부에서 수정이 가능해버릴 수 있기 때문에 어떻게 바뀔 지 나중에 알 수가 없다.
   - 그래서 1번만 호출되는것이 보장된 생성자 주입을 사용하면 위와 같은 걱정을 할 필요가 없다.
2. 실수 방지
   - 컴파일 오류를 일으켜서 프로그램을 실행시키기전에 실수를 방지할 수가 있다.
   - final 키워드를 사용해서 NPE가 발생하지 않도록 방지할 수 있다.


## Spring을 사용하여 DI 컨테이너 사용해보기

책에서는 다음과 같은 다섯 가지 규칙이 있다고 말한다.
> - 인터페이스를 이용하여 의존성을 만든다.
> - 인스턴스를 명시적으로 생성하지 않는다.
> - 어노테이션을 클래스에 부여한다.
> - 스프링 프레임워크에서 인스턴스를 생성한다.
> - 인스턴스를 이용하고 싶은 곳에 어노테이션을 부여한다.


어노테이션을 클래스에 부여함으로써 인스턴스가 생성이 된다는 말이다. 우리가 대표적으로 알 수 있는 것이 `@Component` 라는 친구이다.

```java
@Component
public class A{
    
    
}
```
스프링 프레임워크가 @Component라고 붙여있는 클래스의 인스턴스를 만든다. 이러한 @Component는 @ComponentScan이라는 어노테이션을 통해서 찾게 된다.


```java
@SpringBootApplication
public class Application {

   public static void main(String[] args) {
      SpringApplication.run(ThymeleafBasicApplication.class, args);
   }

}


@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
        @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })

```


사실 우리가 매번 스프링을 사용하면서도 인식하고 있지는 않았지만 `@SpringBootApplication`안에 `@ComponentScan`이 들어가 있다. 그렇기에 해당 프로젝트의 모든 패키지를 스캔을 하게 되었던 것이다.

사실 `@ComponentScan`은 본인 포함 하위 패키지들에 있는 `@Component`를 찾는다!

그리고 용도마다 사실 @Component를 내부에 포함하면서 다른 의미를 내포하고 있는 어노테이션들도 있다. 대표적으로 아래와 같은 어노테이션이 있다.

- @Controller : 인스턴스 생성 지시, 스프링 MVC를 이용할 때 컨트롤러에 부여
- @Service : 인스턴스 생성 지시, 트랜잭션 경계까 되는 도메인(서비스) 기능에 부여
- @Repository : 인스턴스 생성 지시, 데이터베이스 액세스(리포지토리) 기능에 부여
- @Component : 위 용도 이외의 클래스에 부여



### @Autowired

위에서 Spring을 이용해서 DI 컨테이너를 사용하는데 그러면 그렇게 생성한 인스턴스를 컨테이너에 꺼내와서 하는 여러가지 방법들이 있다고 했는데 어노테이션으로써는 @Autowired를 선언함으로써 해당하는 타입에 일치하는 객체의 인스턴스를 끌고 온다.

여기에서 해당하는 타입에 일치한다는 말은 즉, **구현체** 를 의미하는 것이다.

아까 말한 대표적인 예시로 생성자 주입을 사용하면 다음과 같이 선언하게 된다.

아래의 표는 현재 DI 컨테이너에 저장된 내용이다.

| 빈 이름               | 빈 객체                  
|--------------------|-----------------------|
| CheezeBurgerRecipe | CheezeBugerRecipe@x01 |


```java
A라는 클래스에서 


public interface BugerRecipe{
    
    
    //메서드들 
}

@Component
public class CheezeBurgerRecipe{
    
}


public class BugerChef{
    
    private final BugerRecipe bugerRecipe;
    
    @Autowired // 생성자가 하나일때는 @Autowired를 생략해도 자동으로 붙여준다. 
    public BugerChef(BugerRecipe bugerRecipe){
        this.bugerRecipe=bugerRecipe;
    }
    // BugerRecipe는 인터페이스이다. 그에 해당하는 구현체들 클래스에는 @Component가 붙어있어서 DI컨테이너에 등록된 상태이다.
    
}
```


---

## 어노테이션 역할 알아보기


### 어노테이션을 세 가지 항목으로 설명

> - 어노테이션은 주석을 의미하는 영어 표현이다.
> - @xxx 와 같은 형태로 작성이 된다.
> - 외부 소프트웨어에 필요한 처리 내용을 전달한다.


### 레이어별로 사용할 인스턴스 생성 어노테이션

보통 레이어를 나누면 다음과 같이 나눈다고 한다.

- 애플리케이션(Application) 레이어 : 애플리케이션 레이어는 클라이언트와의 데이터 입출력을 제어하는 레이어다.
- 도메인(Domain) 레이어 : 도메인 레이어는 애플리케이션의 중심이 되는 레이어로서 업무 처리를 수행하는 레이어이다.
- 인프라스트럭처(Infrastructure) 레이어 : 인프라스트럭처 레이어는 데이터베이스에 대한 데이터 영속성(Persistence Context)등을 담당하는 레이어이다.


위 내용은 나중에 다루게 되니 그 때 더 자세히 살펴보는 것으로 하자.



우리가 이전에 봤던 @Controller, @Service, @Repository같은 것들도 어찌보면 레이어별로 구분이되는 것이다.

- @Controller : 애플리케이션 레이어의 컨트롤러에 부여
- @Service :  도메인 레이어의 업무 처리에 부여
- @Repository :  인프라 레이어의 데이터베이스 액세스 처리에 부여


### 커스텀 어노테이션

커스텀으로도 어토에시녕르 만들 수 있따. `java.lang.Annotation` 인터페이스를 상속하고 만들게 된다. 이 부분은 구글링 해보면 더 자세히 나온다.

https://mangkyu.tistory.com/130 해당 글에서 만드는 방법이 나와있으니 참고해보면 좋을 거 같다.


위의 글을 참고하다보면 여러 어노테이션이 추가로 나온다. 커스텀 어노테이션을 만들 때 사용하는 어노테이션인데 이를 `메타 어노테이션`이라고 부른다. 다음과 같은 종류들이 있다.


#### @Target

> 커스텀 어노테이션이 무엇을 대상으로 하고 있는지 선언하기 위해 사용

| ElementType 요소              | 추가할 대상                      
|-----------------------------|-----------------------------|
| ElementType.ANNOTATION_TYPE | 어노테이션                       |
| ElementType.CONSTRUCTOR     | 생성자                         |
| ElementType.FIELD           | 필드                          |
| ElementType.METHOD          | 메서드                         |
| ElementType.PACKAGE         | 패키지                         |
| ElementType.PARAMETER       | 인수                          |
| ElementType.TYPE            | 클래스,인터페이스(어노테이션, enum 포함)   |


#### @Retention

> 컴파일할 때나 프로그램을 실행할 때 '어노테이션'의 정보를 보관 및 유지하는 유효 범위를 결정하기 위해 사용.


| 상수      | 내용                                    
|---------|---------------------------------------|
| SOURCE  | 소스가 유효 범위이다. 컴파일할 때 어노테이션 정보가 삭제된다.   |
| CLASS   | 클래스 파일은 유효하지만 JVM에는 읽어 들이지 않는다.(기본값)  |
| RUNTIME | 실행 중일 때 JVM에서 참조할 수 있는 가장 넓은 유효 범위이다. |


#### @Documented

> 지정된 어노테이션을 Javadoc API 문서를 출력할 때 표시되게 한다.


#### @Inherited

> 지정한 어노테이션을 부여한 클래스를 상속하면 하위 클래스도 그 어노테이션을 부여한 것으로 설정한다.

---

## AOP 기초 지식

책에서 다루는 내용이 그렇게 깊지는 않다. 일단 용어를 익히는 식으로 알고 계속 진행하면 될 거 같다.

### AOP 예시

>AOP : Aspect Oriented Programming의 약자로 관점 지향 프로그래밍이라고 불린다. 관점 지향은 쉽게 말해 어떤 로직을 기준으로 핵심적인 관점, 부가적인 관점으로 나누어서 보고 그 관점을 기준으로 각각 모듈화하겠다는 것이다.

우선 관점 지향으로 본다는 것인데 다음과 같은 예제가 있다.

> DB 액세스 처리에는 예외 발생 시 처리하는 내용이 반드시 포함이 된다.
> 다수의 데이터베이스 액세스 처리 코드를 작성하다 보면 예외 처리 내용은 동일하지만 예외 처리는 필수여서 항상 작성해야 한다.
> 구현하고 싶은 프로그램은 DB 액세스 처리이지만 예외 처리는 구현하고 싶은 프로그램에 부수적인 내용으로 바라볼 수 있다.

이처럼 스프링 프레임워크에서 제공하는 AOP 기능을 활용하여 `중심적 관심사`와 `횡단적 관심사`를 분리하여 프로그램을 쉽게 만들 수 있다.


| 용어                | 내용                                                                                      
|-------------------|-----------------------------------------------------------------------------------------|
| 어드바이스(Advice)     | 횡단적 관심사의 구현(메서드). 로그 출력 및 트랜잭션 제어등등                                                     |
| 애스펙트(Aspect)      | 어드바이스를 정리한 것(클래스)dlek.                                                                  |
| 조인포인트(JoinPoint)  | 어드바이스를 중심적인 관심사에 적용하는 타이밍. 메서드(생성자) 실행 전, 메서드(생성자) 실행 후 등 실행되는 타이밍이다.<br/>              |
| 포인트컷(Pointcut)    | 어드바이스를 삽입할 수 있는 위치. 예를 들면, 메서드 이름이 get으로 시작할 때만 처리하는 조건 정의 가능                           |
| 인터셉터(Interceptor) | 처리의 제어를 인터셉트하기 위한 구조 또는 프로그램. 스프링 프레임워크에서는 인터셉트라는 메커니즘으로 어드바이스를 중심 관심사에 추가한 것처럼 보이게 한다. |
| 타겟(Targer)        | 어드바이스가 도입되는 대상을 말한다.                                                                    |


스프링 프레임워크에서는 '인터셉터'라는 메커니즘을 사용해서 횡단적 관심사(advice)를 중심적 관심사(targer)에 삽입하는 것처럼 보일 수 있다.


그래서 구조상으로 보면 다음과 같다.

> - A클래스 : X메서드 호출
> - B클래스 : X메서드안에 중심적 관심사, 횡단적 관심사가 들어있다.
>
> 위 구조를
>
> - A클래스 : X메서드 호출
> - B클래스 : X메서드안에 중심적 관심사
> - 애스팩트 : 어드바이스(횡단적 관심사 분리)

아래처럼 바꾸는 상황이다. 그런데 사실 내부적으로는 AOP 프록시(스프링 프레임워크가 자동 생성)가 가초새고 X 메서드 및 어드바이스의 호출을 제어하게되는 구조이다.

![aop_proxy.png](aop_proxy.png)

사실 다음과 같이 되어있는 구조인 것이다.

스프링 프레임워크가 제공하는 중심적 관심사에 적용하는 어드바이스는 실행 제어 내용별로 다섯 가지 종류가 있다.



| 어드바이스                  | 내용                                                        | 어노테이션           |  
|------------------------|-----------------------------------------------------------|-----------------|
| Before Advice          | 중심적 관심사가 실행되기 '이전'에 횡단적 관심사를 실행                           | @Before         |
| After Returning Advice | 중심적 관심사가 '정상적으로 종료된 후'에 횡단적 관심사를 실행 어노테이션                 | @AfterReturning |
| After Throwing Advice  | 중심적 관심사로부터 '예외가 던져진 후'로 횡단적 관심사를 실행 어노테이션                 | @AfterThrowing  |
| After Advice           | 중심적 관심사의 '실행 후'에 횡단적 관심사를 실행(정상 종료나 예외 종료 등의 결과와 상관없이 실행) | @After          |
| Around Advice          | 중앙적 관심사 호출 전후에 횡단적 관심사를 실행                                | @Around         |



### 포인트컷 식

여러가지 종류의 포인트컷 표현식이 있지만 이 책에선 'execution' 지시자를 설명한다.

- execution 지시자의 구문 : execute(반환값 패키지.클래스.메서드(인수))


### 스프링 프레임워크가 제공하는 AOP 기능 (@Transactional)


```java
@Service
@Transactional
public class xxxService{
    xxxRepository.insert
}

```

이런식으로 진행이 된다면 아래와 같은 구조로 진행이 된다.

![@Transactional.jpg](%40Transactional.jpg)


해석해보면 횡단적 관심사 중심적 관심사는 다음과 같다.

- 횡단적 관심사 : Transaction 처리
- 중심적 관심사 : DB 액세스 처리

너무 많은 용어들이 나오고 아직 깊게 보진 않고 얕게 보긴 하였지만 AOP 프로그래밍을 한 문장으로 정리하면 다음과 같다.

> 중단적 관심사(비즈니스 로직), 횡단적 관심사(부수적 기능)를 분리하여 프로그래밍을 한다.





- 출처
   - https://tecoble.techcourse.co.kr/post/2021-04-27-dependency-injection/
   - https://yeko90.tistory.com/entry/compile-time%EC%BB%B4%ED%8C%8C%EC%9D%BC-%ED%83%80%EC%9E%84-vs-runtime%EB%9F%B0%ED%83%80%EC%9E%84-%EC%B0%A8%EC%9D%B4
   - https://www.javatpoint.com/compile-time-vs-runtime
   - https://www.prkrdevblog.com/transactional-annotation-simplified/
   - https://mangkyu.tistory.com/226

