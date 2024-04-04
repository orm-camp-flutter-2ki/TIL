# Decoration (absract)
[공식문서](https://api.flutter.dev/flutter/painting/Decoration-class.html) 

A description of a box decoration (a decoration applied to a [Rect](/Api%20Flutter/Rect.md)).
Box decoratin에 대한 설명 (decoration은 [Rect](/Api%20Flutter/Rect.md)에 적용된다)

모든 decorations에 대한 추상 인터페이스 클래스이다.  
(구체적인 예제(구현체)는 [BoxDecoration](/Api%20Flutter/BoxDecoration.md)을 참고)

실질적으로 Decoration을 paint하기 위해서는 createBoxPainter 메서드를 사용하여 BoxPainter를 얻어야한다. Decoration 객체는 box들에게 공유될 수 있다. BoxPainter 객체는 resource를 캐싱하여 특정 surface를 paint하는 것을 더 빠르게한다.

### Implementers
BoxDecoration > FlutterLogoDecoration > ShapeDecoration > UnderlineTabIndicator