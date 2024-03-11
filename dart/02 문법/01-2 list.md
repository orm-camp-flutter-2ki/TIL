# 리스트 (List) 
- 순서가 있는 변수들의 집합  
- 순서(Index)가 있다. (0부터 시작)  
- 같은 리스트 내 다양한 데이터 타입 포함 가능   
- 필요에 따라 항목을 추가하거나 삭제 가능
<br/>

## 선언
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

## 값을 하나씩 얻는 방법
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
