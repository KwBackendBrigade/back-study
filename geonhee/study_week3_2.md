# Spring Bean이란?
- - - 
> **Spring IoC 컨테이너가 관리하는 자바 객체**를 **빈(Bean)** 이라고 부른다.
>>기존 자바에서는 클래스를 만들고 new()로 객체를 생성하여 사용하였다. Spring에서는 이렇게 직접 생성하는 것이 아닌 Spring에 의하여 관리 당하는 객체를 사용한다. **이렇게 Spring에서 관리하는 객체를 Spring Bean이라고 한다.**

- _위에서 나온 Ioc와 IoC 컨테이너는 무엇일까?_

>>### IoC(제어 반전) :
>>- 객체의 생성, 생명주기의 관리까지 모**든 객체에 대한 제어권이 바뀌었다는 것**을 의미
>> - 이전까지 객체를 직접 생성하여 메소드 호출을 했다. **즉 사용자가 모든 작업을 제어하는 구조**였다.
     하지만 IoC가 적용된 경우, **객체의 생성을 특별한 관리 위임 주체에게 맡긴다.** 이 경우 **사용자는 객체를 직접 생성하지 않고, 객체의 생명주기를 컨트롤하는 주체는 다른 주체**가 된다.
- - - 
>>### IoC 컨테이너 :
>>- **컨테이너** : 컨테이너는 보통 **객체의 생명주기를 관리, 생성된 인스턴스들에게 추가적인 기능을 제공**하도록 하는 것
>>- Spring에서 컨테이너 역할을 해주는 것이 **Spring 컨테이너(IoC 컨테이너)**
>>- 인스턴스 생성부터 소멸까지의 **인스턴스 생명주기 관리를 개발자가 아닌 컨테이너가 대신** 해준다.
>>- 객체 관리 주체가 사용자가 아니므로 사용자는 로직(Logic)에 집중 가능하다.

- - - 
# Component Scan

> Spring Bean을 Container에 등록하기 전 꼭 알아야 하는 개념이 **Component Scan**이다.
> - _**Component Scan이란?**_
>> - Component scan은 S**pring Framework에서 자동으로 Bean을 검색하고 등록하는 기능**이다. 이 기능을 사용하면 개발자가 Bean을 일일이 등록하지 않고도, 자동으로 Bean을 검색하여 등록할 수 있다.
>> - **즉 Spring이 Spring Bean으로 등록될 준비가 된 클래스들을 스캔하여 Bean으로 등록해주는 과정을 말한다.**
> - _**@Component**_ Annotation(어노테이션)이 붙어 있는 클래스들은 자동적으로 컴포넌트 스캔의 대상이 된다.

- - -



### Spring Bean을 Spring IoC Container에 등록하는 방법 2가지
* _DI 주입은 setter 주입, 필드 주입, 생성자 주입이 있지만 여기서는 생성자 주입 위주로 설명_

> #### 1.  Annotation(어노테이션)을 사용하여 생성자에 등록
> @Controller   
> @Service   
> @Repository
>

- _잠깐 ! 위에서 Component Scan에 등록하려면 @Component Annotation이 있어야 하는데 위에 Annotation들은 어떻게 등록하는 걸까?_
> 사실 **위에 있는 Annotation들의 속을 파보면 @Component가 내장**되어 있다. 다만 종류에 따라 겉을 다르게 만들었다고 보면 될 것 같다 !

> - 다시 본론으로 돌아와서 위 3개의 의존 관계는 다음과 같다.
    **Controller -> Service -> Repository**
    _예시를 코드로 나타내면_
- - - 
>
>```java
>@Controller // Controller Annotation 등록
>public class MemberController {    
>
>	private final MemberService memberService;
>
>	@Autowired
>	public MemberController(MemberService memberService) {
>		this.memberService = memberService;
>	}
>}
>```
>- - - 
>
>```java
>@Service // Service Annotation 등록
>public class MemberService {
>
>	private final MemberRepository memberRepository;
>
>	@Autowired
>	public MemberService(MemberRepository memberRepository) {
>		this.memberRepository = memberRepository;
>	}
>}
>```
>- - - 
>
>```java
>@Repository //Repository Annotation 등록
>public class MemoryMemberRepository implements MemberRepository {}
>```
>- 생성자에 **_@Autowired_** 가 있으면 **스프링이 연관된 객체를 Spring 컨테이너에서 찾아서 넣어준다.** **이렇게 의존관계를 외부에서 넣어주는 것을 _DI(Dependency Injection), 의존성 주입_** 이라고 한다.
>- 이전 테스트에서는 개발자가 직접 주입했고, 여기서는 **@Autowired**에 의해 **스프링이 주입**해준다.

>####  2. Bean Configuration File에 직접 Bean 등록하는 방법
>- _자바 코드로 직접 등록하는 방법 :_
   > **@Bean** 와 **@Configuration**을 이용해 Configuration File에 등록
> - 따로 클래스를 생성한다음 @Configuration Annotation을 등록한 다음, 생성자에 @Bean을 붙여준다. 예시는 아래와 같다.
>```java
>@Configuration //Configuration File이라고 명시
>public class SpringConfig {
>
>	@Bean //@Bean을 이용하여 Bean Container에 수동 등록
>	public MemberService memberService() {
>		return new MemberService(memberRepository());
>		}
>
>
>	@Bean
>	public MemberRepository memberRepository() {
>		return new MemoryMemberRepository();
>		}
>	}
>```

_위 방법을 적용한 그림은 다음과 같다._
![](https://velog.velcdn.com/images/ghlee00125/post/067e2479-994b-41d1-8658-15dbeda52a15/image.png)


- - - 

# Component Scan은 어떤 과정을 거칠까?

>1. 스프링이 컨텍스트를 로드하면, 컨텍스트는 스프링의 **빈 팩토리(Bean Factory)** 를 만든다.
>2. 컨텍스트는 클래스 경로를 스캔하고, **@Component, @Controller, @Service, @Repository 등의 어노테이션이 붙어있는 클래스를 찾는다.**
>3. 찾은 **클래스를 인스턴스화하여 빈으로 등록**한다. 이때, 클래스 이름의 첫 글자를 소문자로 바꾼 이름을 빈의 이름으로 사용한다. 예를 들어, MyClass 클래스가 빈으로 등록되면, 빈의 이름은 "myClass"가 된다.

- - - 

출처 : https://melonicedlatte.com/2021/07/11/232800.html , chatgpt, 영한님 spring 강의, 머리속
