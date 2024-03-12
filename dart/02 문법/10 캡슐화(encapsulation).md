# 캡슐화 (encapsulation)
- 휴먼 에러(human error)를 미연에 방지하기 위한 방법이다.
- 클래스 내부의 field(멤버변수)와 메서드(method)에 대한 접근을 제한한다.  
- 클래스 내부 변경으로 인한 외부 코드에 대한 영향을 최소화한다.  
- 코드의 유지보수성과 재사용성을 향상시킨다.  
<br/>

## 접근 지정자 (access modifier)
- 멤버에 대한 액세스를 제어한다.
- Getter와 Setter를 활용하여 field(멤버 변수)에 접근할 수 있다.  

|제한 범위|명칭|설정 방법|접근 가능 범위|
|---|---|---|---|
|제한이 느슨|public|default|모든 class|
|제한이 엄격|private|(_)name|자기 자신의 class|
<br/>

## getter setter
`getter` : 읽기 전용 프로퍼티를 구현할 때 사용  
`setter` : 쓰기 전용 프로퍼티를 구현할 때 사용
- 클래스의 field(멤버 변수)에 접근할 수 있다.
- 접근할 때 추가적인 기능(method)을 수행할 수 있다.
- field(멤버 변수)에 대한 읽기 전용 `getter` or 쓰기 전용 `setter`을 제공한다.
<br/>

## getter setter의 장점
- Read Only, Write Olny field를 구현할 수 있다.
- 클래스의 내부 설계를 자유롭게 변경할 수 있다.
- 필드로의 액세스를 검사할 수 있다.
<br/>

### getter, setter 사용
- `setter`을 사용하여 값의 타당성을 검사할 수 있다.  
```dart
class Person {
  String _name;

  Person({required String name}) : _name = name;

  // getter
  String get name => _name;

  // setter
  set name(String nameValue) { 
    // if 조건문 사용
    // if (nameValue.length < 3) {
    //   throw Exception('이름이 너무 짧습니다.');
    // }
    //
    // if (nameValue.length > 8) {
    //   throw Exception('이름이 너무 깁니다.');
    // }

    // switch case 사용
    switch (nameValue.length) {
      case < 3:
        throw Exception('이름이 너무 짧습니다.');
      case > 8:
        throw Exception('이름이 너무 깁니다.');
    }
    _name = nameValue;
  }
}
```
<br/>

- setter가 잘 기능하는지 main 함수에서 test
```dart
void main() {
  Person jack = Person(name: 'jack'); // 생성자

  // jack.name = 'J'; // error
  jack.name = 'ILOVEMYCATS'; // error
  // jack.name = 'jack'; // not error
}
```
> // console
> Unhandled exception:  
> Exception: 이름이 너무 짧습니다. or 이름이 너무 깁니다.  
<br/>

