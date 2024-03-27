# test technique
## 대략적인 테스트 코드 구조
```dart
import 'package:test/expect.dart';
import 'package:test/scaffolding.dart';

void main() {
  group('테스트 그룹', () {
    test('테스트 할 내용', () {
      // 테스트 할 코드 작성
      expect(actual, matcher); // 테스트 실행값(actual)과 예상값(expected)이 매치하는지 확인
    });
  });
}
```
<br/>

## setUp()
- 테스트 시작 시, 매번 세팅되는 코드
```dart
setUp(() {
    // 매번 세팅할 코드 내용 작성
    File('$/test.txt').writeAsStringSync('hello dart'); // 파일 생성 후, 덮어쓰기
  });
```
<br/>

## tearDown()
- 테스트 종료 시, 매번 세팅되는 코드
```dart
tearDown(() {
    // 매번 세팅할 코드 내용 작성
    File('test.txt').deleteSync(); // 파일 삭제
```
<br/>

## group()
- 테스트를 그룹화하여 특정 주제나 기능에 대한 테스트를 함께 묶어서 실행할 수 있는 기능을 제공
- 하위 테스트 그룹 또는 개별 테스트를 정의할 수 있음  
- 테스트 코드를 조직화하고 관리할 수 있음
```dart
void main () {
  group('palindrome', () {
    // 여기에 선언된 변수와 메서드는 그룹 내 test들이 공유한다...
    String text;

    test('회문 문자열 넣었을 때', () {
      text = 'Was it a car or a cat I saw';
      expect(palindromeCheck(text), true);
    });

    test('회문이 아닌 문자열을 넣었을 때', () {
      text = 'i love cat';
      expect(palindromeCheck('i love cat'), false);
    });
  });
}
```
<br/>

### group에 async?
- group 생성 시 async를 붙이면 에러가 난다. 필요하다면 test 마다 붙여주자.
```dart
void main() async {
// (...)

// group('bank ', () { // 정상 코드
  group('bank ', () async { 
    test('jsonDecode test', () async {
      final List json = await jsonDecode(bankDataFile);
      json.map((e) => Bank.fromJson(e)).toList();

      expect(DeepCollectionEquality().equals(json, expectedList), true);
    });

// (...)
```
- console
```dart
Failed to load "/Users/yong/Desktop/learn_dart_together/test/0327/model/bank_test.dart": Invalid argument(s): Groups may not be async.
```
<br/>

## test()
- 개별적인 테스트 케이스를 정의할 때 사용
- 테스트 케이스는 실제로 코드 조각을 실행하고 예상 결과와 실제 결과를 비교하여 테스트를 수행
```dart
test('들어간 수 > 0 일 때', () {
      expect(compareNumber([1, 5, 7, 3, 9]), 16);
    });
    test('들어간 수 < 0 일 때', () {
      expect(compareNumber([0, -5, -1, -8, -4, -9]), -1);
    });
```
<br/>

## expect()
- 실제 결과를 예상 결과와 비교하는 함수  
- 테스트 케이스 안에서 사용
- 특정 조건이나 동작을 확인하기 위해 사용
### 실제값과 기댓값 일치 여부로 확인
```dart
void main() {
  test('factorial 양의 수', () {
    expect(factorial(1), 1); // 값 일치 하는지로 확인
  });
```
```dart
void main() {
  test('min transactions', () {
    final expectedResult = 300;
    final actualResult = transactions.map((e) => e.value).min;

    expect(actualResult, expectedResult); // 값 일치 하는지로 확인
  });
}
```
<br/>

### bool true/false 값으로 확인
```dart
void main() {
  test('factorial 양의 수', () {
    expect(factorial(5) == 120, true); // T/F로 확인
  });
```
<br/>

### 예외처리 유/무로 확인
```dart
  test('factorial 0 & 음의 수', () {
    expect(() => factorial(3), returnsNormally); // 예외 처리 없는지
    expect(() => factorial(-4), throwsException); // 예외 처리 있는지
  });
}
```
<br/>

