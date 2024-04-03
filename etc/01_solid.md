# SOLID 원칙

SOLID 원칙이란 객체 지향 설계 5대 원칙입니다.
각각 SRP, OCP, LSP, ISP, DIP로 줄여 말합니다.

### 단일 책임 원칙 : Single Responsibility Principle : SRP
> 한 클래스는 하나의 책임만 가져야 한다.

#### Tip : 외부 객체는 생성자로 주입 받기
```dart
// 좋지 않은 예
class PersonRepository {
  final PersonApi _api = PersonApi;
}

// 좋은 예
class PersonRepository {
  final PersonApi _api;
  PersonRepository(this._api);
}

```

### 개방 폐쇄 원칙 : Open/Closed Priciple : OCP
> 확장에는 열려 있으나 변경에는 닫혀 있어야 한다.

#### Tip : 다향성을 활용하기
```dart
  // 좋지 않은 예
  void eat(Pizza pizza) {
    print('$pizza를 먹어요');
  }
  void eat(Soup soup) {
    print('$soup를 먹어요');
  }

  // 좋은 예
  void eat(Food food) {
    print('$food를 먹어요');
  }
```

### 리스코프 치환 원칙 : Liskov Substitution Priciple : LSP
> 객체는 정확성을 떨어뜨리지 않으면서 하위 타입의 인스턴스로 바꿀 수 있어야 한다.

#### Tip : 상속할 때 is-a 원칙을 지키기

### 인터페이스 분리 원칙 : Interface Segregation Priciple : ISP
> 범용 인터페이스보다 여러 개의 구체적인 인터페이스가 낫다.

#### Tip : 인터페이스는 하나에 다 넣지 말고 쪼개기 (필요에 따라)
```dart
// 좋지 않은 예
abstract interface class Human {}

// 좋은 예
abstract interface class Movable {}
abstract interface class UseableTool {}
abstract interface class Fightable {}
```

### 의존관계 역전 원칙 : Dependency Inversion Priciple : DIP
> 구체화에 의존하지 않고 추상화에 의존해야 한다

#### Tip : 구체적인 클래스보다 인터페이스나 추상 클래스와 관계를 맺기
