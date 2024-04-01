# Result

## 에러처리의 기본

- 기본적으로 예외는 try - catch 를 활용하여 처리 한다.
- 런타임 에러 뿐만 아니라 논리적인 오류나 예외 상황에 대한 처리를 하기에는 부족하다
- Result 패턴은 성공, 실패시 처리에 유용한 패턴이다

## 성공과 실패 중 하나를 리턴하는 Result 클래스 예시

- Result 클래스는 성공시에는 데이터를, 실패시에는 Exception(또는 String)을 담는 객체를 정의한다
- 이 외에도 더 많은 반환 케이스가 필요하면 추가하면 된다.


## Result 패턴 사용시 효과
- enum 과 동일하게 switch 문과 조합하여 모든 처리를 강제할 수 있다
- 여러가지 3개 이상의 성공과 실패를 처리할 있다

## freezed 라이브러리
- 자동 기본 함수 완성 라이브러리
- freezed = json_serializable + Equatable + Immutable 합친 느낌

<설치>
dart pub add freezed_annotation
dart pub add dev:build_runner
dart pub add dev:freezed
// fromJson(), toJson()
dart pub add json_annotation
dart pub add dev:json_serializable

## Result 방법
1. 매개변수를 하나로 -> Exception만 처리가능
2. 매개변수를 두개로 -> 원하는 에러타입 처리 가능

--생각--
- Result를 쓰는 이유
1.  try-catch 문보다 더 많은 케이스를 처리하기 좋다
2.  enum 의 효과를 가진다. ( 모든 처리를 강제 )
- 라이브러리
1. 라이브러리를 이용하면 양식을 가지고 기계적인 코드구성들을 자동으로 해줄 수 있다.



