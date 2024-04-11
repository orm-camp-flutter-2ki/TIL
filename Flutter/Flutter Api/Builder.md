# Builder (class)
[공식 문서](https://api.flutter.dev/flutter/widgets/Builder-class.html)

자신의 builder 콜백을 사용하는 build 메서드를 통해 새로운 자식 위젯을 생성하는 stateless 유틸 위젯

이 위젯은 StatelessWidget 구현체 정의에 대한 inline한 대안이다.  
예를 들어, 아래와 같은 정의되고
```dart
class Foo extends StatelessWidget {
  const Foo({super.key});
  @override
  Widget build(BuildContext context) => const Text('foo');
}
```
다음과 같이 사용되는 위젯을
```dart
const Center(child: Foo())
```
아래와 같이 정의와 사용을 새로운 위젯 클래스를 만들 필요 없이 한번에 가능하다.
```dart
Center(
  child: Builder(
    builder: (BuildContext context) => const Text('foo'),
  ),
)
``` 

child에 바로 자식 위젯을 할당하지 않고, Builder를 통해 할당하는 방식의 차이점은 새로운 BuildContext가 자식 위젯에게 부여된다는 것이다.  

이는 위젯 tree가 inherited 위젯을 포함하고 있는 경우 특히 더 눈여겨 볼만하다.
> inherited 위젯은 Scaffold.of와 같이 자식 위젯의 BuildContext 조상을 따라가는 메서드에 의해 참조되기 때문

아래의 예제에서, 버튼의 onPressed 콜백은 Scaffold.of로 포함중인 ScaffoldState를 찾을 수 없다.
```dart
Widget build(BuildContext context) {
  return Scaffold(
    body: Center(
      child: TextButton(
        onPressed: () {
          // Fails because Scaffold.of() doesn't find anything
          // above this widget's context.
          print(Scaffold.of(context).hasAppBar);
        },
        child: const Text('hasAppBar'),
      )
    ),
  );
}
```

Builder 위젯은 추가적인 BuildContext 요소를 부과하기 때문에, Scaffold.of 메서드는 성공적으로 호출된다.
```dart
Widget build(BuildContext context) {
  return Scaffold(
    body: Builder(
      builder: (BuildContext context) {
        return Center(
          child: TextButton(
            onPressed: () {
              print(Scaffold.of(context).hasAppBar);
            },
            child: const Text('hasAppBar'),
          ),
        );
      },
    ),
  );
}
```

### Inheritance
Object > DiagnosticableTree > Widget > StatelessWidget > Builder