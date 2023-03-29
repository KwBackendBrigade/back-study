## 1주차 노트

------

### 객체지향의 특징?
>  * 캡슐화
>> 데이터와 코드의 형태를 외부로부터 알 수 없게 하고, 데이터의 구조와 역할, 기능을 하나의 캡슐 형태로 만드는 방법
>  * 추상화
>> 클래스들의 공통적인 특성(변수, 메소드)들을 묶어 표현하는 것
>  * 상속화
>> 부모 클래스에 정의된 변수 및 메서드를 자식 클래스에서 상속받아 사용하는 것
>  * 다형화
>> 다양한 형태로 표현이 가능한 구조를 말한다.

### SOLID (객체지향 설계 원칙) 란?
> 객체지향 프로그래밍 및 설계의 다섯 가지 기본 원칙 각 앞글자를 따서 SOLID 라고 부른다.
   * SRP (Single Responsibility Principle) : 단일 책임 원칙
      > * 클래스는 단 하나의 책임만을 갖도록 설계해야 함 (or 최소화)
      > * 객체가 담당하는 책임이 많아질 수록, 객체 변경에 따른 영향도, 양, 범위가 크게 늘어남
      > * 예측하지 못한 새로운 요구사항이나 변경에 대해서 가능한 적게 영향을 받게 해야 함.
      > * 특정 개체의 책임 의존성 과중 문제를 최대한 지향하는 원칙
   * OCP (Open Closed Principle) : 개방 폐쇄 원칙
      > * 기존 코드를 변경하지 않으면서 새로운 기능을 추가할 수 있도록 설계하는 것
      > * 객체의 확장은 개방적으로, 객체의 수정은 폐쇄적으로 대하는 원칙
   * LSP (Liskov Substitution Principle) : 리스코프 치환 법칙
      > * 부모 객체와 이를 상속한 자식 객체가 있을 때, 부모 객체를 호출하는 동작에서 자식 객체가 부모 객체를 완전히 대체할 수 있다는 원칙
      > * 올바른 상속을 위해 자식 객체의 확장이 부모 객체의 방향을 온전히 따르도록 권고하는 원칙
   * ISP (Interface Segregation Principle) : 인터페이스 분리 원칙
      > * 클라이언트는 자신이 이용하지 않는 기능에 의해 영향 받지 않아야 함
      > * 객체는 자신이 호출하지 않는 method에 의존하지 않아야 함
   * DIP (Dependency Inversion Principle) : 의존성 역전 원칙
      > * 의존 관계를 맺을 때 변화하기 쉽거나 변화가 잦은 것 보다는 변화하기 어려운 개념에 의존해야함
      > * 객체는 저수준 모듈보다 고수준 모듈에 의존해야함 (저수준: 구현된 객체, 고수준: abstract, interface)


### spring이 무엇이고 왜 나왔는가?
  > - JAVA의 웹 프레임워크로 JAVA 언어를 기반으로 사용한다. JAVA로 다양한 어플리케이션을 만들기 위한 프로그래밍 틀이라 할 수 있다.
  > - 객체지향의 특징인 다형성을 OCP와 ICP를 위반하지 않으면서 지키기 위해 DI(의존성 주입)컨테이너를 만든 것이 스프링 프레임워크이다.
  > -  스프링이라는 이름은 스프링 이전 EJB에 의존적으로, 객체지향의 장점을 살리지 못하며 개발하던  개발자들의 겨울이 끝났다는 의미로 "스프링"이라고 한다.

