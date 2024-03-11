# Getter & Setter
Getter와 Setter가 무엇이고 Dart에서는 어떤 형식으로 지원하는 지에 대해서 알아보겠습니다.

### 무엇인가?
**Getter**는 말 그대로 값을 받는 역할을 갖고 있고,
**Setter**는 말 그대로 값을 설정해주는 역할을 가지고 있습니다.
Setter로 값을 쓰고 Getter로 값을 읽는 식으로 사용합니다.

이에 Dart에서는 get과 set 키워드를 통하여 만들 수 있습니다.
주로 다른 파일의 private 프로퍼티를 제어하기 위해서 사용합니다.

### 사용법
```dart
class Person {
  String _name;
  int _age;
  Person(this._name, this._age);

  String get name => _name; // Getter (람다식)
  int get age { // Getter
    return _age;
  }
  
  set name(String value) { // Setter
    _name = value;
  }
  set age(int value) { // Setter
    _age = value - 1;
  }
}


```
자료 : https://dart-ko.dev/language/methods#getter-setter
