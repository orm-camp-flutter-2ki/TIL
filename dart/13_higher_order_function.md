# Higher-order function, 고계 함수

고계 함수는 함수형 프로그래밍의 개념에서 활용되며 함수를 파라미터로 받는 함수입니다.
대표적인 함수 몇 가지를 알아보겠습니다.

### where
where()를 사용하면 조건에 맞는 값들을 묶어 Iterable형으로 반환합니다.
```dart
final items = [1, 2, 3, 4, 5];

// where 미사용
for (var i = 0; i < items.length; i++) {
  if (items[i] % 2 == 0) {
    print(items[i]); // 2, 4
  }
}

// where 사용
items.where((e) => e % 2 == 0).forEach(print); // 2, 4
```

### map
map()을 사용하면 원하는 형태로 컬렉션을 재구성할 수 있습니다.
Map 타입과는 다른 개념이며 혼동해서는 안 됩니다.
**
```dart
final items = [1, 2, 3, 4, 5];

// map 미사용
for (var i = 0; i < items.length; i++) {
  if (items[i] % 2 == 0) {
    print('숫자 ${items[i]}'); // 숫자 2, 숫자 4
  }
}

// map 사용
items.where((e) => e % 2 == 0)
  .map((e) => '숫자 $e')
  .forEach(print); // 숫자 2, 숫자 4

```

### toList
toList()를 사용하면 컬렉션을 List형으로 변환합니다.
```dart
final items = [1, 2, 3, 4, 5];

// toList 미사용
final result = [];
items.forEach((e) => {
  if (e % 2 == 0) {
    result.add(e);
  }
});

// toList 사용
final result = items.where((e) => e % 2 == 0).toList();
```

### toSet
toSet()을 사용하면 컬렉션을 Set형으로 변환합니다.
중복 데이터를 제거하는 데에 유용하게 사용할 수 있습니다.
```dart
final items = [1, 2, 2, 3, 3, 4, 5];

// toSet 미사용
List<int> result = [];
Set<int> temp = {};
for (var i = 0; i< items.length; i++) {
  if (items[i] % 2 == 0) {
    temp.add(items[i]);
  }
}
result = temp.toList();
print(result); // 2, 4

// toSet 사용
final result = items
  .where((e) => e % 2 == 0)
  .toSet().toList().forEach(print) // 2, 4;
```

### any
any()는 조건에 맞는 값이 컬렉션 내에 있는지 검사할 때 사용합니다.
```dart
final items = [1, 2, 2, 3, 3, 4, 5];

// any 미사용
var result = false;
for (var i = 0; i< items.length; i++) {
  if (items[i] % 2 == 0) {
    result = true;
    break;
  }
}
print(result); // true

// any 사용
print(items.any((e) => e % 2 == 0)); // true
```

### reduce
reduce()는 반복 요소가 있을 때 유용하게 사용할 수 있습니다.
연산에 맞게 요소끼리 비교합니다.
math 패키지의 max()를 이용해서 최대값을 구하는 예제입니다.
```dart
import 'dart:math';
final items = [1, 2, 3, 4, 5];

// reduce 미사용
var maxResult = items[0];
for (var i = 0; i< items.length; i++) {
  maxResult = max(items[i], maxResult);
}
print(maxResult); // 5

// reduce 사용
print(item.reduce((e, v) => max(e, v))); // 5
```
