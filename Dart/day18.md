# 네트워크 통신

## Json의 

- 서버-클라이언트 통신에서 표준처럼 사용되는 데이터 교환 형식이다.
- 가볍고 사람이 읽기 쉽다
- Map 과 같은 간단한 구조
- 직렬화 하여 문자열로 나타내기 쉽다
- 대부분의 언어가 이를 파싱할 수 있기 때문에 상호 운용성은 걱정할 것이 없다

## HTTP 개념

- HyperText Transfer Protocol
- 원래 문서 전송용으로 설계된 상태 비저장용 프로토콜
- 브라우저가 GET 요청으로 웹 서버의 문서를 읽어오는 용도였음
- 지금은 서버와 클라이언트가 텍스트, 이미지, 동영상 등의 데이터를 주고 받을 때 사용하는 프로토콜로 확장됨
- 웹 상에서 보는 이미지, 영상, 파일과 같은 바이너리 데이터도 HTTP 멀티파트나 Base64 인코딩하여 사용

## 무상태성

- HTTP 는 상태 비저장 프로토콜
- HTTP는 요청 메시지를 보내기 직전까지 대상 컴퓨터가 응답 가능한지 알 방법이 없음
- Stateless 프로토콜, 즉 상태가 없는 프로토콜이라고 함
- Stateful 프로토콜로는 TCP (Transmission Control Protocol)가 있음


## 자주 사용하는 flutter CLI 명령어

- flutter doctor : 문제점 파악
- (flutter/dart) upgrade : 현재 메이저 버전의 하위 버전 중에서 최신 버전으로 업그레이드
- (flutter/dart) pub get : 수정 사항 반영
- flutter clean : 빌드 파일 삭제
- flutter run : 실행
- (flutter/dart) pub upgrade --major-versions : 메이저 버전의 최신 버전으로 업그레이드
- (flutter/dart) pub add [라이브러리이름] : pubspec.yaml 파일에 자동 추가 후 pub get 까지

## TCP

- 속도 있음 연결지향성 앱에 사용
- 신뢰성 있는 연결지향성 앱에서 사용 (이메일, 파일 전송, 웹브라우저)
- Stateful 프로토콜
- 연결되면 연결을 끊기 전까지 계속 메시지를 주고 받는 프로토콜
- 한쪽에 문제가 생기면 다른쪽에서 감지 가능
- 텍스트가 아닌 바이너리 데이터를 전송
- 패킷 크기가 HTTP에 비해 작음 → 속도 빠름
- 각 요청이 소켓 1개를 공유 (HTTP는 각 요청이 소켓 1개씩 사용)
- 따라서 요청을 식별할 식별자가 필요
- 응답을 알 수 있는 방법이 없기 때문에 타임아웃에 대해 직접 구현해야 함

## 세션과 쿠키

- HTTP는 상태라는 개념이 존재하지 않기 때문에 세션과 쿠키를 사용해 구분
- 주로 웹에서 서버는 세션, 클라이언트는 쿠키를 통해 상태 저장
- 
## How to use serializing-json-using-code-generation-libraries

```
dart pub add json_annotation dev:build_runner dev:json_serializable //이거 복사해서 터미널에 입력 
```

1. 라이브 템플릿 수정
2. 변수 세팅
3. 네임드 생성자 생성
4. dart run build_runner build 터미널에 입력 → post 파일 만듦 fromJson toJson 만들어주는 기법이다. 
 + dart run build_runner build --delete-conflicting-outputs (충돌 해결)

서버를 신뢰할수 있을때 사용 합니다.
널값이 있을 경우에 디티오하는게 맞는지 미리 확인
