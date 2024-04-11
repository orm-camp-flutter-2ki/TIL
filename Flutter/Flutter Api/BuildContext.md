# BuildContext (abstract)
[공식 문서](https://api.flutter.dev/flutter/widgets/BuildContext-class.html)

위젯 tree에서 위젯의 위치에 대한 handle(조작부)

BuildContext는 StatelessWidget.build 메서드와 State 객체의 메서드에서 사용되는 메서드들을 제공한다.

BuildContext 객체들은 WidgetBuilder 함수(예, StatelessWidget.build)에 전달되고 State.context 속성으로 접근 가능하다.  

또한 몇몇 static 함수(예, showDialog, Theme.of)들은 build contxt를 사용하기 때문에, 위젯을 호출하는 역할을 하거나, 주어진 context에서 특정한 데이터를 얻을 수 있다.

각각의 위젯들은 StatelessWidget.build나 State.build함수에서 반환된 부모 위젯으로부터 받은 고유의 BuildContext를 가진다. (RenderObjectWidget의 자식인 부모 위젯으로부터 받을 수도 있음)

특히, 이는 build 메서드 내부 위젯의 build context는 해당 build 메서드의 결과로 반환되는 위젯의 build context와 다름을 의미한다. 

이 때문에 몇가지 특이한 경우가 생기는데, 예를 들어, Theme.of(context) 함수는 주어진 build context 내부에서 가장 가까운 Theme를 찾는다. 만약 위젯 tree의 Theme를 포함하고 있는 build 메서드가 위젯 Q를 build할 때, Theme.of 메서드를 통해 자신의 context를 위젯 Q에게 전달하려고 해도, 위젯 Q는 자신의 조상(위젯 tree에서 상위 위젯)의 context를 찾는다(따른다). 만약 위젯 tree 내부의 하위 context가 필요한 경우라면, Builder 위젯을 사용할 수 있다. Builder.builder 콜백에 인자로 전달되는 context는 해당 Builder의 context가 된다.

예를 들어 다음의 코드에서 ScaffoldState.showBottomSheet 메서드는 build 메서드가 스스로 생성한 Scaffold위젯에 대해 호출된다. 만약, Builder 사용되지 않고, build 메서드 인자의 context가 사용되었다면, Scaffold를 찾을 수 없기 때문에 Scaffold.of 함수는 null을 반환할 것이다.

```dart
@override
Widget build(BuildContext context) {
  // here, Scaffold.of(context) returns null
  return Scaffold(
    appBar: AppBar(title: const Text('Demo')),
    body: Builder(
      builder: (BuildContext context) {
        return TextButton(
          child: const Text('BUTTON'),
          onPressed: () {
            Scaffold.of(context).showBottomSheet(
              (BuildContext context) {
                return Container(
                  alignment: Alignment.center,
                  ...

```


몇몇 위젯의 BuildContext는 위젯이 tree안에서 이동함에 따라 위치가 변경될 수 있다. 이 때문에, BuildContext 메서드에서 반환되는 값은 단일 동기 함수 밖에서는 캐싱되어서는 안된다.  
=> 바뀔 수도 있기 때문에 유효하지 않은 캐싱 값이 될 수 있음

BuildContext가 연관되어 있는 위젯이 위젯 tree에서 unmount되어 유효하지 않은 상태가 될 수 있기 때문에 BuildContext 인스턴스를 저장하는 것을 피해야 한다.  

만약, BuildContext가 비동기 갭(비동기 연산이 수행된 이후에)에 걸쳐 사용된다면, mounted를 확인하여 context가 여전히 유효한지 검사한 후 context와 상호작용해야 한다.
> bool mounted: context가 연관되어 있는 위젯이 위젯 tree에서 현재 mount되어 있는지 여부를 나타내는 속성  
> 한번 unmount된 BuildContext는 두번 다시 mount될 수 없다.

BuildContext는 실질적인 Elemnet 객체로 BuildContext 인터페이스는 Element 객체를 직접 조작하는 것을 방지하는 데 사용된다.

### Implementers
Element