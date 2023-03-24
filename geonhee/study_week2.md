### Inflearn Spring 강의 중 모르거나 애매하게 알고 있는 용어 정리
- - - 
- **Spring**
> - Java의 웹 프레임워크로 Java 언어를 기반으로 사용한다. 
>- Java로 다양한 어플리케이션을 만들기 위한 **프로그래밍 틀**이라 할 수 있다.
> - **Java 기술들을 더 쉽게 사용할 수 있게 해주는 오픈소스 프레임 워크**이다.

+ **Spring 주요 특징**
> 1. IoC(Inversion of Control, 제어 반전)
> 2. DI(Dependency Injection, 의존성 주입)
> 3. AOP(Aspect Object Programming, 관점 지향 프로그래밍)
> 4. POJO(Plain Old Java Object) 방식

_~~아직 Spring 공부 시작 단계이므로 특징 이름만 알아두자~~_
- - - 
- **Framework**
> - 프레임 워크는 어떠한 목적을 달성하기 위해 복잡하게 얽혀 있는 문제를 해결하기 위한 구조이다.
> - 소프트웨어 개발에 있어서 하나의 **뼈대 역할**을 한다.
> * 더 간단히 말하자면 **프레임 워크는 자주 쓰일 만한 기능들을 한데 모아 놓은 유틸(클래스)들의 모음(집합)**이라고 정의할 수 있다.
- - - 
- **IDE**
> - **통합 개발 환경(Integrated Development Environment)**
>- 프로그래머가 **소프트웨어 코드를 효율적으로 개발하도록 돕는 소프트웨어 애플리케이션**
_Ex) Intellij, Eclipse, Visual Studio Code etc..._
- - - 
- **Complie**
> 소스 코드를 컴퓨터가 알기 쉬운 기계어로 변경하는 과정
- - - 
- **Build**
> 소스 코드를 **실행 가능한 결과물**로 만드는 일련의 과정 (Compile 과정을 포함)
>>1. 필요한 라이브러리를 다운 받고 *classpath에 추가
>>2. 소스 코드를 컴파일
>>3. 테스트를 실행
>>4. 컴파일된 코드를 패키지(jar, war, zip 등)
>>5. 패키지된 파일을 주로 artifact라고 부르고 서버나 레포지토리에 배포
	 - *_classpath : 사용자 정의 클래스 및 API 패키지의 경로를 지정하는 자바가상머신 또는 Java 컴파일러의 매개 변수_
- - -
- **Gradle**
	   _Build 자동화 시스템_
> - Build를 수동으로 하기에는 번거로워 이런 과정을 자동화 하기 위해** Build Tool**이 고안
> - **Gradle**은 **maven**, **ant**와 같이 **Build Tool의 일종**이다.
> - 이전까지 maven이 주로 사용되었지만 현재는 다양한 언어를 지원하는 Gradle이 주로 사용된다.
- **build.gradle 살펴보기**
```java
// 플러그인 설정
apply plugin: 'java-library'

// 저장소 설정
repositories {
    jcenter()
}

/* 의존 관계 설정
	api, compile, implementation: 프로젝트 컴파일 과정에서 필요한 라이브러리
	runtime: 프로젝트 실행 과정에서 "
	testCompile, testImplementation:테스트 컴파일 과정에서 "
	testRuntime: 테스트 실행 과정에서  "
*/
dependencies {
    api 'org.apache.commons:commons-math3:3.6.1'
    implementation 'com.google.guava:guava:23.0'
    testImplementation 'junit:junit:4.12'
}
```
- - - 
- **MVC**
널리 사용되는 **소프트웨어 디자인 패턴**

**Model, View, Controller** 로 구성되어 있다.
> - **Model** : 데이터(어플리케이션 정보, DB, 사용자가 선언한 변수 등)의 가공을 책임지는 컴포넌트
>- **View** : 사용자의 인터페이스 요소를 책임진다.
> - **Controller** : Model과 View를 잇는 다리 역할을 한다. 흡사 이벤트 처리와 같다. 

아래는 직관적인 이미지이다. _*[사진 출처](https://cocoon1787.tistory.com/733)_

> ![](https://velog.velcdn.com/images/ghlee00125/post/c8182384-19b0-4cdc-a842-69ee214ed0c8/image.png)

- - - 

- **API(Application Programming Interface)**
> - API는 **프로그램들이 서로 상호작용하는 것을 도와주는 매개체이다**
> - 요청과 응답을 사용하여 두 애플리케이션이 **서로 통신하는 방법을 정의**한다. 
>- API 문서에는 개발자가 이러한 요청과 응답을 구성하는 방법에 대한 정보가 들어 있다.

흔히 레스토랑에 빗대어 예시를 든다._ [*사진출처](https://blog.wishket.com/api%EB%9E%80-%EC%89%BD%EA%B2%8C-%EC%84%A4%EB%AA%85-%EA%B7%B8%EB%A6%B0%ED%81%B4%EB%9D%BC%EC%9D%B4%EC%96%B8%ED%8A%B8/)_
> ![](https://velog.velcdn.com/images/ghlee00125/post/08051fc1-0e28-4e04-8ff0-1fed08d6272f/image.png)

- - - 

- **Apache Tomcat**
> - Apache Tomcat(이하 Tomcat)은 **웹 어플리케이션 서버**이다.
> - **웹 서버와 연동하여 실행할 수 있는 자바 환경을 제공**하여 자바서버 페이지(JSP)와 자바 서블릿이 실행할 수 있는 환경을 제공하고 있다
- - - 
- **JSON(JavaScript Object Notation)**
> - 데이터를 저장하거나 전송할 때 많이 사용되는 **DATA 교환 형식**
> - JSON은 **데이터 포맷일 뿐이며** 어떠한 통신 방법도, 프로그래밍 문법도 아닌 **단순히 데이터를 표시하는 표현 방법**일 뿐이다.
- 데이터 형식 : 기본적으로 **Key : Value**로 지정된다.


> ```java
>{
>  "firstName": "Kwon",
>  "lastName": "YoungJae",
>  "email": "kyoje11@gmail.com"
>}
>```


- - - 

출처

> [https://developer.mozilla.org/ko/docs/Glossary/MVC](https://developer.mozilla.org/ko/docs/Glossary/MVC)
> [https://velog.io/@surim014/JSON%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80]
(https://velog.io/@surim014/JSON%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)
