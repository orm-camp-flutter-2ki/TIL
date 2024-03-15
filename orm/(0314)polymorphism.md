## 다형성(Polymorphism)
* 같은 타입으로 여러 인스턴스를 처리할 수 있는 유연성이 있다.
* 기존 코드에 영향을 미치는 범위 및 변경을 최소화하면서 새로운 코드를 작성할 수 있는 확장성이 있다.

### 1. 상속을 통한 다형성

```dart
class Animal {
  void makeSound() {
    print('make sound');
  }
}

class Dog extends Animal {
  @override
  void makeSound() {
    print('왈왈');
  }
}

class Cat extends Animal {
  @override
  void makeSound() {
    print('므야앙');
  }
}

void main() {
  List<Animal> animals = [Dog(), Cat()];
  for( Animal sound in animals ) {
    sound.makeSound();
    // 출력 결과
    // 왈왈
    // 므야앙
  }
}
```
* 다형성을 통해 각 동물이 다른 소리를 내도록 하였다.

<br></br>

### 2. 인터페이스를 통한 다형성

```dart
abstract interface class Drawable {
  void draw();
}

class House implements Drawable {
  @override
  void draw() {
    print('drawing house..');
  }
}

class Dog implements Drawable {
  @override
  void draw() {
    print('drawing puppy..');
  }
}

void main() {
  Drawable house = House();
  Drawable dog = Dog();

  // 화면에 그려질 수 있는 객체만 담아서 어떤 일을 수행하고 싶음
  List<Drawable> items = [house, dog];

  for( Drawable work in items ) {
    work.draw();
  }
}
```

* 다형성을 적용하면 타입이 다른 인스턴스들을 하나로 묶어서 취급할타입이 다른 인스턴스들을 같은 타입으로 묶어서 취급할 수 있다.
* House, Dog는 Drawable 인터페이스를 구현하고 있기 때문에 Drawable을 타입으로 사용할 수 있다.

<br></br>

### 3. 다형성을 활용하는 방법

* 선언을 상위 개념으로, 인스턴스 생성은 하위 개념으로 한다.
* 추상적인 선언 = new 상세 정의 <img width="450" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/be3f5979-3cab-45d0-bc24-fb644b226da9">

* 인터페이스를 변수의 타입으로 사용하기
```dart
abstract interface class Human {
  void speak();
}

void main() {
  Human human = Dancer('나댄서', 100);
}
```

* 타입 변경 시 'as'만 사용할 수 있다.
<img width="427" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/59383cea-7721-4b3d-b2e9-166320dee0ec">

* 인스턴스 확인과 smart cast
* 'is' 키워드를 사용하여 타입 검사
<img width="450" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/b11fddae-59ab-49d1-bc2e-787951b61965">

* 다형성의 장점을 활용한 코드와 활용하지 못한 코드(다형성의 장점: 동일한 취급이 가능하다.)
<img width="450" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5243691e-85c9-4e1c-92c4-9469484069bf">
<img width="409" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/eebbbf9f-a232-4e49-8b17-b2579fde6757">


<br></br>

### 4. 결과 예측

<img width="294" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/ccf48d57-74ea-4b6a-9907-60be04deed1b">
<img width="292" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/2b7b2473-cd3f-4dc8-b89f-7f1876a04d65">
<img width="284" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5832f900-6f42-44ab-a320-fc79f89f5cb7">

<br></br>

```
뚜벅
SlimeA가 도망쳤다.
뚜벅
SlimeB가 도망쳤다.
```
