---
title: 013 Dart - 제네릭, 열거형
author: Kim Donghyeok
created_at: 2024-03-18
updated_at: 2024-03-18
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 제네릭 (Generic)

> 타입이 없을 때의 문제점
>
> 1. 런타임 에러가 나기 쉽다.  
> 2. IDE가 컴파일 에러를 미리 찾을 수 없다.  

타입을 나중에 원하는 형태로 정의 할 수 있다.

Type safe 효과

![[240318_generic_example.png]](/02.Dart/_resources/240318_generic_example.png)

## 제네릭의 사용

제네릭을 사용하지 않았을 때

```dart
class Pocket {
 Object? _data;
 
 void pub(Object data) {
  _data = data;
 }
 
 Object? get() {
  return _data;
 }
}
```

제네릭을 사용했을 때

```dart
class Pocket<E> {
 E? data;
 void pub(E data) {
  data = data;
 }

 E? get() {
  return data;
 }
}
```

제네릭에 제약을 추가한 경우

```dart
class Pocket<E extends Book> {  
  E? data;  
  void put(E data) {  
    data = data;  
  }  
  E? get() {  
    return data;  
  }
}
```

# 열거형 (Enumerate)

정해둔 값만 넣어둘 수 있는 타입

```dart
class AuthState {
 static const authenticated = 1;
 static const unauthenticated = 2
 static const unknown = 3;
}

int authState = AuthState.unknown;

// ...

if (authState == AuthState.authenticated) {
 print( '인증됨');
} else if (authState == AuthState.unauthenticated) {
 print('미인증');
} else {
 print('알 수 없음');
```

열거형을 사용하지 않으면 각종 휴먼에러와 마주할 수 있게 됨

- 매직넘버링
- 다른 입력에 대한 처리 오류
- 다른 객체와 비교해도 에러가 발생하지 않음

```dart
enum AuthState {
 authenticated,
 unauthenticated,
 unknown,
}

AuthState authState = AuthState.unknown,

// ...

switch (authState) {
 case AuthState.authenticated:
  print('authenticated');
  break;
 case AuthState.unauthenticated:
  print('unauthenticated');
  break;
 case AuthState.unknown:
  print('unknown'):
  break;
}
```

switch-case 구문과 조합으로 모든 케이스를 강제로 작성해야 하는 이점이 있음
