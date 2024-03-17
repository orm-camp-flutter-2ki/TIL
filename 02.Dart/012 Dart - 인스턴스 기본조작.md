---
title: 012 Dart - 인스턴스 기본조작
author: Kim Donghyeok
created_at: 2024-03-15
updated_at: 2024-03-15
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# Obejct 클래스

1. 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다.
2. Object 타입 변수에는 모든 인스턴스를 대입할 수 있다.

## Object 의 메서드 프로퍼티

- toString() : 문자열 표현을 얻음
- operator == : 비교
- hashCode : 해시 값을 얻음

## `toString`

어떠한 객체의 정보를 출력하는 메소드

Object를 상속한 클래스에서 toString를 재정의 하여 출력결과를 바꿀 수 있다.

```dart
@override  
String toString() {  
  return 'Person{name: $name, age: $age}';  
}
```

## == 연산자 재정의

객체 사이의 == 연산자는 참조를 비교함  -> 메모리 주소를 비교

== 연산자를 재정의 하여 나만의 동등성 규칙을 정의할 수 있다.

```dart
@override  
bool operator ==(Object other) =>  
    identical(this, other) ||  
      other is Person &&  
      runtimeType == other.runtimeType &&  
      name == other.name;

@override  
int get hashCode => name.hashCode;
```

> 동등성 연산자를 재정의 할 때 기본적으로 모든 레퍼런스의 동등함을 비교해야 함  
> 클래스내부에 클래스 참조변수로 선언된 필드도 해당 클래스 내부에 비교 연산자가 정의 되어있어야 한다.  

## Set, Map 의 동작 원리

Set, Map 계열은 요소를 검색할 때  hashCode 를 사용하여 빠르다. List 는 순차검색이라 느림

1. 모든 객체는 해시값을 가진다.
2. 동일한 객체는 항상 같은 해시값을 가진다.

## 리스트에서 요소 정렬

List.sort() 메서드는 컬렉션 내부를 정렬해줌

```dart
final names = ['Seth', 'Kathy', 'Lars'];
names.sort((a, b) => a.compaerTo(b));

print(names);
```

하지만 sort() 메서드를 사용하기 위해서는 다음과 같은 제약이 따름

1. 정렬대상이 Comparable 인터페이스를 구현
2. sort 함수가 직접 정렬대상의 정렬규칙을 comparator 함수 로 구현해야함

### Comparator

![[240315_instance_compare.png]]

## 인스턴스의 복사

Dart 에서는 인스턴스의 깊은 복사를 별도로 지원하지 않음

직접 복사를 구현해서 사용

```dart
Person origianl = Person(name: '김가네', age: 40);

Person clone1 = original.coyWith();
Person clone1 = original.coyWith(age: 20);
```

```dart
Person copyWith({String? name, int? age}) {
 return Person(
  name: name ?? this.name,
  age: this.age ?? age,
 )
}
```
