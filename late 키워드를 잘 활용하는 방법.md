# late 키워드를 잘 활용하는 방법
## 1. 기본사용법 & 의도
```dart
class Coffee {
  String _temperature;

  void heat() { _temperature = 'hot'; }
  void chill() { _temperature = 'iced'; }
}

main() {
  var coffee = Coffee();
  coffee.heat();
  coffee.serve();
}

// 
```
- 당연하게도 에러가난다. why? 초기화가 안되었으니까여
- 이 때, 일반적으로 찾는 방법은 nullable로 설정해버리는거다.(실제로 에러가 안난다.)

```dart
String? _temperature;
```

- 근데 이 코드를 인수인계 할 때, 다른 관리자에게 넘겼을 때는 어떻게 생각할까?
- "아, temperature라는 변수는 없어도 되는거니 담당자가 nullable로 설정했구나!" 라고 판단하고 그냥 null을 할당해버릴지도
- 그리고 나서 temperature 변수로 인해 발생한 콘솔의 에러를 읽어보고 왜 코드를 이따위로 짰나 욕을하겠지요
- Nullable로 충분히 처리 할 수 있음에도 late라는 키워드를 dart에서 만들어 낸 의도는 '이 late로 선언한 변수는 nullable처럼 초기값이 주어지지는 않지만, 런타임하는 시점에는 반드시 초기화되어야함.' 이라는 설명을 협업자에게 명확하게 전달하려고 이 기능을 만든거같아여

## 2. 지연 초기화
```dart
class Weather {
  late int _temperature = _readThermometer();
}
```
- 런타임에 초기화 표현식의 비용이 많이 들고 필요하지 않을 때 유용함.
- UI작업 or 레이아웃 등 큰 비용이 드는 객체를 지연생성하면 유용할듯.
- 최초 액세스 할 경우에 지연생성됨.

## 3. late final 
```dart
class Coffee {
  late final String _temperature;

  void heat() { _temperature = 'hot'; }
  void chill() { _temperature = 'iced'; }
}

main() {
  var coffee = Coffee();
  coffee.heat(); // 여기서 temperature에 값 할당
  coffee.chill(); // 이 시점에서 에러가 난다: 최초1회만 값 할당 가능
}
```
- 런타임시점에 지연생성한다는 메커니즘은 동일함. 
- 근데 값을 1번 지정해두면 변경불가능함.
- late는 final을 같이쓰면 휴먼에러를 많이 줄일 수 있어보인다.
