# Polymorphism, 다향성

다향성은 대개 하나의 타입에 여러 가지 타입이 들어갈 수 있다는 것을 말합니다.
다향성을 이용하면 타입을 하나로 묶어서 코드 중복을 줄일 수 있습니다.

```dart
abstract interface class Creature {
  void breathe();
}
abstract class Animal implements Creature{
  void makeSound();
}
class Dog extends Animal {
  @override
  void makeSound() => print('멍멍');
  
  @override
  void breathe() => print('개가 숨을 쉰다');
}
class Cat extends Animal {
  @override
  void makeSound() => print('야옹');
  
  @override
  void breathe() => print('고양이가 숨을 쉰다');
  
  void punch() => print('냥냥펀치');
  // Cat 타입인 Cat 인스턴스만 사용 가능
}

void main() {
  Animal animal1 = Dog();
  Animal animal2 = Cat();
  animal1.makeSound();
  // 출력 : 멍멍
  animal2.breathe();
  // 출력 : 고양이가 숨을 쉰다

  List<Animal> animalList = [animal1, animal2];
  animalList.forEach((element) {
    element.makeSound();
  });
  // 출력 : 멍멍
  // 출력 : 야옹

 // animal1.makeSound(); animal2.makeSound().....
 // 일일히 치는 것보다 코드 중복을 줄일 수 있음
}
```
위와 같은 예시로 사용할 수 있습니다.


_추후 내용 추가 예정_
