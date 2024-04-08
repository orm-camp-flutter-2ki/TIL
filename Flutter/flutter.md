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

### MVMM 패턴 
- Repository에 비즈니스 논리가 포함되지 않게 분리하자
- 비지니스 로직을 담당하는 부분을 ViewModel 클래스로 따로 빼 둔다.
- 화면 보여줘야하는 것은 getter로 제공
- ViewModel 하나 더 들어온거밖에 없는데 기능 추가가 쉽다
- 일반적으로 화면 하나 당 하나의 뷰모델을 유지하는 것이 좋다
- 요구사항(수정사항)이 업데이트됐을 때 변경이 용이하다 !
- Repository는 데이터 주고받는것에만 집중하게 한다.
- MVMM 패턴은 모바일 앱에 가장 적합한 아키텍처 : 확장성과 유지보수의 편의성을 고려
  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6be06ad5-191c-4cca-8efa-4c4c060bc652/59a7d992-6aa3-4482-9e18-1722c0a456a6/Untitled.png)
- ChangeNotifier로 View에 알림, 데이터바인딩 기능 구현 가능
  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/6be06ad5-191c-4cca-8efa-4c4c060bc652/59a7d992-6aa3-4482-9e18-1722c0a456a6/Untitled.png)
  - View Layer는 ViewModel Layer는 알 되 Data Layer를 알면 안됨 (계속 캡슐화.)
