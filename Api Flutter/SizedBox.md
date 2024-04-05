# SizedBox (class)
[공식문서](https://api.flutter.dev/flutter/widgets/SizedBox-class.html)

구체적인 크기가 지정된 box

SizedBox는 자식 위젯이 있을 경우, 자식이 특정한 width/height를 가지도록 강제한다. 하지만, 이 위젯의 부모 위젯이 이를 허용하지 않는 경우, SizedBox의 크기 강제는 무시된다.   
=> SizedBox가 Screen(자식 위젯의 크기를 화면과 같도록 강제)이거나, 또 다른 SizedBox인 경우

해결 방법으로, 자식 SizedBox를 부모의 크기 안에서 자유롭게 크기를 가질 수 있는 위젯([Center](/Api%20Flutter/Center.md), Align)으로 wrapping하면 된다.

만약 width/height가 null이라면, SizedBox는 자식의 해당 축의 크기에 맞춰진다. 만약 부모의 크기에 따라 크기가 결정되는 자식 위젯이라면, 반드시 SizedBox의 width와 height를 지정해주어야 한다.

만약 자식이 없다면, SizedBox는 부모로 부터 주어진 constraint에 최대한 근접한 width와 height를 가지게 된다. 만약 height나 width가 null이거나 지정되지 않았다면, 0으로 취급된다.

SizedBox.expand 생성자는 부모의 크기와 동일한 SizedBox를 생성해준다. 이는 width와 height를 double.infity로 지정한 것과 동일하다.

### Inheritance
Object > DiagnosticableTree > Widget > RenderObjectWidget > SingleChildRenderObjectWidget > SizedBox

