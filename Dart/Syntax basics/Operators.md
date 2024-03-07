# Variables

Dart에만 있는 혹은 특별한 연산자만 정리

<br/>

## Conditional expressions
Dart에서 if는 식이 아닌 구문이다.  
대신 if를 대신할 수 있는 연산자를 제공한다.

### [조건식] ? [참일 때 반환 값] : [거짓일 때 반환 값]
if와 동일한 조건식이지만 값을 할당할 수 있다는 차이가 있다.  
`var visibility = isPublic ? 'public' : 'private';`

<br/>

### [nullable] ?? [null일 경우 대체할 값]
nullable한 값을 손쉽게 처리할 수 있게 해준다.  
`String input = stdin.readLineSync() ?? ""`

<br/>

## Cascade notation 
`..` non-nullable한 객체에 대한 cascade   
`?..` nullable한 객체에 대한 cascade  
casecade를 통해 동일한 객체에 대한 일련의 연산과 메서드 호출을 간편하게 처리할 수 있다. (마치 빌더패턴처럼)

단, `void`에 대해 사용할 수 없으며, cascade는 연산자(operator)가 아닌 Dart의 문법적 편의 기능이다.

### 예시
```dart
var paint = Paint();
paint.color = Colors.black;
paint.strokeCap = StrokeCap.round;
paint.strokeWidth = 5.0;
```
위의 코드는 아래와 같다.
```dart
var paint = Paint()
  ..color = Colors.black
  ..strokeCap = StrokeCap.round
  ..strokeWidth = 5.0;
```
또한, cascade는 중첩시킬 수 있다.
```dart
final addressBook = (AddressBookBuilder()
      ..name = 'jenny'
      ..email = 'jenny@example.com'
      ..phone = (PhoneNumberBuilder()
            ..number = '415-555-0100'
            ..label = 'home')
          .build())
    .build();
```