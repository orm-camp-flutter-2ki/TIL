# DTO (Data Transfer Object)
- 데이터 소스를 모델 클래스로 변환하는 과정에서 순수하게 클래스에 담기 위한 중간 전달 객체
- 서버에서 잘못된 데이터 소스(Json)를 받더라도 안터지게 하려는 클라이언트 개발자의 방어수단

  ( 서버를 믿지 말자. 무슨 데이터가 들어올 지 모른다. )
  ### Json -----------> DTO -----------> Model
- Json 파일을 DTO 가 터질만한거 한번 걸러주고 이쁘게 만든 Model 을 사용한다.
- 기본 Model 에서 바로 받아쓰던 fromJson(), toJson() 을 DTO 클래스에서 정의

  ![image](https://github.com/philiplee25/TIL/assets/76925432/e944f980-a9cb-4b49-9f42-8383fa5f8f08)

- DTO 가 필요한 이유
  - Json 데이터는 null 포함 가능한데 그 값을 Model 클래스에 못들어오게 걸러준다.
  - Map -> Model 변환시 null 등 예외를 사전에 걸러내기 용이하다
  - 불완전한 코드가 포함될 것 같다면 DTO 를 도입한다.
  - 완벽한 Json 값이라면 반드시 DTO를 도입할 필요가 없다. 근데? 믿지도 말자.

# Mapper
- toJson() 도 Mapper 다.
- 우린 extension 으로 기능을 분리했다.
- extension 이 선호되는 이유
  - DTO 는 자동으로 만들어진다.
  - mapper는 복잡한 로직이 포함될 수 있고 인간이 작성
  - DTO 와 mapper 코드 분리

# 폴더구조 꿀
- 데이터의 흐름대로 폴더를 생성한다.
- 어떤 개발자는 source 라고 만들지만 데이터 흐름의 순서를 위해 앞에 data를 붙였다.
  ### Json -------> DTO -------> Mapper 를 활용해 모델 클래스로 변환 -------> Model
  ![image](https://github.com/philiplee25/TIL/assets/76925432/46422595-5827-4fa8-8108-a9311b5a940e)

