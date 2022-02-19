# ✍ IP

클라이언트와 서버 사이에 데이터를 주고 받을 때는 노드(컴퓨터)에 데이터를 packet에 담아 전송한다. 그래야 출발지 IP 에서 도착지 IP에 정확하게 데이터가 도착한다. 서버에서 클라이언트도 마찬가지.

하지만 IP의 단점이 존재한다.
* 비신뢰성
여러 패킷을 동시에 보내면 중간에 다른 노드를 거칠 수 있어 패킷이 순서대로 도착하지 않을 수 있다.

![](https://images.velog.io/images/boo1996/post/9200f6fa-b4c3-41a8-8132-d8c7ddaa762b/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2021-10-20.png)

* 비연결성
패킷에 데이터가 들어있지 않거나 서버가 불능상태여도 패킷을 전송한다.

![](https://images.velog.io/images/boo1996/post/c0c06550-544a-4d0a-b8a1-52e9d040570c/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2021-10-11.png)


이 두가지 단점을 해결하기 위해 TCP 개념이 등장했다.

# ✍ TCP
![](https://images.velog.io/images/boo1996/post/d16455a6-4d9d-4fd0-8dad-8faf4c860414/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2021-17-11.png)

네트워크 프로토콜 계층은 두가지 계층으로 나눌 수 있는데,
OSI 7 계층에서 TCP가 IP보다 높은 계층에 있으므로 IP 프로토콜의 한계를 보완할 수 있다.

![](https://images.velog.io/images/boo1996/post/d6f4d876-d03f-42f5-9ceb-a77e52c697c7/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2021-22-35.png)

TCP는 데이터가 packet에 담기기 전 socket 라이브러리로 감싸게 되는데 socket은 '네트워크 환경에 연결할 수 있게 만들어진 연결부'를 말한다. 그렇다면 TCP 방식은 어떤 특징을 갖고 데이터를 전달하는 것일까?

* 3 way handshake(가상연결)
![](https://images.velog.io/images/boo1996/post/644e0fbf-ed50-4582-8764-1b9f71a29a20/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2021-25-00.png)

TCP는 위와 같은 방식으로 데이터를 송수신한다.
SYN은 단방향으로 connection 하는 역할이다.
클라이언트와 서버가 연결되기 위해서는 SYN을 사용한다.

서버에서도 클라이언트와 연결하기 위해 SYN을 보내고 데이터를 전송하기 위해 ACK을 송신한다. 클라이언트와 서버가 연결이되고 다시 클라이언트에서 서버로 ACK을 보내면 데이터 송수신이 완료되어 ESTABLISHED 처리가 된다.

![](https://images.velog.io/images/boo1996/post/0d369753-c759-4668-bfd2-bcd865830bc9/TCP%20connection1.png)

클라이언트와 서버가 연결되면 packet을 보낸다.
서버는 받았다는 신호인 ACK를 보낸다.
클라이언트는 또 새로운 packet을 보낸다.

![](https://images.velog.io/images/boo1996/post/f6bf7527-7900-4833-b163-37ba776a7227/TCP%20connection.png)

connection을 해제하고 싶다면 FIN을 통해 연결해제 신호를 보낸다. 서버가 받았다는 신호를 보내고 잠시 뒤에 FIN을 보낸다. 클라이언트는 기다렸다가 FIN 신호를 받았다는 ACK를 보내면서 연결이 해제된다.

위에서 살펴본 3-handshake를 통해 클라이언트와 서버가 서로 응답해야 연결이 되기 때문에 IP의 비연결성을 보완할 수 있고, 데이터를 보낸 순서대로 응답하기 때문에 비신뢰성 또한 보완할 수 있다.

하지만 TCP의 문제점으로는 전송의 신뢰성을 보장하지만 매번 connection을 연결하기 때문에 시간 손실이 발생한다.
그리고 패킷이 조금만 손실해도 재전송하는 단점이 있다.

반복적인 재연결과 패킷을 검증없이 보낼 수 있는 방법은 없을까?

이를 개선하기 위해 나온 개념이 UDP다.

# ✍ UDP

User Datagram Protocol의 약자로 한마디로 말하자면 
TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠른 프로토콜이다.

단방향으로 통신하기 때문에 connection이 끊어져 있다.
TCP의 제어기능이 없고 수신 시 에러만 검출한다.
그렇기 때문에 영상 스트리밍 처럼 비교적 데이터의 신뢰성이 중요하지 않을 때 사용한다.

![](https://images.velog.io/images/boo1996/post/45495ae3-65c6-4598-92cf-e4ea7275749c/%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7,%202022-02-16%2023-13-56.png)

