# BoxPainter (class)
[공식문서](https://api.flutter.dev/flutter/rendering/BoxConstraints-class.html) 

RenderBox layout을 위한 불변 layout constratins(제약)

Size는 아래의 관계가 성립할 때만, BoxConstraints를 따른다.  
- minWidth <= Size.width <= maxWidth  
- minHeight <= Size.height <= maxHeight
 
constraint는 아래의 관계를 꼭 만족해야 한다.  
- 0.0 <= minWidth <= maxWidth <= double.infinity  
- 0.0 <= minHeight <= maxHeight <= double.infinity  

double.infinity는 각(min, max) constraint에서 유효한 값이다.

### Box layout 모델
Flutter에서 Render 객체는 한번만(one-pass) 순회하는 layout 모델에 의해 배치된다. layout 모델은 render tree를 하향식으로 순회하며 constraint를 전달하고, 다시 거슬러오면서 실제 배치정보(geometry)를 render tree에게 전달한다.

box의 경우 최소/최대 넓이/높이, 4개의 숫자로 이루어진 BoxConstraints를 constraint로 가진다.

box의 배치 정보는 위에서 설명한 constraint 규칙을 반드시 만족해야 하는 Size로 구성되어 있다.

각각의 RenderBox(box 위젯으로부터 layout 모델을 제공받는 객체)는 부모로부터 BoxConstraints를 받는다. 이 후, 각 자식들을 배치하고 BoxConstraints를 만족하는 크기를 결정한다.

Render 객체는 자식을 배치하는 것과 별개로 위치를 지정한다. 주로 부모는 자식의 크기를 사용하여, 자식의 위치를 결정한다. 자식은 자신의 위치를 알지 못하고, 위치가 변경되더라도 다시 배치되거나 다시 그려질 필요가 없다.

### Terminology(용어)

동일한 축에 대해 최소 constraint와 최대 constraint가 같은 경우 **tight** constrained이라고 한다.  
=> 관련: BoxConstraints.tightFor, BoxConstraints.tightForFinite, tighten, hasTightWidth, hasTightHeight, isTight.

최소 constraint가 0.0인 축은 **loose**라고 한다(최대 constraint와 무관하게).  
최대 constraint도 0.0인 경우, 해당 축은 tight이면서 동시에 loose이다.
=> 관련: BoxConstraints.loose, loosen.

최대 constraint가 무한이 아닌 축은 **bounded**라고 한다.
=> 관련: hasBoundedWidth, hasBoundedHeight.

최대 constraint가 무한인 축은 **unbounded**라고 한다.
최소와 최대 constraint가 모두 무한인 축은 tight이면서 **expand**이다.
=> 관련: BoxConstraints.expand.

최소 constraint가 무한인 축은 단순히 **infinite**라고 한다(당연히 최대 constraint도 무한).
=> 관련: hasInfiniteWidth, hasInfiniteHeight.

크기가 BoxConstraints를 만족하는 경우, constrained되었다고 한다.
=> 관련: constrain, constrainWidth, constrainHeight, constrainDimensions, constrainSizeAndAttemptToPreserveAspectRatio, isSatisfiedBy.


### Inheritance
Object > Constraints > BoxConstraints
