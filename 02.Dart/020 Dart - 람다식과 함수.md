---
title: 020 Dart - 람다식과 함수
author: Kim Donghyeok
created_at: 2024-03-20
updated_at: 2024-03-20
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 1급 객체

변수에 대입 가능한 객체를 1급 객체 (first class object) 라고 한다.

대표적인 1급객체 : 값, 인스턴스, 함수

# 함수

함수도 1급 객체로 취급됨

입력이 동일할 때 항상 동일한 출력을 한다.

## 함수의 표현방법

일반적인 함수

```dart
bool isNobel(int atomicNumber) {
	return _nobelGases[atomicNumber] != null;
}
```

람다식 (Lambda expression)

```dart
bool isNobel(int _atomicNumber) => _nobelGases[atomicNumber] != null;
```

## Named parameter

`{}` 을 사용하여 파라미터에 이름을 붙이도록 강제한다.

```dart
void enableFlags({bool? bold, bool? hidden}) {};
```

## 파라미터에 기본값 지정

`=` 으로 기본값을 지정할 수 있다.

```dart
void enableFlags({bool bold = false, bool hidden = false}) {}
```

## required 로 필수 파라미터 지정

`required` 키워드를 붙이면 반드시 값을 지정해야 함

default 값을 지정할 수 없음

nullable 가능 (null 값을 반드시 전달해야 함)

```dart
void enableFlags({
	required bool? bold,
	required bool hidden,
}) {}
```

## Optional positional parameter

[] 를 사용하여 위치를 지정하는 옵션 파라미터를 사용할 수 있음

반드시 세번재에 device를 설정하거나 안하거나 할 수 있음

default 값 지정 가능

```dart
void say(String from, String msg, [String? device]) {}
```

## 함수를 값으로 전달 하는 예

입출력 타입만 같다면 같은 함수로 볼 수 있다.

```dart
void printElement(int element) {
	print(element);
}

var list = [1, 2, 3];

list.forEach(printElement);
```

## 메서드와 함수의 차이

메서드는 클래스에 속하고 클래스를 조작하기 위한 일종의 함수

메서드는 이름이 있지만 함수에게 이름은 중요하지 않다.

```dart
void printElement(int element) {
	print(element);
}
```

```dart
void main() {
final list = [1, 2, 3];

list.forEach((element) { print(element); })
}
```

위 코드와 아래 코드는 완전히 동일한 동작을 하는 코드

```dart
void main() {
	final list = [1, 2, 3];

	list.forEach(printElement);
}
```

## 람다식

함수내용을 바로 정의하여 사용할 때 사용 가능

```dart
var loudify = (msg) => '!!! #{msg.toUpperCase()} !!!';
assert(loudify('hello') == '!!! HELLO !!!');
```

## 익명함수

이름이 없는 함수

```dart
list.forEach((element) { print(element); });
```

# 함수형  프로그래밍

- 다트는 객체 지향 프로그래밍(OOP)과 함수형 프로그래밍(FP) 특징을 모두 제공하는 멀티패러다임 언어
- 함수형 프로그래밍은 자료 처리를 수학적 함수의 계산으로 취급하는 프로그래밍 패러다임 가변데이터를 멀리하는 특징을 가짐. 

## 고계함수 (higher-order function)

> 함수를 파라미터로 받는 함수

### where

특정조건으로 입력을 필터링 함

```dart 
final items =[1,2,3,4,5];

items.where((e) => e % 2 == 0).forEach(print);
```

### map

컬렉션의 원소를 순회하며 특정 연산을 실행

```dart
final items =[1,2,3,4,5];

items.where((e) => e % 2== 0).map((e) => '숫자 $e').forEach(print);
```

### toList()

다트에서 함수형 프로그래밍을 지원하는 함수 대부분은 `Iterable<T>` 라는 타입을 반환함

실제로 활용시에 List 형태로 변환하여 사용하는 일이 많음

```dart
final result = items.where((e) => e % 2== 0).toList();
```

### toSet()

자료구조 Set으로 변환하는 함수

중복을 허용하지 않기 때문에 간단히 중복데이터를 제거할 수 있음

```dart
final items = [1,2,2,3,3,4,5];

final result = items.where((e) => e % 2== 0).toSet().toList(); // 2, 4
```

### any

특정 요건을 충족하는 요소가 존재하는지 검사할 때 사용

```dart
final items = [1,2,2,3,3,4,5];

print(items.any((e) => e % 2 == 0)); // true
```

### reduce

반복요소를 줄여가면서 결과를 만들 때 사용

```dart
import 'dart:math';

final items = [1,2,3,4,5];
final result = items.reduce(max) // 5
```