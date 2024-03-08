---
title: 003 Dart - Null Safety
author: Kim Donghyeok
created_at: 2024-03-07
updated_at: 2024-03-07
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# Null Safety

> Null 이란?  

## Null 이 가능한 타입

null 을 허용하려면 타입 뒤에  ?를 붙여야 함

```dart
int i = null; // error

int? i = null; // OK
```

## Null 계층 구조

### 기존 타입 시스템

기존 시스템은 모든 타입이 Null 을 허용

![[dart_type_system_before.png]](/02.Dart/_resources/dart_type_system_before.png)

### Null Safety 가 적용된 타입 시스템

모든 타입은 Null 을 허용 하지 않음

![[dart_type_system_after.png]](/02.Dart/_resources/dart_type_system_after.png)

### Nullable

Null 허용 타입과 허용 하지 않는 타입

![[dart_nullable_hierarchy.png]](/02.Dart/_resources/dart_nullable_hierarchy.png)

### 최상위 객체인 Object

마찬가지로 Nullable 타입이 추가 됨

![[dart_nullable_object_hierarchy.png]](/02.Dart/_resources/dart_nullable_hierarchy.png)

### 최하위 객체

기존에 Null 이 최하위 객체였다면

지금은 Never 라는 특수한 타입이 추가 됨.

![[dart_hierarchy_never.png]](/02.Dart/_resources/dart_hierarchy_never.png)

## Null 처리

### `??`

앞의 객체가 null 인 경우 `??` 뒤에 작성한 값으로 변환 한다.

```dart
int value = nullableVlaue ?? 0;
```

### `!`

nullable 인 값을 Null 이 아님을 보증함

개발자에 책임이 따르므로 주의해서 사용해야 함

```dart
int? nullableValue = 10;
int value = nullableValue!;
```

### `?.`

nullable 객체를 안전하게 사용하고자 할 떄 사용

null 이 아니면 해당 코드를 수행하고

null 이면 null 을 반환

```dart
int ? nullableValue = 10;
print(nullableValue?.toString()); // 10 출력

int? nullableValue = null;
print(nullableValue?.toString()); //null 출력
```

### 타입을 명확하게

다음 네 타입은 모두 다른 타입

항상 명확한 타입을 정의하는 것이 중요

```dart
List<String>
List<String>?
List<String?>
List<String?>?
```

## NullSafety 의 장점

- null을 허용하지 않는 변수는 null 이 아님을 100% 보장한다.
- 따라서 개발자의 실수를 미연에 방지 할 수 있음
- 항상 예측이 가능한 코딩을 할 수 있다.
- 컴파일러가 변수의 null 검사를 진행하지 않아도 되기 때문에 컴파일 속도가 대폭 향상 된다.
