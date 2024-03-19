---
title: 018 Dart - 여러가지 데이터 형식
author: Kim Donghyeok
created_at: 2024-03-19
updated_at: 2024-03-19
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 다양한 데이터 형식

## CSV(Comma-Separated Values)

- 데이터를 콤마로 나눈 형식
- csv 라이브러리 활용 <https://pub.dev/packages/csv>

```
String str = "홍길동,한석봉,신사임당";
```

## Property 형식의 파일 읽기

- Properties 클래스를 사용하여 키와 값 쌍의 읽고 쓰기가 가능
- properties 라이브러리 활용 <https://pub.dev/packages/properties>

## XML(Extensible Markup Language) 형식

- <> 태그를 활용한 기술 방식
- 포함관계를 기술 할 수 있음
- xml parser 라이브러리 활용 <https://pub.dev/packages/xml_parser>

## JSON(JavaScript Object Notation) 형식

- 네트워크 통신에서 가장 많이 사용되고 있음
- XML에 비해 적은 용량
- `[]` 로 리스트, `{}` 로 객체를 표현
- key : value 형태
- Dart의 Map<String, dynamic> 과 똑같이 생김

# 직렬화

- 데이터 구조나 객체 상태를 저장하고, 나중에 재구성 할 수 있는 포맷으로 변환하는 과정
- 객체를 파일의 형태 등으로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정을 의미
- **클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리를 해줘야 함**

![[240319_serialization_deserialization.png]](/02.Dart/_resources/240319_serialization_deserialization.png)

## Dart의 직렬화와 역직렬화

> 직렬화 : 클래스 -> JSON
>
> 역직렬화 : JSON -> 클래스

```dart
final json = {
 "name": "Jons Doe",
 "email": "John@Doe.com"
};

print(json.runtimeType);
```

### 직렬화 (Serialization)

`Map<String, dynamic>` 형태로 선언된 컬렉션을 `jsonEncode()` 메소드를 통해 json 형식의 String 으로 변환

```dart
Map<String, dynamic> json = {"name": "John Doe", "email": "john@doe.com"};
String jsonString = jsonEncode(json);
```

### 역직렬화 (Deserialization)

json 형식의 String 을 `jsonDecode()` 메소드를 통해 `Map<String, dynamic>` 형태로 역직렬화

```dart
String jsonString = '{"name": "John Doe", "email": "john@doe.com"}';
Map<String, dynamic> json = jsonDecode(jsonString);
```
