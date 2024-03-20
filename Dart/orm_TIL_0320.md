240320 (wed)

플러터 과정 13일차

# 디버깅

소프트웨어가 올바르게 작동하는지 확인하는 데 필수적이다.

상상코딩

→ 버그생기면 디버거를 사용한다.

- 로깅
    - 로깅은 코드가 실행되는 동안 발생하는 이벤트를 기록하는 데 사용할 수 있습니다.
- 브레이크포인트
    - 브레이크 포인트는 코드의 특정 지점에서 실행을 중지하는 데 사용할 수 있습니다.
- 디버거
    - 디버거는 디버깅을 도와주는 도구입니다. 다양한 기능을 제공하며 디버깅을 더 쉽게 만들 수 있습니다.
- 스택 추적
    - 스택추적은 호출 스택을 추적하여 코드가 실행 줒인 위치를 확인하는 데 사용할 수 있습니다.

### 로깅

print() 함수를 활용하는 방법 → flutter에서는 debugprint를 사용해야 합니다.

---

디버깅 팁

- 작게 시작
    - 디버깅할 때 작은 문제부터 시작하는 것이 중요하다. 이렇게 하면 더 큰 문제로 넘어가기 전에 한 번에 한 가지 문제에 집중할 수 있습니다.
- 단순하게 유지
    - 디버깅할 때 코드를 단순한게 유지하는 것이 중요하다. 이렇게 하면 오류의 원인을 파악하기가 더 쉽습니다.
- 인내심을 가지세요
    - 디버깅은 시간이 많이 걸리 수 있으므로 인내심을 갖는 것이 중요하다. 오류를 찾는 데 즉시 성공하지 못하더라도 낙심하지 마십시오.
 
람다식과 함수
=

#### 1급 객체

변수에 대입 가능한 객체를 1급 객체라고 한다.

대표적인 1급 객체 : 함수, 인스턴스, 값

##### 함수 (function)

함수도 1급 객체로 취급 됨 입력이 동일할 때 항상 동일한 출력을 한다.

함수의 표현 방법

일반과 람다식이 있다.

```dart
bool isNoble(int atoicNumber) {
  return _nobleGases[atomicNumber] != null
}

bool isNoble(int atomicNumber) => _nobleGases[atomicNumber] != null;
```

### 함수형 프로그래밍
- 다트는 객체지향 프로그래밍과 함수형 프로그래밍 특징을 모두 제공하는 멀티 패러다임 언어이다.
- 함수현 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하는 프로그래밍 패러다임이고 가변 데이터를 멀리하는 특징을 가집니다.

## 고계 함수
함수를 파라미터로 받는 함수

### where 함수

```dart
final items = [1, 2, 3, 4, 5];

for (var i = 0; i < items.length; i++) {
    if ( item[i] % 2 == 0) {
      print( items[i]);
    }
}

//or

items.where((e) => e % 2 == 0).forEach(pirnt);

//답: 2, 4
```
### map 함수

```dart
final items = [1, 2, 3, 4, 5];

for (var i = 0; i < items.Length; i++) {
  if (items[i] % 2 == 0) {
    print('숫자 ${items[i]}'); // 숫자 2, 숫자 4
  }
}

//or

items.where((e) => e % 2 == 0).map((e) => '숫자 $e').forEach(print);

//답 2, 4
```
### toList()

```dart

final result = [];
items. forEach((e) {
  if (e % 2 == 0) {
    result.add(e);
  }
});

//or

final result = items.where((e) => e % 2 == 0).toList();

// 답 2,4
```

### toSet()

```dart
final items = [1, 2, 2, 3, 3, 4, 5];

var result = [];
var temp = <int>{};
for (var i = 0; i < items.length; i++) {
    if (items[i] % 2 == 0) {
    temp.add(items[i]);
    }
}
result = temp.toList();
print(result); // 2, 4

//or

final result = items.where((e) => e % 2 == 0).toSet().toList();

// 2, 4
```

### any

```dart
final items = [1, 2, 2, 3, 3, 4, 5];

var result = false;
for (var i = 0; i < items. length; i++) {
  if (items[i] % 2 == 0) {
    result = true;
    break;
  }
}
print(result); // true

//or

print(items.any((e) => e % 2 == 0)); // true
```

### reduce

```dart
import 'dart:math';

final items = [1, 2, 3, 4, 5];

var maxResult = items[0];
for (var i = 1; i < items. length; i++) {
maxResult = max(items[i], maxResult);
}
print(maxResult); // 5

//or

final items = [1, 2, 3, 4, 5];
print(items.reduce((e, v) => max(e, v))); // 5

final result = items.reduce(max); // 5
```


