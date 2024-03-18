---
title: 014 Dart - 문자열 조작
author: Kim Donghyeok
created_at: 2024-03-18
updated_at: 2024-03-18
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 문자열 조작

- concat (+, StringBuffer)
- interpolation
- substring
- replaceAll
- split
- toLoweCase
- toUpperCase
- indexOf
- length, isEmpty

# String Buffer

write() 메소드로 결합한 결과를 내부 메모리 (버퍼) 에 담아두고 toString() 으로 결과를 얻음

```dart
final buffer = StringBuffer('dart');

buffer
 ..write(' and ')
 ..write('Flutter');

print(buffer.toString());
```

> `..`(cascase) 연산자
>
> void 리턴인 함수의 앞에서 사용하면 해당 객페의 레퍼런스를 반환하여 메소드 체인을 사용 할 수 있음.

## +연산자가 느린이유

String 객체는 불변 객체 (immutable) 이기 때문

```dart
const string = 'Dart is fun';  
print(string.substring(0, 4)); // 'Dart'
print(string); // Dart is fun
```

위 코드와 같이 String 객체에 어떠한 연산을 하더라도 문자열 자체는 변경되지 않는다.

메소드에 의해서 조작된 값이 반환 되는 것이지 조작에 사용된 문자열 자체가 변경되지 않음.

```dart
const string = 'Dart is fun';  

string = 'Dart';
```

위 코드는 문자열 객체의 값이 바뀐 것이 아님.

Dart 에서는 모든 것들이 Object 를 상속한 객체이므로 문자열의 내용이 바뀐 것이 아니라  
새로운 문자열 객체가 생성되면서 변수가 가리키는 레퍼런스 값이 바뀐 것이지 초기에 선언된 문자열의 값이 바뀐 것이 아님.

# 코드 성능 측정

```dart
final stopwatch = Stopwatch()..start();

// 시간 측정할 코드

print(stopwatch.elapsed);
```

객체를 생성하는 new 키워드는 그 자체 만으로 컴퓨팅 자원을 많이 소모함

따라서 위에서 배운 + 연산자 보다 StringBuffer 를 사용하는 것이 성능적으로 이득임
