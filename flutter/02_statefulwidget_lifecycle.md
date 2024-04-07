# StatefulWidget Lifecycle

### Stateless Widget
StatelessWidget은 한 번 빌드되는 위젯입니다.
상태를 가지지 않기에 변화되지 않는 위젯입니다.

### StatefulWidget
StatefulWidget은 변경이 가능한 상태(State)를 갖는 위젯입니다.
UI상에서 데이터 변동에 따른 변화를 주고 싶을 때 유용하게 사용할 수 있습니다.
따라서 빌드도 상태에 따라 여러 번 가능합니다.

StatefulWidget 인스턴스 자체는 변동할 수 없습니다.
그러나 StatefulWidget이 생성될 때 호출되는 createState() 메소드로 탄생하는 State 객체(또는 State가 구독하는 객체)에 변경 가능한 상태를 저장할 수 있습니다.

이러한 StatefulWidget이 어떻게 시작되고 끝나는지
생명 주기에 대해 알아보겠습니다.


### StatefulWidget Lifecycle

**1. createMethod()**
StatefulWidget이 생성될 때 호출하며, State 객체를 생성합니다.
```dart
class MainScreen extends StatefulWidget {
  const MainScreen({Key? key}) : super(key: key);

  @override
  State<MainScreen> createState() => _MainScreenState();
  // createState()로 MainScreen의 State 생성
}

class _MainScreenState extends State<MainScreen> {...}
```


**1.5. mounted**
State 객체는 BuildContext와 연결되어 mounted라는 속성이 true가 됩니다.

**2. initState()**
생성자 다음에 호출이 되며, State 객체가 생성될 때 1번만 호출됩니다.
주로 초기 상태 혹은 데이터를 설정할 때 사용합니다.
```dart
@override
void initState() {
  super.initState();
}
```

**3. didChangeDependencies()**
initState() 다음에, 혹은 의존성이 변경될 때 호출됩니다.
예를 들어 상속한 위젯이 업데이트된 경우에 호출됩니다.
```dart
@override
void didChangeDependencies() {
  super.didChangeDependencies();
}
```

**4. build()**
위젯을 반환해서 UI로 렌더링하는 메소드입니다.
이 메소드는 StatefulWidget을 사용하는 이상 반드시 오버라이딩해서 작성해야 합니다.
처음 호출되는 것은 didChangeDependencies() 다음이지만
상태 변화에 따라 여러 번 호출될 수 있습니다.
```dart
@override
Widget build(BuildContext context) {
  return Scaffold(...);
}
```

**5. setState()**
상태가 변경되었을 때, 상태가 변경되었다고 알립니다.
그리고 다시 build()를 실행합니다.
```dart
setState(() {
});
```

**6. didUpdateWidget()**
위젯이 다시 빌드되었을 때 이전 위젯 속성과 현재 위젯 속성을 비교하는 데 쓰입니다.
인자로 oldWidget을 받습니다.
```dart
@override
void didUpdateWidget(MainScreen oldWidget) {
  super.didUpdateWidget(oldWidget);
}
```

**7. deactivate()**
State 객체가 위젯트리에서 삭제될 때마다 호출됩니다.
메모리에서 삭제된 것은 아니라 사용은 가능합니다.
다른 화면으로 이동될 때에도 호출됩니다.
```dart
void deactivate() {
  super.deactivate();
}
```

**8. dispose()**
State 객체가 영구적으로 삭제될 때 호출됩니다.
또한 오버라이딩해서 Controller를 정리할 때에도 많이 사용합니다.
```dart
void dispose() {
  super.dispose();
}
```

**Fin. mounted false**
State가 삭제된 시점에서 mounted는 false 상태가 됩니다.
이 상태에서 setState()를 실행하면 오류가 발생할 수 있습니다.
