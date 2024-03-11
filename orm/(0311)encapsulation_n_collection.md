    

## 1. Test 코드 작성

1.1. test 할 파일의 경로를 복사한다.

<img width="532" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/39ab88ef-e7a6-4a4f-a5cb-31c1b1851d6a">

<br></br>

1.2. test 폴더에 복사한 경로의 파일을 _test 붙이고 생성한다.
만약, test 폴더가 없으면 생성해준다.

<img width="284" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d43255e5-fef9-49e9-905d-7865404cce24">

<br></br>

1.3. test 파일에 test import와 main() 함수를 작성한다.

```dart
import 'package:test/test.dart';
```

여러 테스트 기법 중 given > when > then 기법을 사용한다.
expect() 함수로 검증한다.  

<img width="472" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/c92d3ae7-3c2e-4cb7-8674-28c48f0d1c6d">

<br></br>

## 2. 캡슐화(Encapsulation)

<img width="472" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/bbd64473-10eb-4443-bb31-8e04174c0831">


캡슐화는 데이터와 해당 데이터를 처리하는 메서드(또는 함수)를 하나의 단위로 묶는 것을 의미한다.  
캡슐화는 코드의 모듈화, 코드의 재사용성, 코드의 유지보수성을 향상시키는 주요 이점을 제공한다.  

은닉화  
은닉화는 캡슐화의 일종으로, 객체의 내부 상태를 외부에서 직접 접근하지 못하도록 하는 것을 의미한다.  
일반적으로 캡슐화에 의해 묶인 데이터는 private으로 지정되고, 외부에서는 해당 데이터에 간접적으로 접근하는 방법을 제공한다.  

<br></br>

### 캡슐화 구현 방법 1. 접근 지정자(access modifier)  
public, private 키워드로 접근 제어.

```dart
class Example {
  String publicVariable;    // public variable
  String _privateVariable;  // private variable

  void publicMethod() {
    // public method
  }

  void _privateMethod() {
    // private method
  }
}
```
<br></br>

### 캡슐화 구현 방법 2. Getter, Setter  
멤버 변수에 직접 접근하는 대신 Getter, Setter를 통해 간접적으로 접근할 수 있다.

```dart
class Person {

  String _name;
  int _age;

  Person(String name, int age)
      : _name = name, // _name 초기화
        _age = age;   // _age 초기화

  String get name => _name;
  set name(String value) {
    _name = value;
  }

  int get age => _age;
  set age(int value) => _age = value;
}
```

<br></br>

## 3. 컬렉션(자료 구조)

**List**
**Map**
**Set**

1. List
- 순서대로 쌓여있는 구조(아이템의 중복 허용)
- 크기를 정해두지 않고 요소를 추가할 때마다 커진다.

```dart
List<String> names = ['Alice', 'Bob', 'Charlie'];
```

<br></br>

2. Set
- 순서가 없는 집합(중복 불가)
- 속도가 빠르다.

```dart
Set<String> uniqueNames = {'Alice', 'Bob', 'Charlie'};
```

<br></br>

3. Map
- 키(key)와 값(value)의 쌍을 저장하는 자료 구조
- 순서가 없고 키의 중복은 허용되지 않는다.

```dart
Map<String, int> ages = {'Alice': 25, 'Bob': 30, 'Charlie': 35};
```

<br></br>

## 4. Property(프로퍼티)
property(프로퍼티)는 클래스 내부의 멤버 변수에 대한 접근자(getter)와 설정자(setter)를 통합한 개념이다.

<br></br>

```dart
Person 클래스를 작성하시오.
이름과 태어난 해를 생성자로 받는다 (name, birthYear)
이름과 태어난 해는 한번 정해지면 수정이 불가능하다.
age 프로퍼티를 통해 나이를 제공하지만, 임의로 수정은 불가능하다.
나이 계산은 올해년도에서 birthYear 년도를 뺀 값을 리턴한다.
현재 시간과 날짜는 DateTime 클래스를 활용하면 얻을 수 있다.
```

이 문제에서 age 프로퍼티는 다음과 같다.

```dart
// age 프로퍼티
int get age {
  final currentYear = DateTime.now().year;
  return currentYear - birthYear;
}
```
