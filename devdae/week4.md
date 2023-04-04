# List in java

## Q. array와 list의 차이를 아십니까?
## A. 언뜻 보면 비슷한 단어지만, array는 크기가 고정된 데이터 구조라면 list는 java collection이라는 framework 하단에 존재하는 인터페이스이다.
![list](https://media.geeksforgeeks.org/wp-content/cdn-uploads/20210315172345/Java-Collections-Framework-Hierarchy.png)
</br>

## bonus.
### java에서 array를 사용하는 방식
```java
int arr[] = new int[10]; 
```
### java에서 List(ArrayList)를 사용하는 방식
```java
Arraylist<Type> al = new ArrayList<Type>();
```
- array와 list의 차이를 설명하면서 generic을 언급하지 않을 수 없는데 array에선 generic을 사용하지 않고, arraylist에선 사용 -> safe의 문제?
- 기본형 데이터가 바로 사용되냐 안되냐의 차이도 존재, array는 Primitive data를 바로 사용하지만, list에선 그러지 않음(auto boxing unboxing wrapper class등)
</br>

## Q. 위 사진을 보면 리스트 인터페이스를 구현한 class들이 다양한데 무엇이 다른건가요?
## A. List 인터페이스를 구현한 클래스들이라는 점에서 순서가 있는 데이터 집합에 접근한다는 공통점을 가지지만, 내부적으로 데이터 구조에 접근하는 방식 혹은 클래스들간의 성능이 서로 다르다.
</br>

## Q. 구체적으로 ArrayList와 LinkedList의 차이를 알아보자.
### 1) ArrayList
- 단방향 포인터를 가지기 때문에 배열의 원소에 접근하는데 constant한 시간이 소요된다. 하지만 배열의 원소를 remove하거나 삽입할 시에는 resize를 해야하기 때문에 상대적으로 시간이 소요된다.
- Dynamic resize가 발생한다.(가변적으로 메모리를 늘렸다 줄임)
- LinkedList보다 삽입, 삭제가 느리다.
### 2) LinkedList
- doubly linked list 구조로 구현
- arraylinked list와 다르게 삽입, 삭제시 constant한 시간이 소요되지만, 반대로 배열의 원소에 접근하는데에는 시간이 소요된다.
- 원소들 간에 link를 저장해야하기 때문에 arraylist보다 더 많은 메모리가 필요하다.
### 3) 결론
- 순서가 존재하는 데이터 집합에 접근한다는 공통점을 가지지만, arraylist는 배열내 원소들을 순환하는데 constant한 시간이 소요된다는 장점을 가지고, LinkedList는 배열에 원소들을 삽입하거나 삭제하는데 비교적 빠른 속도를 가진다는 점에서 적용하고자하는 상황과 환경에 따라 적절히 둘 중에 하나를 선택해서 사용하면 된다. 하지만 LinkedList가 메모리를 더 차지한다는 점은 참고해야한다. 

## 출처
- https://www.geeksforgeeks.org/array-vs-arraylist-in-java/
- https://www.geeksforgeeks.org/difference-between-list-and-arraylist-in-java/
- https://gangnam-americano.tistory.com/41
- chatGPT


