## 📖 HTTP
<br>


### 📄 HTTP 개념

- HyperText Transfer Protocol
- 원래 문서 전송용으로 설계된 상태 비저장용 프로토콜
- 브라우저가 GET 요청으로 웹 서버의 문서를 읽어오는 용도였음
- 지금은 서버와 클라이언트가 텍스트, 이미지, 동영상 등의 데이터를 주고 받을 때 사용하는 프로토콜로 확장됨
- 웹 상에서 보는 이미지, 영상, 파일과 같은 바이너리 데이터도 HTTP 멀티파트나 Base64 인코딩하여 사용
<br>


### 📄 HTTP와 함께 사용하는 다른 기술들

- JSON 등을 HTTP와 함께 사용하는 RESTful API
- HTTP에 전송 계층 보안(TLS: Transport Layer Security)을 더해 만든 HTTPS
<br>

### 📄 요청 메서드

- GET : 데이터 요청
- POST : 데이터가 포함된 요청
- DELETE : 삭제
- PUT : 업데이트
<br>

### 📄 상태 코드


- 모든 HTTP 응답에는 상태 코드와 상태 메시지가 있음
- 200 OK
- 400 Bad Request
- 404 Not Found
- 500 Internal Server Error
