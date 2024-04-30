240429 (Mon)

플러터 과정 35일

오늘 메모
=

오늘 사용한 플러터 위젯 

ShowDialog
-

사용 가능한 메소드

```dart
Future<T?> showDialog<T>(
{required BuildContext context,
required WidgetBuilder builder,
bool barrierDismissible = true,
Color? barrierColor,
String? barrierLabel,
bool useSafeArea = true,
bool useRootNavigator = true,
RouteSettings? routeSettings,
Offset? anchorPoint,
TraversalEdgeBehavior? traversalEdgeBehavior}
)
```

showDialog<T> 메소드는 Flutter 에서 다이얼로그를 띄우는 역할을 합니다.
이 메소드는 사용자가 지정한 위젯을 기반으로 모달 다이얼로그를 화면 상단에 표시합니다.
모달 다이얼로그는 사용자가 다른 화면으로 이동하기 전에 다이얼로그와 상호작용하도록 강제하는 것입니다.

메소드 매개변수 설명

- context (required): 다이얼로그를 표시할 빌드 컨텍스트입니다. 보통 현재 활성화된 위젯의 컨텍스트를 넘겨줍니다.
- builder (required): 다이얼로그의 내용을 정의하는 위젯 빌더 함수입니다. 이 함수는 BuildContext 를 인자로 받아서 다이얼로그의 내용을 포함하는 위젯을 반환합니다.
- barrierDismissible (optional, default: true): 다이얼로그 외부를 클릭했을 때 다이얼로그를 닫을 수 있는지 여부를 설정합니다.
- barrierColor (optional): 다이얼로그 외부 배경의 색상을 설정합니다. 기본값은 Colors.black54 입니다.
- barrierLabel (optional): 다이얼로그 외부 배경에 대한 접근성 레이블을 설정합니다. TalkBack과 같은 화면 읽기 도구에서 사용됩니다.
- useSafeArea (optional, default: true): 상단 상태바나 하단 시스템 바 영역을 피해서 다이얼로그를 표시할지 여부를 설정합니다.
- useRootNavigator (optional, default: true): 앱의 루트 네비게이터를 사용하여 다이얼로그를 표시할지 여부를 설정합니다. 하위 네비게이터 스택이 있는 경우 이 옵션을 설정해야 합니다.
- routeSettings (optional): 다이얼로그에 대한 라우트 설정 객체입니다.
- anchorPoint (optional): 다이얼로그를 화면의 특정 위치에 고정하는 데 사용하는 앵커 포인트입니다.
- traversalEdgeBehavior (optional): 포커스 이동 시 다이얼로그의 동작을 설정합니다.

반환값

showDialog<T> 메소드는 Future<T?> 객체를 반환합니다. 이 객체는 다이얼로그에서 사용자가 선택한 값 (있을 경우)을 나타냅니다. 
다이얼로그를 빌드하는 builder 함수에서 Navigator.pop(context, value) 메소드를 호출하여 값을 반환할 수 있습니다.

showdialog를 사용할 때 팝업 창처럼 가운데에 창을 띄우려면 AlertDialog를 사용해야 한다.

Flutter AlertDialog 클래스 설명 (한글)
AlertDialog 클래스는 Flutter에서 Material Design 기반의 간단한 알림 다이얼로그를 생성하는 데 사용되는 위젯입니다.

AlertDialog 위젯은 다음과 같은 주요 기능을 제공합니다:

제목 및 내용 표시: 다이얼로그 상단에 제목과 본문 내용을 표시할 수 있습니다.
버튼 추가: 확인, 취소, 중립 등 다양한 버튼을 추가하여 사용자의 선택을 구할 수 있습니다.
이벤트 처리: 버튼 클릭, 다이얼로그 취소 등 다양한 이벤트를 처리할 수 있는 콜백 함수를 설정할 수 있습니다.
스타일 설정: 다이얼로그의 모양, 크기, 색상, 글꼴 등을 원하는 대로 설정할 수 있습니다.
AlertDialog 위젯을 사용하는 기본적인 방법은 다음과 같습니다:

AlertDialog 위젯 생성
title 속성: 다이얼로그 제목 설정
content 속성: 다이얼로그 본문 내용 설정
actions 속성: 버튼 목록 설정 (TextButton, ElevatedButton 등 사용 가능)
onPressed 콜백 함수: 버튼 클릭 시 처리 코드 작성

예제 코드:
```dart
AlertDialog(
  title: Text('제목'),
  content: Text('내용'),
  actions: <Widget>[
    TextButton(
      onPressed: () {
        // 확인 버튼 클릭 시 처리
      },
      child: Text('확인'),
    ),
    TextButton(
      onPressed: () {
        // 취소 버튼 클릭 시 처리
      },
      child: Text('취소'),
    ),
  ],
)
```
 setNegativeButton(), setNeutralButton() 등의 메서드를 사용하여 다이얼로그의 내용과 버튼을 설정합니다.
show() 메서드를 호출하여 다이얼로그를 표시합니다.


