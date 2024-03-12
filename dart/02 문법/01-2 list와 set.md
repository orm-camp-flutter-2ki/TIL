# 리스트(List)와 Set
## 리스트(list)
`중복가능`, `순서있음`
- 순서(index)가 있는 변수들의 집합   
- 같은 리스트 내 다양한 데이터 타입 포함 가능 (중복 가능)   
- 필요에 따라 항목을 추가하거나 삭제 가능
<br/>

### list 선언
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

### list 값을 하나씩 얻는 방법
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

  //[3-2] forEach
  names.forEach(print);

  //[4] iterator
  final iterator = liteName.iterator;
  while (iterator.moveNest()) {
    print(iterator.current);
}
```
<br/>

## Set
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

