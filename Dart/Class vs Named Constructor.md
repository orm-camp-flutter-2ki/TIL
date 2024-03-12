## 📖 Class vs Named constructor
<br>

```dart
class Person {

  String name;

  int birthYear;


  Person({

    required this.name,

    required this.birthYear,

  });


  // named constructor

  Person.babo()

      : name = '바보',

        birthYear = 2000;


  int get age => 0;

  
  static Person mungchunge() {

    return Person(name: '멍청이', birthYear: 2000);

  }

}


void main() {

  Person person = Person(name: 'sss', birthYear: 2000);

  final babo = Person.babo();

  final babo2 = Person.mungchunge();

  print(babo);

  print(babo2);

}
```
- class와 named constructor 는 구분이 잘 안됨
- named constructor는 잘 쓰이지 않음
- 다수의 생성자를 구현하거나, 코드의 명확성을 더하고 싶다면 named constructor를 사용
- named constructor는 상속되지 않음
