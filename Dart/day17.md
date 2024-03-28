# DTO

## Data Transfer Object

- 데이터 소스를 모델 클래스로 변환하는 과정에서 **순수**하게 클래스에 담기 위한 중간 전달 객체
- 왜?  잘못된 데이터 소스 (Json)를 받더라도 안 터지게 하려는 클라이언트 개발자의 방어 수단
- Json → Dto → Model Class
- dto 디렉토리 → dto,model,mapper 디텍토리 → dto.dart, class.dart, mapper.dart
  

## 모델 클래스와 비교하여 어떤 특징이 있는가?

- 모든 필드가 Nullable 변수
- 직렬화, 역직렬화 제공

즉, Json을 무지성으로 받아들인다 기존 모델 클래스를 Dto 가 대체한다.


## 모델 클래스 재정의

- 모든 필드가 non-nullable 상수
- ~~직렬화~~
- ~~역직렬화~~
- ==
- hashCode 재정의
- toString() 재정의
- 깊은 복사 제공 copyWith()
- Json 을 그냥 받지 않고 내 앱에서 필요한 형태로 필드를 수정할 수 있음
- 데이터 소스의 모양을 확인하지 않고 미리 정의할 수 있음
- Dto를 모델로 변환해서 사용해야 함

## Mapper 코드 작성 방법

- toJson() 도 Mapper 다. 이와 비슷하게 만들어도 된다.
- 또는 extension 을 활용하여 기능을 분리해도 된다
    - https://dart.dev/language/extension-methods
- extension을 선호하는 이유가 있다.
    - DTO 는 자동으로 만들 것이다. (무지성, 다른 코드 개입 no)
    - mapper 는 복잡한 로직이 포함될 수 있고 인간이 작성
    - DTO와 mapper 코드를 분리
      

## DTO 가 필요한 이유

- Model Class 는 non-nullable 한 값만 가지고 있도록 한다
- Json 데이터는 null 값을 포함할 수 있음 (문서에 명시되어 있지 않더라도…)
- Map -> Model Class 변환시 null 값 등의 예외를 사전에 걸러내기 용이함
- 불완전한 코드가 포함될 것 같다면 Dto를 도입하자
- Json 값에 예외가 없다면 반드시 Dto를 도입할 필요는 없다
  

## DTO를 모델 클래스로 전환

- 순수한 데이터 소스(Dto) 를 원하는 모델 클래스로 변환하려면 fromJson(), toJson() 처럼 변환 기능이 필요함
  

## 정리

기존에 작성한 모델 클래스(6종 세트 포함 : 데이터 클래스)는
DTO 와 모델 클래스의 역할을 **모두 가지는** 클래스 였다
DTO 가 도입된다면 역할 분담 가능

- DTO : fromJson(), toJson()
- 모델 클래스 : 불변 객체 (+ 나머지 4개는 옵션)
  
