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

HTTP는 statelsess 프로토콜이기 떄문에 서버는 클라이언트의 정보를 별도로 저장하거나 유지하지 않습니다. 따라서 클라이언트는 매 요청마다 클라이언트의 정보를 서버에게 전달을 해야합니다.

위와 같은 이유로 많은 수의 reqeust(연결)는 대역폭의 사용량을 증가 시키게 됩니다.

### HTTP/1.1

HTTP/1.0 등장으로부터 약 3년뒤에 HTTP/1.1이 개시되었습니다. 1.1은 1.0에 비해 많은 부분이 개선되었고 대표적인 개선점들을 보자면

* 새로운 HTTP 메소드가 추가되었습니다. PUT, PATCH, OPTIONS, DELETE
* Hostname Identification Hedaer가 필수로 바뀌었습니다. (HTTP/1.0 에서는 필수가 아니었음)
* 지속적인 연결을 도입했습니다. 지속적인 연결을 통해 클라이언트는 여러개의 요청을 보낼 수 있게되었습니다. 요청에 Connection:close 헤더가 포함되어있다면 연결이 종료 되었습니다.
* 파이프 라이닝을 도입했습니다. 클라이언트는 동일한 연결에서 서버의 응답을 기다리지 않고 서버에 여러 요청을 보낼 수 있게되었습니다. 동시에 서버는 요청이 수신된 동일한 순서로 응답을 보냈습니다. 이와 동시에 클라이언트에서 각 요청에 대한 응답의 마지막 지점 (이자 동시에 다음 응답의 시작점) 을 알기위해 Content-Length 헤더가 도입되었습니다.


* ... 그 외 더 많은 것들

HTTP/1.1은 1999년에 소개된 이후 여러 해 동안 표준이였습니다. HTTP/1.1은 전 버전과 비교하면 많이 개선 되었습니다. 하지만 시간의 지남에 따라 web은 계속 변해갔고 HTTP/1.1은 한계를 드러냈습니다.

오늘날의 웹 페이지 로딩은 그 어느때 보다도 resource-intensive 합니다. 단순한 웹페이지도 30개 이상의 커넥션을 필요로 합니다. HTTP/1.1은 지속적 연결을 가지고 있습니다. 하지만 같은 시간에 하나의 연결만 처리 가능합니다. 이 문제를 해결하기위해 파이프 라이닝을 도입했지만, 문제를 완전히 해결하진 못했습니다. 만약 느리거나 무거운 요청이 파이프라인에 걸리면 기다려야 했기 때문입니다.


### SPDY

구글은 웹페이지의 로딩속도 향상, 보안성, 대기시간 감소 등을 위해 대체 프로토콜 실험을 시작했습니다.
2009년 구글은 SPDY를 발표합니다.

대역폭을 계속 증가시키면 처음에는 네트워크의 성능이 향상했습니다. 하지만 곧 성능향상이 되지 않는 지점에 도달했습니다. 하지만 지연율에 대해 동일한 일을 했을때, ( 지연율을 지속적으로 떨어뜨릴 때) 지속적으로 성능이 향상 되었습니다. 지연율을 떨어뜨려서 네트워크의 성능을 향상시키기 <- SPDY의 핵심 아이디어 입니다.

2015년 구글은 두 경쟁 표준을 원하지 않았기 떄문에 HTTP/2를 탄생시킴과 동시에 HTTP/2로 병합되었습니다.

### HTTP/2

HTTP/2 짧은 지연시간을 가지는 콘텐츠 전송을 위해 고안되었습니다. HTTP/1.1과 다른 부분중 핵심 특징은 다음을 포합합니다.

* 텍스트를 대체한 바이너리
* Multiplexing - 단일 통신에서 여러개의 비동기 HTTP 요청
* HPACK을 이용한 Header 압축
* Server Push - 단일 연결에서 다수 응답
* Request 우선순위
* 보안


##### 1. Binary Protocol

HTTP/2는 HTTP/1.x 에 존재하는 지연율 증가 문제를 binary protocol을 만듦으로써 해결하려 했습니다. binary protocol은 파싱하기에 더욱 용이했습니다. 하지만 사람이 알아보기에는 어려워 졌습니다. HTTP/2을 구성하는 주요한 요소는 Frame과 Stream 입니다.


###### Frames and Streams

HTTP 메세지는 하나이상의 frame으로 구성됩니다. frame에는 meta data를 담는 HEADERS frame과 payload를 담기 위한 DATA frame이 있습니다. 이외에도 다른 종류의 frame이 있습니다.

