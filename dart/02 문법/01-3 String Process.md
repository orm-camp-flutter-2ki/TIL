# 문자열 String
[스트링 클래스 공식문서](https://api.dart.dev/stable/3.0.2/dart-core/String-class.html)
- 문자열(String)은 불변(immutable)한 데이터 타입으로, 한번 생성된 문자열은 수정할 수 없다.
문자열에 어떤 변경이 가해지면 새로운 문자열이 생성되고, 그 값을 새로운 메모리에 할당하는 것이다.
즉, 원래의 문자열은 변경되지 않고 그대로 유지되고, 가비지 컬렉터가 청소한다.  

> String을 통해 선언하면 문자열을 담을 수 있는 접시가 생기는 것이다. 음식을 계속 바꿔가며 담을 수 있다.
> 원래 음식은 먹거나 버리는 등 다른 곳으로 보내고(?) 새 음식을 넣을 수 있다. 그렇지만 원래 음식은 없어지는게 아니라 내 뱃속이나 쓰레기 통 속에 있는 것...
> 이렇게 이해했는데 맞는지는 모르겠다...  
<br/>

# 문자열 처리   
## ⏰ .stopwatch
- 코드의 성능을 측정할 수 있다.  
```dart
final stopwatch = Stopwatch()..start();
// 코드가 실행되는 동안의 시간...
print(stopwatch.elapsed);
```
### 성능 테스트
**test1: new**
```dart
  final stopwatch1 = Stopwatch()..start();
  var test1 = '';
  for (int i = 0; i < 100000; i++) {
    test1 += i.toString();
  }
  print(stopwatch1.elapsed);
```
```dart
0:00:04.124108
```
**test2: buffer**
```dart
  final stopwatch2 = Stopwatch()..start();
  var test2 = StringBuffer('');
  for (int i = 0; i < 100000; i++) {
    test2.write(i.toString());
  }
```
```dart
0:00:00.008062
```
<br/>

## 💬 ..(cascade)
- void 리턴인 함수 앞에 사용하면 해당 객체의 레퍼런스를 반환하여 메서드 체인을 사용할 수 있다.
```dart
  final buffer = StringBuffer('Cat');

  buffer
    ..write(' is')
    ..write(' so cute');

  print(buffer.toString()); // 'Cat is so cute'
  print(buffer); // 'Cat is so cute'
```
<br/>

## ➕ 결합
### ${수식}
- dart에서는 `+`보다는 `$`을 활용하여 문자열을 결합한다.  
```dart
String name = 'yongyong';
int age = 5;
String text = '$name의 나이는 ${age + 1}살 입니다.';
// 출력
// yongyong의 나이는 6살 입니다.
```
### buffer
- 결합한 결과를 내부 메모리(buffer)에 담아두고 toString()으로 결과를 업음
<br/>

## ✂️ 자르기
### .substring(a, b)
- 인덱스 a에서 b 앞까지 자른다.
```dart
  const String intro = 'HELLO';
  print(intro.substring(0,2)); // 'HE'
  print(intro); // 'HELLO'
```
### .trim()
```dart
  const String intro = '    HELLO           ';
  print(intro.trim()); // 'HELLO'
```
<br/>

## 💱 치환
### .replaceAll(a, b)
```dart
  const String intro = 'HELLO';
  print(intro.replaceAll('LL', 'XX')); // HEXXO
  print(intro); // HELLO
```
### .toLowerCase() / .toUpperCase()
```dart
// 대문자 -> 소문자
  const String intro = 'HELLO';
  print(intro.toLowerCase()); // 'hello'
  print(intro); // HELLO

// 소문자 -> 대문자
  const String intro2 = 'hello';
  print(intro2.toUpperCase()); // 'HELLO'
  print(intro2); // hello
```
<br/>

## 👐 분리
### .split()
```dart
  final String numList = '1,2,3';
  final split = numList.split(',');

  for (var element in split) {print(element);} //'1', '2', '3'
  // split.forEach((element) {print(element);});
  print(numList); // '1,2,3'
```
<br/>

## 🔎 검색
### .indexOf()
```dart
  const String intro = 'HELLO';
  print(intro.indexOf('E')); // 1
  print(intro); // HELLO
```
### .lastIndexOf() 
```dart
  const String intro = 'HELLO';
  print(intro.lastIndexOf('L')); // 3
  print(intro); // HELLO
```
### .contains() : 포함
```dart
  const String intro = 'HELLO';
  print(intro.contains('O')); // true
```
### .endsWith() : 끝나는 단어 매치
<br/>

## 🧑🏻‍⚖️ 비교
### == operator
```dart
  const String intro = 'HELLO';
  const String intro2 = 'hello';

  print(intro == intro2); // false
  print(intro == intro2.toUpperCase()); // true

  print(intro2); // 'hello'
```
<br/>

## 📏 길이
### .length
```dart
  const String intro = 'HELLO';
  print(intro.length); // 5
  print(intro); // 'HELLO'
```
### .isEmpty
```dart
  const String intro = 'HELLO';
  print(intro.isEmpty); // false
  print(intro); // 'HELLO'
```
<br/>




