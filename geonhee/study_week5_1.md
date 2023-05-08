## 함수형 인터페이스(Functional Interface)

### 함수형 인터페이스란?
함수형 인터페이스를 구현하는 클래스는 `람다 표현식`, `메서드 참조` 등의 기능을 활용하여 **코드를 간결하게 작성**할 수 있다.
- 함수형 인터페이스란 한개의 `추상 메소드(abstract method)`를 가지는 인터페이스를 말한다.
- 한개의 추상 메소드을 포함하면 되기 때문에 **`default method` , `static method`는 여러개 있어도 상관없다.**
- Annotation으로 `@FunctionalInterface`를 사용하는데, 이는 **컴파일러가 해당 인터페이스가 함수형 인터페이스인지 확인**해준다.


한번 예시로 함수형 인터페이스를 보자.
>```java
>@FucntionalInterface
>interface MyFunctionalInterface{
>	int add(int a, int b); 
>	//한개의 추상 메소드를 가지는 FunctionalInterface
>}
>
>//적용방법
>public class Main{
>	public static void main(String[] args){
>
>		MyFunctionalInterface mFunc = (x,y) -> {x+y};
>		//함수형 인터페이스의 추상 메소드를 람다식으로 정의한다.
>
>		System.out.println(mFunc.add(1,2));
>		//위에서 정의된 함수형 인터페이스 메소드를 호출한다.
>		}
>}

다음으로 `default method`, `static method`가 포함된 함수형 인터페이스를 보자.
>```java
>@FunctionalInterface
>interface MyFunctionalInterface{
>	int add(int a, int b); 
>	//한개의 추상 메소드
>
>	default void defaultPrint(){
>		System.out.println("이것은 default method입니다.");
>		//FunctionalInterface의 default method
>		}
>		
>	static void staticPrint(){
>		System.out.println("이것은 static method입니다.");
>		//FunctionalInterface의 static method
>		}
>}
>
>//적용방법
>public class Main{
>	public static void main(String[] args){
>		MyFunctionalInterface mFunc = (x,y) -> {x+y};
>		//FunctionalInterface의 추상 메소드 정의
>
>		mFunc.defaultPrint();
>		//결과 : 이것은 default method입니다.
>
>		mFunc.staticPrint();
>		//결과 : 이것은 static print입니다.
>	}
>}
>```
>위와 같이 `default method`, `static method`을 포함해도 추상 메소드 한개만을 포함하면 사용 가능하다.

- _참고 : interface안 method는 모두 public으로 선언되어 public 생략가능_

- - -
## Stream reduce() 메소드
### reduce()란?
- 스트림의 **최종 연산**이다!
- 스트림의 **모든 요소를 하나의 데이터로 줄이는 작업**을 한다.
- 작동 원리는 다음과 같다.
	1. 스트림의 첫번째와 두번째 요소를 개발자가 지정한 식을 사용해 		연산한다.
    2. 1에서 연산 된 결과와 세번째 요소를 연산한다.
    3. 이를 반복하여 모든 요소에 대해 적용한다.
- - - 
### 사용 방법

_우선 BinaryOperator에 대해 알아보자_
- `BinaryOperator<T>` 인터페이스는 두 개의 동일한 타입 T의 인수를 가지고 연산을 수행한 다음, 결과를 동일한 타입 T로 반환하는 **함수형 인터페이스**이다.
- 이는 함수형 프로그래밍에서 두 값을 합치는 연산을 표현하기 위해 사용된다.
- BinaryOperator 인터페이스에는 apply() 메소드가 정의되어 있다. 이 메소드는 BinaryOperator 인터페이스의 구현체에서 두 개의 인수를 받아서 연산을 수행하고, 동일한 타입의 결과를 반환한다.
```java
  BinaryOperator<Integer> add = (a,b) -> {a+b};
  int result = add.apply(1,2);
  //결과 : 3
```
- - - 
### 1. Parameter가 하나 있는 경우
>```java
>Optional<T> reduce(BinaryOperator<T> accumulator)
>``` 
>위와 같이 reduce 함수의 Parameter로 BinaryOperator 함수가 지>정되었으므로, 원하는 함수의 식을 넣고 스트림 객체에 대해 해당 연>산을 한 결과를 반환한다.
>
>```java
>List<Integer> numbers = Arrays.asList(1,2,3,4,5);
>int sum = numbers.stream().reduce((x,y) -> x+y);
>//결과 : 15
>```

### 2. Parameter가 두개 있는 경우
>```java
>T reduce(T identity, BinaryOperator<T> accumulator)
>```
> 추가된 `T identity`는 초기값을 지정해준다. 다음 예제를 보며 이해해보자.
>```java
>List<Integer> numbers = Arrays.asList(1,2,3,4,5);
>int sum = numbers.stream().reduce(10, (x,y) -> x+y);
>//결과 : 25
>```
>초기값을 10으로 지정했으니 다음과 같이 연산된다.
> _10(초기값) + 1_ , _11 + 2_ , _13 + 3 etc..._

### 3. BinaryOperator 구현 후, apply 함수 Override
- 식이 복잡한 경우 사용한다.

>```java 
>class CompareStrings implements BinaryOperator<String>{
>	@Override
>	public String apply(String s1, String s2){
>		if(s1.length() > s2.length()) return s1;
>		else return s2;
>		}
>	}
>//BinaryOperator 구현하여 apply Override
>
>class Main{
>	public static void main(String[] args){
>		ArrayList<String> strings = Arrays.asList("hi","hello","안녕하세요");
>		String result = strings.stream().reduce(new CompareStrings());
>		//따로 구현해둔 CompareStrings 적용하기
>```
  
- - -
출처 : chatgpt
