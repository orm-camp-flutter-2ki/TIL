240417 (Wed)

플러터 과정 27일차

# Use Case / 클린 아키텍쳐

#### Use Case
- 사용사례
- => ViewModel  내부의 메소드
- => 로직이 변경되면 ViewModel이 아니고 로직만 수정하려면?

```dart
abstract interface class UserRepository {
  Future<List<User>> getUsers();

  Future<List<User>> getUsersTop10ByUserName();
}
```
repository에서는 비즈니스 로직이 없어야함
그래야 범용적 사용가능

```dart
Future<List<User>> getUsersTop10ByUserName();
```
이 비즈니스 로직이 ViewModel에 있도록 이동


### Clean Architecture

구조나 설계에 신경쓰지 않고 오직 기능 구현에만 몰두한 소프트웨어의 유지보수는 매우 힘들다.
새로운 형태의 UI나 기술을 추가해야 할 때 거의 처음부터 만들어야 할 수도 있기 때문에 폴더 정리가 필요하다.

#### 클린 아키텍쳐의 장점
1. 확장 가능한 앱
2. 쉬운 테스트
3. 다른 사람도 이해하기 쉬운 구조

--------------------------------------------------------------------------------------
![Blue Purple Futuristic Modern 3D Tech Company Business Presentation](https://github.com/BAUu/TIL/assets/44741680/468a3e8a-902a-4b90-ac61-7ec154bb3e9b)

구분은 Presentation, domain, data 레이어로 구분

#### Data Layer
- Database, Remote API, Preference 등 구현
- DB 엔터티 맵퍼 & DTO
- 레포지토리 구현
- 데이터 형태에 따라 local / remote 로 구분할 수 있다


#### Domain Layer
- 아키텍처의 가장 핵심이 되는 레이어
- 비즈니스 로직이 포함된 Use Case를 포함
- 모델 클래스를 포함
- repository 정의
- 이외에도 service, logic, exception, validation, event, command 등 도메인에 필요한 내용이 올 수 있음


#### Presentation Layer
- 모든 화면, 컴포넌트를 포함한 위젯들 (UI)
- ViewModel을 포함

--------------------------------------------------------------------------------------------
#### Use Case를 사용하는 이유

ViewModel 이 어떤 기능을 하는지 직관적으로 파악 가능
Repository 수정사항에 따른 ViewModel 에서의 의존성 제거
클린 아키텍처의 목적 중 하나인 변경의 최소화를 만족하기 위해
여러 ViewModel 에 동일한 기능이 있을 경우 기능의 재사용

#### Use Case 이름 규칙
현재 시제의 동사 + 명사 / 대상(선택 사항) + UseCase


-----------------------------------------------------------------------------------------------
#### 좋은 아키텍쳐가 클린 아키텍쳐인가?
=> 아니다.

- 대부분의 개발자는 좋은 아키텍처를 가지려면 항상 클린 아키텍처를 고수해야 한다고 맹신한다
- 클린 아키텍처는 좋은 아키텍처를 달성하기 위한 도구이다
- 좋은 아키텍처
    - 관심사 분리 (앱을 별개의 레이어로 나누기)
    - 모듈식 (낮은 결합도, 높은 응집력)
    - 프로젝트의 조건에 맞는 (친구랑 둘이 할 때와, 10명이서 할 때는 다른 방식이 필요)
- 클린 아키텍처가 모든 시나리오에 적합한 솔루션은 아니다
- 클린 아키텍처에 집중하기 보다는 아키텍처를 좋게 만드는 요소에 집중해라
