## 📖 DTO, Mapper

<br>

### 📄DTO

- 데이터 소스를 모델 클래스로 변환하는 과정에서  순수하게 클래스에 담기 위한 중간 전달 객체
- 잘못된 데이터를 받더라도 터지지 않음
- 무조건 널러블로 받고 final 사용하지 않음

#### ✏️ DTO가 필요한 이유

- Model Class 는 non-nullable 한 값만 가지고 있도록 함
- Json 데이터는 null 값을 포함할 수 있음
- Map -> Model Class 변환 시 null 값 등의 예외를 사전에 걸러내기 용이함
- 불완전한 코드가 포함될 것 같다면 DTO를 도입
- Json 값에 예외가 없다면 반드시 DTO를 도입할 필요는 없음

<br>

### 📄 Mapper

- fromJson과 toJson 작성 (Mapper)
- extension을 사용
	-  DTO 는 자동으로 만듦
	+ Mapper는 복잡한 로직이 포함될 수 있고 인간이 작성
	+ DTO와 Mapper 코드를 분리
- 
<br>

### 📄 Modle Class

- Json 처리는 Mapper 에서 함 데이터 클래스는 옵션

<br>

### 📄 데이터 흐름

- JSON -> DTO -(Mapper)> Model Class
