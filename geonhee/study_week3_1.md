# 몰랐던 자바 문법 클래스

### ArrayList
_Python을 주로 사용하다보니 ArrayList나 다른 자료구조들을 까먹었다. 다시 차근차근 알아나가보자_

- ArrayList는 Collection Framework의 일종이며 java.util 패키지에 속해있다. **표준 배열보단 느리지만 많은 조작이 필요한 경우 유용**하다.
- 크기가 자동적으로 늘어난다.
- **ArrayList = 배열 + 메소드 모음**
#### 선언
```java
ArrayList<Type> array = new ArrayList<Type(생략가능)>(초기크기or초기값);
//초기값 세팅시 Arrays.asList(1,2,3,4);
```
- _타입 선언시, 해당 타입만 추가 가능_

#### 메소드
>**1) 데이터 추가**
>>- **boolean add(E e)** : 리스트의 끝에 데이터 e를 추가합니다.
>>- **void add(int index, E element)** : index의 위치에 데이터 element를 추가한다.

>**2) 데이터 삭제**
>>- **void clear()** : 리스트의 모든 데이터를 삭제한다.
>>- **E remove(int index)** : index의 위치에 있는 데이터를 삭제한다.
>>- **boolean remove(Object o)** : 리스트에서 Object o와 처음 일치하는 데이터를 삭제한다. 


>**3) 데이터 확인**
>>- **int size()** : 리스트의 데이터 개수를 반환한다. 
>>- **boolean isEmpty()** : 리스트가 비어있는지 여부를 반환한다.(비어있을 경우 true)
>>- **boolean contains(Object o)** : 리스트에 Object o가 포함되어 있는지 여부를 반환한다. (포함된 경우 true)
>>- **int indexOf(Obejct o)** : 리스트에서 Object o와 처음 일치하는 데이터의 index 정보를 반환한다. (없을경우 -1 반환)
>>- **int lastIndexOf(Obejct o)** : 리스트에서 Object o와 마지막으로 일치하는 데이터의 index 정보를 반환한다. (없을경우 -1 반환)
 
>**4) 데이터 반환**
>>- **E get(int index)** : 리스트에서 index의 위치에 있는 데이터를 반환합니다. 
>>- **Object[ ] toArray( )** : 리스트의 모든 데이터가 포함된 Object 배열을 반환합니다.  

 

>**5) 데이터 변경**
>>- **E set(int index, E element)** : index의 위치에 있는 데이터를 element로 변경합니다. 

- - - 
### Optional 클래스


> - 개발을 할 때 가장 많이 발생하는 예외 중 하나가 바로 _**NPE(NullPointerException)**_이다. NPE를 피하려면 null 여부를 검사해야 하는데, null 검사를 해야하는 변수가 많은 경우 코드가 복잡해지고 번거롭다. 그래서 널리 사용되는 것이 **Optional 클래스**이다.
>- Optional<T> 클래스는 Integer나 Double 클래스처럼 'T'타입의 객체를 포장해 주는 래퍼 클래스(Wrapper class)이다.
> - Optional 인스턴스는 모든 타입의 참조 변수를 저장할 수 있다.

- 객체 생성
  >- of() 메소드나 ofNullable() 메소드를 사용하여 Optional 객체 생성이 가능하다. 
  >- of() : 값이 null이면 NPE 발생 > 값이 null이 아닐 때 사용
  >- ofNullable() : 값이 null 이어도 빈 Optional 객체 반환
  
- 실행 예제
  ```java
  Optional<String> opt = Optional.ofNullable("자바 Optional 객체");
  System.out.println(opt.get());
  ```

- 객체 접근
  > **get() 메소드**를 사용시 Optional 객체에 접근 가능
  - 만약 Optional 객체에 저장된 값이 null이면 NoSuchElementException 에러가 발생
  - 따라서 get() 호출 전에 **isPresent() 메소드를 사용하**여 값이 null인지 아닌지 판단한 후 호출 **_isPresent > null이면 false, null이 아니면 true 반환_**
  
 - 실행 예제
  ```java
  Optional<String> opt = Optional.ofNullable("자바 Optional 객체");
  
  if(opt.isPresent()){
	System.out.println(opt.get())
  }
 ```
 
  - - - 
  ### 단위 테스트 (JUnit - AssertThat)
  
  - JUnit이란 Java를 위한 단위 테스트 오픈소스 라이브러리이다.
  개발자가 일일이 print문을 작성하는 대신 쉽게 테스트를 도와준다.
  
>#### 사용법
>>데코레이터로 @Test를 추가하여 해당 메소드가 테스트 메소드임을 알린다.
>> - 메소드 사용 방법은 다음과 같다.
>>```java
>>assertThat(target).method().method()
>> ```
 >>_* 사용 가능한 메소드 : isEqualTo(e), contains(e), doesNotContain(e), startsWith(e), endsWith(e), isNotEmpty(), isPositive(n), isGreaterThan(n) 등_
  
- **단위 테스트 후 초기화(AfterEach)**
> 단위 테스트는 독립적이여야한다. 따라서 어느 한 단위 테스트가 **다른 단위 테스트에 영향을 미치는 일이 없도록 해야한다**. 따라서 단위 테스트 후 해당 테스트의 영향을 초기화 시켜주는 **AfterEach를 사용**한다.
>>#### 사용법
  >> ```java
  >>@AfterEach
  >>public void afterEach(){
  >>	  repository.clearStore()
  >> }
>> ```
>> _이 방식을 사용할 시, 단위 테스트가 끝날 때마다 해당 함수가 실행된다._
  
- **단위 테스트 전 실행(BeforeEach)**
> **BeforeEach 어노테이션**을 붙이면 AfterEach와 반대로 ** 테스트 메소드 실행전에 실행**된다.
>> **사용법**
>>```java
>>@BeforeEach
>>  public void beforeEach(){
>>  	System.out.println("beforeEach");
>>  }
>>  ```
   - __초기화는 단위 테스트에서 중요한 역할을 담당하니 꼭 기억하자__
  - - - 
  ### Lambda
  - Lambda는 **익명 메소드**로 **함수를 보다 간결하게 작성하기 위해 사용**한다. 파이썬에서 주로 사용했던 것과 표현 문법만 다르다고 생각하면 될 것 같다._(ex . lambda x : len(x))_
>- **사용법**
>>```java
>>  (매개변수, ...) -> {실행문}
>>  //왼쪽에는 오른쪽 실행문을 실행하기 위한 매개변수,
>>  //오른쪽에는 실행문이 들어간다.
>>  public int sum(int a, int b){
>>  	return a + b;
>>  }//이러한 함수식을 아래와 같이 작성할 수 있다.
>>  (a + b) -> {return a + b}
>>  ```
  - - -
  ### AssertThrows
  - 테스트 케이스를 작성하다보면 **예외 상황을 테스트 하는 것도 매우 중요**하다. 자바에서는 이러한 상황을 assertThrows 함수로 지원한다.
  
  > **사용법**
  >>```java
>> //기본적 문법
>>  assertThrows(예상되는 예외상황, () -> {예외를 발생시키는 실행문});
>>  //실질적인 예시
>>  assertThrows(NullPointerException.class, () -> {List<String> list = null});
  - - -
  
  ### 
  > 출처 : 
  http://www.tcpschool.com/java/java_stream_optional
  https://velog.io/@helenason/JAVA-assertThat
