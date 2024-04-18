## 클린 아키텍처
* 앱이 커질수록 더 많은 모델, UI, ViewModel이 생성될 것이고 무언가를 찾을 때 고통을 받을 것이다.
* 구조나 설계에 신경 쓰지 않고 오직 기능 구현에만 몰두한 소프트웨어의 유지보수는 매우 힘들다.
* 새로운 형태의 UI나 기술을 추가해야 할 때 거의 처음부터 새로 만들어야 할 수도 있다.

<p align="center"><img width="750" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aeebc4dd-bf95-4594-8d39-0ec0f41fe841"></p>

|Data Layer|Domain Layer|Presentation Layer|
|----------|------------|------------------|
|Databse, Remote, Api, Preferences 등 구현|아키텍처의 가장 핵심이 되는 레이어|모든 화면, 컴포넌트를 포함한 위젯들(UI)|
|DB entity Mapper&DTO|비즈니스 로직이 포함된 Use Case를 포함|ViewModel 포함|
|repository 구현(impl class)|repository 정의(repository interface class)||
|데이터 형태에 따라 local/remote로 구분할 수 있다.|모델 클래스||
||service, logic, exception, validation, event, command 등 도메인에 필요한 내용이 올 수 있음||

#### Domain Layer => 비즈니스 로직이 포함된 useCase를 포함하기 때문에 아키텍처의 핵심이다.
#### repository 인터페이스 클래스도 이 곳에 있어서 어떤 데이터를 가져오는 지 확인할 수 있다. 

<br></br>

### 권장 디렉토리 구조
<img width="484" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/cf82800a-ea1a-41bd-b877-0bbd44472620">

### 클린 아키텍처의 장점
* 확장 가능한 앱
* 쉬운 테스트
* 다른 사람도 이해하기 쉬운 구조

<br></br>

## Use Case(= 사용 사례)
* 사용자들의 액션들을 처리하는 viewModel 안의 메서드들을 따로 분리해 정의한 클래스
* viewModel이 어떤 기능을 하는지 직관적으로 파악 가능(useCase 클래스를 보면 기능이 몇 개인지 보인다.)
* 여러 viewModel에 동일한 기능이 있을 경우 기능의 재사용
> repository 인터페이스를 수정하면 viewModel이 영향을 받는다.  
-> 레포는 수정이 빈번할 수밖에 없음  
-> 뷰모델이 레포에 의존이 큼을 볼 수 있음. 따라서 의존성 분리  
-> 뷰모델이 인터페이스 같은 역할이 된다.(단순히 전달자 역할이 된다.)

<img width="468" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d7d98564-03a2-4dca-b5e1-63e418cc46da">

Repository에는 비즈니스 로직이 없어야 한다.(예시로 이름순 정렬 등) 그래야 범용적으로 활용이 가능하다.  
-> 현재는 이런 로직들을 viewModel에서 사용 중이다.  
#### 📝 그런데 만약 viewModel에서 로직이 너무 길거나 커진다면 ?
-> 별도의 클래스로 분리  
-> 기능을 useCase에서 사용해서 캡슐화한다.  
-> viewModel에서 사용했던 repository도 viewModel에서 제거하고, useCase에서 사용한다.  
-> 그리고 viewModel에서는 useCase 클래스를 주입하여 사용한다.

<br></br>

## Use Case 코드 적용해 보기
* 하나의 클래스가 하나의 동작만 수행한다.(useCase 당 기능 한 개 = 단일 책임의 원칙)
#### -> 뷰모델에서 다른 기능이 있으면 또 다른 use case 만든다!
* (뷰모델 state를 변경해야하면 usecase에 state를 전달해줘야 하나요?)  
=> state는 뷰모델에서 구현하고 useCase는 (리턴이 필요한 경우) 값을 리턴한다.
=> state는 뷰에 나타낼 상태이기 때문에 viewModel에 둔다.  
* 여러 repository와 다른 useCase를 활용할 수도 있다.
* class 이름 형식 => 현재 시제 동사 + 명사/대상 + UseCase
(FormatDateUseCase, LogOutUserUsecase, MakeLoginRequestUseCase)

<img width="450" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/93ad87b0-c16b-4bbe-af89-4710e0b92387">

* **꼭 필요한 경우에만 useCase를 사용하는 것이 좋다.**

<br></br>

## 정리
<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/e47c742d-3bf8-47a0-a8be-8a84434d1d16">

* 클린 아키텍처는 좋은 아키텍처를 달성하기 위한 도구이다. 맹신하지 말자. 정답은 없다.
* 좋은 아키텍처
  - 관심사 분리(앱을 별개의 레이어로 나누기)
  - 모듈식(낮은 결합도, 높은 응집력)
  - 프로젝트의 조건에 맞는 방식 사용
* 클린 아키텍처에 집중하기 보다 아키텍처를 좋게 만드는 요소에 집중하자.


<br></br>

## 기타

### 도메인(인증 기능, 프로필 기능 등) 별로 클린 아키텍처 구조를 가지도록 한다.
* 더 복잡한 프로젝트를 수행하기 위함
* 각 기능의 크기가 제한되어 있기 때문에 훨씬 더 잘 확장됨
* 앱이 성장하더라도 기존 기능에 영향을 덜 준다.
* 기능 별로 나눠 작업이 가능하기 때문에 역할 분담에도 좋다.

<img width="249" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/4e58a0a0-0fcb-4609-a786-c2d39b685823">

### presentation 추천 구조
* 한 눈에 구조를 파악할 수 있다.
<img width="343" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/63ca715b-d7fd-4005-b63c-aa8a1774b4c7">

### 도메인 유형의 기반 구조
* 확장 가능한 소규모 앱의 경우 선호
* 폴더 구조가 직관적임
* 모델 클래스가 많으면 폴더가 커지고 찾기가 어려워짐
<img width="245" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/44bc6646-027a-4c88-a1f5-e0b4e840d573">

### 도메인의 객체 기반 구조
* 대규모 앱의 경우 선호
* 객체별로 기능을 찾기 수월
* 비즈니스 로직이 단순하고 변경 가능성이 적을 경우 용이
* 모델 클래스가 엄청 많은 경우 추천

<img width="384" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/a353854a-f756-460e-9c99-553d403d254c">

### 모든 모듈이 참조해야 하는 공통 기능이 있는 경우
* core 디렉토리에 공통 부분을 작성한다.(result class 등)
<img width="300" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/68135052-52e3-4dae-9719-7b4a567bc8ad">

#### * 공통 UI는 presentation 폴더 내의 components로.
#### * 도메인은 기본 지식이라는 뜻?(예시: 개발에 대한 도메인이 있다.)
#### * Domain 안의 폴더들은 순수 dart 코드(라이브러리 의존이 없는, 프레임 워크에 오염되지 않은)로 이루어져 있다.(freezed 예외)
#### => 프레임워크가 핵심 코드 안으로 들어오지 못하게 한다.(순수한 코드들로 유지하자)

#### 📝 [선생님의 클린 아키텍처 적용 코드 예시](https://github.com/junsuk5/flutter-clean-architecture-note-app-1/blob/master/lib/domain/use_case/note_use_cases.dart)


### Facade Pattern
* 어떠한 행위에 필요한 공통 기능들을 정의하기 위해 useCase 클래스들을 사용한다.  
예시 두 가지 :  
<img width="450" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d6ee709f-7139-48eb-a945-aad542bebc14">

<img width="377" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/fbcb48d0-6a76-489c-bc19-d70d7bb63232">

