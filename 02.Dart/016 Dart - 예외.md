---
title: 016 Dart - 예외
author: Kim Donghyeok
created_at: 2024-03-19
updated_at: 2024-03-19
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 예외 (Exception)

프로그램을 설계할 때 실행 시에  예외  상황이 발생할 가능 성이 있는 것을 예측하여 사전에 예외처리가 되도록 할 필요가 있음

## 에러의 종류와 대응책

1. 문법에러
2. 실행 시 에러
3. 논리 에러

## 에러 상황별 처리

|             | syntax error                | runtime error                                   | logic error                             |
| ----------- | --------------------------- | ----------------------------------------------- | --------------------------------------- |
| 원인        | 코드의 형식적 오류          | 실행중에 예상외의 사태가 발생하여 동작이 중지됨 | 기술한 처리 내용에 논맂거인 오류가 있음 |
| 알아채는 법 | 컴파일 하면 에러 발생       | 실행하면 도중에 강제로 종료 됨                  | 실행 하면 예상외의 값이 나옴            |
| 해결방법    | 컴파일러의 지적의 보고 수정 | 에러                                            | 원인을 스스로 찾아서 해야 함            |

## 예외적인 상황들

- 메모리 부족
- 파일을 찾을 수 없음
- 네트워크 통신 불가 등

## 예외 처리의 흐름

### try-catch 구문

```dart
try {
 // 에러가 날 것 같은 코드 작성
} catch (e) {
 // e : 에러의 정보를 담고 있는 객체
}
```

### Exception 발생

```dart
throw runtimeException('에러메세지');
```

### try-catch 문으로 Exception 계열 예외를 처리

```dart
try {
 someError();
} catch (e) {
 print(e);
}

void someError() {
 throw FormatException('에러가 발생했습니다');
}
```

### rethrow 로 에러처리를 미룸

여러 단계에 걸쳐서 함수가 중첩되어 있을 때, 발생한 예외에 대해서 현재 단계의 코드에서 처리하는 것이 아닌 상위에서 에러를 처리하고자 할 때 `rethrow` 를 사용하여 다음 try-catch 로 처리를 지연

```dart
void main() {
 try {
  someError2();
 } catch (e) {
  print(e);
 }
}

void someError() {
 throw FormatException('에러가 발생했습니다');
}

void someError2() {
try {
 someError();
} catch (e) {
 rethrow;
}
}
```

### 특정 예외를 캐치

`on`  키워드로 해당하는 예외가 발생 했을 때 처리

```dart
try {
 someError2();
} on  FormatException {
 print('formatException 이 발생 했습니다.');
}
```

### finally로 예외처리 이후 작업 실행

try-catch 이후에 항상 실행자고자 하는 코드는 finally 에서 처리

```dart
try {
 someError2();
} on  FormatException {
 print('formatException 이 발생 했습니다.');
} finally {
 print('무조건 실행되는 코드');
}
```

## 오리지널 예외 클래스 정의

```dart
class UnsupportedMusicFileExcpetion implements Exception {
 final String? _message;

 UnsupportedMusicFileExcpetion([this._message]);

 String toString() {
  if(_message == null ) return 'UnsupportedMusicFileExcpetion';
  return 'UnsupportedMusicFileExcpetion: $_message';
 }
}
```

---

# 정리

에러

- syntax error, runtime error, logic error 의 3종류
- 예외처리를 할 때는, runtime error를 대처한다

예외의 종류

- API에는 여러가지 예외적 상황을 표현하는 예외 클래스가 준비되어 있다.
- 예외 클래스를 상속하여 오리지날 예외 클래스를 정의할 수 있다.

예외 처리

- try-catch 문을 사용하면, try 블록 내에 예외가 발생했을 때 catch 블록에서 처리가 옮겨진다
- finally 블록으로 나중에 꼭 해야하는 처리를 할 수 있다
- throw 문을 사용하면 임의로 예외를 발생시킬 수 있다
