>🙋🏻RESTful API ? <br>
서버와 클라이언트가 메시지를 주고받을 때 가장 많이 사용하는 `통신 규격` (암묵적인 룰)<br>
간단하고 유연한 구조를 가지고 있으며, 다양한 클라이언트 및 서버 간의 통신을 지원합니다. 이러한 이점으로 인해 현재 많은 웹 서비스와 모바일 애플리케이션에서 사용되고 있습니다.<br>

> 
- GET<br>
일반적으로 웹 브라우저가 서버에 웹 페이지를 요청할 때 사용
읽기 요청
body를 포함할 수 없음<br>
?와 & 문자를 사용하는 쿼리 파라미터를 추가할 수 있다<br>
- POST<br>
클라이언트에서 서버로 데이터가 포함된 요청을 보낼 때 사용<br>
로그인, 주문 요청 등<br>
- DELETE(삭제), PUT(전체수정),PATCH(부분수정)<br>

>[**상태 코드**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)<br>
모든 HTTP 응답에는 상태 코드와 상태 메시지가 있음<br>
200 OK<br>
400 Bad Request<br>
404 Not Found<br>
500 Internal Server Error<br>

>관련자료<br>
- [RESTful API 공식문서](https://aws.amazon.com/ko/what-is/restful-api/)<br>
- [RESTful API 테스트 도구 - PostMan](https://www.postman.com/)<br>
- [JSON 직렬화 코드 제네레이션 기법](https://docs.flutter.dev/data-and-backend/json#serializing-json-using-code-generation-libraries)<br>
- 코드 제네레이션을 활용한 fromJson, toJson 작성<br>
_**(서버가 믿음직스러울때만 사용 가능 아니면 mapper사용)**_
내가 사용할 필요한 내용으로만 간단히 구성 [(JsonSerializable)](https://docs.flutter.dev/data-and-backend/serialization/json#serializing-json-using-code-generation-libraries)



