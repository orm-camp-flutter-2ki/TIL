# Generic, 제네릭

제네릭은 타입이 외부에서 지정되는 것이 아닌 사용자에 의해 지정되는 것을 말합니다.
그렇다면 dynamic이나 Object같이 광범위한 타입을 쓰면 되지 않느냐는 의문이 있을 수 있지만
위의 경우는 타입이 맞지 않아 런타임 에러가 날 수도 있는 위험한 타입입니다
따라서 제네릭을 사용하여 이러한 문제를 해결할 수 있습니다.
Dart에서는 제네릭을 어떻게 사용하는지 알아보겠습니다.

### <>
사실 생소한 개념이 아니라 이미 List를 선언할 때 사용 중인 <>가 제네릭입니다.

```dart
List<int> list = [1, 2, 3, 4, 5]
```
<> 안에 있는 int 타입에 맞는 값만 해당 리스트에 들어갈 수 있습니다.
클래스를 구성할 때에도 유용히 사용할 수 있습니다.
```dart
class Test<E>() {
  E? _data;
  
  void put(E data) {
    _data = data;
  }
  
  E? get() {
    return _data;
  }
}

void main() {
  Test<int> a = Test<int>();
  a.put(3);
  print(a.get()); // 3 출력
  
  final b = Test<String>(); // final로 자동으로 타입 지정.
  // b는 Test<String> 타입.
  b.put('test');
  print(b.get()); // test 출력
  b.put(3); // 컴파일 오류
}
```
이와 같이 인자값의 타입으로 안전하게 사용이 가능합니다.
또한 extends를 사용하여 이용 가능한 타입에 제약을 줄 수도 있습니다.
```dart
class Test<E extends Practice> {}
```
주로 제네릭에 들어가는 매개 변수는 통상적으로 아래와 같이 단일 문자로 사용합니다.
이는 관례로써, 당연하지만 이를 사용하지 않고 개발자 임의로 지정이 가능합니다.
- E : Element
- K, V : Key, Value
- R : Return
- T, S, U


자료 :
https://dart.dev/language/generics
https://dart.dev/effective-dart/design#do-follow-existing-mnemonic-conventions-when-naming-type-parameters
