# Object 의 기본 기능
- 모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다.
- Object 타입 변수에는 모든 인스턴스를 대입할 수 있다.
## Object 클래스의 대표 메소드 및 프로퍼티
  ```
  1. toString() : String type 을 얻는다.
  2. operater== : 비교
  3. hashCode : 해시값을 얻는다.
  ```
## 비교연산자 == 재정의
  ```
  @overridd
  bool operator ==(Object other) =>
    identical(this, other) ||
    other is Book && runtimeType == other.runtimeType && title == other.title;
  ```
- runtimeType 과 title 을 비교하여 boolean 값을 리턴
- String, int type 은 이미 동등석 비교 규칙이 작성되어 있다.

## hashCode
- 모든 객체는 해시값을 갖는다.
- 동일한 객체는 항상 같은 해시값을 갖는다.
- Set, Map 은 요소를 검색할 때 빠른 이유 -> hashCode 를 사용하기 때문

## sort() -> List 를 정렬해주는 메소드
- sort 메소드를 사용하기 위한 조건 (2가지 중 하나만 만족해도 된다.)
  1. 정렬 대상이 Comparable interface 를 구현할 것
  2. 직접 정렬 대상의 정렬 규칙을 Comparator 함수로 구현할 것
- defalut 는 오름차순이지만 내림차순으로 만들고 싶다면 * -1 을 하면 된다.

## deep copy
- dart 에서는 깊은 복사를 지원해주지 않는다.
- 따라서 직접 만들어야 한다
- 우린 copyWith() 을 만들어서 복사했다.
  ![deepshallow](https://github.com/philiplee25/TIL/assets/76925432/69fd06d7-20bc-4a85-b6b4-3c491e2363bd)
