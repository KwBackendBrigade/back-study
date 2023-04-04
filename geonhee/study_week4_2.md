# Java Enumeration

### Java에서 Enumeration이란?
- 자바에서 Enumeration(열거형)이란 상수 값을 나열하는 Data Type이다. **특별한 상수 집합 클래스**라고 보면 될 것 같다.
- 상수를 의미별로 묶어 사용하고 싶을 때 사용한다.
- 예를 들어 월, 화, 수, 목, 금, 토, 일과 같이 요일을 하나로 묶어 관리 할 수 있고, 데이터 값을 명확하게 전달할 수 있다.
- 클래스처럼 변수와 메소드를 가질 수 있지만, 상속이나 인스턴스를 생성할 수 없다.

### Enumeration 선언법
- enum 키워드를 사용해서 선언하며, 보통 Enumeration의 첫글자는 대문자, 안의 상수 값은 대문자를 사용한다.
```java
enum Week { MON, TUE, WED, THU, FRI, SAT, SUN }
```

### Enumeration Methods
1. **valueOf(String str)** : 지정된 이름과 일치하는 enum 상수를 반환한다.
2. **name()** : enum 상수의 이름을 문자열로 반환한다.
3. **ordinal()** : enum 상수가 정의 된 순서를 정수로 반환한다.
4. **values()** : enum의 모든 상수를 배열로 반환한다.

### Enumeration에 추가적인 값 부여하기
- Enum에는 생성자를 통해 새로운 열거 상수와 대응하는 데이터를 생성자를 통해 연결시킬 수 있다.
만약 코드가 이렇게 있다고 치자.

```java
public class realMain{
    public enum Week{ 
        //이렇게 enum은 클래스 안에 선언할수도 있고 따로 클래스를 만들어 선언할수도 있다.
        MON("월요일"),
        TUE("화요일"),
        WED("수요일"); //마지막 열거 상수에는 ;붙여주기
    
        private String week;
        //열거형 상수와는 다른 값을 입력하기 위해 생성한 변수
    
        private Week(String week){
            this.week = week;
            //enum의 생성자는 private만 허용한다.
            //week을 매개 값으로 전달 받아, 열거 상수 ( )에 있는 데이터를 하나씩 가져온다.
        }
    
        public String getWeek(){
            return week;
        }//열거형 메소드
    }

    public static void main(String[] args){
        System.out.println(Week.MON.week);
        System.out.println(Week.MON.getWeek());
        //두개의 출력 값은 같다.
    }
}
```

언뜻보면 코드가 이해가 되지 않는다. 차근차근 알아가보자.
```java
MON("월요일"),
TUE("화요일"),
WED("수요일");
```
- 위와 같이 상수에 소괄호가 선언 되어 있고, 그 안 String 타입의 매개변수가 들어가 있다.
- 이는 **생성자**로 열거 상수 옆에 붙는 형식으로 사용된다. - 
  - _왜냐하면 **enum의 생성자는 private이라 외부에서 접근할 수 없다 !**_
- ex. MON을 생성할시 MON의 매개변수 week = 월요일로 초기화 된다 !
  - 따라서 각 상수 옆 소괄호에 있는 변수가 각각의 매개변수로 초기화된다.

```java
public static void main(String[] args){
        System.out.println(Week.MON.week);
        System.out.println(Week.MON.getWeek());
        //두개의 출력 값은 같다.
    }
```

- - -
출처: chatGPT, 각종 블로그 보고 정리
