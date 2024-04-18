## **Use Case**

- 사용 사례→ 실제 사용자의 행동에 따른 로직
- ⇒ ViewModel 내부의 메소드
- ⇒ 로직이 변경되면 ViewModel 이 아니고 로직만 수정하려면?

→ 뷰모델에서 분리

Repository 에서는 비즈니스 로직이 없어야 함 (10만 가지고 오기)

그래야 범용적으로 활용 가능함

뷰모델에서 상태(변수) 따로 모으고 

뷰모델에서 하나의 기능을 클래스로 뺀다. 이것이 usecase

그래서 뷰모델에서 기능이 여러개 있는 경우 usecase 여러개 주입받는다.

## **Clean Architecture**

- 행위 가치
    - 소프트웨어 기능 이 잘되는것
- 구조 가치
    - 소프트웨어 아키텍트의 구조를 잘짜는 것 (클래스를 작게 , 인터페이스를 사용해서)

구조나 설계에 신경 쓰지 않고 오직 기능 구현에만 몰두한 소프트웨어의 유지보수는 매우 힘들다

새로운 형태의 UI나 기술을 추가해야 할 때 거의 처음부터 새로 만들어야 할 수도 있다

![Untitled](https://github.com/happysong3914/TIL/assets/130008915/a409b3f5-94c9-4e85-af88-77e0d6cb7c9a)


![Untitled 1](https://github.com/happysong3914/TIL/assets/130008915/157d9d3e-365e-4c5a-9097-ad6c2290f1d7)

![Untitled 2](https://github.com/happysong3914/TIL/assets/130008915/34e8d1d2-ac4c-48a6-902f-9e5bcb261d8e)



**클린 아키텍처 장점**

1. 확장 가능한 앱
2. 쉬운 테스트
3. 다른 사람도 이해하기 쉬운 구조

Data Layer

- Database, Remote API, Preference 등 구현
- DB 엔터티 맵퍼 & DTO
- 레포지토리 구현
- 데이터 형태에 따라 local / remote 로 구분할 수 있다

**Domain Layer**

- 아키텍처의 가장 핵심이 되는 레이어
- 비즈니스 로직이 포함된 Use Case를 포함
- 모델 클래스를 포함
- repository 정의
- 이외에도 service, logic, exception, validation, event, command 등 도메인에 필요한 내용이 올 수 있음

usecase가 따로 빠져 있으면 몇개의 기능이 있는지 한번에 파악 가능 

구조가 분리됨으로써 의미적으로  시스템을 파악하기 쉽다 

Presentation Layer

- 모든 화면, 컴포넌트를 포함한 위젯들 (UI)
- ViewModel을 포함

**왜 Use Case를 사용하는가?**

- ViewModel 이 어떤 기능을 하는지 직관적으로 파악 가능
- Repository 수정사항에 따른 ViewModel 에서의 의존성 제거
- 클린 아키텍처의 목적 중 하나인 변경의 최소화를 만족하기 위해
- 여러 ViewModel 에 동일한 기능이 있을 경우 기능의 재사용(중복코드 삭제가능)

Use Case 코드 

하나의 클래스가 하나의 동작만 수행함

= 진정한 단일책임 원칙

최근에는 여러가지 이유 때문에

call() 대신 execute() 를 사용함

**call() 메서드**에 기능을 구현하면 호출부에서 함수명이 아닌 클래스 이름만으로 호출 가능 (Dart 의 특성) →  코드 추적 시 힘들다.

- UseCase는 1개의 기능만을 가짐
- call() 함수를 재정의 하거나, 다른 함수이름을 정의해도 됨
    - 예) execute()
- 인터페이스 등을 통해 UseCase 를 강제하는 것도 하나의 방법이다

2개 이상의 Repository, 기능 클래스 를 사용하는 UseCase존재함 또한 UseCase는 다른 UseCase의존할 수 있음

uses case는 future 를 반환 가능 그럴경우  뷰모델에서  await를 사용해야 한다. 하지만 뷰모델에서 future 를 반환 자제

Use Case 의 이름 규칙

*현재 시제의 동사* + *명사/대상(선택사항)* + *UseCase*.

더 나은 대안

**도메인 별로 클린 아키텍처 구조를 가지도록 한다**

- 훨씬 더 복잡해 보이지만 우리의 목표는 더 복잡한 프로젝트를 수행하기 위함
- 각 기능의 크기가 제한되어 있기 때문에 훨씬 더 잘 확장됨
- 앱이 성장하더라도 기존 기능에 영향을 덜 줌
- 이 구조는 명확하고 일관성이 있어 새로운 개발자가 빠르게 이해할 수 있음

![Untitled 3](https://github.com/happysong3914/TIL/assets/130008915/2833642c-3f77-4af8-a639-67d436bb1da7)


### Good architecture != Clean Architecture

- 대부분의 개발자는 좋은 아키텍처를 가지려면 항상 클린 아키텍처를 고수해야 한다고 맹신한다
- 클린 아키텍처는 좋은 아키텍처를 달성하기 위한 **도구**이다
- 좋은 아키텍처
    - 관심사 분리 (앱을 별개의 레이어로 나누기)
    - 모듈식 (낮은 결합도, 높은 응집력)
    - 프로젝트의 조건에 맞는 (친구랑 둘이 할 때와, 10명이서 할 때는 다른 방식이 필요)
- 클린 아키텍처가 모든 시나리오에 적합한 솔루션은 아니다
- **클린 아키텍처에 집중하기 보다는 아키텍처를 좋게 만드는 요소에 집중해라**
