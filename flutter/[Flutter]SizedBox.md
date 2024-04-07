>[**공식문서**](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)


> If given a child, this widget forces it to have a specific width and/or height.
  - 자식이 주어지면 이 위젯은 특정 너비 및/또는 높이를 갖도록 강제합니다.

> These values will be ignored if this widget's parent  does not permit them
  - 이 위젯의 부모가 이를 허용하지 않으면 이 값은 무시됩니다.
  
>For example, this happens if the parent is the screen (forces the child to be the same size as the parent), or another SizedBox (forces its child to have a specific width and/or height).
  - 예를 들어, 부모가 화면(자식을 부모와 동일한 크기로 강제)이거나 다른 SizedBox (자식을 특정 너비 및/또는 높이를 갖도록 강제)인 경우 이런 일이 발생합니다. 
  
>This can be remedied by wrapping the child SizedBox in a widget that does permit it to be any size up to the size of the parent, such as Center or Align.
  - 이 문제는 Center 또는 Align 과 같이  부모크기까지 크리를 허용하는 SizeBox에 래핑하면 해결 할 수 있다
  
>If not given a child, SizedBox will try to size itself as close to the specified height and width as possible given the parent's constraints. If height or width is null or unspecified, it will be treated as zero.
  - 자식이 주어지지 않으면 SizedBox는 부모의 제약 조건에 따라 지정된 높이와 너비에 최대한 가깝게 크기를 조정하려고 시도합니다. 높이 또는 너비가 null이거나 지정되지 않은 경우 0으로 처리됩니다.
  
>The SizedBox.expand constructor can be used to make a SizedBox that sizes itself to fit the parent. It is equivalent to setting width and height to double.infinity.
  - SizedBox.expand 생성자를 사용하면 부모에 맞게 크기가 조정되는 SizedBox를 만들 수 있습니다. width ,height를 double.infinity로 설정하는 것과 같습니다.

### See also:


> ConstrainedBox, a more generic version of this class that takes arbitrary BoxConstraints instead of an explicit width and height.
  -  **ConstrainedBox** - 명시적인(표면적? 값을 지정한) 너비와 높이 대신 임의의 BoxConstraints를 사용하는 이 클래스의 보다 일반적인 버전인 ConstrainedBox입니다.
  
> UnconstrainedBox, a container that tries to let its child draw without constraints
  - **UnconstrainedBox** - 자식이 제약 없이 그리도록 하는 컨테이너
  
> FractionallySizedBox, a widget that sizes its child to a fraction of the total available space. 
  - **FractionallySizedBox** - 사용 가능한 전체 공간의 일부로 자식 크기를 조정하는 위젯
  
 > AspectRatio, a widget that attempts to fit within the parent's constraints while also sizing its child to match a given aspect ratio.
   - **AspectRatio** 는 부모의 제약 조건에 맞추는 동시에 주어진 가로세로 비율과 일치하도록 자식의 크기를 조정하는 위젯입니다.
  
> FittedBox, which sizes and positions its child widget to fit the parent according to a given BoxFit discipline.
  - **FittedBox** - 주어진 BoxFit 규율에 따라 부모 위젯에 맞게 자식 위젯의 크기와 위치를 조정하는 위젯
  
 ###  👉  [Container](https://velog.io/@hee462/fultterContainer-class)
