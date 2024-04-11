# InheritedWidget (class)
[공식 문서](https://api.flutter.dev/flutter/widgets/InheritedWidget-class.html)

tree 하위로 정보(데이터)를 효율적으로 전파하는 위젯의 기반(상위) 클래스

Build context에서 가장 가까운 특정 타입의 inherited 위젯 인스턴스를 얻어야 한다면, BuildContext.dependOnInheritedWidgetOfExactType를 사용하면 된다.

Inherited 위젯이 위와 같이 참조되는 상황에서 Inherited 위젯의 상태가 변경되면 consumer로 하여금 다시 build하도록 만든다.

### of, maybeOf 메서드 구현
BuildContext.dependOnInheritedWidgetOfExactType를 호출하는 InheritedWidget에 of maybeOf 메서드를 구현하는 것이 일반적인 컨벤션이다. 이를 통해서 범위 내에 위젯이 없는 경우에 대한 대체 로직을 정의할 수 있다. 

of 메서드는 일반적으로 non-nullable 인스턴스를 반환하고 InheritedWidget을 찾지 못하는 경우를 assert로 제한한다. maybeOf 메서드는 nullable 인스턴스를 반환하고 InheritedWidget을 찾지 못한 경우 null을 반환한다. of 메서드는 보통 내부적으로 maybeOf 메서드를 호출하도록 구현된다.

때때로 of와 maybeOf 메서드는 inherited 위젯 대신 inherited 위젯 내부의 특정한 데이터를 반환할 수도 있다.

가끔 inherited 위젯이 다른 클래스의 내부 속성으로 구현되어 private 속성이 될 수도 있다. 이 경우, of와 maybeOf 메서드는 public 클래스 내부에 구현하는 것이 일반적이다. 예를 들어, Theme는 StatelessWidget의 구현체로 private inherited 위젯을 가진다. Theme.of 메서드는 BuildContext.dependOnInheritedWidgetOfExactType 메서드를 통해 private inherited 위젯을 찾고 해당 위젯 내부의 ThemeData를 반환한다.

### of, maybeOf 메서드 호출
of와 maybeOf 메서드를 사용할 때, context는 반든시 InheritedWidget의 자손이어야한다(tree에서 반드시 InheritedWidget 아래에 있어야 한다는 뜻).

아래의 코드에서 사용되는 context는 FrogColor 위젯의 자식인 Builder에서 온 것이기 때문에 정상적으로 동작한다.
```dart
class MyPage extends StatelessWidget {
  const MyPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: FrogColor(
        color: Colors.green,
        child: Builder(
          builder: (BuildContext innerContext) {
            return Text(
              'Hello Frog',
              style: TextStyle(color: FrogColor.of(innerContext).color),
            );
            ...
```

아래의 코드에서 사용되는 context는 FrogColor 위젯의 부모인 MyOtherPage 위젯에서 온 것이기 때문에, 정상적으로 동작하지 않고, FrogColor.of가 호출되면 assert에서 막힌다.
```dart
class MyOtherPage extends StatelessWidget {
  const MyOtherPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: FrogColor(
        color: Colors.green,
        child: Text(
          'Hello Frog',
          style: TextStyle(color: FrogColor.of(context).color),
        ),
        ...
```

### dependOnInheritedWidgetOfExactType\<T extends InheritedWidget\> abstract method

주어진 타입 T에 해당하는 가장 가까운 위젯을 반환하고, 그에 대한 의존성을 생성한다. 적적한 위젯이 없는 경우, null을 반환한다. 

찾는 위젯은 InheritedWidget을 상속한 구현 클래스이고 dependOnInheritedWidgetOfExactType 메서드를 호출하면 현재 build context를 반환되는 위젯에 등록한다. 찾는 타입의 위젯이 새롭게 추가되거나 기존의 위젯이 사라지거나 위젯이 변경되면, build context는 다시 build되고 변경된 새 값을 해당 위젯으로 부터 얻어온다.

이것은 보통 암시적으로 of() static 메서드를 호출됨으로써 이루어진다.

이 메서드는 위젯 생성자나 State.initState메서드에서 호출되면 안된다. 그 이유는 생성자나 initState 메서드는 inherited 값이 변경되어도 다시 호출되지 않기 때문이다. inherited 값이 변경되었을 때 스스로 위젯이 정확히 업데이트되게 하려면, 이 메서드를 build 메서드, layout이나 paint 콜백, State.didChangeDependencies에서 호출하는 것이 좋다.

State.dispose 메서드에서는 element tree가 더이상 안정적인 상태가 아니기 때문에, disopose에서는 이 메서드를 호출하면 안된다. dispose에서 조상에 대한 참조가 필요하다면, State.didChangeDependencies에서 조상에 대한 참조를 저장하는 것이 좋다. State.deactivate에서 이 메서드를 호출하는 것은 안전한데, 해당 메서드는 위젯이 tree에서 제거된 이후에는 절대 호출되지 않기 때문이다.

이 메서드를 통해 얻은 값을 캐싱하거나 재사용하는 것이 아니라면, 이 메서드를 이벤트 핸들러나 timer에서 호출하는 것도 괜찮다.

이 메서드를 호출하는 것은 거의 O(1)이지만 위젯의 build를 몇 번 발생시킨다.

이 메서드를 호출함으로써 위젯이 특정 타입에 대한 dependency가 등록되고나면, 연관된 위젯에 변경이 생기거나, 조상 위젯이 tree내부에서 사라지거나 위치가 변경될 때마다 위젯은 다시 build되고 State.didChangeDependeicies가 호출된다. 

이 메서드에 필요한 파라미터는 오직 InheritedWidget을 상속한 클래스의 타입을 나타내는 타입 파라미터 T뿐이다.

### Implementation
`T? dependOnInheritedWidgetOfExactType<T extends InheritedWidget>({ Object? aspect });`