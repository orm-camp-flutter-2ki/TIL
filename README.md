상태관리 라이브러리

임시상태
- PageView의 index
- BottomNavigationView의 index
- 애니메이션 상태

그 외, 어플리케이션 상태
- Preference
- 로그인 정보
- 쇼핑몰의 카트
- 메이랩의 읽은 메일/ 안 읽은 메일
- 소셜앱의 알림

상태 관리

상태는 데이터 데이터는 변수
변수를 수정하면 알아서 UI도 바뀌게 할 수 있다

Provider 라이브러리
Provider는 InheritedWidget을 심플하게 사용하도록 한 것이다.

상태관리를 편하게 하기 위한 라이브러리 4가지
- Provider
- Bloc
- Riverpod
- GetX


Provider의 장점
InheritedWidget과 가장 흡사하다
제약이 많아서 에러 내기가 어렵다

----------------------------------
240417

클린 아키텍처

클린 아키텍처의 장점
1. 확장 가능한 앱
2. 쉬운 테스트
3. 다른 사람도 이해하기 쉬운 구조

작업 방법

presentation, domain & data 레이어로 코드를 나눈다

Data Layer
- Database, Remote API, Preference 등 구현
- DB엔터티 맵퍼 & DTO
- 레포지토리 구현
- 데이터 형태에 따라 local / remote로 구분할 수 있다.

Domain Layer
- 아키텍처의 가장 핵심이 되는 레이어
- 비즈니스 로직이 포함된 Use Case를 포함
- 모델 클래스를 포함
- repository 정의
- 이외에도 service, logic, exception, validation, event, command 등 도메인에 필요한 내용이 올 수 있음

Presentation Layer
- 모든 화면, 컴포넌트를 포함한 위젯들 (UI)
- ViewModel을 포함

Use Case를 사용하는 이유
- ViewModel이 어떤 기능을 하는지 직관적으로 파악 가능
- Repository 수정사항에 따른 ViewModel에서의 의존성 제거
- 클린 아키텍처의 목적 중 하나인 변경의 최소화를 만족하기 위해
- 여러 ViewModel에 동일한 기능이 있을 경우 기능의 재사용

Use Case의 이름 규칙

현재 시제의 동사 + 명사/대상(선택사항) + UseCase

예)
FormatDateUseCase
LogOutUserUseCase
GetLatestNewsWithAuthorsUseCase
makeLoginRequestUseCase

정리
- 클린 코드에 정답은 없다
- 프로젝트 성격에 따라 아키텍처는 달라질 수 있다.
- 더 좋은 구조는 계속 등장할 것이다.

