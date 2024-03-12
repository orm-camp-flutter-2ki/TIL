---
title: 008 Dart - 컬렉션
author: Kim Donghyeok
created_at: 2024-03-11
updated_at: 2024-03-11
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 컬렉션

데이터 구조에 따른  대표적인 컬렉션 (자료구조)

1. List : 순서대로 쌓여있는 구조 (아이템의 중복 허용) (Stack)
2. Map : 키(Key) 값 (Value) 의 쌍으로 저장 (키의 중복 불가) ({Py})
3. Set : 순서가 없는 집합 (중복 불가)

# List

Dart 에는 Array(배열)이 없고 List 만 있음

```dart
final names = <String>

names.add('aaa');  
names.add('bbb');  
names.add('ccc');
```

## List 의 탐색 방법

```dart
for (int i = 0; i < names.length; i++) {
 print(names[i]);
}
```

```dart
for (final name in names) {
 print(name);
}
```

```dart
names.forEach((name) {
 print(name);
})
```

```dart
names.forEach(print);
```

# Set

중복값을 허용하지 않는 집합

get() 메소드는 제공하지 않기 때문에 반복이 필요하면 iterator 를 사용하거나 forEach() 를 사용

List의 contains 보다 압도적으로 빠름

```dart
Set<int> lotoSet = = {1, 2, 3, 4};

print(lotoSet.contains(1)); // true
print(lotoSet.contains(5)); // false
```

# Iterator

List 나 Set 은 요소를 탐색 할 수 있는 iterator 를 제공

```dart
List<int> subjects =[10, 50, 100, 100, 50];

final iterator = subjects.iterator;
while(iterator.nextMove( {
 print(iterator.current);
}))
```

```dart
Set<int> lottoSet = {1, 2, 3, 4, 5};

final iterator = lottoSet.iterator;
while(iterator.nextMove( {
 print(iterator.current);
}))
```

# Map

키(key) : 값(value) 의 쌍으로 이루어진 요소를 담는 자료구조

키의 중복은 허용되지 않음

```dart
Map<String, dynamic> gildong = {
 'name' : '홍길동',
 'id' : 0,
 'age' : 20
}
```

## Map 에 저장된 값을 하나씩 얻기

Map 은 순서를 보장하지 않기 때문에 매번 출력 결과의 순서가 다르게 표시 될 수 있음

```dart
gildong.entries.forEach((element) {
 print(element.key);
});

gildong.entries.forEach((element) {
 print(element.value);
})
```
