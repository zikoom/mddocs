WebSocket
=====



### 웹 소켓

서버와 클라이언트 간의 메세지 교환을 위한 프로토콜



### 웹소켓의 작동 원리

<br />
<img src='https://assets.website-files.com/5ff66329429d880392f6cba2/63fe488452cc63cf1cb0ae45_148.2.png' />
<br />

<br />
최초 접속요청은 HTTP를 통해 진행합니다. 웹소켓 연결을 위해 클리이언트는 handShake request를 보냅니다. 서버도 이에 응답하여 response를 보냅니다. 아래가 각각 request, reponse 예시입니다.

```
GET /chat HTTP/1.1
Host: server.example.com
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Key: x3JJHMbDL1EzLkh9GBhXDw==
Sec-WebSocket-Protocol: chat, superchat
Sec-WebSocket-Version: 13
Origin: http://example.com
```

```
HTTP/1.1 101 Switching Protocols
Upgrade: websocket
Connection: Upgrade
Sec-WebSocket-Accept: HSmrc0sMlYUkAGmm5OPpG2HaGWk=
Sec-WebSocket-Protocol: chat
```

연결이 성공하면 프로토콜을 HTTP 양방향 프로토콜로 전환합니다. 그 후 클라이언트, 서버 어느 한쪽이 연결을 종료하면 다른 쪽도 동시에 연결이 종료됩니다.

### 언제 웹소켓을 사용해야 할까

WebSocket 프로토콜은 양방향 프로토콜 입니다. 주로 지속적인 데이터 전승을 지원하는 실시간 응용 프로그램 개발에 사용합니다.

- 채팅 프로그램
- SNS
- 등등

출처:
</br />

https://ably.com/topic/websockets
<br />
https://en.wikipedia.org/wiki/WebSocket
<br />
https://doozi0316.tistory.com/entry/WebSocket%EC%9D%B4%EB%9E%80-%EA%B0%9C%EB%85%90%EA%B3%BC-%EB%8F%99%EC%9E%91-%EA%B3%BC%EC%A0%95-socketio-Polling-Streaming