# enum, 열거형

enum은 enumerated type의 줄임말로
서로 관련된 상수를 묶은 자료형입니다.
사용법은 아래와 같습니다.
```dart
enum Element {
  fire,
  water,
  wind,
  earth
}
```
Element라는 enum에 네 가지 상수가 포함되었습니다.

이는 switch문에서 유용하게 사용할 수 있습니다.

```dart

switch(value) { // 임의의 원소값이 있는 value 변수
  case Element.fire:
    print('Fire!');
  case Element.water:
    print('Water!');
  case Element.wind:
    print('Wind!');
  case Element.earth:
    print('Earth!');
}
```

**왜 사용하는가?**
enum을 이용하면 개발자의 오타나 실수를 미연에 방지할 수 있습니다.
```dart
switch(value) { // String으로 원소의 값을 담음
  case 'fire':
    print('Fire!');
  case 'water':
    print('Water!');
  case 'wind':
    print('Wind!');
  case 'aerth': // 오타가 나도 컴파일 에러가 나지 않음.
    print('Earth!');
}
```
위와 같은 경우에 개발자는 오타를 인지하지 못하고 지나칠 수 있습니다.
따라서 확실하게 타입을 정해주는 enum을 활용하면
더 안전하게 분기 처리를 할 수 있습니다.

자료 : https://dart.dev/language/enums
