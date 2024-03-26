# Flutter TIL

Today I Learned about Flutter

오늘 학습한 내용을 정리하는 것


## Github

github와 IDE 연동

IDE에서 github로 커밋하기

## Dart

dart.dev 공식 문서로 기본 문법 학습

dart
-2011년 공개
-자바 대체어
-플러터 활용
-객체지향 + 함수형

기본 자료형

int(정수) - double(실수) - String(문자) - bool(논리)

문자열 포멧 = '문자열'

숫자
정수(int)
실수(double)
숫자(num)

형변환
자료형(int형, double형, String형 등)간의 변환

var 활용 타입 추론

final name = '정지원';
name <- 수정 불가

증감 연산자
뒤에++ -> num = 1
++앞에 -> num = 2

비교 연산자


형변환 as 위험

컴파일 = 사람 -> 기계어 번역

## 클래스

오브젝트 (object) : 현실 세계의 모든 객체

클래스 (class) : 오브젝트 -> 가상 구체화 (붕어빵 틀)

인스턴스 (instance) : 클래스를 -> 메모리 (붕어빵)

클래스명 : 명사 / 단어 맨 처음 대문자

필드명 : 명사 / 최초이외 단어 대문자 시작

메서드명 : 동사 / 최초이외 단어 대문자 시작

함수 : 단독 동작

메서드 : 클래스의 기능 

## 클래스 정의 효과

인스턴스 생성 가능

새로운 변수 타입 이용 가능

이용가능 타입의 종류 증가

인스턴스-클래스

인스턴스 =/= 클래스

가상 활동 = 인스턴스(=오브젝트)

인스턴스 생성 틀 = 클래스

## 필드-메서드

클래스 속성 = 필드
      동작 = 메서드
	 
final = 상수, 변경불가

## 레퍼런스? 참조 ?

Dart 에서는 타입 = 레퍼런스

ex.) int, double, String 등등 = 레퍼런스

## BSS vs Data

초기화 안된거 = BSS

초기화된 전역변수 & static 변수 할당 영역

##Heap

동적 할당 메모리 저장 <- 인스턴스가 여기에

## Stack

지역 & 매개 변수 저장소

## 캡슐화

캡슐화를 하여 멤버나 클래스로의 접근을 제어할 수 있음

특히, 필드에 “현실세계에서 불가능한 값"이 들어가지 않도록 제어

멤버에 대한 접근 지정

private 멤버는, 동일 파일내에서만 접근 가능

public 멤버는, 모든 클래스에서 접근 가능

클래스에 대한 접근 지정

함수, 변수와 동일한 규칙


## 컬렉션

List : 순서 대로 쌓여있는 구조 (아이템의 중복 허용)

Map : 키(key)와 값(value)의 쌍으로 저장 (키의 중복 불가)

Set : 순서가 없는 집합 (중복 불가)

## 상속의 기초

extends를 사용하여 기존 클래스를 기초로 하는 새로운 클래스를 정의 할 수 있다

부모 클래스의 멤버는 자동적으로 자식 클래스에 상속되므로, 자식 클래스에는 추가 된 부분만 기술 하면 된다

부모 클래스에 있는 메소드를, 자식 클래스에서 재작성 할 경우 이것을 오버라이드 한다고 한다

올바른 상속이란 “자식 클래스 is-a 부모 클래스"

상속에는 “추상적, 구체적" 관계에 있다는 것을 정의하는 역할도 있음

## 인스턴스

인스턴스는 내부에 부모클래스의 인스턴스를 가지는 다중구조를 가진다

보다 외측의 인스턴스에 속하는 메소드가 우선적으로 동작한다

외측의 인스턴스에 속하는 메소드는 super 을 사용하여 내측 인스턴스의 멤버에 접근할 수 있다

## 생성자 동작

다중구조의 인스턴스가 생성되는데, 자동적으로 가장 외측 인스턴스의 생성자가 호출 됨

모든 생성자는, “부모 인스턴스의 생성자"를 호출 할 필요가 있다

## 상속의 재료를 작성하는 개발자의 입장과 역할

다른 사람이 상속의 재료로 사용할 부모 클래스를 만드는 입장의 개발자도 존재 한다

미래의 개발자가 효율 좋게 안심하고 이용할 수 있는 상속의 재료를 작성하는 것이 그의 사명

