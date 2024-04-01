### 1. DTO(Data transfer object)

데이터 소스를 모델 클래스로 변환하는 과정에서

**순수**하게 클래스에 담기 위한 중간 전달 객체(json→dto→model class)

왜?  잘못된 데이터 소스 (Json)를 받더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단

- 모델 클래스와 비교하여 ① 모든 필드가 Nullable 변수 ②직렬화, 역직렬화 제공
- 즉, Json을 무지성으로 받아들인다. 기존 모델 클래스를 Dto 가 대체

### 2. mapper 코드 작성법

- mapper란?

-Mapper는 데이터를 한 형식에서 다른 형식으로 변환하는 역할을 하는 클래스 또는 함수를 말함.

-보통 DTO(Data Transfer Object)와 모델 객체(Model Object) 사이의 변환에 사용

-일반적으로 데이터베이스나 외부 API로부터 데이터를 가져올 때 DTO를 사용하여 데이터를 전달하고, 이후에 이 DTO를 모델 객체로 변환하여 애플리케이션 내부에서 사용 이런 경우 변환 작업은 Mapper에 의해 이루어 짐

### 3.Mapper 코드 작성 방법

- toJson() 도 Mapper 다. 이와 비슷하게 만들어도 됨. 또는 extension 을 활용하여 기능을 분리해도 된다(https://dart.dev/language/extension-methods)
- extension을 선호하는 이유: DTO 는 자동으로 만들 것이다. (무지성, 다른 코드 개입 no), mapper 는 복잡한 로직이 포함될 수 있고 인간이 작성, DTO와 mapper 코드를 분리

### 4. Dto가 필요한 이유

- Model Class 는 non-nullable 한 값만 가지고 있도록 한다
- Json 데이터는 null 값을 포함할 수 있음 (문서에 명시되어 있지 않더라도…)
- Map -> Model Class 변환시 null 값 등의 예외를 사전에 걸러내기 용이함
- 불완전한 코드가 포함될 것 같다면 Dto를 도입하자
- Json 값에 예외가 없다면 반드시 Dto를 도입할 필요는 없다