모든 HTTP/2 request와 response는 고유한 stream ID를 가지고 있고 이것은 frame안에 나뉘어져 들어가 있습니다. frame은 데이터의 binary 조각입니다. frame들이 모여 Stream이 됩니다. 각각의 frame은 자신이 속한 strema을 특정할 수 있는 stream ID를 가지고 있고 이것은 각각의 frame 공통 header에 있습니다. 고유한 stream ID 외에도 모든 클라이언트가 시작한 요청의 stream ID는 홀수이고 서버로부의 요청 stream ID는 짝수 입니다.

RES_STREAM frame은 특별한 역할을 하는데, 서버에게 해당 stream이 더이상 필요 없다는 것을 알려줍니다. HTTP/1.1에서 서버가 데이터를 보내는 것을 멈추는 유일한 방법은 연결의 종료 였습니다. 반면에 HTTP/2 에서는 RST_STREAM을 사용하여 특별한 stream의 응답을 보내는 것을 멈추게 할 수 있습니다.


###### Multiplexing

HTTP/2가 binary protocol이 됨에 따라 request와 response에서 frame과 stream을 사용하게 되었습니다. TCP 연결이 열리면, 모든 stream들이 같은 연결 내에서 비동기적으적으로 전송 됩니다. 동시에 같은 방법을 사용하는 서버의 응답 또한 비동기적으로 순서를 가지지 않고 보내게 됩니다. 순서와 상관없이 클라이언트는 stream id를 통해 전송된 데이터를 파악합니다. 이것은 HTTP/1.x 에서 존재하던 head-of-line blokcing 이슈를 해결해 주었습니다. 클라이언트는 요청을 보내기 전에 다른요청이 완료될 때까지 기다릴 필요가 없어졌습니다.


###### Header Compression

전송된 헤더를 최적화 하는 것은 RFC의 일부였습니다. 핵심내용은 동일한 client가 서버로 지속적으로 접속할 때 헤더에 반복 데이터가 전송되고 때로는 쿠키가 헤더의 크기를 늘려 대역폭의 사용량을 증가시키고 지연율을 높인다는 것입니다. HTTP/2는 이문제를 헤더 압축으로 극복 했습니다.

request와 response와 다르게 헤더는 gzip 이나 기타 다른 포맷으로 압축되지 않습니다. 값이 허프만 코드를 사용하여 인코딩되고 해당 테이블이 서버와 클라이언트 모두에서 유지관리되는 헤더압축 메카니즘을 사용합니다. 후속 요청 or 응답에서 반복적인 헤더를 생략합니다.

###### Server Push

서버 푸시는 HTTP/2의 놀라운 기능입니다. 서버는 클라이언트가 특정 리소스를 요청할 것임을 미리 안다면 이것을 클라이언트가 요청하지 않아도 클라이언트에게 정보를 보낼수 있습니다.

서버 푸쉬는 서버가 미리 데이터를 보냄으로써 요청/응답을 줄일 수 있습니다. 서버는 PUSH_PRMISE라는 frame을 보내 clinet에게 정보를 미리 보내니 서버에게 추가로 요청하지 말라고 알립니다. PUSH_PROMISE frame은 서버 푸쉬를 발생시긴 stream과 연결되며 약속된 스트름 ID를 포합합니다.


###### Request Prioritization

클라이언트는 HEADER frame에 우선순위 정보를 포함시킴으로서 stream의 우선순위를 정할수 있습니다. 또한 PRIORITY frame을 보내 stream의 우선순위를 변경할 수 있습니다.

우선순위 정보가 없다면 서버는 request 들을 순서에 상관없이 비동기적을 처리합니다. 반면에 우선순위가 있다면 서버는 우선순위에 따라 리소스 제공정도를 결정합니다.


###### Security

HTTP/2에 대한 보안(TLS를 통한)을 필수로 지정해야 하는지 여부에 대한 광범위한 논의가 있었습니다. 결국 의무화하지 않기로 했다. 그러나 대부분의 공급업체는 TLS를 통해 사용될 때 HTTP/2만 지원할 것이라고 밝혔습니다. 따라서 HTTP/2는 사양에 따른 암호화를 요구하지 않지만 어쨌든 기본적으로 필수가 되었습니다. 그런 식으로 TLS를 통해 구현될 때 HTTP/2는 몇 가지 요구 사항을 부과합니다. TLS 버전 1.2 이상을 사용해야 하며 일정 수준의 최소 키 크기가 있어야 하고 임시 키가 필요합니다.