### 플러터 폴더 구조

- data
- presentation
- router goroute()


- 화면 하나에 하나의 viewModel 이어야지 이상적


---

- 콜백 함수 (Callback Function):

특정 이벤트가 발생했을 때 호출되는 함수로, 다른 함수의 인자로 전달되어 사용
예를 들어, 버튼 클릭 시 실행되는 함수나 비동기 작업 완료 후 호출되는 함수 등이 있음



- with 코드 조각 (뭉탱이):
with 키워드는 다중 상속을 허용하지 않는 Dart에서 mixin을 사용하는 방법
with 키워드를 사용하여 클래스에 여러 mixin을 적용할 수 있음 이를 통해 클래스에 여러 기능을 추가할 수 있음



- addListener:
리스너를 등록하여 특정 이벤트가 발생했을 때 호출되는 메서드
일반적으로 상태 변화를 감지하고 처리하는데 사용됩니다. 예를 들어, 데이터 변경 시 UI를 업데이트하는 등의 작업에 사용될 수 있음


- removeListener:
등록된 리스너를 제거하는 메서드
더 이상 필요하지 않은 리스너를 제거하여 메모리 누수를 방지하고 성능을 최적화하는데 사용


- initState:
StatefulWidget의 생명주기 메서드 중 하나로, 위젯이 최초로 생성될 때 호출
초기화 작업이 필요한 경우, initState 내에서 수행됩니다. 예를 들어, 데이터 로드, 컨트롤러 초기화 등이 있음


- dispose:`
StatefulWidget의 생명주기 메서드 중 하나로, 위젯이 제거될 때 호출
위젯이 제거되기 전에 정리(clean-up) 작업이 필요한 경우, dispose 메서드 내에서 수행됩니다. 예를 들어, 리소스 해제, 이벤트 리스너 제거


- MVVM (Model-View-ViewModel):
앱의 아키텍처 중 하나로, Model, View, ViewModel 세 가지 요소로 구성
Model은 앱의 데이터와 비즈니스 로직을 담당하고, View는 사용자 인터페이스를 나타내며, ViewModel은 View와 Model 사이의 통신과 데이터 변환을 담당
MVVM 아키텍처는 앱의 구조를 명확히 정의하고 유지보수와 확장성을 향상시키는데 도움이 됨

---

### MVP와 MVVM 의 차이

- 패턴 구성:
MVP: Model, View, Presenter로 구성됩니다. Presenter는 View와 Model 사이에서 중재자 역할을 함
MVVM: Model, View, ViewModel로 구성됩니다. ViewModel은 View와 Model 사이의 중개자 역할을 하며, 데이터 바인딩을 통해 View와 Model을 동기화

- 역할 분리:
MVP: Presenter가 View와 Model 사이의 모든 상호 작용을 처리/ View는 사용자 인터페이스를 표시하고 사용자 이벤트를 Presenter로 전달
MVVM: ViewModel은 View와 Model 사이의 상호 작용을 처리/ View는 사용자 인터페이스를 나타내고, ViewModel은 이를 통해 데이터를 제공하며 사용자 입력을 처리

- 데이터 바인딩:
MVP: 데이터 바인딩을 지원하지 않음. Presenter는 View와 Model 사이에서 수동으로 데이터를 전달
MVVM: 데이터 바인딩을 통해 View와 ViewModel이 자동으로 동기화. 이로 인해 UI 업데이트가 자동으로 처리되고, 개발자는 일부 상태 관리 로직을 줄일 수 있음

- 테스트 용이성:
MVP: Presenter와 View는 서로 독립적으로 테스트할 수 있음. 이로 인해 유닛 테스트가 쉬움
MVVM: ViewModel과 View의 결합이 더 강하므로 유닛 테스트가 조금 더 복잡할 수 있습니다. 하지만 ViewModel은 비즈니스 로직을 포함하므로 테스트 가능한 부분이 많음


- Android 및 iOS에서의 사용:
MVP: Android에서 많이 사용되는 패턴 중 하나/ Android의 Activity 및 Fragment는 View 역할을 하고, Presenter는 비즈니스 로직을 처리
MVVM: iOS 및 Android 모두에서 사용되는 패턴 Android에서는 데이터 바인딩 라이브러리를 통해 MVVM을 구현하고, iOS에서는 SwiftUI와 같은 프레임워크를 사용하여 MVVM을 구현

간단히 말하면, MVP는 Presenter가 중심 역할을 하고 View와 Model을 분리하는데 중점을 둠. 반면에 MVVM은 ViewModel이 중심 역할을 하고 View와 Model을 중재하는 데 초점을 둠







