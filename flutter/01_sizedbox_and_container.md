# SizedBox and Container

두 위젯 다 width와 height를 가지면서 어떠한 위젯의 크기를 지정해 주는 용도로 자주 쓰입니다.
그러나 두 위젯은 상황에 맞게 써야 하며, 두 위젯의 차이를 알아보겠습니다.

### SizedBox
SizedBox 위젯은 key와 child를 제외하고 width와 height 속성만 가지고 있습니다.
정말로 크기만 지정해주는 용도로 사용하는 위젯이며, 주로 고정된 크기를 설정해주는 용도로 사용합니다.
width와 height 중 하나라도 설정하지 않는다면 child에 맞게 크기가 설정됩니다.
```dart
SizedBox(
  child: Container(
  color: Colors.yellow
    child: Text('Hello World!')
  )
)
```

<img src="https://velog.velcdn.com/images/chojja7188/post/a799e066-2702-4c41-90c0-4fc9fd17d559/image.png" width="200">

### Container
Container 위젯은 width와 height 말고도 padding, color, decoration, transform 등 다양한 속성을 지니고 있습니다.
크기를 지정해줄 뿐만 아니라 다양한 부가적인 속성을 추가로 지정해줄 수 있습니다.
width와 height를 설정하지 않는다면 최대 크기로 설정됩니다.
```dart
Container(
  color: Colors.yellow,
  child: Center(
    child: Text('Hello World!')
  )
)
```
<img src="https://velog.velcdn.com/images/chojja7188/post/fc14bad5-cc9d-4ea1-b965-22a8a52ce26c/image.png" width="200">


### 차이
width와 height를 설정하지 않는다면 SizedBox는 최소 크기, Container는 최대 크기가 됩니다.
SizedBox는 주로 간격을 주거나 간단한 고정된 크기 설정 용도로 사용되며,
Container는 크기 설정 외에도 기타 부가적인 옵션을 더하기 위해 사용됩니다.

Container를 사용할 때 width와 height만 설정하면 SizedBox를 사용하라고 Lint가 나타납니다.
그 이유는 SizedBox는 const가 가능하기 때문에 메모리를 절약할 수 있습니다.
따라서 크기만 설정하는 경우에는 SizedBox를 우선적으로 사용해야겠습니다.
