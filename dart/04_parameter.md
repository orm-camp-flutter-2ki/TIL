# Parameter, 매개 변수
Dart에서의 메소드나 생성자에선 여러 종류의 Parameter를 만날 수 있습니다.
```dart
String setValue(String parameter) {...}
setValue('값');
// 첫 번째 줄의 parameter는 매개 변수(Parameter)에 해당되고
// 두 번째 줄의 '값'은 인자(Argument)에 해당됩니다.
```
Parameter에는 어떤 종류가 있고, 어떻게 사용하는 지에 대해 알아보겠습니다.

_Nullable에 관한 내용이 있으니 Null-safety에 관해 이해하고 보시는 것이 좋습니다.
-> https://velog.io/@chojja7188/Dart-Null-safety_

### Required Positional Parameter
> 정해진 위치가 있는 Parameter

일반적으로 기본적인 코드에서 흔하게 볼 수 있는 방식입니다.
,(콤마)를 기준으로 매개 변수 순서대로 인자값이 전달됩니다.
```dart
class Person {
  String name;
  int age;
  String? hobby;
  
  Person(this.name, this.age, this.hobby);
}

void main() {
  Person person = Person('홍길동', 24, '코딩');
}
// 순서대로 name에는 '홍길동', age에는 24, hobby에는 '코딩'을 전달
```
기본적으로 모든 매개 변수가 들어가야 합니다.

### Named Parameter
> 이름에 맞게 값을 넣는 Parameter

정해진 이름에 따라 값을 넣을 수 있는 방식입니다.
[Nullable 타입](https://velog.io/@chojja7188/Dart-Null-safety#nullable-type--question-mark)이 아닐 경우에는 앞에 required를 붙여야 합니다.
앞에 required가 있으면 매개 변수에 인자를 반드시 전달해야 합니다.
```dart
class Person {
  String name;
  int age;
  String? hobby;
  
  Person({
    required this.name, required this.age, this.hobby
  });
}

void main() {
  Person person = Person(name: '홍길동', age: 24, hobby: '코딩');
  Person person2 = Person(name: '박세훈', age: 24);
  // hobby는 required가 없는 Nullable 타입이기에 인자값을 주지 않을 수 있음
}
```
Positioned Parameter와 혼용하여 쓸 수도 있습니다.
단 그 경우 Positioned Parameter가 앞에 와야 합니다.
```dart
class Person {
  String name;
  int age;
  String? hobby;
  
  Person(this.name, {required this.age, this.hobby});
}

void main() {
  Person person = Person('홍길동', age: 24, hobby: '코딩');
  Person person2 = Person('박세훈', age: 20);
}
```
추가로 Named Parameter는 순서에 상관없이 해당되는 이름에 맞게 값을 넣으면 되지만
순서대로 넣는 것이 가독성에 좋다고 볼 수 있겠습니다.

### Optional Positional Parameter
> 있어도 되고 없어도 되는 Parameter

[] 대괄호를 사용하는 Parameter로, 값을 넣지 않아도 정상적으로 동작합니다.
또한 기본값으로 초기화할 수도 있습니다.
Nullable 타입이 아닌 필드들은 기본값 초기화가 필수적입니다.
```dart
class Person {
  String name;
  int age;
  String? hobby;

  Person(this.name, [this.age = 30, this.hobby]);
}

void main() {
  Person person = Person('홍길동', 24, '코딩');
  Person person2 = Person('박세훈'); // name에 박세훈, age에 30, hobby에 null
}
```

### 정리
- 여러 종류의 파라미터를 적재적소에 활용할 수 있다.
- Required Positional : 간단한 코드에 용이
- Named : 가독성과 확장성에 용이
- Optional Positional : 옵션을 만들 때 용이

자료 : https://dart.dev/language/functions#parameters
