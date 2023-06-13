Everything you need to know about HTTP
===
※출처: https://cs.fyi/guide/http-in-depth




### What is HTTP?

HTTP는 TCP/IP 계층을 기반으로 하는 프로토콜입니다. 서버와 클라이언트가 통신하는 방법을 표준화합니다. HTTP는 콘텐츠가 인터넷을 통해 어떻게 요청되고 전송되는지 정의합니다. TCP 포트 80을 사용합니다. HTTPS의 경우에는 443을 사용합니다.


### HTTP/0.9 - THE One Liner

HTTP/0.9는 최초로 기술된 HTTP 버전 입니다. 정말로 단순한 프로토콜인데, 단 하나의 메소드 GET을 가지고 있었습니다. 클라이언트가 어떤 서버를 통해 웹페이지에 접근하려 할떄, 다음과 같은 단순한 요청을 보냈습니다.

> GET /indexlhtml

그리고 서버는 다음과 같은 응답을 보내줬습니다.

> (response body)
(connection closed)

별도의 헤더나 응답 상태코드는 존재하지 않았고, 서버로부터의 응답은 반드시 HTML 이여야 했습니디.


### HTTP/1.0

오직 HTML 응답을 위해 다지안된 HTTP/0.9와 다르게, HTTP/1.0은 다양한 형태의 응답이 가능해졌습니다. (이미지, 비디오 파일 등등...) 다양한 메소드도 추가 되었습니다. (ex) POST, HEAD) request/response 포맷이 변경 되었고, request/response 양쪽 모두에게 HTTP 헤더가 추가되었습니다. response의 상태를 알 수있는 status code가 추가되었습니다. content-type, content encoding, authorization, caching 등 많은 것들이 새로 포합되었습니다.

HTTP/1.0 request와 response의 간단한 예시입니다.

> GET / HTTP/1.0
Host: cs.fyi
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: * /*

client는 request에 개인정보를 담아 보냅니다. header가 존재하지 않았던 HTTP/0.9에서는 볼 수 없었던 모습입니다.

위 request에 대한 response는 아래와 같은 모습이 될 것 같내요

>HTTP/1.0 200 OK
Content-Type: text/plain
Content-Length: 137582
Expires: Thu, 05 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 5 August 1996 15:55:28 GMT
Server: Apache 0.84
(response body)
(connection closed)

-> 응답의 가장 첫 줄에 HTTP/버전, 상태코드, 상태코드에 대한 이유가 포함되어 있는 것을 볼 수 있습니다.

HTTP/1.0에서 request/response의 header는 여전히 ASCII로 인코딩 되었습니다만 response body에는 다양한 type의 값을 가질 수 있게되었습니다. 이제 서버는 다양한 형태의 콘텐츠를 클라이언트에게 보낼 수 있게 되었습니다.

HTTP/1.0은 하나의 연결 당 여러개의 request를 보낼 수 없는 단점이 있었습니다. 즉 하나의 요청당 한번의 TCP 연결 open> reqeust > response > TCP 연결 close 라는 일련의 과정이 필요했습니다. 로딩할 컨텐츠의 개수가 늘어날 수록 (reqeust가 더욱 많이 필요 할수록) 성능에 악영향을 주게 되었습니다.

### Three-way Handshake

Three-way Handshake: 모든 TCP 연결에서 클라이언트와 서버가 데이터 공유를 시작하기 전에 일련의 패킷을 공유하는 과정 입니다. 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 양쪽 모두에게 이 사실을 알게합니다.

<br />
<img src="https://t1.daumcdn.net/cfile/tistory/225A964D52F1BB6917" />
<br />
이미지출처: https://mindnet.tistory.com/entry/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-22%ED%8E%B8-TCP-3-WayHandshake-4-WayHandshake
<br />
<br />

* STEP1
클라이언트는 서버에게 접속을 요청하는 SYN 패킷을 보냅니다. SYN 패킷을 보낸 이후 클라이언트는 응답을 기다리는 SY_SENT 상태가 됩니다.

* STEP2
서버는 SYN 요청을 받고 A클라이언트에게 요청을 수락한다는 의미의 ACK 와 SYN flag가 설정된 패킷을 발송하고 클라이언트가 이에 응답하길 기다리는 SY_RECEIVED 상태가 됩니다.

* STEP3
클라이언트가 서버에게 ACK를 보내고 연결이 이루어지고 데이터가 오가게 됩니다. 서버는 ESTABLISHED 상태가 됩니다.

