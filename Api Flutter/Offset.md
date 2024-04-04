# Offset (class)
[공식문서](https://api.flutter.dev/flutter/dart-ui/Offset-class.html)  

2D, 실수 좌표를 가지는 불변 변위차이다.

> 변위차(offset): 주어진 요소나, 지점까지의 차이

일반적으로 offset은 2가지로 해석(사용)된다.

1. 데카르트 좌표계에서 별도로 주어진 원점으로부터 특정 거리만큼 떨어진 좌표를 나타낸다.
2. 좌표계에 적용될 수 있는 벡터를 나타낸다. 예를 들어 RenderObject를 paint하는 경우, 부모는 화면의 원점으로 부터 넘겨받은 offset을 넘겨받아 자식들의 Offset을 결정함으로써 자식들도 화면의 원점에 대한 Offset을 갖도록 한다.  

하나의 offset은 위의 두가지 해석으로 모두 사용될 수 있다.

### Inheritance

Object OffsetBase Offset