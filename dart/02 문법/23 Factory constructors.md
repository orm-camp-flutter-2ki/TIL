# factory
- factory :
- 물건을 만드는 곳
- 무엇을 줄 지(리턴) 정할 수 있음. `{}` 영역
- 다형성에 의해서 어떤 형태로 줄 지도 정할 수 있음
<br/>

## design pattern
- factory pattern
- singleton pattern
<br/>

## factory pattern
- 인스턴스를 만드는 하나의 패턴
```dart
class User {
// (...)

  factory User.fromMap(Map<String, dynamic> json) {
    return User(
      name: json['name'],
      age: json['age'],
    );
  }

// (...)
}
```
<br/>

## singleton pattern
- 1개의 인스턴스만 생성되는 것을 보증하기 위한 패턴 (const가 아닌 애들 가지고 const 기능 구현)
- 인스턴스 생성을 여러번 시도해도 1개의 인스턴스가 공유됨. 렌터카 같은 개념..🚙 하나로 돌려 사용
- 캐시, 공유 데이터, 처리 효율화 등에 사용되는 테크닉
<br/>

### 사용 방법
```dart
class RentCar {
  static final RentCar _instance = RentCar._internal(); // 스테틱, 이미 여기서 인스턴스가 생성됨

  int _count = 0;

  // RentCar(); // 기본 생성자
  // RentCar.internal(); // named constructor
  RentCar._internal(); // private, 외부에서 인스턴스 생성 불가, 기본 생성자 삭제
  // 막아두고 factory를 만들어서 리턴을 강제..

  factory RentCar.Instance() { // 이것 때문에 외부에서도 생성 가능.. 그러나 같은 것만 내어 준다. 이름을 지을 때, 인스턴스 느낌 나게 지어주면 좋다.
    return _instance; // 스태틱한 나를 만들어서 리턴
  }

  void increment() {
    _count++;
  }
}
```
### 호출
```dart
void main() {
  final car1 = RentCar.Instance();
  final car2 = RentCar.Instance();

  car1.increment();

  print(identical(car1, car2)); // true

  print(car2._count); // 1
}
```





