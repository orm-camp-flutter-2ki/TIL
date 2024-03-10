# 생성자 (constructor)
## 생성자란
- 인스턴스를 생성하는 방법을 제공한다.
- 클래스와 동일한 이름을 가지는 함수를 만들어 생성자를 선언할 수 있다.  
<br/>

## 기본 생성자 (default constructor)  
- 생성자를 선언하지 않았다면 `default`로 생성된다.
- 생성자가 존재하는 경우 기본 생성자는 제공되지 않는다.
- 그러나 선택적 매개변수를 사용할 경우 기본 생성자도 제공한다.
```dart
class Person {
  Person() { // 기본 생성자, 클래스와 동일한 이름을 가지고, 매개변수가 없다.
  }
}

void main() {
  Person dad = Person();  // 기본 생성자로 인스턴스 생성
}
```

- 하위(자식) 클래스는 상위(부모) 클래스의 생성자를 상속받지 않는다.
```dart
class Person {
  Person(); // 생성자
}

class Family extends Person { // Person 클래스를 상속받고 있다
  // 기본 생성자만 가지고 있다
  // Family();
}
```
<br/>

## 이름있는 생성자 (named constructor)  
- 한 클래스 내에 여러개의 생성자를 생성하거나, 생성자를 명확하게 하기 위해 사용한다.
```dart
class Person {
  String name = '';
  int age = 0;

  // 기본 생성자
  Person(this.name, this.age);

  // named 생성자
  Person.guest() {
    name = 'lola';
    age = 74;
  }
}

void main() {
  // 기본 생성자를 사용해 인스턴스 생성
  Person man = Person('jack', 54);
  print('Guest Name:${man.name} Age:${man.age}');

  // named 생성자를 사용해 인스턴스 생성
  Person women = Person.guest();
  print('Guest Name:${women.name} Age:${women.age}');

}
```
- 자식 클래스에서 부모 클래스와 같은 명명된 생성자를 사용하고 싶다면, 자식 클래스에서도 똑같이 구현해야 한다.
```dart
class Parent {
  String lastName = '';
  int famNum = 0;

  // 부모 클래스의 named 생성자 구현
  Parent.info() {
    lastName = 'Kim';
    famNum = 5;
  }
}

class Child extends Parent {
  // 자식 클래스의 named 생성자 구현
  Child.info() : super.info() {
  }
}

void main() {
  // 부모 클래스의 named 생성자 호출
  Parent parent = Parent.info();
  print('[Parent] last name: ${parent.lastName}, family: ${parent.famNum}');

  // 자식 클래스의 named 생성자 호출
  Child child = Child.info();
  print('[Child] last name: ${child.lastName}, family: ${child.famNum}');

}
```
<br/>

