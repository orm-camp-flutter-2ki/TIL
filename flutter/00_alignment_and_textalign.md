# Align 위젯의 alignment 속성과, Text 위젯의 textAlign 속성

Flutter에서 위젯을 왼쪽/오른쪽 등으로 정렬 및 배치하는 방법으로 여러 가지가 있는데 그 중 Align 위젯의 alignment 속성과 Text 위젯의 textAlign 속성의 차이가 조금 헷갈려서 정리합니다.
Column을 사용한다면 유의해야 합니다.

### Align의 alignment 속성
Align 위젯은 부모 위젯에 맞춰서 자식 위젯을 배치합니다.
따라서 넓은 범위를 가지고 있고 그 범위 내에서 배치합니다.
alignment 속성을 이용해서 배치할 수 있습니다.
topRight, centerRight, bottomRight 등을 줄 수 있으며
Align 영역이 여유 높이가 있으면 top, center, bottom에 맞춰 배치할 수 있습니다.
```dart
Column(children: [
  Align(alignment: Alignment.center, child: Text('Center')),
  Align(alignment: Alignment.bottomRight, child: Text('Right'))
])
```
![](https://velog.velcdn.com/images/chojja7188/post/2af1284b-93a8-4bb5-ad50-157f34debac7/image.png)
보시다시피 Align은 이렇게 넓은 범위의 영역을 가지고 있습니다.
이 영역 내에서 왼쪽, 오른쪽 정렬이 됩니다.
Text 위젯을 가운데 정렬, 오른쪽 정렬을 하고 있습니다.

### Text의 textAlign 속성
Text 위젯에서도 정렬과 관련된 속성이 존재합니다.
textAlign 속성을 이용할 수 있으며 left, right, center, start, end 등을 줄 수 있습니다. 그러나 여기서 textAlign을 Align 위젯처럼 사용하려다 헷갈려하는 부분이 있습니다.
```dart
Column(children: [
  Text('Center', textAlign: TextAlign.center),
  Text('Right', textAlign: TextAlign.right)
])
```
![](https://velog.velcdn.com/images/chojja7188/post/d22f555b-c855-460b-a5a0-31772798b636/image.png)
이런 식으로 사용하면 기대와 달리 TextAlign.right을 지정해도 오른쪽 정렬이 되지 않습니다.
textAlign은 Text 위젯 내에서 정렬을 시켜주는 속성입니다.
따라서 Text 위젯의 영역이 그림처럼 글자에 맞춰져 있기 때문에 정렬이 되지 않는 것입니다.
Text 위젯의 영역의 너비가 크다면 정렬이 가능합니다.
```dart
Column(children: [
  SizedBox(width: 200, child: Text('Center', textAlign: TextAlign.center)),
  SizedBox(width: 200, child: Text('Right', textAlign: TextAlign.right))
])
```
![](https://velog.velcdn.com/images/chojja7188/post/58a9f812-25ef-46ba-ad36-8ec412f0c516/image.png)

이 경우에는 Text 위젯의 너비가 부모 위젯인 SizedBox 위젯에 맞춰집니다.
