## 인스턴스의 기본 조작

### 오브젝트 클래스의 기본 기능

1. 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다
2. Object 타입 변수에는 모든 인스턴스를 대입할 수 있다

<Object 클래스의 대표 메서드 및 프로퍼티>

- toString() : 문자열 표현을 얻음
- operator == : 비교
- hashCode : 해시값을 얻음
- 모든 클래스의 조상님 = 슈퍼클래스

### final 이 들어간 클래스

- 상속 금지
- class final int
- class A extends int (오류)

<img width="421" alt="1" src="https://github.com/jungeun272/TIL/assets/131224099/e13a939d-bb0b-44f9-a34e-f816c894ad44">

`Object` 클래스의 대표적인 메서드와 프로퍼티

### `toString():`
- 이 메서드는 객체의 문자열 표현을 반환
- Dart에서 모든 클래스는 `toString()` 메서드를 재정의(override)할 수 있습니다. 만약 클래스가 `toString()` 을 재정의하지 않으면, 기본적으로는 객체의 식별자를 포함한 문자열이 반환됩니다.
        
```dart
Instance of 'Person'
```
        
`toString()`은 객체를 보다 읽기 쉬운 형태로 출력하거나 디버깅할 때 유용

### `operator ==:`
- 이 연산자는 두 객체가 동일한지를 비교
- Dart에서는 `==` 연산자를 사용하여 두 객체를 비교할 때 기본적으로는 객체의 레퍼런스를 비교합니다. 즉, 두 객체의 메모리 주소가 같은지를 확인합니다.
- 클래스마다 `operator ==`를 재정의하여 객체의 내용을 기준으로 동등성(equality)을 정의할 수 있습니다.
  
### `hashCode:`
- `hashCode`는 객체의 해시코드를 반환
- 해시 코드는 객체를 해시 기반 컬렉션(예: `Map` 또는 `Set`)에 저장할 때 사용하면 빠르다
- 동일한 객체에 대해 여러 번 호출되어도 항상 같은 정수 값을 반환해야 합니다. 동일한 객체는 동일한 해시 코드를 가져야 하지만, 서로 다른 객체가 같은 해시 코드를 가질 수 있음
- 일반적으로 `==` 연산자를 오버라이드할 때 함께 `hashCode`를 오버라이드하여 일관성 있는 동등성 검사(equality check)를 제공하는 것이 좋음
  
### `copy with()`

```dart
class Person {
  final String name;
  final int age;

  Person({required this.name, required this.age});

  Person copyWith({String? name, int? age}) {
    return Person(
      name: name ?? this.name,
      age: age ?? this.age,
    );
  }
}

void main() {
  var person1 = Person(name: 'Alice', age: 30);
  var person2 = person1.copyWith(name: 'Bob');

  print(person1.name); // Output: Alice
  print(person2.name); // Output: Bob
  print(person1.age);  // Output: 30
  print(person2.age);  // Output: 30 (age는 변경되지 않았으므로 원래 값과 같음)
}
```
  }
불변성을 유지하는 객체를 업데이트하는 편리한 방법을 제공
클래스의 모든 필드를 복사하면서 하나 이상의 필드를 새 값으로 대체하여 새로운 객체를 생성
final로 선언하여 해당 필드가 불변임을 나타낼 수 있음. 이런 불변 필드는 해당 클래스의 인스턴스가 생성된 후에는 변경할 수 없음
따라서 객체의 상태를 변경하려면 새로운 객체를 만들어야 하는데, `copywith()` 메서드가 사용됨
새로운 객체를 생성하여 기존 객체의 상태를 변경하는데 사용
변경하려는 필드를 새 값으로 대체하여 새 객체를 반환

### 장점
복잡한 객체의 상태를 변경할 때 더욱 안전하고 효율적인 방법을 제공
코드의 예측 가능성을 높이고, 병렬 처리와 상태 관리에 유리

### Object class가 가지고 있는 메서드

```dart
toString() //객체를 문자열로 표현하는 메서드
hashCode: 객체의 해시 코드를 반환하는 메서드 동일한 객체는 항상 동일한 해시 코드를 가짐. 객체가 == 연산자에 따라 같은지 판별하는 데 사용됩니다.
==: 객체의 동일성을 비교하는 메서드입니다. 두 객체가 동일한지 여부를 확인합니다. 기본 구현은 객체의 참조(메모리 위치)를 비교합니다.
runtimeType: 객체의 런타임 유형을 나타내는 Type 객체를 반환
noSuchMethod(): 객체가 존재하지 않는 메서드에 접근하려고 할 때 호출되는 메서드
copyWith(): 불변성을 유지하면서 객체를 업데이트할 때 사용되는 메서드 copyWith() 메서드를 사용하여 기존 객체의 상태를 변경하지 않고 새로운 객체 생성
Object: 객체의 문자열 표현을 반환
```
