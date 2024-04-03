### Layout(레이아웃)

- Widget : Flutter의 화면을 그리는 기본 구성요소
  - 필수 위젯
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

- StatefulWidget : 상태가 있는 위젯, 화면 갱신에 영향을 주는 변수가 있으면 이 위젯을 사용. setState()와의 조합을 사용하여 화면을 갱신한다.
- StaelessWidget : 상태를 가지지 않는 위젯, 화면 갱신에 영향을 주는 변수가 없다면 이 위젯을 사용
  - 처음 앱을 구성할 때는 StatelessWidget으로 작성을 시작하고, 영향을 주는 변수가 필요하다면 StatefulWidget으로 변경한다.
    - 영향을 주는 변수가 생겼을 때 StatelessWidget(StatefulWidget)에 커서를 대고 Alt+Enter를 누르면 StatefulWidget(StatelessWidget)로 변경 가능

- 플러터 공식문서 공부하기
  - [상호 작용](https://docs.flutter.dev/ui/interactive)
