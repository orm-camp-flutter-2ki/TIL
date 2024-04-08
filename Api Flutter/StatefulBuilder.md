# StatefulBuilder (class)
[공식 문서](https://api.flutter.dev/flutter/widgets/StatefulBuilder-class.html)

상태(state)를 갖고 있고, 자식 위젯을 얻기 위해 클로저를 호출하는 platonic? 위젯
> 상태를 갖고 있는 자식 위젯을 생성하는 Builder 느낌

builder에게 전달되는 StateSetter 함수는 특정한 State의 State.setState를 대신하여 rebuild를 실행하도록 하는데 사용된다.

builder는 StateSetter가 호출될 때 다시 실행될수 있기 때문에, 상태를 나타내는 모든 변수는 builder 함수 밖에 위치해야 한다.

아래는 상태를 가지고 있고, rebuld를 실행하는 inline StatefulBuilder를 사용하는 예제이다.  
```dart
await showDialog<void>(
  context: context,
  builder: (BuildContext context) {
    int? selectedRadio = 0;
    return AlertDialog(
      content: StatefulBuilder(
        builder: (BuildContext context, StateSetter setState) {
          return Column(
            mainAxisSize: MainAxisSize.min,
            children: List<Widget>.generate(4, (int index) {
              return Radio<int>(
                value: index,
                groupValue: selectedRadio,
                onChanged: (int? value) {
                  setState(() => selectedRadio = value);
                },
              );
            }),
          );
        },
      ),
    );
  },
);
```

### Inheritance
Object > DiagnosticableTree > Widget > StatefulWidget > StatefulBuilder
