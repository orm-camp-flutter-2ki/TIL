# MVVM이란?

- 모델-뷰-뷰 모델(model-view-viewmodel, MVVM)의 약자로, 소프트웨어 아키텍처 디자인 패턴 중 하나이다.  최근 앱 개발쪽에서 이 패턴이 유행이다.
- 데이터 객체 변환 하는 책임을 지기 때문에 객체를 관리하고 표현하기가 쉬워진다.

### Model

- 우리가 Dart를 배울 때 Repository에 작성한 기능들중 데이터관련 부분만 남겨놓는다고 보면된다.
- 데이터를 가져오고 삭제하는 등의 로직이 담겨있다.

### View

- 외관에 해당한다. 사용자와 상호 작용에 대한 처리를 데이터 바인딩을 통하여 뷰 모델로 전달한다.

### ViewModel

- 그동안 Repository에 작성한 비즈니스 로직을 작성하는 곳.
- 새로운 값을 리턴해주는게 아닌, 기존의 변수를 가지고 지지고 볶는 곳. 따라서 모든 메서드를 void로 만들어 준다.(게터와 비슷하다. 반대로, 뷰에는 상수만 남는다.)
- 통상적으로 뷰마다 하나씩. 쓰지 않으면 줄여도 된다.

## ChangeNotifier

- View와 ViewModel이 데이터 바인딩을 구현 할 수 있게 도와준다. 뷰모델에서는 notifyListeners()를 메서드안에 넣어주고, 뷰에서는 initState에서 addListener()를 넣어주어 데이터가 바뀌면 감지하여 뷰가 바뀔 수 있도록 해준다.
- 사용후에는 dispose하여 메모리누수를 방지해준다.
  
```dart
class CounterModel with ChangeNotifier {
  int _count = 0;
  int get count => _count;

  void increment() {
    _count += 1;
    notifyListeners();
  }
}
```
