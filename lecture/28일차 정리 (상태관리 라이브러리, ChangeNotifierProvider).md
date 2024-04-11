# **상태관리 라이브러리**

화면에 필요한 변수를 관리하는 것이 상태관리 

데이터(초기값 및 변수를)을 생성자에 넣으면 ui가 생성 또는 변화되는 것이 플러터의 컨셉

**상태 관리 (State Management)**

상태 = 데이터 = 변수

변수를 수정하면 알아서 UI도 바뀌게 하자

= InheritedWidget + (ValueNotifier 또는 ChangeNotifier)

굉장히 복잡하지만 가능

**Provider**

- InheritedWidget 과 가장 흡사함 = 근본
- 제약이 많음 = 에러 내기가 어려움
- 구글에서 여전히 공식적으로 밀고 있음
- 다른 라이브러리는 제대로 알고 쓰지 않으면 코드가 위험
- Remi 가 개발함 (freezed 개발자)

**Riverpod**

- Provider 철자를 섞었음
- 현재 가장 인기 있음
- Provider 의 단점을 보완하려고 만들다가 완전 다른 것이 됨
- 코드 제네레이션 기법을 사용하여 런타임 에러를 없앴음
- 근본과 많이 멀어져서 Riverpod 자체를 공부해야 함
- 기능 위주로 Top level 에 모두 정의해 놓고 어디서든 가져다 쓰는 개념
- MVVM, 클린 아키텍처와는 별개의 리버팟만의 아키텍처 공부가 필요

## **ChangeNotifierProvider**

provider 는 단발성 사용은 watch(build안에서 사용 관찰됨)사용시 컴파일 오류 발생 read(initstat에서 사용 관찰안됨)  대신 사용해야 함

provider를 사용하더래도 StatelessWidget 만 사용할 수 있는 것은 아님

모델을 제공할 곳에 Consumer 배치 (Consumer 부분만 리빌드 됨)

StreamBuilder, ListenableBuilder 같은 느낌이라고 보면 됨

- 원하는 부분만 다시 그리기 가능
- StreamBuilder, ListenableBuilder 느낌
- UI 성능을 극한으로 끌어올려야 할 때 검토
