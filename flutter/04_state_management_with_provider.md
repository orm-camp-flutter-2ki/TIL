# State Management with Provider

변수, 데이터 등의 값이 바뀔 때 그에 맞춰 UI상으로 변화를 줘야 할 상황이 있습니다.
그럴 땐 setState()로 화면을 다시 빌드할 수도 있지만 setState() 말고도 관리하기 좋은 여러 방법들이 있습니다.
InheritedWidget과 ChangeNotifier와 같은 기본 위젯을 사용할 수도 있지만
이를 편리하게 관리하기 위해서 여러 라이브러리들이 있습니다.

Riverpod : https://pub.dev/packages/riverpod
Provider : https://pub.dev/packages/provider
BLoC : https://pub.dev/packages/flutter_bloc
GetX : https://pub.dev/packages/get

그 중 Provider라는 패키지의 기본 사용법에 대해 알아보겠습니다.

### Provider
Provider는 InheritedWidget의 특성을 살렸으며 자주 쓰이는 패키지입니다.

그 중 ChangeNotifierProvider를 이용한 상태 관리를 살펴보겠습니다.

1. ViewModel에 with ChangeNotifier
```dart
class ViewModel with ChangeNotifier {
...
}
```
2. ChangeNotifierProvider 배치
```dart
ChangeNotifierProvider(
  create: (_) => ViewModel(),
  child: View()
)
```
3-1. View에서 context를 통한 ViewModel 접근
```dart
@override
initState() {
  // initState에서 context로 바로 접근이 힘들기 때문에
  // Future.microtask()로 텀을 줌
  Future.microtask(() {
    context.read<ViewModel>().method();
    // read는 단발성 접근
  });
}

@override
Widget build(BuildContext context) {
  final viewModel = context.watch<ViewModel>();
  // watch는 지속적인 관찰, build 메소드 내에서 사용
  return Container(child: Text(viewModel.value));
}
```

3-2. Consumer 사용
```dart
Consumer<ViewModel>(
  builder: (context, model, child) {
    return Text(model.value);
  }
)
```
