# test code
- 코드가 올바르게 작동하는지 확인기 위한 것이다.
<br/>

## test 종류
- 유닛 테스트 (Unit test)
- 위젯 테스트 (Component test)
- 통합 테스트 (Integration and end-to-end test)
<br/>

## 기본 테스트 프레임워크
[Dart-testing](https://dart.dev/guides/testing)

### 0. test code 작성
- 여러가지의 테스트 기법 중 밑의 기법을 사용한다.  
> 준비(given) -> 실행(when) -> 검증(then)
```dart
void main() {
  test('cleric test', () {
    // 준비 given
    Cleric cleric = Cleric('지존법사', hp: 70, mp: 10);
    
    // 실행 when
    cleric.pray(3);
    
    // 검증 then
    expect(cleric.mp, equals(20));
  });
}
```
<br/>

### 1. test directory
- 없다면 만들어 준다. 일반적인 directory를 만드는 방법과 똑같다. 이름은 'test'로 생성한다.    
- test directory는 아이콘이 조금 다르다.  
![image](https://github.com/yujiyeong/TIL/assets/149862753/913f95a2-a198-414c-8434-9d93b590b0b4)
<br/>

### 1-1. test file
- 테스트 할 파일이 있는 경로와 같은 경로로 만들어 준다.  
- 파일명은 '[테스트할 파일과 동일한 이름]_test'로, 항상 `test`로 끝나야 한다.  
![image](https://github.com/yujiyeong/TIL/assets/149862753/6d75ad6a-67ab-4faf-8125-bdcd94ff4f3b)
<br/>

### 2. test package
- main 함수에 test를 입력하면 함수 밖에 자동으로 import 된다.  
- 만약 자동 생성이 되지 않는다면 밑의 코드를 수기로 작성해준다.  
```dart
import 'package:test/test.dart';
```
- 수기로 작성했을 때 에러가 난다면 [pubspec.yaml] 파일을 열어 'dev_dependencies'에 'test'가 있는지 확인해본다.  
![image](https://github.com/yujiyeong/TIL/assets/149862753/2888906b-c7f5-4d16-99d3-0f9330cbed14)
- 그래도 에러가 난다면 Android Studio를 완전히 종료 후 재실행 해본다.
<br/>

### 3. test()와 expect
- main 함수에 작성 해야한다.  
```dart
import 'package:test/expect.dart';
import 'package:test/scaffolding.dart';

void main() {
  test('테스트 할 내용', () {
    // 테스트 할 코드 작성
    print('this is just test');
    
    // 테스트 실행값(actual)과 예상값(expected)이 매치하는지 확인
    expect(actual, matcher);
  });
}
```
- test() : 테스트를 할 때 사용하는 함수
- expect() : 실행값과 예상값을 비교하는 함수
<br/>
