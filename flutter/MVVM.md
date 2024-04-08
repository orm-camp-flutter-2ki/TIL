# MVVM이란?

- Model - View - ViewModel의 약자로, 소프트웨어 아키텍처 디자인 패턴 중 하나이다.  최근 앱 개발쪽에서 이 패턴이 유행이다.
- 기존에 Dart 배울 때 Repository에서 View에 대한 비즈니스 로직을 모조리 추가했다. 그러나 각 View에 필요한 비즈니스 로직들은 각 ViewModel에 대응하여 분리하는것이 큰 프로젝트일 수록 구조적으로 유지보수에 용이할것이다.

### Model

- 우리가 Dart를 배울 때 Repository와 같다고 보면된다.
- 데이터를 가져오고 삭제하는 등의 로직이 담겨있다.
- 데이터베이스나 네트워크 요청(안드로이드에서 Retrofit2)과 같은 역할이라고 이해했다.

### View

- 말 그대로 View이며 UI를 담당한다
- ViewModel에서 호출하는 메서드가 무엇을 하는지 View는 알 필요가 없기 때문에 오로지 UI에 사용되는 위젯들만 신경쓰면된다. 단일 책임 원칙을 따르는 셈으로 이해했다.

### ViewModel

- View와 Model사이의 중재자 역할을 수행한다.
- RepositoryImpl을 View에서 직접 가져오는게 아니라 그 View만의 ViewModel을 만들어서 비즈니스 로직을 구현한다.
- ViewModel은 여러가지의 Repository를 가져와서 조합할 수 있고, 필드 변수들은 숨기되 get으로 참조할 수 있게는 해놔야 한다.

## ChangeNotifier

- 상태 관리에 용이한 도구이며, 상태가 변할 때 View에게 알리고 UI를 업데이트할 수 있도록 돕는 역할을한다.
- 안드로이드에서 sealed class로 상태관리를 하며 LiveData로 필드를 만들고, View에서 Observe패턴으로 관찰하는 느낌과 유사하다고 이해했다.

```dart
void updateUi() => setState(() {});

@override
void initState() {
  super.initState();
  viewModel.getPhotos();
  viewModel.addListener(updateUi);
}

@override
void dispose() {
  viewModel.removeListener(updateUi);
  super.dispose();
}
```

- 다음과 같은 공식(?)으로 View에서 간편하게 상태를 관찰하고 setState()를 호출할 수 있다,..
