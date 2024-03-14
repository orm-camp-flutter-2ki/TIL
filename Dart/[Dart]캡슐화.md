> 캡슐화(Encapsulation)?
객체의 속성(data fields)과 행위(methods)를 하나로 묶고, 실제 구현 내용 일부를 외부에 감추어 은닉화함
- 장점 : 객체의 속성과 행위를 묶으면 응집도가 올라가므로 자율적인 객체가 된다, 그러므로 자율적인 객체가 되면 다른 객체의 영향을 덜 받기 때문에 자신의 상태를 스스로 잘 처리할 수 있게 된다.
- 단점 : 그런데 이상황에서 캡슐화가 잘 이루어지지 않는다면 내부 속성에 접근하여 사용할수 있기때문에 결합도가 높아지고 응집도가 낮아져, 객체는 수동적인 객체가 되고 다른 객체의 영향을 크게 받기때문에 자신의 상태를 스스로 처리하기 힘들어져 유지보수가 어렵다.


예제코드)
```dart
class Person {
  // Private 필드
  String _name;
  int _age;
  // Person 생성자
  Person(this._name, this._age);
  // name 필드에 대한 게터
  String get name => _name;
  // age 필드에 대한 게터와 세터
  int get age => _age;
  set age(int value) {
    if (value >= 0) {
      _age = value;
    }
  }
}
void main() {
  var person = Person('John Doe', 30);
  // 게터를 사용하여 name과 age 출력
  print(person.name); // John Doe
  print(person.age); // 30
  // 세터를 사용하여 age 수정
  person.age = 32;
  print(person.age); // 32
}
```

>  - 정리)
`Person` 클래스는 `_name`과 `_age`라는 두개의 private 필드를 가지고 있습니다. 이 필드들은 클래스 외부에서 직접 접근을 할 수 없으며, 대신 `name`과 `age`에 대한 게터와 `age`에 대한 세터를 제공하여 필드에 안전하게 접근할 수 있게 합니다. 이렇게 캡슐화를 구현함으로써, `Person` 객체의 사용자는 객체의 내부 구현에 대해 알 필요 없이, 필요한 기능을 사용할 수 있습니다.
