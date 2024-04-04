# Widget

Flutter 의  화면을 그리는 기본 구성 요소

위젯은 화면의 구성요소(element)를 그리는 청사진(blueprint) 이다.

## 필수위젯

- Scaffold
- AppBar
- Container
- Text
- Center
- Column
- Row
- ElevatedButton
- Navigator.push (화면 전환)
- Image.network
- Image.asset
- TextField
- ListView
- SizedBox
- Stack
- Form
- Padding
- SingleChildScrollView
- FloatingActionButton

# StatefulWidget

> 라이브템플릿 `stful`

상태를 가지는 위젯

변경사항에 따라 화면을 다시 그려야 하는 경우에 사용

`setState()` 와 조합하여 화면을 갱신함.

`initState()`, `dispose()` 와 같은 생명 주기 함수를 사용

```dart
class NewPage extends StatefulWidget {  
  const NewPage({super.key});  
  
  @override  
  State<NewPage> createState() => _NewPageState();  
}  
  
class _NewPageState extends State<NewPage> {  
  @override  
  Widget build(BuildContext context) {  
    return const Placeholder();  
  }  
}
```

# StatelessWidget

> 라이브 템플릿 `stless`

상태가 없는 위젯

정적인 화면을 나타낼 때 사용

```dart
class NewPage extends StatelessWidget {  
  const NewPage({super.key});  
  
  @override  
  Widget build(BuildContext context) {  
    return const Placeholder();  
  }  
}
```

# 오늘의 배운 것들

## 가상 디바이스 디버그 배너 없애기

```dart
@override  
Widget build(BuildContext context) {  
  return MaterialApp(  
    title: 'Flutter Demo',  
    debugShowCheckedModeBanner: false,  
    theme: ThemeData(  
      colorScheme: ColorScheme.fromSeed(seedColor: Colors.deepPurple),  
      useMaterial3: true,  
    ),  
    home: Scaffold(),  
  );  
}
```

`debugShowCheckedModeBanner: false` 를 추가시켜서  가상 디바이스에서 디버그 배너를 없앨 수 있다.

## PageView 위젯

`PageView` 위젯을 활용하여 좌우로 스크롤 하는 화면을 개발할 수 있다.

PageView를  컨트롤 하기위한 `PageConroller`  을 선언하여 PageVIew 에 넘겨준다.

```dart
// controller
final pageController = PageController(  
  initialPage: 0,  
);
```

```dart
PageView(  
  controller: pageController,  
  children: const [
    BirthdayCard(to: 'kim', from: 'emma'),  
    BirthdayCardWithBackground(to: 'kim', from: 'emma'),  
    BirthdayCardWithLottie(to: 'kim', from: 'emma')  
  ],  
)
```
