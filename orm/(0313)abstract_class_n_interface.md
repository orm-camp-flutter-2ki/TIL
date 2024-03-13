## 1. 추상 클래스(Abstract class)

* 추상 클래스는 다른 클래스들의 설계 도면으로 사용된다.
* 블럭을 가지지 않은 추상 메서드를 만들 수 있다.
* 하위 클래스에 공통 인터페이스를 정의한다.
* 추상 클래스의 인스턴스는 생성할 수 없다.
* 각 하위 클래스들은 강제 override를 통해 추상 클래스의 필드와 메서드를 구현해야 한다.

```dart
abstract class Asset {
  String name;
  int price;

// named parameter
  Asset({required this.price, required this.name});
}
```

```dart
// 무형자산
abstract class IntangibleAsset extends Asset {
  String ownerName;

  IntangibleAsset({
    required super.price,
    required super.name,
    required this.ownerName,
  });

  // 가치 평가(추상 메서드)
  void value();
}
```
<br></br>

## 2. 인터페이스(Interface)

* 특정 행동을 정의
* 모든 메서드는 추상 메서드여야 한다.
* 필드를 가지지 않는다.
* 클래스에서 'implements' 키워드를 사용해서 구현한다.
* 해당 인터페이스를 구현한 클래스는 인터페이스가 정의한 모든 메서드와 속성을 제공해야 한다.
* 따라서, 같은 인터페이스를 구현한 클래스들은 공통 메서드를 구현하고 있음이 보장된다.
* 코드의 재사용성과 유지보수성을 높일 수 있다.
* 한 클래스에서 여러 개의 인터페이스를 구현할 수 있다.
  

<img width="558" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/812af25b-be13-4812-96bb-58027eb867d4">

<img width="534" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c26d28a2-8a99-4324-a79f-05e40fd44c2d">

<br></br>

## 차이점

|추상 클래스                |인터페이스|
|--------                |-------|
|공통의 속성을 추상화         | 특징을 정의|
|다중 상속 x               | 다중 구현 ㅇ|
|`extends`를 사용하여 상속   | `implements`를 사용하여 구현|
|구현이 된 메서드도 가지고 있다.| 구현이 안된 메서드만 가지고 있다.|


<img width="324" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/05761d21-9811-4f68-8101-be5406171e81">

<br></br>

## 3. 기타

### 상속의 궁극적인 이유 = 기능의 확장
### Test code 작성이 필요없는 경우
- 리턴이 없는 함수
- 상태가 변하지 않는 함수(예: 출력)

### ternary : 삼항 연산자
### conditional operator
* Conditional AND
* Conditional OR
* Ternary Operator

<img width="819" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/f9c12e63-d833-41d5-9895-ec45b38417ca">



[참고]
[Conditional Operator in Java](https://www.javatpoint.com/conditional-operator-in-java)
