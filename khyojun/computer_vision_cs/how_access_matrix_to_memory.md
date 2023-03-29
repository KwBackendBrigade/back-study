# matrix에 access할때 메모리에 저장하는 방식

1. 메모리 chunk : 메모리 덩어리
2. 거의 대부분의 row major언어 (c++,java 등등) 에서는

```java
for(int row=0; row<row.size(); row++){
	for(int col=0; col<col.size(); col++{

}
}

for(int col=0; col<col.size(); col++){
	for(int row=0; row<row.size(); row++{

}
}
```

위에가 아래보다 살짝 빠르다. 그 이유는 바로 cpu가 애초에 메모리에 access할때 한 곳을 access하면 그곳 포함하여 chunk(덩어리)지게 데이터를 캐시에 넣어놓기 때문에 메모리 저장방식에 따라 위에 경우가 빠를 수도 있고 밑의 경우가 빠를수도 있다.

1,2,3

4,5,6

7,8,9

라는 것을 저장할 때 row 에서는 1,2,3,4,5,6,7,8,9, 이런식이고 col 에서는 1,4,7,2,5,8,3,6,9 이런식으로 저장한다. cpu의 l1,l2캐시에 저장해 놓는다고 한다.

그래서 위의 반복문이 속도에 측면에서 더 빠르게 돈다. 그리고 이 캐시하는 방식은 모든 cpu에서 다 이렇게 작동한다! 그래서 continuous하게 하면 좋다는 것이 이런의미인가 보다. chunk해서 캐시할때 연속된걸 찾게 되면 캐시 히트가 되기 때문인거 같다.