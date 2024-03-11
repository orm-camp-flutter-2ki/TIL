---
title: 007 Dart - 캡슐화
author: Kim Donghyeok
created_at: 2024-03-11
updated_at: 2024-03-11
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 캡슐화 (Encapulation)

객체지향에서 캡슐화

- 데이터와 함수(메소드)들을 객체 안에 넣어서 묶는다는 의미

# 멤버에 대한 엑세스 제어

접근지정자 (access modifier)

|  제한범위   | 명칭    |      설정방법      |  접근 가능한 범위  |
|:-----------:| ------- |:------------------:|:------------------:|
| 제한이 엄격 | private | 멤버앞에 \_ 붙이기 | 자기 자신의 클래스 |
| 제한이 느슨 | public  |       기본값       |    모든 클래스     |

# public, private 의 권한 제어

![[240311_private,public_access_control.png]](/02.Dart/_resources/240311_private,public_access_control.png)

## private, public

Dart 에서 private 와 public 을 선언하는 방법

_ (언더스코어) 키워드를 통해서 private 로 선언한다.

```dart
class Person {
 int age;
 int name;
 String _address;

 String _changeAddress() {}
}
```

### private field

Dart 클래스에서 private field 를 선언하는 방법

변수명 앞에 `_` 를 붙여준다.

```dart
String _address;
```

### private method

Dart 클래스에서 private method 를 선언하는 방법

메소드 명 앞에 `_` 를 붙여준다

```dart
String _changeAddress() {}
```

## 클래스에 대한 엑세스 제어

함수, 변수와 동일한 규칙을 가짐

```dart
class A {}

class _B {}
```

# getter 와 setter

메소드를 경우하여 필드를 조작함

- **getter** : 읽기 전용 프로퍼티를 구현할 때 사용
- **setter** : 쓰기 전용 프로퍼티를 구현 할 때 사용 (잘 사용하지 않음)

```dart
class Person {
 int age;
 int name;
 String _address;

 String _changeAddress() {}

 int get address {
  return _address;
 }

 void set address(String newAddress) {
  _address = newAddress;
 }
}
```

## getter 메소드

```dart
int get address {
 return _address;
}
// 람다식으로 표현 가능 int get address => _address
```

## setter 메소드

```dart
void set address(String newAddress) {
 _address = newAddress;
}
```

## getter setter 의 메리트

1. Read Only, Write Only 필드의 실현
2. 필드의 이름 등, 클래스의 내부 설계를 자유롭게 변경 가능
3. 필드로의 엑세스를 검사 가능

---

# 정리

캡슐화의 개요

- 캡슐화를 하여 멤버나 클래스로의 접근을 제어 할 수 있음
- 특히, 필드에 "현실세계에서 불가능한 값" 이 들어가지 않도록 제어

멤버에 대한 접근 지정

- private 멤버는, 동일 파일 내에서만 접근 가능
- public 멤버는 모든 클래스에서 접근 가능

클래스에 대한 접근 지정

- 함수, 변수와 동일한 규칙
