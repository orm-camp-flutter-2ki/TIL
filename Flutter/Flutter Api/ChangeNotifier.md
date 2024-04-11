# ChangeNotifier (class)
[공식문서](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html) 

VoidCallback을 통해 변화 알림(change notification) API를 제공하는 상속, 믹스인 가능한 클래스

> VoidCallback: 인자와 반환 값이 없는 콜백에 대한 시그니처  
> typedef VoidCallback = void Function();

listener 추가에 O(1), listener 삭제 및 알림 전송에 O(n)이 걸린다. (n은 리스너의 수)

## 데이터 모델 구현체로 ChangeNotifier 사용하기

데이터 객체는 ChangeNotifier를 상속 또는 믹스인 함으로써 [Listenable](/Api%20Flutter/Listenable.md) 인터페이스를 구현하고, ListenableBuilder 같은 위젯에서 Listenable에 대한 변화 감지가 가능하게 한다.

### 예제
아래는 ListenableBuilder를 활용하여 count가 변경될 때 Text만 다시 build되도록하는 예제이다.  
현재 count의 값은 count 값이 변할 때 다시 ListenableBuilder의 내용을 다시 build하는 ChangeNotifier의 구현 클래스에 저장되어 있다.  
[예제 코드1](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html#foundation.ChangeNotifier.1)

다음은 ChangeNotifier 구현체가 list를 캡슐화하고 리스트에 새로운 아이템이 추가되면 언제든 알림을 주는 예제이다.  
이 예제는 아이템 추가만 지원한다.  
[예제 코드2](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html#foundation.ChangeNotifier.2)

## 메서드 뜯어보기

### void notifyListeners()

등록된 모든 listener를 실행한다.

객체가 변경되면 이 메서드는 호출되어, client에게 객체가 변경되었음을 알려준다. 순차적으로 알림을 주는 과정 중에 추가되는 listener는 알림을 받을 수 없다. 순차적으로 알림을 주는 과정 중에 삭제되는 listener는 삭제된 이후에 알림이 가지 않는다.

listener에서 발생하는 exception은 FlutterError.reportError로 잡을(catch) 수 있고 보고될 수 있다.

이 메서드는 dispose가 호출된 이후에는 호출되어서는 안된다.

여러번 반복하여 등록된 listener를 제거하면 예상치 못한 결과나 나타날 수 있다. (아래에서 자세히)

<br>

### void addListener(VoidCallback listener)
객체가 변경되었을 때 호출되는 클로저를 등록한다.

만약 주어진 클로저가 이미 등록되었다면, 추가적인 인스턴스가 또 추가된다. 따라서 추가한 만큼 삭제해주어야 클로저가 호출되는 것을 막을 수 있다.

이 메서드는 dispose메서드가 호출된 이후에는 호출되어서는 안된다.

만약, listener가 두번 등록되고 한번만 제거된다면, 여전히 변경에 대한 알림이 전송된다.  
반면 등록된 listenr의 수보다 더 많이 제거를 할 경우는 더 이상 알림이 전송되지 않는다.

이는 listenr가 구분됨(identical)에도 ChangeNOtifier가 그들을 구분할 수 없기 때문에 나타나는 이상한 행동이다. 
그래서 ChangeNotifier는 등록된 listener가 하나라도 남아있으면 여전히 모든 listener에 대해 알림을 전송한다.

이 때문에, 두 개의 서로 다른 객체에서 등록한 listenr가  예상치 못한 행동이 나타날 수 있다.  
This surprising behavior can be unexpectedly observed when registering a listener on two separate objects which are both forwarding all registrations to a common upstream object.

<br>

### void removeListener(VoidCallback listener)
객체가 변경되었을 때, 알림을 주는 클로저가 담긴 listener에 등록된 클로저를 제거한다.

만약 제거하려는 listener가 등록되지 않은 listener인 경우 무시된다.

만약 dispose 메서드가 호출되었다면 이 메서드는 즉시 반환(종료)된다.

<br>

### void dispose()

객체이서 사용되던 모든 resource를 해제한다.   
이 메서드가 호출되고 나면, 객체는 사용될 수 없는 상태가 되며, 폐기되어야 한다.  
(객체가 dispose된 후에, addListener 메서드가 호출되면 에러가 발생한다)  

이 메서드는 객체의 owner에 의해 한번만 호출되어야 한다.

이 메서드는 listener에게 알림을 주지 않으면, 호출될 때 listener list를 한번에 비운다.  
해당 ChangeNotifier의 소비자 클래스는 dispose하기전에 알림을 줄 것인지를 결정해야만 한다.