Everything you need to know about HTTP
===
※출처: https://cs.fyi/guide/http-in-depth




### What is HTTP?

HTTP는 TCP/IP 계층을 기반으로 하는 프로토콜입니다. 서버와 클라이언트가 통신하는 방법을 표준화합니다. HTTP는 콘텐츠가 인터넷을 통해 어떻게 요청되고 전송되는지 정의합니다. TCP 포트 80을 사용합니다. HTTPS의 경우에는 443을 사용합니다.


### HTTP/0.9 - THE One Liner

HTTP/0.9는 최초로 기술된 HTTP 버전 입니다. 정말로 단순한 프로토콜인데, 단 하나의 메소드 GET을 가지고 있었습니다. 만약 클라이언트가 어떤 서버를 통해 웹페이지에 접근하려 할떄, 다음과 같은 단순한 요청을 보냈습니다.

> GET /indexlhtml

그리고 서버는 다음과 같은 응답을 보내줬습니다.

> (response body)
(connection closed)

별도의 헤더, 응답 상태코드는 존재하지 않았고, 서버로부터의 응답은 반드시 HTML 이여야 했습니디.


### HTTP/1.0

오직 HTML 응답을 위해 다지안된 HTTP/0.9와 다르게, HTTP/1.0은 다양한 형태의 응답이 가능해졌습니다.