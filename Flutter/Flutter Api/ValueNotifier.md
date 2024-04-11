# ValueNotifier<T> (class)
[공식문서](https://api.flutter.dev/flutter/foundation/ValueNotifier-class.html)

오직 하나의 값만 관리하는 [ChangeNotifier](/Api%20Flutter/ChangeNotifier.md)

객체가 관리하는 값이, 동등성 연산자`==`을 통해 이전 값과 다르다고 판별되는 새로운 무언가로 교체되면 listenr에게 알림을 준다.

### 한계

이 클래스는 값의 식별자가 변경되었을 때만 알림을 주는 것으로, 가변 상태의 내부 값이 변경되었을 때는 알림을 주지 않는다.

예를 들어, `ValueNotifier<List<int>>`는 리스트 내부의 원소가 변경되는 경우는 listener에게 알림을 주지 않는다.

때문에, 불변 데이터 타입을 값으로 사용하는 것이 좋다.  
=> 가변 데이터 타입의 경우 ChangeNotifier를 확장하는 것을 고려할 것.

### Inheritance
Object > ChangeNotifier > ValueNotifier