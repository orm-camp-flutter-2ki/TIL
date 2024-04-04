## Flutter Ui Basic

### StatelessWidget & StatefulWidget

+ StatelessWidget
  + 상태가 없는 위젯. 한 번 생성되면 그 상태를 변경할 수 없음.
  + UI도 빌드되면 변경될 수 없음.
+ StatefulWidget
  + 상태가 있는 위젯. 상태를 관리하는 State 객체와 함께 사용된다.
  + 상태를 변경할 수 있으며, 변경된 상태에 따라 UI를 업데이트할 수 있다.
  + onPress나 onChange등 각종 이벤트에 유연하게 대처한다
 
### Scaffold & Container

+ Scaffold
  + 앱의 기본적인 레이아웃 구조를 정의하고, 여러 구성 요소를 통합하여 관리한다. 주로 전체적인 화면 구조를 정의하는 데 사용된다.
  + 다양한 구성 요소를 포함하고, 이들을 조직화하여 관리한다.
  + 예를들어 AppBar, NavigationBar와 같은 위젯을 포함할 수 있다.
+ Container
  + 단일 자식 위젯의 레이아웃, 위치 밑 스타일을 지정하는데 사용된다.
  + UI 요소의 모양, 크기, 배경색, 패딩 등을 설정하고 구성할 때 사용된다.
  + 단일 자식 위젯만 포함할 수 있으며, 이 자식 위젯의 레이아웃 및 스타일을 조정한다.
  + Scaffold 에 비해 상대적으로 단순한 UI 요소를 구성하는데 사용된다.
+ 요약
  + Scaffold는 앱의 전체적인 구조를 정의하고 관리하는 데 반면 Container는 단일 자식 위젯의 스타일링 및 레이아웃을 조정하는 데 사용된다.

### Row & Column

+ Row : 가로방향. Horizontal
+ Column : 세로방향. Vertical

### Stack

+ 위젯을 겹쳐 배치하고 싶을 때 사용한다.
+ 겹치는 순서는 위에서부터 아래순으로 위에있는 위젯이 가장 밑에 위치한다. 즉, 아래에 있을수록 상단에 존재하여 다른 위젯과 겹쳐 보이게 된다.

```dart
Stack(
  children: [
    Icon(
      Icons.notifications,
      color: Colors.white,
    ),
    Positioned(
      top: 0,
      right: 0,
      child: Container(
        padding: EdgeInsets.all(2),
        decoration: BoxDecoration(
          shape: BoxShape.circle,
          color: Colors.red,
        ),
        child: Text(
          '+9',
          style: TextStyle(
            color: Colors.white,
            fontSize: 10,
          ),
        ),
      ),
    ),
  ],
),
```
+ Positioned로 겹칠 위젯의 좌표를 찍어 위치시킨다.

### SizedBox

+ 자식 위젯의 크기를 지정할 때 사용된다.
+ 단순히 위젯끼리의 거리를 넓힐 때도 사용되지만, 이런식으로 사용되는것이 바람직한지 아직 긴가민가하다.

```dart
// 자식 위젯을 구성하며 크기와 구성 요소를 설정한다.
Widget _video() { 
  return SizedBox(
    width: double.infinity,
    height: 700,
    child: ListView(
      scrollDirection: Axis.vertical,
      children: videos.map((e) => ThumbnailCardWidget(video: e)).toList(),
    ),
  );
} 
```

### NavigationBar

+ 화면 하단에 위치한 네비게이션바 이며 사용자에게 메뉴를 편리하게 선택할 수 있게한다.
+ 일반 BottomNavigationBar보다 최신버전이며, 디자인적으로 더 많은 이점이 있다.

### Icon, Image

+ Icon 넣는법
```dart
Icon(
  Icons.search,
  color: Colors.white,
),
ImageIcon(
  AssetImage("assets/add.png"),
  color: Colors.white,
),
```
+ Image 넣는법
```dart
Image.network(
  video.profileUrl,
  width: double.infinity,
  height: 300,
),
Image.asset(
  "assets/compass.png",
  width: 25,
  height: 25,
  color: Colors.white,
),
```

### Expanded & Align

+ Expanded
  + 화면에서 여백을 최대한 활용하고, 자식 위젯이 화면의 가능한 많은 공간을 차지하도록 한다.
  + 부모 위젯이나 다른 자식 위젯이 가진 여분의 공간을 확장한다.
  + 남은 공간을 모조리 채운다는 개념이다
+ Align
  + 자식 위젯을 특정 위치에 정렬한다
  + alignment 속성을 사용하여 방향을 선택해서 정렬할 수 있다.
