# Container

A convenience widget that combines common painting, positioning, and sizing widgets.
> 일반적인 그리기, 위치 지정 및 크기 조정 위젯을 결합한 편리한 위젯이다.

A container first surrounds the child with padding (inflated by any borders present in the decoration) 
and then applies additional constraints to the padded extent (incorporating the width and height as constraints, if either is non-null).
The container is then surrounded by additional empty space described from the margin.
> 컨테이너는 먼저 패딩(decoration에 있는 테투리로 inflate된)으로 자식을 둘러쌉니다.
> 그런 다음 패딩된 범위에 추가 제약 조건을 적용한다.(둘 중 하나라도 null이 아닌 경우, 넓이와 높이를 제약 조건으로 통합)
> 그럼 그 컨데이너는 margin(여백)에서 설명한 추가 빈 공간으로 감싸진다.

During painting, the container first applies the given transform, 
then paints the decoration to fill the padded extent, then it paints the child, 
and finally paints the foregroundDecoration, also filling the padded extent.
> 그려지는 동안, 컨테이너는 먼저 지정된 transform(변환)을 적용한 다음, decoration을 칠하기 위해 패딩된 범위를 채운 다음, 자식을 칠하고
> 마지막으로 foregroundDecoration을 페인트하여 패딩된 범위도 채운다.

Containers with no children try to be as big as possible unless the incoming constraints are unbounded, in which case they try to be as small as possible. 
Containers with children size themselves to their children. The width, height, and constraints arguments to the constructor override this.
> 하위 위젯이 없는 컨테이너는 들어오는 제약들이 제한되지 않는 한 가능한 커지려고 하며, ***이 경우에는 가능한 한 작게하려고 한다.***
> 하위 위젯들을 가진 컨테이너는 하위 위젯에 맞게 크기가 조정된다. 생성자에 대한 넓이, 높이, 제약 사항들이 이것을 재정의(override)한다.

By default, containers return false for all hit tests. 
If the color property is specified, the hit testing is handled by ColoredBox, which always returns true. 
If the decoration or foregroundDecoration properties are specified, hit testing is handled by Decoration.hitTest.
> 기본적으로, 컨테이너는 모든 ***적중?*** 테스트에 대해 false를 반환한다.
> 컬러 속성이 지정되면, 테스트는 항상 true를 반환하는 ColoredBox에 의해 처리된다.
> decoration 또는 foregroundDecoration 속성이 지정된 경우는 적중 테스트는 Decoration.hitTest에 의해 처리된다.

<br></br>

# Layout behavior

See BoxConstraints for an introduction to box layout models.
> box layout 모델에 대한 소개는 BoxConstraint를 참조.

Since Container combines a number of other widgets each with their own layout behavior, Container's layout behavior is somewhat complicated.
> 컨테이너는 각 각 고유한 레이아웃 동작을 가진 여러 위젯들을 하나로 결합하므로, 컨데이너의 레이아웃 동작은 다소 복잡하다.

Summary: Container tries, in order: to honor alignment, to size itself to the child, to honor the width, height, and constraints, to expand to fit the parent, to be as small as possible.
> 요약: 컨테이너는 정렬을 따르고, 자식 자체의 사이즈에 맞추고, 넓이와 높이의 제약에 따르고, 부모에 맞게 확장하고, 가능한 작아지려고 한다.

More specifically:

If the widget has no child, no height, no width, no constraints, and the parent provides unbounded constraints, then Container tries to size as small as possible.
> 위젯에 하위가 없고, 높이, 넓이도, 제약 조건도 없다면, 부모가 무제한 제약들을 제공하는 경우 컨테이너는 가능한 한 작은 크기를 시도한다.

If the widget has no child and no alignment, but a height, width, or constraints are provided, then the Container tries to be as small as possible given the combination of those constraints and the parent's constraints.
> 위젯에 하위 및 정렬이 없지만, 높이, 넓이 또는 제약 조건이 제공되는 경우, 컨테이너는 해당 제약 조건과 상위 제약 조건의 조합을 고려하여 가능한 한 작게 만들어지려고 한다.

If the widget has no child, no height, no width, no constraints, and no alignment, but the parent provides bounded constraints, then Container expands to fit the constraints provided by the parent
> 만약 자식 위젯도, 높이, 넓이도, 제약 조건도 없는데 부모가 제한된 제약 조건을 제공한다면, 컨테이너는 부모에 의해 제공된 제약에 맞게 확장된다.

If the widget has an alignment, and the parent provides unbounded constraints, then the Container tries to size itself around the child.
> 위젯에 정렬이 있고 부모가 무제한 제약 조건을 제공하는 경우, 컨테이너는 자식을 기준으로 크기를 조정하려 한다.

If the widget has an alignment, and the parent provides bounded constraints, then the Container tries to expand to fit the parent, 
and then positions the child within itself as per the alignment.
> 위젯에 정렬이 있고 부모가 제한된 제약 조건을 제공하는 경우 컨테이너는 부모에 맞게 확장을 시도한 다음 정렬에 따라 자체 내에 자식을 배치 합니다.

Otherwise, the widget has a child but no height, no width, no constraints, and no alignment, and the Container passes the constraints from the parent to the child and sizes itself to match the child.
> 그렇지 않으면, 그 위젯은 자식은 있지만 넓이, 높이, 제약 조건, 정렬 모두 없다.
> 그리고 그 컨테이너는 부모에서 자식으로 제약 조건을 전달하고 크기 자체를 자식과 일치시킨다.

The margin and padding properties also affect the layout, as described in the documentation for those properties. (Their effects merely augment the rules described above.)
> 해당 속성들의 설명서에 설명된 대로 마진과 패딩 속성도 레이아웃에 영향을 미친다.(그 효과는 위에서 설명된 규칙을 확장할 뿐이다.)
The decoration can implicitly increase the padding (e.g. borders in a BoxDecoration contribute to the padding); see Decoration.padding.
> decoration은 암묵적으로 패딩을 증가시킬 수 있다.(예: BoxDecoration의 테두리는 패딩에 기여한다.


<img width="539" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d0e2e557-ccfb-4360-ac3e-17d3e479e111">

```dart
class SizedBox extends SingleChildRenderObjectWidget {}

class Container extends StatelessWidget {}
```
SingleChildRenderObjectWidget  
렌더링 객체의 특징을 조정: SingleChildRenderObjectWidget를 사용하면 자식 위젯을 감싸는 렌더링 객체의 특성을 조정할 수 있습니다. 이는 위젯의 모양, 크기, 위치 등을 설정하는 데 사용됩니다.
=> 화면에 그려지는 방식을 조정한다..?

