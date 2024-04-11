# LayoutBuilder (class)
[공식 문서](https://api.flutter.dev/flutter/widgets/LayoutBuilder-class.html)

부모 위젯의 크기에 따라 다른 위젯 tree를 생성하게 해주는 class

프레임워크가 배치(layout) 시점에 builder 함수를 호출하고 부모 위젯의 constraint를 제공하는 것을 제외하면, Builder 위젯과 유사하다.  
> builder: layout 시점에 호출되어 위젯 tree를 생성하는 함수  
> `final Widget Function(BuildContext context, ConstraintType constraints) builder;`  

부모 위젯이 자식 위젯의 크기를 제한하고 자식의 자체크기(intrinsic size)를 고려하지 않아도 되는 상황에서 유용하다.

LayoutBuilder의 최종 크기는 자식의 크기에 맞춰진다.

builder 함수는 다음과 같은 상황에서 호출된다.  
- 위젯이 매치되는 첫 시점
- 부모 위젯이 다른 constraint을 전달하였을 때
- 부모 위젯이 이 위젯을 update 하였을 때
- builder 함수가 구독하고 있던 의존성이 변경되었을 때

부모 위젯이 같은 constraint를 반복해서 전달하는 경우, builder 함수는 layout 과정에서 호출되지 않는다.

만약 자식 위젯이 부모보다 작아야 하는 경우, 자식을 Align 위젯으로 감싸는 것을 고려해볼만 한다. 만약 자식 위젯이 더 큰 크기를 원하는 경우에는, SingleChildScrollView나 OverflowBox로 감싸는 것을 고려하라.

다음 예제는 가능한 width에 따라 다른 위젯을 build하는 LayoutBuilder을 보여준다.  
[예제 코드](https://api.flutter.dev/flutter/widgets/LayoutBuilder-class.html#widgets.LayoutBuilder.1)

### Inheritance
Object > DiagnosticableTree > Widget > RenderObjectWidget > ConstrainedLayoutBuilder\<BoxConstraints\> > LayoutBuilder