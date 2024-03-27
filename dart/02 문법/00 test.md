# test
- [[🔗 유닛 테스트 작성방법]](https://yozm.wishket.com/magazine/detail/2483/)  
- 코드가 의도대로 작동하는지 확인하기 위한 것이다.
<br/>

## 테스트를 하는 방법들
- 수동 테스트 : 인간이 하는 테스트 (print)
- 단위 테스트 : 1개의 함수를 테스트 (test 코드)
- 통합 테스트 : 여러개 연관된 클래스나 함수를 함께 테스트 (UI test, Integration test)
<br/>

## test 종류
### 유닛 테스트 (Unit test)
- 새로운 기능을 추가하거나 기존 기능을 변경해도 의도한 대로 작동하는지...  
- 특정 모듈이 의도한 대로 잘 작동하는가를 테스트하는 가장 작은 단위의 테스트  
- 모듈 = 메서드, 기능  
### 위젯 테스트 (Component test)
### 통합 테스트 (Integration and end-to-end test)
<br/>

## 테스트 방법론
### 블랙박스 테스트
- 소프트웨어의 내부 구조를 무시하고 기능을 테스트하는 방법
- 시스템이 어떻게 동작하는지에 대한 내부 정보를 알 필요 없이 사용자 관점에서 테스트
- 테스트 케이스는 입력 값과 예상 출력 값에 기반하여 설계
- 요구 사항을 충족하는지 확인하고, 시스템의 기능적 및 비기능적 요구 사항을 테스트
- 주요 기법으로는 등가 분할, 경계 값 분석, 상태 전이 테스트 등이 있다
<br/>

### 화이트박스 테스트
- 내부 구조와 동작에 중점을 두고 테스트하는 방법
- 코드의 내부 로직, 제어 흐름, 데이터 흐름 등을 이해하고 검증하는 데에 사용
- 테스트 케이스를 설계할 때 코드의 특정 부분을 직접 확인
- 주요 기법으로는 구문 검사, 경로 검사, 조건/분기 검사 등이 있다
<br/>

### 테스트 케이스
> 동등 분할, 경계값 분석 등의 기법이 있음
- 가능한 모든 가능성의 범위를 테스트하는 것이 좋은 테스트 케이스
<br/>

## 기본 테스트 프레임워크
[[🔗 Dart - testing guides]](https://dart.dev/guides/testing)

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
<br/>는 함수
- expect() : 실행값과 예상값을 비교하는 함수
<br/>
