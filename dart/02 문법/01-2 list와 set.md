# 리스트(list)
`중복가능`, `순서있음`
- 순서(index)가 있는 변수들의 집합이며, 같은 리스트 내 다양한 데이터 타입 포함 가능하다.  
- 필요에 따라 항목을 추가하거나 삭제 가능하며, 중복을 허용한다.  
<br/>

## list 선언
```dart
// 생성과 함께 초기화
List<int> numbers = [1, 2, 3, 4, 5];
```
```dart
// 리스트에 값, 요소, 데이터, 변수 추가
numbers.add(6);

// 리스트의 특정 인덱스에 접근
int firstNumber = numbers[3]; // 4;

// 리스트의 길이 확인
int M = numbers.length; // M == 6

// 리스트 출력
print(numbers); // 출력 결과: [1, 2, 3, 4, 5, 6]
```
<br/>

## list 값을 하나씩 얻는 방법
```dart
  //[1] for i 문
  for (int i = 0; i < names.length; i++) {
    print(names[i]);
  }

  //[2] for in 문
  for (final name in names) {
    print(name);
  }

  //[3-1] forEach
  names.forEach((name) {
    print(name);
  });

  //[4] iterator
  final iterator = liteName.iterator;
  while (iterator.moveNest()) {
    print(iterator.current);
}
```
<br/>

## List 정렬 방법
- 정렬을 하기 위해서는 `set`이 아닌 순서가 있는 `List`를 사용해야 한다.
- 정렬 기능은 operator == 기반으로 동작한다. ==은 참조의 비교(주소의 비교)이다.
- 정렬은 클래스 설계에 관여하는 implements를 통한 방법과 런타임에 정렬 규칙을 정하는 방법, 두가지가 있다.

### implements를 통해 클래스 설계 시 정렬 규칙을 정하는 방법
- 클래스 선언부에 ComparableTo<비교할_클래스> implements 해준다.
- 아래 코드는 name으로 정렬된다.
```dart
class Student implements Comparable<Student>{
/// 누구와 비교할지 정해주는 것, 클래스 설계에 관여가 된다.
String name;
String classNum;
int number;

Student({
  required this.name,
  required this.classNum,
  required this.number,
});

@override
String toString() {
  return '$name, $classNum반, $number번';
}

/// implement Comparable 시 자동으로 override 된다.
/// Student 클래스의 name을 비교한다.
@override
int compareTo(Student other) {
  return name.compareTo(other.name);
  }
}
```
```dart
void main() {
  Student stuA = Student(name: '다학생', classNum: '2', number: 1);
  Student stuB = Student(name: '가학생', classNum: '3', number: 2);
  Student stuC = Student(name: '나학생', classNum: '1', number: 3);

  List<Student> students = [stuA, stuB, stuC];

  students.sort();

  for (var element in students) {
    print(element);
  }
}

/// console 출력 결과
가학생, 3반, 2번
나학생, 1반, 3번
다학생, 2반, 1번
```
<br/>

### 런타임에 정렬 규칙을 정하는 방법
- 이 방법을 더 자주 사용한다. 정렬이 필요할 때 비교할 요소를 선택할 수 있기 때문이다.  
```dart
  Student stuA = Student(name: '다학생', classNum: '2', number: 1);
  Student stuB = Student(name: '가학생', classNum: '3', number: 2);
  Student stuC = Student(name: '나학생', classNum: '1', number: 3);

  List<Student> students = [stuA, stuB, stuC];

  // number의 오름차순 정렬
  students.sort((a, b) => a.number.compareTo(b.number));

  // number의 내림차순 정렬
  // students.sort((a, b) => a.number.compareTo(b.number) * -1);

// console 오름차순 출력 결과
2반 1번 다학생
3반 2번 가학생
1반 3번 나학생
```
<br/>

# Set
`중복불가`, `순서없음`
- 순서가 없는 변수들의 집합  
- 중복 값을 허용하지 않는 집합
- get() 메서드를 제공하지 않기 때문에 반복 시 `iterator` or `forEach()`를 사용
- 검색 속도(contains)가 압도적으로 뛰어나다.  
<br/>

## set 선언
```dart
// 선언과 함께 초기화
Set<int> numbers = {1, 2, 3, 4, 5};
```
```dart
// 요소 추가
numbers.add(6);

// 리스트의 길이 확인
int N = numbers.length; // N == 6

// 출력 확인
print(numbers); // 출력 결과: {1, 2, 3, 4, 5, 6}

// 검색 contains
print(numbers.contains(1)); // true 출력
print(numbers.contains(7)); // false 출력
```
<br/>

### set 값을 하나씩 얻는 방법
```dart
//[1] forEach
  numbers.forEach((name) => print(name));

//[2] iterator
  final iterator = setName.iterator;
  while (iterator.moveNext()) {
    print(iterator.current);

//[3] stdout : 줄바꿈 없이 출력
import 'dart:io'; // stdout 사용하기 위한 import

numbers.forEach((name) {
stdout.write('$name '); // 줄 바꿈 없이 출력
});
```
<br/>

