# InheritedWidget
- InheritedWidget은 원하는 위젯으로 원하는 객체를 의존성 주입(Dependency Injection)을 해 주는 위젯입니다.
- 의존성 주입이란 ?
  예시
```dart
class Car{
  Engine engine;
  Car(this.engine);

  void start(){
  engine.start();
   }
}
```

- Flutter의 위젯 트리 구조에서, 위젯은 화면에 그려지는 구성 요소입니다.
  이 구성 요소들은 불변의 특성을 가지고 있어, 데이터 변경 시 새로운 위젯을 생성하여 업데이트 해야 합니다.
  이 과정에서 InheritedWidget이 중요한 역할을 합니다.

- 변화가 필요한 위젯 필요한 데이터를 받기 위해서는 트리의 Top 에서 Bottom 까지 생성자를 통한 데이터 전달이 필요합니다.

- InheritedWidget은 주로 위젯 트리의 상위에 위치하여 하위 위젯들에게 데이터를 효율적으로 전달할 수 있는 방법을 제공합니다.
  특정 데이터를 관리하고, 해당 데이터에 의존하는 하위 위젯들이 변경사항을 쉽게 인지하고 반응할 수 있도록 돕습니다.

 예시
```dart
bool isHandset = MediaQuery.of(context).size.width < 600;
return Flex(
    children: [Text("Foo"), Text("Bar"), Text("Baz")],
    direction: isHandset ? Axis.vertical : Axis.horizontal);
```

### XXX.of(context) 형태로 아무데서나 사용할 수 있도록 내가 만드는 법
- context 필요
- updateShouldNotify
- 오버라이드 후에 파라미터 타입 수정을 허용
- 작성한 InheritedWidget을 전달하고자 하는 위젯 트리의 최상위에 배치
- 하위 위젯 트리에서 of(context) 로 참조 가능