## 추상 클래스

내용이 정의되지 않고 상세정의 미정인 메소드가 있는 클래스는 abstract 를 붙여서 추상메소드로 한다

추상 클래스는 인스턴스화 할 수 없다

추상 클래스와 추상 메소드를 활용한 상속의 재료로서의 부모클래스를 개발하면, 예기치 않은 인스턴스화나 오버라이드의 미 구현의 걱정이 없다

## 인터페이스

추상 클래스 중에, 기본적으로 추상메소드만 가지고 있는 것을 인터페이스 로서 특별 취급 한다

복수의 인터페이스를 부모로 두는 다중상속 효과가 가능

인터페이스를 부모로 두는 자식 클래스 정의에 implements 를 사용

interface 키워드는 Dart 3에 추가되었음


## 인스턴스를 애매하게 퉁치기

상속에 의한 is-a 관계가 성립한다면, 인스턴스를 부모 클래스 타입의 변수에 대입할 수 있다

부모 클래스 타입 변수에 대입하는 것으로, 퉁 칠 수 있음

## 상자의 타입 과 내용의 타입 의 역할

어떤 멤버를 이용할 수 있는가는 상자의 타입이 결정한다

멤버가 어떻게 움직이는지는 내용의 타입이 결정한다

## 취급 변경

as 키워드를 사용하여 타입 캐스팅을 수행한다

is 키워드를 사용하여 타입을 검사할 수 있다

## 다형성

같은 부모를 가지는 다른 인스턴스를 동일시하여, 부모 클래스 타입의 에 담을 수 있다

마찬가지로, 부모 클래스 타입의 인수나 리턴 값을 이용하여, 다른 클래스를 모아서 처리 가능

동일시 취급 해도, 각각의 인스턴스는 각 클래스의 정의를 따르고 다른 동작을 한다.

## Object 클래스의 기본 기능

모든 클래스는 Object 클래스의 메서드와 프로퍼티를 가지고 있다

Object 타입 변수에는 모든 인스턴스를 대입할 수 있다

## Object 클래스의 대표 메서드 및 프로퍼티

toString() : 문자열 표현을 얻음

operator == : 비교

hashCode : 해시값을 얻음

## toString()

오버라이드하여 원하는 결과를 얻도록 수정할 수 있음

## == 연산자 재정의 

== : 참조의 비교

== 연산자를 재정의 하여 나만의 동등성 규칙을 정의할 수 있다

## Set, Map 의 동작 원리

Set, Map 계열은 요소를 검색할 때 hashCode 를 사용하여 빠르다

List는 순차검색이라 느림

모든 객체는 해시값을 가진다

동일한 객체는 항상 같은 해시값을 가진다

## sort( ) 제약

정렬 대상이 Comparable 인터페이스를 구현

sort 함수가 직접 정렬 대상의 정렬 규칙을 Comparator 함수로 구현

## deep copy

Dart에서는 깊은 복사를 위한 별도의 기능 X

직접 작성해서 사용

## 타입이 없을 때 문제

1. 런타임 에러 발생 확률 상승
2. IDE가 컴파일 에러 확인 불가능

## 제네릭

타입을 나중에 원하는 형태로 정의 가능 = 타입 안저(type safe) 효과

## 열거형

정해 둔 값만 넣을 수 있는 타입

## 문자열 처리(검색)

1. contains() : 포함 관계
2. endsWith() : 끝나는 단어가 맞는지
3. indexOf() : 단어가 몇 번째에 있는지
4. lastIndexOf() : 뒤에서 몇 번째에 단어가 있는지

## 문자열 결합 방법

1. +연산
2. Srting interpolation
3. StringBuffer

## +연산자가 느린 이유

String 인스턴스는 불변 객체(immutable) 라서 느림

## 에러의 종류와 대응책

1. 문법(syntax) 에러
2. 실행(runtime) 시 에러
3. 논리(logic) 에러

## 문법(syntax) 에러

원인 : 코드의 형식적 오류

확인 : 컴파일

해결 : 컴파일러 지적사항 수정

## 실행(runtime) 시 에러

원인 : 실행 중 예상외의 사태 발생

확인 : 실행 도중 강제종료

해결 : 에러

## 논리(logic) 에러

원인 : 기술한 처리 내용의 논리 오류

확인 : 실행하면 예상외의 값 출력

