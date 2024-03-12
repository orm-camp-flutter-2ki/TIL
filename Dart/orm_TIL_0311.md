240311

플러터 과정 6일차


test 코드
-

테스트 코드를 할 때 기본 코드
```dart
import 'package:test/test.dart';

void main() {
  test( 'testCode', () {
    // 여기에 코드를 작성
  });
}
```

test 코드는 given > when > then 기법을 사용한다.
expect() 함수를 활용하여 결과를 검증한다.

## 캡슐화 encapsuation
> 클래스나 인스턴스를 이용하여 현실세계를 객체 지향 프로그램으로 자유롭게 개발 할 수 있게 되었다. 하지만 실수로 속성을 덮어 쓰거나,
잘못된 조작하는 등의 휴먼 에러(human error)를 완전히 없앨 수는 없다. 그래서 dart에 캡슐화라는 것이 있다.

멤버에 대한 엑세스 제어
#### 접근 지정자(access modifier)
| 제한범위 | 명칭 | 설정 방법 | 접근 가능한 범위 |
| --- | --- | --- | --- |
| 제한이 엄격 | private | 멤버 앞에 _ 붙이기 | 자기 자신의 클래스 |
| 제한이 느슨 | public | 기본 값 | 모든 클래스 |

_ <= 언더 바, 언더 스코어

받을 때 _hp : hp

프로퍼티 개념
필드에 있는 항목들을 프로퍼니라고 한다. ' _ ' 붙인 항목들에 한에서

## getter 와 setter

##### getter 쓰는 법
```dart
int get hp => _hp();
or
int get hp{
  return _hp;
  }
```
안의 변수와 바깥의 변수를 지정 할 수 있다.

###### setter 쓰는 법
```dart
void set hp(int value){
  _hp = value;
}
```
숨긴 언어에 값을 부여할 수 있다.

위의 getter와 setter의 메리트
1. read only, write only 필드의 실현
2. 필드의 이름 등, 클래스 내부 설계를 자유롭게 가능

캡슐화 -> 은닉화

## 컬랙션

array 배열 행렬 메모리 저장 구

list : 순서 대로  쌓여있는 구조( 아이템의 중복 허용)

map : 키(key)와 값( value)의 쌍으로 저장(키의 중복 불가)

set : 순서가 없는 집합( 중복 불가)
