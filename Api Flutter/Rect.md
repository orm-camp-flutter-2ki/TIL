# Rect (absract)
[공식문서](https://api.flutter.dev/flutter/dart-ui/Rect-class.html)  

2D, 축에 정렬된, 실수 값을 가지는 불변 사각형이다.  
각 꼭짓점의 좌표는 원점을 기준으로 결정된다.

Rect는 생성자나, [Offset](/Api%20Flutter/Offset.md)과 Size를 & 연산자로 연결하여 생성할 수 있다.

```dart
Rect myRect = const Offset(1.0, 2.0) & const Size(3.0, 4.0);
```

> Size(class): 2D, 실수 좌표의 크기를 가진다.   
> => 원점으로부터의 offset과 동일