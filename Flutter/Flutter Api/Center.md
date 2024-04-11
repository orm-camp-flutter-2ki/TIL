# Center (class)
[공식문서](https://api.flutter.dev/flutter/widgets/Center-class.html)

자식 위젯을 자신 내부의 중앙에 배치하는 위젯

### Center의 크기

크기에 대한 constraint(제약)이 있고, widthFactor/heightFactor 값이 null이라면 가능한 최대의 크기를 갖게 된다. 

크기에 대한 constraint(제약)이 없고, widthFactor/heightFactor 값이 null이라면 자식의 크기에 맞춰 진다.

widthFactor/heightFactor 값이 null이 아니라면, 자식의 크기에 대해 (factor 값 만큼)비례한 크기를 갖게 된다.  
=> widthFactor: 2.0 인 경우, 자식 width의 2배의 width를 갖는다.

### Inheritance
Object > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > Align > Center