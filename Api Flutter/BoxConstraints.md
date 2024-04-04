# BoxPainter (class)
[공식문서](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html) 

RenderBox layout을 위한 불변 layout constratins(제약)

Size는 아래의 관계가 성립할 때만, BoxConstraints를 따른다.  
- minWidth <= Size.width <= maxWidth  
- minHeight <= Size.height <= maxHeight
 
constraint들 끼리는 아래의 관계를 꼭 만족해야 한다.  
- 0.0 <= minWidth <= maxWidth <= double.infinity  
- 0.0 <= minHeight <= maxHeight <= double.infinity  

double.infinity는 각(min, max) constraint에서 유효한 값이다.

### The Box layout 모델
Flutter에서 Render 객체는 한번만(one-pass) 순회하는 layout 모델에 배치된다. layout 모델은 render tree를 하향식으로 순회하며 constraint를 전달하고, 다시 거슬러오면서 실제 배치정보(geometry)를 render tree에게 전달한다.

box의 경우 최소/최대 넓이/높이, 4개의 숫자로 이루어진 BoxConstraints를 constraint로 가진다.

box의 배치 정보는 상위 위젯에서 정의된 constraint를 반드시 만족해야 하는 Size로 구성되어 있다.

...