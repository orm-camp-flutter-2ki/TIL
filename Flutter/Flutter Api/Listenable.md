# Listenable (abstract)
[공식문서](https://api.flutter.dev/flutter/foundation/Listenable-class.html) 

listener 리스트를 유지하고 있는 객체

listener는 일반적으로 객체가 업데이트 되었을 때 client에게 알림을 주는데 사용된다.

이 인터페이스에는 2가지 유형이 있다.
1. ValueListenable: current value(현재 값)에 대한 개념을 가진 Listenable 인터페이스를 확장(augment)하는 인터페이스
2. Animation, 방향(순행 혹은 역행)의 개념을 추가하기 위해 ValueListenable 인터페이스를 확장하는 인터페이스

Flutter API의 많은 클래스들은 이 인터페이스를 사용하거나 구현한다.  

아래는 특히 더 연관있는 구현체들이다.
- [ChangeNotifier](/Api%20Flutter/ChangeNotifier.md): Listenable 인터페이스를 구현하는 객체를 생성하기 위해 상속 혹은 믹스인 하는 클래스
- [ValueNotifier](/Api%20Flutter/ValueNotifier.md): 수정에 대해 알림을 유발하는 변화하는 값을 가진 ValueListenable 인터페이스를 구현하는 클래스

'notify cleint', 'send notification', 'trigger notifications', 'fire notification'은 모두 같은 말이다.  
=> 알림 생성, 유발, 전송, 작동, ~~발사~~
