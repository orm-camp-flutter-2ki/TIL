240314 

플러터 과정 9일차

#### 강의 중 알면 좋은 정보
1. 이름을 바꾸는 rename의 단축키는 shift + f + u
2. 최근 파일을 열때는 ctrl + e

컬랙션
==

1) List : 순서 대로 쌓여있는 구조 (아이템의 중복 허용)
2) Map : 키(key)와 값(value)의 쌍으로 저장 (키의 중복 불가)
3) Set : 순서가 없는 집합 (중복 불가)

List
-
```dart
final names = <String>['aaa','bbb','ccc'];
```
List의 탐색 방법
```dart
for(int i = 0; i < names.length; i++){
  print(names[i]);
}

for (final name in names){
  print(name);
}

names.forEach((name){
  print(name);
});

names.forEach(print);
```

set
-
중복 값을 허용하지 않는 집합
get() 메서드는 제공하지 않기 때문에 반복이 필요하면 Iterator를 사용하거나 forEach()를 사용한다.

List의 contains 보다 압도적으로 빠름
```dart
Set<int> lottoSet = {1, 2, 3, 4};

print(lottoSet.contains(1)); // true
print(lottoSet.contains(5)); // false
```
#### Iterator
List나 Set 은 요소를 탐색할 수 있는 iterator 를 제공한다
```dart
//List
List<int> subjects = [10, 50, 100, 100, 50];

// iterator 활용법
final iterator = subjects.iterator;
while (iterator.moveNext()) {
print(iterator.current);
}
```
```dart
//Set
Set<int> lottoSet = {1, 2, 3, 4, 5, 6};

// iterator · 활용법
final iterator = lottoSet.iterator;
while (iterator.moveNext()) {
  print(iterator.current);
}
```

Map
-
키와 값의 쌍으로 이루어진 요소를 담는 자료구조 키의 중복은 허용되지 않음

```dart
Map<String, dynamic> name ={
  'name' : '김첨지',
  'id' : 0,
  'age' : 20,
};

//JSON처럼 사용할 수 있음
List<Map<String, dynamic>> students = [
  {
    'name' = '홍길동',
    'id'   = 0,
    'age'  = 20,
  }
  {
    'name' = '구한성',
    'id'   = 1,
    'age'  = 29,
  }
];
```
Map에 저장된 값을 하나씩 얻기
```dart
Map<String, dynamic> gildong = {
' name': '홍길동',
'id': 0,
'age': 20,
};

gildong.entries.forEach((element) {
print(element.key);
});

gildong. entries.forEach((element) {
print(element.value);
});

```
Map은 순서를 보장하지 않기 때문에 매번 출력 결과의 순서가 다르게 표시 될 수 있다.

###컬랙션의 선택
key, value 쌍 : Map
중복 가능 : List
중복 불가 : Set
순서 중요 : List
순서 안 중요 : Set
검색 속도 중요 : Set




