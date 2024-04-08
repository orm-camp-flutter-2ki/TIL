# ListenableBuilder (class)
[공식문서](https://api.flutter.dev/flutter/widgets/ListenableBuilder-class.html)

[Listenable](/Api%20Flutter/Listenable.md)(값이) 변경될 때, 하위 위젯 tree를 생성하기 위해 사용되는 위젯

ListenableBuilder은 거대한 build 함수 내부에서 다른 객체의 값에 대한 변화를 감지(listen)하기를 바라는 위젯을 위한 클래스이다.  
=> ListenableBuilder을 통해 위젯을 생성하고 해당 위젯을 builder 함수에 전달하면(넣으면)된다.

ListenableBuilder를 Listenable과 함께 사용하여, Listenable이 자신의 listener에게 알림을 줄 때, 위젯의 특정 부분만 다시 build되도록 할 수 있다.  
(Listenable을 상속하여 구현한 클래스는 다 가능 = [ChangeNotifier](/Api%20Flutter/ChangeNotifier.md), [ValueNotifier](/Api%20Flutter/ValueNotifier.md), Animation)  
물론 Listenable을 상속한 구현 클래스들은 각각의 특징이 있으므로 적절한 Builder를 사용하는 것이 더 가독성이 좋다.  
(예, Anibation의 경우 AnimatedBuilder)

### 예제

아래의 예제의 ChangeNotifier 구현체는 counter라는 상태를 가지고 있다. ListenableBuilder는 counter의 값이 변경될 때마다 Text위젯의 렌더링을 업데이트하는(다시 그리는) 데 사용된다.  
[예제 코드1](https://api.flutter.dev/flutter/widgets/ListenableBuilder-class.html#widgets.ListenableBuilder.1)

다음 예제는 ValueNotifier를 사용하여, 하나의 불변 값에 대한 변화를 추적한다.  
[예제 코드2](https://api.flutter.dev/flutter/widgets/ListenableBuilder-class.html#widgets.ListenableBuilder.2)

<br>

## 성능 최적화

만약 builder 함수가 listenable에 의존하지 않는 하위 tree를 포함하고 있다면, listenable의 변화에 따라 다시 build하지 않고 단 한번만 build하는 것이 더 효율적이다.

때문에 이미 build한 자식(pre-built) 속성을 그대로 다시 사용함으로써 변경할 필요없는 위젯을 특정함으로써 성능을 향상 시킬 수 있다.  
ListenableBuilder 이러한 (변하지 않기에 미리 build 해놓은)자식을 builder 콜백에 전달함으로써 build 과정에서 사용될 수 있도록 할 수 있다.

미리 build한 자식을 사용하는 것은 선택사항이지만, 몇몇 경우 눈에 띄는 성능 향상을 가져올 수 있는 좋은 방법이다.

### 예제

아래의 예제는 FocusNode(=ChangeNotifier)을 감지하고 있는 ListenableBuilder이, 어떻게 하위 위젯 tree에 대한 focus가 변경될 때 이를 감지하여 decoration을 변경하는지 보여준다.  
FocusNode가 변경되면 오직 Container만이 다시 build되고 tree의 나머지 부분은 변화되지 않고 그대로 유지된다.
[예제 코드1](https://api.flutter.dev/flutter/widgets/ListenableBuilder-class.html#widgets.ListenableBuilder.3)

### Inheritance
Object > DiagnosticableTree > Widget > StatefulWidget > AnimatedWidget > ListenableBuilder