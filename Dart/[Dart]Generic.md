> 타입이 없을때의 문제점
1)런타임 에러가 나기 쉽다.
2)IDE가 컴파일 에러를 미리 찾을 수 없다.



> 🙋🏻 Generic?<br>
`타입 안전성(type safety)`을 제공하기 위한 강력한 기능입니다. <br>
타입을 나중에 원하는 형태로 정의할 수 있어, `재사용성`과 `유연성`을 높일 수 있습니다.<br>

> ex)<br>
```dart
class Box<T> {
  T value;
  Box(this.value);
}
void main() {
  // 정수형 데이터를 담는 상자
  var intBox = Box<int>(10);
  print('정수 상자의 값: ${intBox.value}');
  // 문자열 데이터를 담는 상자
  var stringBox = Box<String>('Hello, Dart!');
  print('문자열 상자의 값: ${stringBox.value}');
}
```
 Box 클래스는 제네릭 클래스로 정의<br>
 Box 클래스는 단일 필드 value를 가지고 있으며, <br>
 이 필드의 유형은 T(type)로 정의됩니다.<br>
 따라서 Box 클래스의 인스턴스를 만들 때, 그 인스턴스가 담을 데이터의 유형을 지정할 수 있습니다.<br>
main() 함수에서는 `intBox`와 `stringBox`라는 두 개의 Box 인스턴스를 만듭니다.<br>
첫 번째 상자는 정수형 데이터를, 두 번째 상자는 문자열 데이터를 담고 있습니다.<br>

> **⭐️ tip**<br>
타입 매개변수는 보통 T(type), E(element), K(key), V(vlaue)와 같은 알파벳으로 표현됩니다<br>
선생님이 M,E이랑 같이 사용하셧을때에는 message,error였다고함<br>
사용자에 따라 달라지니 유의!<br>
