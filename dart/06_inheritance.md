# Inheritance, 상속

상속은 중복되는 코드를 줄이고 재사용과 확장을 용이하게 할 수 있게 도와줍니다.
Dart에서 상속은 어떻게 쓰는지에 대해 알아보겠습니다.

### extends
Dart에서는 extends를 통하여 클래스를 상속할 수 있습니다.
```dart
class Cat extends Animal {}
// Cat 클래스는 Animal 클래스를 상속받는다
```
extends 왼쪽에는 상속받는 클래스를, 오른쪽에는 상속할 클래스를 작성합니다.
비교적으로 왼쪽이 범위가 작고 오른쪽이 범위가 커야 합니다.
왼쪽의 클래스를 자식 클래스, 오른쪽 클래스를 부모 클래스라 부릅니다.

상속을 올바르게 사용했는지 알아볼 때 "is-a" 원칙을 사용합니다.

>**is-a 원칙**
**[자식 클래스] is a [부모 클래스]** 를 했을 때 어색하지 않아야 합니다.
_ex) Cat is a Animal (o) &nbsp&nbsp&nbspFish is a Shark (x)_

이 원칙대로 작성하여 잘못된 상속이 되지 않도록 하는 것이 중요합니다.
```dart
class Animal {
  String sound;
  Animal(this.sound);
}

class Dog extends Animal {
  Dog(super.sound);
  // super 키워드를 사용하여 Animal 클래스의 sound에 접근
}

class Cat extends Animal {
  Cat(super.sound);
}

void main() {
  Dog dog = Dog('멍멍');
  print(dog.sound); // 멍멍
}
```

### Method Override
부모 클래스에서 정의되어 있는 메소드를 자식 클래스에서 재정의하는 것을 오버라이드라고 합니다.
상속한 클래스에 있는 메소드를 그냥 쓸 수도 있지만, 부연적으로 추가하거나 수정해야 할 때 사용합니다.
```dart
class Animal {
  String sound;
  Animal(this.sound);
  
  void makeSound() {
    print('동물이 소리를 냅니다');
  }
}

class Dog extends Animal {
  Dog(super.sound);
  
  @override // 오버라이드 Annotation
  void makeSound() {
    super.makeSound(); // Animal 클래스에서 정의된 makeSound에 접근
    print('${super.sound}하고 짖습니다.');
  }
}

class Cat extends Animal {
  Cat(super.sound);
  
  @override
  void maineSound() {
    print('${super.sound}하고 웁니다.');
  }
}

void main() {
  Dog dog = Dog('멍멍');
  Cat cat = Cat('야옹');
  dog.makeSound();
  // 동물이 소리를 냅니다.
  // 멍멍하고 짖습니다.
  cat.makeSound();
  // 야옹하고 웁니다.
}
```
super 키워드를 통해서 이미 정의된 메소드를 사용할 수도 있습니다.

### 정리
- extends를 사용하여 기존에 정의된 클래스를 기초로 하는 새로운 클래스를 정의할 수 있다.
- '자식 클래스 is a 부모 클래스'를 지키자.
- super를 통해 부모 클래스로 접근이 가능하다.
- @override를 통해 메소드를 재정의할 수 있다.

자료 : https://dart.dev/language/extend
