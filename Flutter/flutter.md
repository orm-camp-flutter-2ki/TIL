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

- 주요 위젯
  - [BottomNavigationBar](https://api.flutter.dev/flutter/material/BottomNavigationBar-class.html)
    - 하단 탭 바를 의미. 하단 탭 바를 만드는데 사용.
  - [Column](https://api.flutter.dev/flutter/widgets/Column-class.html)
    - 아래로 정렬되는 레이아웃 위젯. 이미지나 텍스트를 정렬하거나 할 때 사용
  - [Row](https://api.flutter.dev/flutter/widgets/Row-class.html)
    - 수평으로 정렬하기 위한 레이아웃 위젯
    - mainAxisxSize 속성에서는 화면에 꽉 채우는 max, 내부 아이템의 크기에 맞추는 min을 설정할 수 있다
    - mainAxisAligment는 정렬 방법을 결정한다. spaceEvenly는 자식 위젯들 간에 적절한 여백을 두며 정렬되므로 유용하다
  - [SizedBox](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)
    - 상하/좌우 여백을 표시하는데 사용될 수 있으며, width, height 속성에 값을 할당하여 크기를 결정하는 위젯이다.
  - [Card](https://api.flutter.dev/flutter/material/Card-class.html)
    - 카드 형태의 레이아웃 위젯
  - [PageView](https://api.flutter.dev/flutter/widgets/PageView-class.html)
    - 좌우로 슬라이드되는 화면을 만들 때 유용한 위젯이다. children 속성에 여러 화면을 배치하면 된다.
  - [Image](https://api.flutter.dev/flutter/widgets/Image-class.html)
    - 프로젝트 내부 이미지를 표시하려면 asset 메서드를, 네트워크 이미지를 표시하려면 network 메서드를 사용한다.
  - [SingleChildScrollView](https://api.flutter.dev/flutter/widgets/SingleChildScrollView-class.html)
    - 화면에 표현할 내용이 많다면 이 위젯으로 감싸서 스크롤을 생기게 할 수 있다. child 속성에 자식 위젯을 배치하기만 하면 된다.
  - [Opacity](https://api.flutter.dev/flutter/widgets/Opacity-class.html)
    - 위젯에 투명도를 부여한다. opacity 속성은 0.0~1.0 까지 설정할 수 있고 0에 가까울수록 투명, 1에 가까울수록 불투명하다.
  - [Divider](https://api.flutter.dev/flutter/widgets/Divider-class.html)
    - 수평 라인을 표시합니다.
  - [Text](https://api.flutter.dev/flutter/widgets/Text-class.html)
    - 글자를 표시합니다.
  - [Expanded](https://api.flutter.dev/flutter/widgets/Expanded-class.html)
    - child 위젯의 길이를 꽉 채우거나 Expanded끼리 비율을 정할 수 있다.

---

### FutureBuilder

- Future를 UI로 표현하는 방법
  - 1. StatefulWidget + setState()
  - 2. [FutureBuilder](https://api.flutter.dev/flutter/widgets/FutureBuilder-class.html)
       - Future 함수의 결과를 Widget으로 변환하는 위젯
       - snapshot 에 데이터와 에러 정보 등이 들어 있음  
         <img src="https://github.com/algochemy/TIL/assets/152131529/ffa0ad7c-4b2f-46b0-a661-4e224a861c34" width="300" height="150">
       
       - snapshot 객체에서 연결 상태를 알 수 있음  
         <img src="https://github.com/algochemy/TIL/assets/152131529/fae0fd72-57df-4dd3-a4b5-ba3cbbb0d288" width="350" height="200">
         <img src="https://github.com/algochemy/TIL/assets/152131529/5763b72b-b8d5-4525-9b74-b2797260f92f" width="300" height="150">  
         
       - 에러 체크 가능  
         <img src="https://github.com/algochemy/TIL/assets/152131529/1876061f-7470-4986-b3c7-cc007909adf4" width="300" height="150">

- Stateful의 생명주기 조사
  - 초기 실행 : **Widget Constructor -> createState -> initState -> didChangeDepedencies -> build**
  - 종료 : **deactivate -> dispose**
  - 핫 리로드(StatefulWidget의 파라미터 변경사항 적용) : **Widget Constructor -> didCUpdateWidget -> build**
  - 종료(**deactivate -> dispose**) 상태가 되지 않은 이상, 상태는 유지된다.
  
---

### Navigation  

- Navigation
  - 화면 전환을 말 함
  - 화면 표시는 Stack 구조로 관리된다
    - 다른 화면으로 전환 : push
    - 다시 되돌아 오기 : pop

- [Navigation 공식 문서](https://docs.flutter.dev/ui/navigation)
  - 새로운 화면으로 이동 (navpush) : push() 함수는 Future를 리턴하는 타입
    <img src="https://github.com/algochemy/TIL/assets/152131529/e60bb4a1-9d1b-4064-9d1b-4516f0245e14" width="500" height="150">
  - 원래 화면으로 돌아가기 (navpop)  
    <img src="https://github.com/algochemy/TIL/assets/152131529/ea8a4452-f6ec-44ce-a273-0dd67f438a59" width="500" height="150">

---

### [MVMM 패턴](https://learn.microsoft.com/ko-kr/dotnet/architecture/maui/mvvm)
- Repository에 비즈니스 논리가 포함되지 않게 분리하자
- 비지니스 로직을 담당하는 부분을 ViewModel 클래스로 따로 빼 둔다.
- 화면 보여줘야하는 것은 getter로 제공
- ViewModel 하나 더 들어온거밖에 없는데 기능 추가가 쉽다
- 일반적으로 화면 하나 당 하나의 뷰모델을 유지하는 것이 좋다 (화면(View) 하나에 하나에 대한 로직(Model))
- 요구사항(수정사항)이 업데이트됐을 때 변경이 용이하다 !
- Repository는 데이터 주고받는것에만 집중하게 한다.
- MVMM 패턴은 모바일 앱에 가장 적합한 아키텍처 : 확장성과 유지보수의 편의성을 고려
  ![image](https://github.com/algochemy/TIL/assets/152131529/a8911936-0c9b-433b-a223-f531359afdeb)
- ChangeNotifier/addListner로 **View에 알림, 데이터바인딩** (*setState()를 자동으로 처리) 기능 구현 가능
- 아키텍처의 핵심은 단방향 의존성 그리고 Action과 Data의 명확하고 일관된 흐름에 있음
  <img src="https://github.com/algochemy/TIL/assets/152131529/4cc288b6-ed3b-4b17-83e8-d362176666cd" width="400" height="300">  
  - View Layer는 ViewModel Layer는 알 되 Data Layer를 알면 안됨 (계속 캡슐화.)

- 추가 할 내용 : goRouter, ChangeNotifier

---

### InheritedWidget

- InhertiedWidget : 원하는 위젯으로 원하는 객체를 의존성 주입(Dependency Injection)을 해 주는 위젯
  - 의존성 주입이란?
    - 어떤 객체가 다른 객체에서 사용되도록 하는 것
    - 생성자를 통해 필요한 객체를 전달하는 것이 일반적
    - 생성자를 통한 의존성 주입은 의존성 트리가 깊어질수록 단계를 많이 타야되는 단점이 있음
    - 즉, 변화가 필요한 위젯에서 필요한 데이터를 받기 위해서는 트리의 Top 에서 Bottom 까지 생성자를 통한 데이터 전달이 필요하다
    - InheritedWidget은 이런 단점을 해소  
    <img src="https://github.com/algochemy/TIL/assets/152131529/15cbb063-1560-47a3-80a3-457077ac4ddc" width="300" height="400">  

- 정리
  - 위젯 트리에 접근하려면 반드시 context 가 필요하다
  - InheritedWidget : 의존성 주입용 위젯
  - BuildContext : 위젯 트리 정보를 알고 있는 객체 (신)
    - BuildContext 없으면 화면 이동도 못 함
    - BuildContext 없으면 다이얼로그도 실행 안 됨

- 코드 샘플 분석
```dart
import 'package:flutter/material.dart';

void main() {
  runApp(
    ChangeNotifierProvider<MyViewModel>(
      value: MyViewModel(),
      child: const MyApp(),
    ),
  );
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  // This widget is the root of your application.
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

class ChangeNotifierProvider<T extends ChangeNotifier> extends InheritedWidget {
  final T value;

  const ChangeNotifierProvider({
    super.key,
    required super.child,
    required this.value,
  });

  static ChangeNotifierProvider<T> of<T extends ChangeNotifier>(
      BuildContext context) {
    return context
        .dependOnInheritedWidgetOfExactType<ChangeNotifierProvider<T>>()!;
  }

  @override
  bool updateShouldNotify(ChangeNotifierProvider oldWidget) {
    return value != oldWidget.value;
  }
}

class MyViewModel with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class MyViewModelTest extends StatefulWidget {
  const MyViewModelTest({super.key});

  @override
  State<MyViewModelTest> createState() => _MyViewModelTestState();
}

class _MyViewModelTestState extends State<MyViewModelTest> {
  @override
  Widget build(BuildContext context) {
    final viewModel = ChangeNotifierProvider.of<MyViewModel>(context).value;

    return Scaffold(
      appBar: AppBar(
        title: Text(viewModel.count.toString()),
      ),
      body: Center(
        child: Column(
          children: [
            ElevatedButton(
              onPressed: () {
                setState(() {
                  viewModel.increment();
                });
              },
              child: const Text('+'),
            ),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(builder: (context) => const NextScreen()),
                );
              },
              child: const Text('Next'),
            ),
          ],
        ),
      ),
    );
  }
}

class NextScreen extends StatefulWidget {
  const NextScreen({super.key});

  @override
  State<NextScreen> createState() => _NextScreenState();
}

class _NextScreenState extends State<NextScreen> {
  @override
  Widget build(BuildContext context) {
    final viewModel = ChangeNotifierProvider.of<MyViewModel>(context).value;

    return Scaffold(
      appBar: AppBar(
        title: Text(viewModel.count.toString()),
      ),
      body: Center(
        child: Column(
          children: [
            ElevatedButton(
              onPressed: () {
                setState(() {
                  viewModel.increment();
                });
              },
              child: const Text('+'),
            ),
            ElevatedButton(
              onPressed: () {
                Navigator.push(
                  context,
                  MaterialPageRoute(builder: (context) => const NextScreen()),
                );
              },
              child: const Text('Next'),
            ),
          ],
        ),
      ),
    );
  }
}
```

  - main() 함수: Flutter 앱의 진입점
    - 여기서는 ChangeNotifierProvider를 사용하여 MyViewModel을 앱의 루트에 제공하고 있습니다. 이렇게 함으로써 앱 전체에서 MyViewModel에 접근할 수 있게 됩니다.
  
  - MyApp 위젯: 앱의 루트 위젯
    - MyApp은 StatelessWidget이며, build() 메서드를 통해 앱의 UI를 생성합니다.
    - 여기서는 MaterialApp을 사용하여 앱의 기본적인 구성을 설정하고 있습니다. 또한 ChangeNotifierProvider를 통해 MyViewModel을 제공하고 있습니다. 이로써 앱 전체에서 MyViewModel에 접근할 수 있게 됩니다.
  
  - ChangeNotifierProvider 클래스: 상태를 제공하고 관리하는 데 사용
    - ChangeNotifierProvider는 InheritedWidget을 확장한 클래스입니다. 따라서 상위 위젯에서 하위 위젯으로 데이터를 전달할 수 있습니다.
    - ChangeNotifierProvider 클래스는 제네릭 타입 T를 받습니다. T는 ChangeNotifier 클래스를 상속받은 클래스여야 합니다.
    - of 메서드를 통해 현재 위젯 트리에서 ChangeNotifierProvider의 인스턴스를 찾고, 해당 인스턴스의 value를 반환하여 상태에 접근할 수 있습니다. 이때, BuildContext를 매개변수로 받습니다.
    - updateShouldNotify 메서드를 재정의하여 상태 변경을 감지하고 업데이트할지 여부를 결정합니다.
  
  - MyViewModel 클래스
    - MyViewModel은 상태를 관리하는 데 사용됩니다.
    - MyViewModel은 ChangeNotifier 클래스를 상속받아 상태를 관리하고 있습니다.
    - MyViewModel 클래스에는 count 변수와 increment() 메서드가 있습니다.
    - count 변수는 현재 상태를 나타내며, increment() 메서드를 호출할 때마다 1씩 증가하고 상태 변경을 알립니다.
  
  - MyViewModelTest와 NextScreen : 화면을 구성하는 위젯
    - 각 위젯은 StatefulWidget이며, 상태를 가지고 있습니다. MyViewModelTest와 NextScreen 위젯에서는 ChangeNotifierProvider.of() 메서드를 사용하여 MyViewModel에 접근합니다. 이를 통해 상태를 표시하고 상태를 변경할 수 있습니다.
    - 버튼을 누르면 viewModel.increment()가 호출되고, 해당 버튼을 포함하는 위젯 setState()를 통해 다시 빌드되어 UI가 업데이트됩니다.
    - 또한 Navigator.push() 메서드를 사용하여 화면 전환을 수행합니다.
---

### 상태관리, 상태관리 라이브러리

- 상태관리
  - 상태 = 데이터 = 변수
  - 변수를 수정하면 알아서 UI도 바뀌게 하자 = **InheritedWidget + (ValueNotifier 또는 ChangeNotifier)** 굉장히 복잡하지만 가능
  - **더 나은 방법 = 상태관리 라이브러리**
  - 상태관리 라이브러리 중 Provier는 InheritedWidget을 단순하게 사용하도록 한 것. (Provier는 구글에서 권장)
  - 상태관리에 대한 Golden Rule은 없다. 대부분의 경우 setState()만으로 충분하다. 하지만 대규모 프로젝트에서는 관리가 어렵다

- 상태관리 라이브러리 4대장
  - **Provider**
    - InheritedWidget과 가장 흡사함. (근본에 가까움)
    - 제약이 많음 = 에러 내기가 어려움
    - 구글에서 여전히 공식적으로 밀고 있음
    - 다른 라이브러리는 제대로 알고 쓰지 않으면 코드가 messy해짐. (예 : GetX)
    - freezed 개발자인 Remi가 개발함
  - **RiverPod**
    - Provider의 애너그램 (철자를 섞음)
    - Provider의 단점을 보완하려고 만들다가 완전 다른 것이 됨
    - 코드 제네레이션 기법을 이용하여 런타임 에러를 없앴음
    - 근본과 멀어져서 RiverPod 자체를 공부해야 함
    - 기능 위주로 Top Level에 모두 정의해놓고 어디서든 가져다 쓰는 개념
    - MVMM, 클린 아키텍처와는 별개로 리버팟만의 아키텍쳐 공부가 필요
  - **Bloc**
    - 가장 처음 구글이 밀어줬던 상태관리 라이브러리
    - 대형 프로젝트 위주로 사용
  - **GetX**
    - 상태관리에 대한 기본적인 이해 부족한 경우에도 개발 가능 
    - 복잡한 상태를 관리해야하는 경우 좋지 않음
    - 제약이 없다 = 버그 발생률 UP
    - 테스트, 유지 보수가 어려움
 
- Flutter에서 Provider 상태관리 구성
  - ChangeNotifierProvider, ChangeNotifier 조합
    - 위젯트리 최상단 위젯에 ChangeNotifierProvider을 둔다. (ChangeNotifier을 감시)
    - 변경이 필요한 위젯만 자동 갱신
      - Provider.of<ChangeNotifier>(context)
      - context.read<ChangeNotifier>
        - read()는 지속적인 관찰이 아닌 단발성 접근에 사용 : initState() 또는 버튼 클릭
      - context.watch<ChangeNotifier>
        - watch()는 지속적인 관찰을 하고 변경시 build()를 리빌드함. (build 메서드 내에서 사용)
    - 변경을 통지
      notifiyListener()
      
  - ChangeNotifier를 제공할 부분에 ChangeNotifierProvider 위젯 배치  
    <img src="https://github.com/algochemy/TIL/assets/152131529/299e07eb-39ad-4edb-af3b-b52fd60b2f7d" width="300" height="150">

  - UI 전체 코드  
    <img src="https://github.com/algochemy/TIL/assets/152131529/825f2364-4a0a-4a05-acc6-213ec8acfa93" width="400" height="500">  
    - 다음 룰을 따를 것
      - build() 에서는 watch
      - 단발성 실행은 read
      - initState() 에서는 Future.microstask() 후에 read  
        <img src="https://github.com/algochemy/TIL/assets/152131529/d0bbc75a-ba98-4061-aad4-1546e06c65a0" width="300" height="150">  
      - 또는 didChangeDependencies() 에서 viewModel 접근가능 ( 단, 매번 실행하는 코드는 여기에 두면 안 됨 )

---

### 상태 모으기

- 정리
  - 화면 하나에 하나의 UI 상태 홀더를 가지도록 한다
  - 일반적으로 ViewModel 에서 처리한다
  - 상태 홀더가 반드시 필요한 것은 아니다. 간단한 UI 는 간단히 처리하자
  - ViewModel은 전체 화면에서만 사용해야 한다
  - ViewModel의 인스턴스를 하위 UI 요소에 전파하지 않는다
    - 이렇게 되면 UI 재사용성도 떨어지고
    - 테스트 불가
    - 디버깅도 어렵다
 
- [상태 홀더 클래스](https://developer.android.com/topic/architecture/ui-layer/stateholders?hl=ko#state-holders)
  - **상태 홀더 클래스의 책임**
    - 상태 홀더의 책임은 앱이 읽을 수 있도록 상태를 저장하는 것입니다. 로직이 필요한 경우 상태 홀더는 중개자 역할을 하며 필요한 로직을 호스팅하는 데이터 소스에 대한 액세스 권한을 제공합니다. 이러한 방식으로 상태 홀더는 로직을 적절한 데이터 소스에 위임합니다.
  - 이점
    - 간단한 UI: UI가 상태를 바인딩합니다.
    - 유지관리: 상태 홀더에 정의된 로직을 UI 자체를 변경하지 않고도 반복할 수 있습니다.
    - 테스트 가능성: UI 및 상태 생성 로직을 독립적으로 테스트할 수 있습니다.
    - 가독성: 코드 리더가 UI 표시 코드와 UI 상태 생성 코드 간의 차이점을 명확하게 알아볼 수 있습니다.
  - 꼭 필요한지?
    - 상태 홀더가 반드시 필요한 것은 아닙니다. 간단한 UI는 표시 코드와 함께 로직을 인라인으로 호스팅할 수 있습니다.

  - [상태 홀더의 유형](https://developer.android.com/topic/architecture/ui-layer/stateholders?hl=ko#types-state)
    - **비즈니스 로직 상태 홀더**
      - 비즈니스 로직 상태 홀더는 사용자 이벤트를 처리하고 데이터 또는 도메인 레이어에서 화면 UI 상태로 데이터를 변환합니다.
      - 비즈니스 로직을 활용하는 상태 홀더에 다음 속성이 있어야 합니다.
        - UI 상태 생성
        - 활동 재생성을 통해 유지됨
        - 장기 지속 상태 보유
        - UI에 고유하며 재사용할 수 없음
      - 비즈니스 로직에 대한 액세스 권한을 제공하고 화면에 표시하기 위한 애플리케이션 데이터를 준비하는 데는 ViewModel이 적합합니다.
      
    - **UI 로직 상태 홀더**
      - UI 로직은 UI 자체에서 제공하는 데이터에 작동하는 로직입니다. 이는 UI 요소의 상태 또는 UI 데이터 소스(예: 권한 API나 Resources)에 있을 수 있습니다.
      - UI 로직을 활용하는 상태 홀더에는 일반적으로 다음 속성이 있습니다.
        - UI 상태 생성 및 UI 요소 상태 관리
        - Activity 재생성 시 유지되지 않음:
        - UI 범위 데이터 소스 참조가 있음
        - 여러 UI에서 재사용 가능
      - 일반적으로 UI 로직 상태 홀더는 일반 클래스로 구현됩니다. 이는 UI 자체가 UI 로직 상태 홀더 생성을 담당하고 UI 로직 상태 홀더의 수명 주기가 UI 자체의 수명 주기와 동일하기 때문입니다.
   
  - [구현 방법 : ViewModel 또는 일반 클래스 중에서 선택](https://developer.android.com/topic/architecture/ui-layer/stateholders?hl=ko#choose-viewmodel)
    - ViewModel과 일반 클래스 상태 홀더 중 하나를 선택하는 일은 UI 상태에 적용되는 로직과 로직이 작동하는 데이터 소스에 따라 결정됩니다.  
      <img src="https://github.com/algochemy/TIL/assets/152131529/b79a8c7e-d36c-4ba9-8792-43af8f8197b3" width="300" height="350">  
    - 비즈니스 로직에 액세스해야 하며 화면이 이동될 수 있는 한 UI 상태를 유지해야 하는 경우 비즈니스 로직 상태 홀더 구현에 ViewModel을 사용하는 것이 좋습니다.
    - 단기 지속 UI 상태 및 UI 로직의 경우 수명 주기가 UI에만 종속되는 일반 클래스로 충분합니다.

  
