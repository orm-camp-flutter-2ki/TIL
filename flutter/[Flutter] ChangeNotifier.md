>[**공식문서**](https://api.flutter.dev/flutter/foundation/ChangeNotifier-class.html)

>A class that can be extended or mixed in that provides a change notification API using VoidCallback for notifications.
- 알림에 VoidCallback을 사용하여 변경 알림 API를 제공하는 확장 또는 혼합이 가능한 클래스입니다.

>It is O(1) for adding listeners and O(N) for removing listeners and dispatching notifications (where N is the number of listeners).
- 리스너를 추가할 때는 O(1), 리스너를 제거하고 알림을 발송할 때는 O(N)입니다(여기서 N은 리스너의 수입니다).
  - O(1)이 추가되면 받는애들 O(N)들이 자동으로 바뀐다 -> 화면이 다시그려진다 <br>
_  O(1)'상수시간' 입력의 크기와 관계없이 일정한 시간에 실행
  O(N)'선형시간' 입력의 크기에 비례하여 동작 수행_
  
>Using ChangeNotifier subclasses for data models
- 데이터 모델에 ChangeNotifier 서브클래스 사용

>A data structure can extend or mix in ChangeNotifier to implement the Listenable interface and thus become usable with widgets that listen for changes to Listenables, such as ListenableBuilder.
- 데이터 구조는 ChangeNotifier를 확장하거나 혼합하여 Listenable 인터페이스를 구현할 수 있으므로 ListenableBuilder와 같이 Listenables 변경 사항을 수신하는 위젯에서 사용할 수 있게 됩니다.

 
### Listenable class (abstract)
 listeners 일반적으로 객체가 업데이트되었음을 클라이언트에 알리는 데 사용
ChangeNotifier - 하위 클래스로 분류하거나 혼합하여 Listenable 인터페이스를 구현하는 객체를 생성할 수 있습니다.

ValueNotifier - 수정 시 알림을 트리거하는 변경 가능한 값으로 ValueListenable 인터페이스를 구현합니다 .


###  ⭐️ 한장보기 
![](https://velog.velcdn.com/images/hee462/post/13b7e6c2-5cb3-4ef0-b1c9-3ec97e157a4e/image.png)
