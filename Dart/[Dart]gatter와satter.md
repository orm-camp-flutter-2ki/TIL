> getter : 값을 받는 역할 (read -only)
setter : 값을 설정해주는 역할 (write -only) _~~잘 사용하진않음~~_

* 프로퍼티(property) : 객체 지향 프로그래밍 언어에서 필드와 메소드 간 기능의 중간인 클래스 멤버의 특수한 유형

Dart 에서는 `get`,`set` 키워드를 통해 만들 수 있음
주로 다른 파일의 private(_)property 를 제어하기위해 사용

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
