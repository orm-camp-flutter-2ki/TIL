# 인스턴스의 기본 조작
- 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다
- Object 타입 변수에는 모든 인스턴스를 대입할 수 있다

## Object 클래스의 대표 메서드 및 프로퍼티
- toString() : 문자열 표현을 얻음
- operator == : 비교
- hashCode : 해시값을 얻음
- 모든 클래스의 조상님 = 슈퍼클래스
- runtimeType : 객체의 런타임 유형을 나타내는 Type 객체를 반환
- copyWith() : 불변성을 유지하면서 객체를 업데이트할 때 사용되는 메서드 copyWith() 메서드를 사용하여 기존 객체의 상태를 변경하지 않고 새로운 객체 생성
- Object : 객체의 문자열 표현을 반환
- 
## final 이 들어간 클래스
- 상속 금지
- class final int                      //int 를 상속 못하는 이유
- class A extends int (오류)



copy with() 예시
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

  }
```
불변성을 유지하는 객체를 업데이트하는 편리한 방법을 제공
클래스의 모든 필드를 복사하면서 하나 이상의 필드를 새 값으로 대체하여 새로운 객체를 생성
final로 선언하여 해당 필드가 불변임을 나타낼 수 있음. 이런 불변 필드는 해당 클래스의 인스턴스가 생성된 후에는 변경할 수 없음
따라서 객체의 상태를 변경하려면 새로운 객체를 만들어야 하는데, copywith() 메서드가 사용됨
새로운 객체를 생성하여 기존 객체의 상태를 변경하는데 사용
변경하려는 필드를 새 값으로 대체하여 새 객체를 반환

장점
복잡한 객체의 상태를 변경할 때 더욱 안전하고 효율적인 방법을 제공
코드의 예측 가능성을 높이고, 병렬 처리와 상태 관리에 유리
