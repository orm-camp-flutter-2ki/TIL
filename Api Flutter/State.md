# State<T extends StatefulWidget> (class)
[공식문서](https://api.flutter.dev/flutter/widgets/State-class.html)

State는 StatefulWidget의 로직과 내부 상태(state)이다.

State는 아래 2가지로 이루어진 정보이다.
(1) 위젯이 build될때 동기적으로 읽혀지는 정보
(2) 위젯의 생명주기에 전반에서 변경되는 정보

위젯 구현자(implementer)는 위젯의 상태가 변경되는 경우, 반듯이 State.setState를 통해 State에게 즉시 알려주어야 한다.

State 객체들은, tree(위젯의 구성)에 추가하기 위해 StatefulWidget을 그릴때(inflating), 프레임워크에 의해 StatefulWidget.createState 메서드가 호출됨으로써 생성된다.

주어진 StatefulWidget 인스턴스는 여러번 그려질수 있기 때문에(예, 트리의 여러곳에서 하나의 위젯이 사용되는 경우), 하나 이상의 State 객체가 주어진 StatefulWidget 인스턴스에 연관될 수 있다.

만약 StatefulWidget이 트리에서 제거되고 이 후에 다시 트리에 추가된다면, 프레임워크는 StatefulWidget.createState를 다시 호출하여 새로운 State 객체를 생성한다. 이로써 State 객체의 생명주기를 단순하게 만든다.

### State의 생명주기

1. 프레임워크가 StatefulWidget.createState를 통해 State 객체를 생성한다.  
=> 새롭게 생성된 State 객체는 BuildContext에 연관된다. 이 연관은 영구적이다 (State 객체는 자신의 BuildContext를 절대 변경하지 않는다). 하지만 BuildContext는 자신 스스로를 tree에서 자신의 위치에서 하위 tree로 자유롭게 이동시킬 수 있다. 이 경우, State 객체는 mount 된 것으로 간주된다.
    > mounted: State 객체가 현재 tree에 속해 있는지 여부를 나타내는 프로퍼티  
    > => State 객체를 iniState를 통해 생성한 후, 프레임워크는 State 객체를 BuildContext에 연관시킴으로써 'mount'한다. State 객체는 프레임워크가 dipose를 호출하기 전까지 mount되어 있고, dispose가 호출된 이후에는 프레임워크가 State 객체를 다시 build하도록 절대 요청하지 않는다.   
    > (mounted가 false 일 때, setState 호출하면 에러 발생)

2. 프레임워크가 initState를 호출한다.
=> State를 상속한 클래스는 initState를 오버리이드하여, initState가 호출될 때 context나 위젯의 속성으로 사용가능한,  BuildContext나 위젯에 의존하는 초기화 작업을 한번만 수행하도록 할 수 있다. 

3. 프레임워크가 didChangeDependencies를 호출한다.
- State를 상속한 클래스는 didChangeDependencies를 오버라이드하여 inheritedWidget을 포함한 초기화 작업을 수행할 수 있다. 만약, BuildContext.dependOnInheritedWidgetOfExactType이 호출되고 상속한 위젯이 이 후에 변경되거나 트리 내부에서 이동하는 경우, didChangeDependencies 메서드는 다시 호출된다.
- 이 시점에서, State 객체는 초기화가 완료되고 프레임워크는 State의 build를 여러번 호출하여 하위 tree의 UI 정보르 얻는다. State 객체는 내부 상태가 변경되어 하위 tree의 UI에 영향이 가는 경우, setState 메서드를 호출하여 자발적으로 자신의 하위 tree를 다시 build하도록 할 수 있다.
- 그렇게되면, 부모 위젯은 같은 rumtimeType과 Widget.key를 가진 새로운 위젯을 다시 build하고 tree의 같은 위치에서 표시되도록 업데이트한다. 이때, 프레임워크는 새로운 위젯을 위해 위젯의 속성을 업데이트하고 didUpddateWidget(이전 위젯을 인자로 받는) 메서드를 호출한다. State 객체는 didUpdateWidget을 오버라이드하여 자신과 연관된 widget의 변화에 대응할 수 있다(예, 명시된 애니메이션 시작하기). 프레임워크는 항상 didUpdateWidget을 호출한 이후에, build를 호출한다. 이는, didUpdateWidget에서 호출하는 setState는 의미없다는 뜻이다.

4. 개발 과정에서 핫 리로드가 발생한다면, reassemble 메서드가 호출된다.
- reassemble 메서드는 initState 메서드에서 준비완료되는 어떠한 데이터든, 다시 초기화될 수 있도록 한다.

5. 만약 State 객체를 포함하고 있는 하위 tree가 tree에서 제거된다면 (예, 부모가 다른 runtimeType이나 Widget.key로 다시 build하는 경우), 프레임워크는 deactivate 메서드를 호출한다. 
- State를 상속한 객체는 이 메서드를 오버라이드하여, 자신과 트리의 다른 요소 사이의 링크(예, 상위 위젯으로 부터 받은 poiter를 자식 위젯의 RenderObject에게 넘겨준 경우)를 제거할 수 있다.

6. 프레임워크는 해당 하위 tree를 tree의 다른 부분으로 다시 삽입할 수도 있다. 이 경우, 프레임 워크는 build를 다시 호출하도록 하여, State 객체가 tree의 새로운 위치에서 올바르게 적용되도록 한다. 만약 프레임워크가 하위 tree를 다시 삽입하는 경우, 이 작업은 하위 트리가 tree에서 제거되면서 발생하는 애니메이션 프레임이 종료되기 전에 완료된다. 이러한 이유로, State 객체는 프레임워크가 dispose 메서드를 호출하기 전까지 대부분의 리소스를 해제하는 것을 연기한다.

7. 만약 프레임워크가 현재 애니메이션 프레임이 끝나기 전까지 하위 트리를 다시 삽입하지 않는 다면, 프레임워크는 dispose메서드를 호출하고 해당 State 객체가 두번 다시 build되지 못하게 한다. State를 상속한 클래스는 dispose 메서드를 오버라이드하여, 해당 객체에서 유지하고 있던 자원들을 해제하도록 할 수 있다(예, 애니메이션 중지).

8. 프레임워크가 dispose를 호출하고나면, State 객체는 mounted 속성이 false인 mount되지 않은 것으로 여겨진다. 이 때, setState를 호출하면 에러가 발생한다. 이 단계의 생명주기는 종료로써 dispose가 호출된 State 객체를 다시 mount하는 것은 불가능하다.
