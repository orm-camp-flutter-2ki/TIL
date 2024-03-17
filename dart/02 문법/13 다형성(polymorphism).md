# 다형성(polymorphism)
- 객체 지향 프로그래밍에서 가장 중요한 개념이다. 객체 지향의 꽃.. 💮  
- 다형성은 abstract와 interface를 통해 상속/구현된다.  
- 한 번 작성한 코드를 다양한 타입의 객체에 적용할 수 있으며, 새로운 타입이 추가되더라도 기존 코드를 수정하지 않고도 사용할 수 있다.  

#### 예를 들면
> 어떤 것을 이렇게도 볼 수 있고 저렇게도 볼 수 있는 것이다.    
> 예를 들면 `달걀🥚` 이 있을 때, 이걸 `생명🐣` 으로 분류할 수 있고 혹은 `음식🍳` 으로 분류할 수 있다는 것...  
> 음식으로 본다면 요리, 먹기 등..을 할 수 있고, 생명으로 보면 부화, 죽음 등..을 할 수 있는 것이다.
<br/>

## 다형성 구현 방법
### 추상클래스 (abstract class)
> 서브클래스가 슈퍼클래스의 메서드를 override하거나 확장함으로써 다형성을 구현할 수 있으며, 서브클래스의 인스턴스를 슈퍼클래스의 타입으로 다룰 수 있다.
### 인터페이스 (interface - implements)
> 인터페이스는 클래스가 구현해야 하는 메서드의 집합을 정의하며 인터페이스를 구현한 클래스들은 해당 인터페이스의 타입으로 다룰 수 있다.
<br/>

## 구현해보기
### 추상화 Animal class
```dart
abstract class Animal {
  String name;

  Animal({required this.name});

  void animalSound();

  void eat(String foodValue) {
    print('$name은 $foodValue를 먹었다.');
  }
}
```

### 인터페이스 Drawable class
```dart
abstract interface class Drawable {
  void draw();
}
```
<br/>

## 두 클래스를 사용한 Cat, Dog class
### 클래스 작성
```dart
// cat
class Cat extends Animal implements Drawable {
  Cat({required super.name});

  @override
  void animalSound() {
    print('$name: 야옹야옹');
  }

  @override
  void eat(String foodValue) {
    print('$name은 $foodValue가 질렸다고 한다.');
  }

  @override
  void draw() {
    print('나는 $name을 그렸다.');
  }

  void golgolSong() {
    print('$name은 기분이 좋아 골골송을 한다.')
  }
}

// dog
class Dog extends Animal implements Drawable {
  Dog({required super.name});

  @override
  void animalSound() {
    print('$name: 멍멍멍멍');
  }

  @override
  void draw() {
    print('나는 $name을 잘 그렸다.');
  }

  void tugPlay() {
    print('$name은 신나게 터그놀이를 한다.')
  }
}
```
<br/>

### 인스턴스 생성 및 호출
- 다형성의 메리트를 활용하지 못한 코드  
```dart
void main() {
  // Drawable 타입으로 인스턴스 생성
  Drawable drawCat = Cat(name: '치즈냥');
  Drawable drawDog = Dog(name: '시고르자브르');

  drawCat.draw();
  drawDog.draw();

  // Animal 타입으로 인스턴스 생성
  Animal myCat = Cat(name: '순덕베티');
  Animal myDog = Dog(name: '레오');

  myCat.eat('츄르');
  myCat.animalSound();
  myDog.eat('저키');
  myDog.animalSound();
  }
```
```dart
// 콘솔 출력 결과
나는 치즈냥을 그렸다.
나는 시고르자브르을 잘 그렸다.
순덕베티은 간식가 질렸다고 한다.
순덕베티: 야옹야옹
레오은 간식를 먹었다.
레오: 멍멍멍멍
```
<br/>

### 다형성의 메리트 : 동일한 타입으로 취급, 코드 중복 제거
- 동일한 타입으로 취급해서 묶을 수 있다.  
- 코드 중복을 줄여 생산성을 향상했다.   
```dart
void main() {
  Drawable drawCat = Cat(name: '치즈냥');
  Drawable drawDog = Dog(name: '시고르자브르');

  // forEach
  // List<Drawable> drawingNow = [drawCat, drawDog];
  // drawingNow.forEach((element) {
  //   element.draw();
  // });

  // for in, IDE가 이걸 추천
  List<Drawable> drawingNow = [drawCat, drawDog];
  for (var element in drawingNow) {
    element.draw();
  }

  Animal myCat = Cat(name: '순덕베티');
  Animal myDog = Dog(name: '레오');

  // forEach
  // List<Animal> cuteAnimal = [myCat, myDog];
  // cuteAnimal.forEach((element) {
  //   element.eat('간식');
  //   element.animalSound();
  // });

  // for in
    List<Animal> cuteAnimal = [myCat, myDog];
    for (var element in cuteAnimal) {
      element.eat('간식');
      element.animalSound();
 }
```
```dart
// 콘솔 출력 결과
나는 치즈냥을 그렸다.
나는 시고르자브르을 잘 그렸다.
순덕베티은 간식가 질렸다고 한다.
순덕베티: 야옹야옹
레오은 간식를 먹었다.
레오: 멍멍멍멍
```
<br/>

## 타입 cast 방법
### as 사용
- 지양되었던 `as` 사용이 불가피하다. 우리가 만든 class는 `.toString`.. 등을 사용한 cast가 불가능하기 때문이다.  
<br/>

### 어떤 경우에 사용?
- 아래와 같이 선언한 경우, Cat과 Dog이 가진 메서드 golgolSong(), tugPlay()를 사용할 수 없다.
```dart
  Animal aniCat = Cat(name: '순베냥');
  Animal aniDog = Dog(name: '멍뭉망');

  // 사용 불가능
  // aniCat.golgolSong();
  // aniDog.tugPlay();
```

- as로 타입을 cast하면 사용 가능하다.
```dart
  Cat catCat = aniCat as Cat;
  Dog dogDog = aniDog as Dog;

  aniCat.golgolSong(); 
  aniDog.tugPlay();
  // catCat, dogDog로 메소드를 호출해도 되는데 주소는 하나라...
```

```dart
// 콘솔 출력 결과
순베냥은 기분이 좋아 골골송을 한다.
멍뭉망은 신나게 터그놀이를 한다.
```

- 이런건 Animal과 Drawable 타입 간의 관계가 없기 때문에 불가능 하다.
```dart
  Animal aniCat = Cat(name: '순베냥');
  Animal aniDog = Dog(name: '멍뭉망');

  // 불가능
  // Drawable draCat = aniCat;
```
<br/>

### 형변환 시 주의할 점
- as로 강제 형변환 시 문제가 있을 때, 컴파일 에러는 안뜨지만 돌리면 터진다.  
```dart
// 터지는 코드..
Animal aniDog2 = drawDog as Cat;
```

- 타입 검사 후 사용하는 if is 검사 문을 통과하면 된다.
```dart
  // 스마트 캐스트
  if (drawDog is Dog) {
    Animal aniDog2 = drawDog;
  }

  // IDE 가 위 코드로 변경해줬다. if is로 이미 검증이 되었기 때문에 as가 없어도 괜찮다.
  // if (drawDog is Dog) {
  //   Animal aniDog2 = drawDog as Dog;
  // }
```
<br/>





