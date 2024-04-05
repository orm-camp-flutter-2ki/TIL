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








