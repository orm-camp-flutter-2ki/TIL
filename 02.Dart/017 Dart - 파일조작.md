---
title: 017 Dart - 파일조작
author: Kim Donghyeok
created_at: 2024-03-19
updated_at: 2024-03-19
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 파일 조작

## 파일 조작의 기본 순서

1. 파일을 연다.
2. 파일을 읽거나 쓴다
3. 파일을 닫는다.

## File 쓰기

File 클래스를 이용하여 파일읽어들이고 writeAsStringSync() 메소드로 파일에 write 한다.

```dart
File file = File('파일경로');

file.writeAsStringSync('Hello, world!);
```

## File 읽기

File 클래스를 이용하여 파일 읽어들이고 readAsStringSync() 메소드로 파일 내용을 read 한다.

```dart
File file = File('파일경로');

final text = file.readAsStringSync('Hello, world!);
```
