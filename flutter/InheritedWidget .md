# InheritedWidget란?

부모 위젯에서 자식 위젯까지 데이터를 전달하는 역할을 하는 매우 중요한 개념이다.

DI와 같은 개념으로, 앱 자체에 의존성을 주입하는 Koin, Hlit같은 느낌으로 이해했다.

# 샘플 코드 분석

```dart
void main() {
  runApp(
    ChangeNotifierProvider<MyViewModel>(
      value: MyViewModel(),
      child: const MyApp(),
    ),
  );
}
```

- 메인함수에서 ChangeNotifierProvider를 사용하여 의존성 주입을 한다. 본 코드에서는 MyViewModel의 인스턴스만 제공하지만 실제로는 더 많은 뷰모델을 관리할 수 있는것으로 보인다.

```dart
class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),
        useMaterial3: true,
      ),
      home: const MyViewModelTest(),
    );
  }
}

```

- 앱의 전반적인 테마와 화면 구성을 설정하는 MyApp 클래스이다. 첫 화면을 MyViewModelTest()클래스로 지정한 모습이다.

```dart
class ChangeNotifierProvider<T extends ChangeNotifier> extends InheritedWidget {
  final T value;

  const ChangeNotifierProvider({
    Key? key,
    required Widget child,
    required this.value,
  }) : super(key: key, child: child);

  static ChangeNotifierProvider<T> of<T extends ChangeNotifier>(BuildContext context) {
    return context.dependOnInheritedWidgetOfExactType<ChangeNotifierProvider<T>>()!;
  }

  @override
  bool updateShouldNotify(ChangeNotifierProvider oldWidget) {
    return value != oldWidget.value;
  }
}

```

- InheritedWidget을 상속받고, 전달받은 ViewModel을 관리하는 ChangeNotifierProvider클래스이다.

- of 메서드는 BuildContext를 매개변수로 받고 해당 컨텍스트에서 가장 가까운 ChangeNotifierProvider 위젯을 찾고, 해당 위젯으로부터 ChangeNotifier 인스턴스를 반환한다.자식 클래스에서 부모 클래스 쪽으로 올라가면서 ChangeNotifier를 상속받은 뷰모델을 찾고, 찾으면 반환한다! 라는 느낌으로 이해했다.

- updateShouldNotify 메서드는 InheritedWidget 클래스를 상속받으며 오버라이딩한 메서드이다. 상태 변경을 감지하는데, 새로운 뷰모델이 이전 뷰모델과 다른지 확인해서 다른 경우에만 업데이트가 필요 하다는 bool형 신호를 반환한다…

```dart
class _MyViewModelTestState extends State<MyViewModelTest> {
  @override
  Widget build(BuildContext context) {
    final viewModel = ChangeNotifierProvider.of<MyViewModel>(context).value;
  }
}

class _NextScreenState extends State<NextScreen> {
  @override
  Widget build(BuildContext context) {
    final viewModel = ChangeNotifierProvider.of<MyViewModel>(context).value;
  }
}
```

- 이렇게 두 개의 화면에서 ChangeNotifierProvider의 of 메서드로 MyViewModel을 사용할 수 있게 된다. InheritedWidget 개념을 사용하면 뷰모델이 매우 많아지는 큰 프로젝트인 경우에도 부모 클래스에서 자식 클래스까지 긴 통로를 뚫는 듯한 무분별한 생성자를 만드는 일은 없어지므로 매우 편리하고 가독성도 좋아질것으로 보인다.
