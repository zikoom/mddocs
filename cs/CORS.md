

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






출처: https://developer.mozilla.org/ko/docs/Web/HTTP/CORS