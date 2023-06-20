

Cross-Origin Resource Sharing  (CORS)
====


CORS는 HTTP-header를 기반으로 하는  체제 입니다. 어떤 출처 A에서 불러온 문서나 스크립트가 다른 출처에게 리소스를 요청하는 것을 제한 혹은 허용하는 방식입니다.


corss-origin request의 예시:

> https://domainAAA.com 에서 제공된 javascript가 https://domainBBB.com 에게 fetch API 를 사용해 어떤 요청을 보내는 경우


보안상의 이유로 web application은 다른 출처 응답에 올바른 CORS 헤더가 포함되지 않는다면 해당 웹 어플리케이션을 제공한 서버에게만 리소스를 요청할 수 있습니다.

<br />
<img src="https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS/cors_principle.png" />
<br />

-> 동일한 출처에 대한 리소스 요청은 언제나 허용됩니다. 동일하지 않은 출처에 대한 리소스 요청은 CORS에 의해 통제됩니다.




### CORS preflight

CORS preflight는 CORS 요청을 보내기 전 서버 측에서 해당 요청이 사용가능한지 확인하기 위해 보내는 요청입니다.

cors preflight를 보내야 하는 상황이라면 브라우저에서 자동으로 전송합니다.


### CORS 요청 시나리오
<br />

#### 단순요청

몇몇 요청은 CORS preflight를 발생시키지 않습니다. 이런 요청들을 simple request 라고 부릅니다.

다음 요청을 만족하는 요청을 simple request라고 부릅니다.

- 다음 중 하나의 메소드
  - GET
  - HEAD
  - POST
- ([Fetch 명세에서 “CORS-safelisted request-header”로 정의한 헤더](https://fetch.spec.whatwg.org/#cors-safelisted-request-header))
  - Accept
  - Accept-Language
  - Content_language
  - Content-type (application/x-www-form-urlencoded, multipart/form-data, text/plain)

- ReadableStrema 객체가 사용되지 않아야함


### CORS preflight 요청

요청을 보내기전 OPTIONS 메소드를 통해 요청을 보낼 도메인을 preflight 요청을 보내 실제 요청을 보내기에 안전한지 확인합니다.

<br />
<br />
출처: https://developer.mozilla.org/ko/docs/Web/HTTP/CORS
https://developer.mozilla.org/en-US/docs/Glossary/Preflight_request