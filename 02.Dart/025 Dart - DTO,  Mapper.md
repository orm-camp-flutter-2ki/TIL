---
title: 025 Dart - DTO, Mapper
author: Kim Donghyeok
created_at: 2024-03-28
updated_at: 2024-03-28
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

> 동적 JSON 과 같은 데이터 소스는 모델로 변경하기가 어렵다
> 서버에서 데이터를 잘못 보내는 경우도 존재

> ```dart
> [
>     {
>         "id": “1”,
>         "type": "article",
>         "title": "This is an article",
>         "content": "This is the content of the article.",
>         “created_at”: “2020-01-01”
>     },
>     {
>         "id": 2,
>         "type": null,
>         "url": "https://example.com/image.jpg",
>         "caption": "This is an image.",
>         “created_at”: “2020-02-02”
>     },
>     {
>         "id": 3,
>         "url": "https://example.com/video.mp4",
>         "caption": "This is a video.",
>         “created_at”: “2020-03-03”
>     }
> ]
>```

# DTO

DTO : Data Tranfer Object

데이터 소스를 모델 클래스로 변환하는 과정에서 **순수**하게 클래스에 담기 위한 중간 전달 객체

JSON -> DTO -> Model Class

> **데이터 소스에 잘못된 값이 포함되어있더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단**

## DTO가 모델클래스와 다른 점

  **모든 필드가 Nullable 변수**
  
 **직렬화, 역직렬화 제공**

> 즉, JSON 데이터를 무조건적으로 받아들인다.  
> 기존 모델 클래스를 DTO 가 대체  

> **DTO는 필드, 생성자, fromJson(), toJson() 을 선언한 후 내부에 추가적인 메소드나 생성자를 구현하지 않는다**

# Mapper

순수한 데이터 소스 (DTO) 를 원하는 모델 클래스로 변환하려면 fromJson(), toJson() 처럼 변환 기능이 필요함

**→ Dart의 extension 을 활용하여 DTO를 Model Class 로 변환하는 기능을 추가해준다.**

# DTO 가 필요한 이유

- Model Class 는 non-nullable 한 값만 가지고 있도록 함
- JSON 데이터는 null 값을 포함 시킬 수 있음
- Map -> Model Class 변환 시 null 값 등의 예외를 사전에 걸러내기 용이함
- 불완전한 코드가 포함 될 것 같다면 DTO 를 도입하자
- JSON 값에 예외가 없다면 반드시 DTO 를 도입 할 필요는 없다.

---

# 정리

기존 Model Class 는 DTO와 Model Class 의 역할을 모두 가지는 클래스였음

→ `fromJson()`, `toJson()`, `== operator`, `hashCode`, `toString()`, `copyWith()`

DTO가 도입 된다면 역할 분담이 가능함.

- DTO : `fromJson()`, `toJson()`
- Model Class : 불변 객체 + `== operator`, `hashCode`, `toString()`, `copyWith()`
