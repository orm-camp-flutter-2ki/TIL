### Provider

- Provider 는 `InheritedWidget` 을 심플하게 사용하도록 한 것
- 상태 관리를 위한 패키지
- 애플리케이션의 데이터를 효율적으로 관리하고 상태를 공유
- `InheritedWidget`을 기반으로 구현
- 보다 간편한 상태 관리와 상태 공유를 가능하게 함

  ---

Provider를 사용하는 주요 이점:

간편한 상태 관리:
- 앱의 상태를 관리하기 위한 복잡한 코드를 작성할 필요가 없음
- Provider를 사용하여 상태를 관리하면 훨씬 간결하고 읽기 쉬운 코드를 작성할 수 있음

상태 공유:
- 앱의 여러 부분에서 동일한 데이터를 손쉽게 공유할 수 있음
- 데이터를 여러 위젯 간에 전달하고 동기화할 수 있음

성능 향상:
- 효율적으로 상태를 업데이트하고 위젯을 리빌드 이를 통해 앱의 성능을 향상시킬 수 있음

다양한 기능 제공:
- `ChangeNotifierProvider`, `StreamProvider`, `FutureProvider` 등 다양한 종류의 Provider가 있음
-
- ChangeNotifierProvider: 자식 위젯에서 데이터를 감지하고 필요에 따라 UI를 업데이트. 단순한 상태 관리부터 복잡한 UI의 상태를 관리

StreamProvider: 스트림을 통해 비동기 데이터를 제공하고 UI를 업데이트. 네트워크 호출이나 데이터베이스 쿼리와 같은 비동기 작업의 결과를 즉시 반영

FutureProvider: 비동기 함수의 결과를 즉시 제공. 이는 초기 데이터 로딩이나 사용자 입력에 따른 비동기 작업을 처리할 때 유용

---

### 예시코드

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class TextModel extends ChangeNotifier {
  String _text = '안녕하세요!';

  String get text => _text;

  void updateText(String newText) {
    _text = newText;
    notifyListeners(); // 상태 변경을 Provider에 알림
  }
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => TextModel(), // TextModel 제공
      child: MaterialApp(
        title: 'Text App',
        home: MyHomePage(),
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final textModel = Provider.of<TextModel>(context); // TextModel 인스턴스 가져오기

    return Scaffold(
      appBar: AppBar(
        title: Text('Text App'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text(
              textModel.text, // 공유된 텍스트 표시
              style: TextStyle(fontSize: 24),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // 버튼 클릭 시 텍스트 업데이트
                textModel.updateText('반갑습니다!');
              },
              child: Text('텍스트 변경'),
            ),
          ],
        ),
      ),
    );
  }
}

```
