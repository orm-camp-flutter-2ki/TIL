>🙋🏻DTO(Domain Transfer Object)?
데이터를 전송하기 위한 객체
주로 네트워크 통신이나 데이터베이스 액세스와 같은 데이터 전송 작업
- 필요한 이유?
  - Model Class 는 non-nullable 한 값만 가지고 있도록 한다
  - Json 데이터는 null 값을 포함할 수 있음 
_(문서에 명시되어 있지 않더라도…)_
  - Map -> Model Class 변환시 null 값 등의 예외를 사전에 걸러내기 용이함
  - 불완전한 코드가 포함될 것 같다면 Dto를 도입하자
  ? Dto를 nullable 한 형태를 만들어 사용 ->
   필요한 데이터가 없는 경우 null로 처리하여 코드를 더욱 견고하고 유연하게 만들 수 있음
  - Json 값에 예외가 없다면 반드시 Dto를 도입할 필요는 없다


>🙋🏻Mapper ?

다른 데이터 모델 간에 데이터를 변환
데이터의 구조와 형식을 변경하여 원하는 형태로 데이터를 변환하고 매핑

<img src="https://velog.velcdn.com/images/hee462/post/c1b44458-e2fa-4980-ab94-a2f932d82fb3/image.png" width="500" height="300">


이전에 배운 [Repository](https://velog.io/@hee462/DartRepository) 와 mapper와 혼동

>Repository (저장소):
메모 어플리케이션은 여러분의 메모를 저장하는 곳입니다. 
이 저장소에는 `CRUD` 가능


>DTO (Data Transfer Object): ` 임시저장소느낌 `
` 데이터를 내부 에서 전달 가능 외부 전달 가능`
메모 어플리케이션에서는 `새 메모`를 작성할 때 , 
사용되는 메모 객체가 DTO와 유사합니다.
이 객체에는 메모의 내용, 작성 일자, 수정 일자 등의 정보가 포함됩니다.

>Data Class (데이터 클래스):   `전체 리스트 `
메모 어플리케이션에서는 `각각의 메모를 나타내는 데이터 클래스`가 있습니다.
이 클래스에는 메모의 내용, 작성 일자, 수정 일자 등의 속성이 포함됩니다.

>Mapper (매퍼):  `임시저장소데이터를 -> 찐데이터로 변환하는데 사용`
여러분이 새 메모를 작성하고 저장할 때,  
메모 어플리케이션은 DTO와 데이터 클래스 간의 변환을 담당하는 매퍼를 사용합니다.
사용자가 입력한 정보는 DTO로 변환되어 데이터 클래스에 저장됩니다. 그리고 이 데이터 클래스가 저장소에 저장됩니다.

<img src="https://velog.velcdn.com/images/hee462/post/2d896e93-4fe7-4644-ace9-e020e2149ebd/image.png" width="500" height="300">



만드는 형식은 어플과 기능마다 차이가 있지만
되도록이면 Model,Dto를 만들고 기능에 따라 맞춰서 코드를짜는것이 좋다
