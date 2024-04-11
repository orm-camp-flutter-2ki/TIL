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
