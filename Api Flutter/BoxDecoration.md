# BoxDecoration (class)
[공식문서](https://api.flutter.dev/flutter/painting/BoxDecoration-class.html)

box를 어떻게 paint할지를 나타내는 불변 객체.

BoxDecoration 클래스는 box를 그릴 수 있는 다양한 방법을 제공한다.

box는 border(테두리)와 body를 가지고 boxShadow(그림자)를 지정해줄 수도 있다.

box의 모양은 원이나 사각형이 될수있다. 만약 사각형이라면, borderRadius 프로퍼티를 통해 모서리의 둥근 정도를 조절할 수 있다.

box의 body는 layer에 paint된다. 
> layer: 계층 구조를 의미. 
> => 여러 layer가 쌓여서 하나의 box로 보여지게 됨  

가장 아래의 layer는 box를 채우는 color이다. 그 다음 layer는 box를 채우는 gradient이다.
> gradient 프로퍼티가 지정되면, color는 무시된다.

마지막으로, DecorationImage 클래스에 의해 정렬되는 image가 표시된다. 

border는 body위에 그려지고, boxShadow는 기본적으로 아래(box외부)에 그려진다.

```dart
Container(
  decoration: BoxDecoration(
    color: const Color(0xff7c94b6),
    image: const DecorationImage(
      image: NetworkImage('https://flutter.github.io/assets-for-api-docs/assets/widgets/owl-2.jpg'),
      fit: BoxFit.cover,
    ),
    border: Border.all(
      width: 8, // 값이 커질수록 테두리가 box 내부쪽으로 넓어짐
    ),
    borderRadius: BorderRadius.circular(12),
  ),
)
```

shape와 borderRadius는 꾸며지는 Container의 자식 위젯에게는 적용되지 않는다.  
(ClipRect, ClipRRect, ClipPath와 같은 clip 위젯을 자식 위젯으로 사용할 것) 

### Inheritance
Object > Decoration > BoxDecoration