# 📖 Null Safety
<br>

## 📄 Null 이란?


- null : 값이 존재하지 않는다는 뜻
- dart 2.12 버전부터 지원
```dart
String string = null;// eroor

String? string = null;// OK
```
- String과 String?은 타입이 다름
<br>
<br>

## 📄 null 처리에 관한 기능


### ✏️ ?? 연산자
```dart
int value = nullableValue ?? 0;
```
- 앞의 객체가 null인 경우 ?? 뒤에 작성한 값으로 반환
<br>


### ✏️ ! 연산자
```dart
int? nullablevalue = 10;

int value = nullablevalue!;
```
- ! nullavle 인 값을 null이 아님을 보증
- 개발자에게 책임이 따르므로 주의해서 사용해야 함
<br>

### ✏️ ?. 연산자
```dart 
int? nullableValue = 10;

print(nullableValue?.toString()); // 10 출력

  

int? nullableValue = null;

print(nullableValue?.toString()); // null 출력
```
- ?. nullable 객체를 안전하게 사용하고자 할 때 사용
- 최대한 안 쓰는 게 좋음
<br>
<br>

## 📄 Null Safety의 장점과 주의점


### ✏️ 장점
- 널을 허용하지 않는 변수는 널이 아님을 100% 보장
- 개발자의 실수를 미연에 방지할 수 있음
- 항상 예측 가능한 코딩을 할 수 있음
- 컴파일러가 변수의 널 검사를 진행하지 않아도 돼 컴파일 속도가 향상됨
<br>

### ✏️ 주의점
- 사용 중인 외부 라이브러리도 모두 널 안정성을 지원해야 함
- ?, !, ?., late 등의 새로운 연산자나 키워드는 초보자에게 어렵게 느껴질 수 있음
- 사용 중인 프로젝트에 갑자기 컴파일 에러가 발생할 수 있고, 수정하기 위한 추가작업이 필