해결 : 알아서

## 예외 처리

실행(runtime) 시 에러 대처법

1. try-catch 문을 사용 -> catch 블록에서 처리
2. finally 블록으로 나중에 꼭 해야하는 처리 실행
3. throw 문을 사용 -> 임의로 예외를 발생

## 파일 조작의 기본 순서

열기 -> 읽기/쓰기 -> 닫기

## 직렬화

1. 데이터 구조나 객체 상태를 저장하고 나중에 재구성할 수 있는 포맷으로 변환하는 과정

2. 객체를 파일의 형태 등으로 저장하거나, 통신하기 쉬운 포맷으로 변환하는 과정

3. 클래스 내부의 필드에 다른 클래스가 있다면 모두 직렬화 처리

## 디버깅

소프트웨어의 오류를 식별하고 수정하는 과정

SW가 올바르게 작동하는지 확인하는 데 필수

디버깅이 없으면 오류발생 확률 및 설계대로 작동하지 않을 가능성 상승

## 디버깅 기술

1. 로깅 = 코드가 실행되는 동안 발생하는 이벤트 기록

2. 브레이크 포인트 = 코드의 특정 지점에서 실행을 중지한는 데 사용

3. 디버거 = 디버깅을 쉽게 만들어주는 도구

4. 스택 추적 = 호출 스택을 추적해서 코드가 실행중인 위치 확인

## 디버깅 Tip

1. 작게 시작 = 작은 문제부터 한 가지 씩 집중

2. 단순하게 = 코드가 단순해야 오류의 원인 파악이 쉬움

3. 인내심 = 디버깅은 많은 시간이 소모되므로 인내심이 필요

## 함수형 프로그래밍

자료 처리를 수학적 함수의 계산으로 취급

가변 데이터를 멀리하는 특징

Dart는 객체지향(OOP)와 함수형(FP)의 특징을 모두 제공

## 고계 함수

함수를 파라미터로 받는 함수

1. where : 조건 필터링

2. map : 변환

3. forEach : 전체 뺑뺑이

4. reduce : 하나씩 줄이기

5. fold : 하나씩 접기

6. any : 있는지 없는지

## Named Parameters

{ } <- 를 사용하여 파라미터에 이름 붙이기 강제

## 파라미터 기본값 지정

= <- 를 사용하여 기본값 지정

## Optional positional parameter

[ ] <- 를 사용하여 위치를 지정하는 옵션 파라미터 사용

반드시 세번째에 device 설정/미설정 가능

default값 지정 가능

## 동기(sync) 프로그래밍

1. 순차적 코드 실행.
2. 작업이 완료될 때까지 프로그램이 중단될 수 없다.
3. 모든 작업은 이전 작업의 실행이 완료될 때까지 기다려야 한다.

## 비동기(async) 프로그래밍

1. 임의 순서 또는 동시 작업 실행이 가능.
2. 콜백, Future, async - await 방식이 있다.

## 콜백

실행 가능한 함수를 인자로 전달하여, 특정 상황이 발생할 때 호출

## Future

1. 미래에 완료되는 객체

2. Javascript 의 Promise와 동일

3. Future 는 ‘미래'에 받아올 값을 의미

## then( ) 사용의 문제점

1. 동기식 코드 보다는 결과 예측이 어렵다.
2. 단계가 많아지면 사용 어렵다.
3. 로직이 복잡해 지면 예외처리가 힘들다.

## async - await 문법

1. 비동기 코드 작성 시 유용.
2. await 키워드는 해당 Future 가 끝날 때까지 함수 실행을 대기.

## 데이터 소스

데이터의 근본

프로그램이 사용하는 원천 데이터 전부

## 데이터 소스 변환

1. 데이터 소스에서 추출
2. 추출한 데이터(미가공 상태) 사용 가능한 데이터로 변환

변환 : 문자열 형태의 Json to Dart Map 

## 데이터 소스 종류

1. Text
2. File
3. JSON
4. XML
5. CSV
6. RDBMS
7. NoSQL

등등

## 데이터 클래스 6개

1. final
2. fromJson
3. toString()
4. ==
5. hashCode
6. copyWith

-------------------
알고리즘 학습 필요

## 샘플
- https://github.com/namjunemy/TIL
- https://github.com/milooy/TIL
- https://github.com/YutoMizutani/til
