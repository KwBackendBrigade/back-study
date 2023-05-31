# 소켓 통신
## 1. 소켓이란 무엇인가?
```
프로세스가 네트워크 세계로부터 데이터를 전달하거나 받을 수 있게 해주는 연결고리, 이때 프로세스란 프로그램 및 application을 의미 
```
!['socket'](https://i2.wp.com/ipwithease.com/wp-content/uploads/2020/06/port-vs-socket-dp.jpg?w=1000&ssl=1)

* IP 주소 : 컴퓨터에 부여된 고유의 주소
* 포트 넘버 : 네트워크상에서 프로세스가 할당 받아야할 고유한 숫자(컴퓨터내에서 네트워크를 통해 받거나 전달될 데이터가 프로그램을 식별하기 위해 사용하는 번호)
* PID : 프로세스에 부여되는 고유한 번호로 포트 넘버와 비슷하지만 다름, 컴퓨터내에서 식별이 가능한 번호

<br>

## 2. 소켓 통신의 흐름
!['socket'](https://velog.velcdn.com/images/khsfun0312/post/27027a5a-6059-4286-9d06-4551ff659ba8/image.png)

### Client socket)
1. socket() 함수를 이용하여 소켓을 생성
2. connect() 함수를 통해 통신할 서버의 설정된 ip와 port 번호에 통신을 시도
3. 서버가 accept() 함수를 사용하여 클라이언트의 socket descriptor를 반환
4. 이를 통해 클라이언트와 서버가 서로 read(), write()하며 통신 반복

### Server socket)
1. socket() 함수로 생성
2. bind() 함수로 ip와 port 번호를 설정
3. listen() 함수로 몇개의 클라이언트 접근 요청을 대기 시킬지 결정
4. accept() 함수를 사용하여 클라이언트와의 연결

tip) 실제 데이터 통신은 client socket에서만 발생한다는 얘기가 있음 -> 서버 소켓이 여러개의 클라이언트와 송수신할 수 있도록 하는거랑 관련이 있는데, 서버 소켓은 클라이언트의 신호를 accept하면 새로운 client 소켓을 만들어서 생성된 소켓과 기존 client 소켓간의 통신이 가능하도록하기 떄문이다.

<br>

## 3. socket descriptor
```
- 리눅스상에서 파일 디스크립터를 사용하여 소켓을 열면 소켓 디스크립터
- 프로그램이 네트워킹을 할 때 소켓 디스크립터를 사용

※ 리눅스에선 기본적으로 모든 것을 파일 단위로 처리, 
   리눅스 시스템이 파일에 접근하기 쉽게 해주는 도구
```
<br>

## 4. type of socket
데이터를 보내기 위한 프로토콜
![TCP/UDP](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F1520A0544D94705D09)
### 1. TCP
- 연결 지향 방식 -> 논리적 경로 배정
- 3-way handshaking 방식 -> 목적지와 수신지를 확실하게 설정
- 신뢰성있는 전송이 중요할때 채택
- 오버헤드가 발생(다양한 정보가 필요)
  
### 2. UDP
- 데이터 크기에 제한이 있음
- 데이터를 독립적으로 처리
- 실시간 멀티미디어 정보를 처리하기 위해 주로 사용
- 확실하게 전달이 보장되지 않지만 속도는 빠름

<br>

## 5. 참고
- https://helloworld-88.tistory.com/215
- https://codinghero.tistory.com/98
- https://leoheo.github.io/tcp-udp/#:~:text=TCP%EC%9D%98%20%EB%8B%A4%EC%96%91%ED%95%9C%20%EC%A0%9C%EC%96%B4%20%EA%B8%B0%EB%8A%A5,%ED%97%A4%EB%93%9C(Overhead)%20%EB%9D%BC%EA%B3%A0%20%EB%B6%80%EB%A5%B8%EB%8B%A4.
- https://mangkyu.tistory.com/15