# Abstraact class vs Interface
>추상 클래스와 인터페이스

언뜻 보면 비슷해 보이지만 다른 추상 클래스와 인터페이스는
Dart에서 어떻게 사용하고 어떤 차이점이 있는지 알아보겠습니다.

### Abstract class
추상 클래스를 사용하려면 abstract 키워드를 사용해야 합니다.

```dart
abstarct class Animal {
  String name;
  String sound;
  Animal(this.name, this.sound);
  
  void makeSound();
  // abstract를 붙였기 때문에 추상 메소드 사용 가능
  void move() {...};
  // 일반 메소드도 사용 가능
}

class Dog extends Animal {
  Dog(super.name, super.sound);
  
  // 상속받는 클래스가 추상 클래스가 아닐 경우
  // 슈퍼 클래스의 추상 메소드를 구현하지 않을 시 컴파일 에러
  @override
  void makeSound() {
    print(super.sound);
  }
}
```
추상 클래스도 일반적인 클래스처럼 extends를 통해 상속하는 것이 일반적입니다.
올바르게 사용했는지 알아보기 위해 is-a 원칙을 사용할 수 있습니다.

**자식 클래스 is a 부모 클래스**가 어색하지 않아야 합니다.

### Interface
인터페이스를 사용하려면 interface 키워드를 사용해야 합니다.
인터페이스에서는 모든 것이 추상 메소드입니다.
```dart
abstract interface class animal {
  void makeSound(); // 추상 메소드 선언
}

class Dog implements Animal {
  String name;
  String sound;
  Dog(this.name, this.sound);

  // 구현해야 하는 클래스가 추상 클래스가 아닐 경우
  // 슈퍼 클래스의 추상 메소드를 구현하지 않을 시 컴파일 에러
  @override
  void makeSound() {
    print(sound);
  }
}

```
인터페이스의 추상 메소드를 구현하려면 implements를 사용합니다.
extends는 한 클래스, implements는 여러 인터페이스를 받을 수 있습니다.

**자식 클래스 has a 부모 클래스**가 어색하지 않아야 합니다.
