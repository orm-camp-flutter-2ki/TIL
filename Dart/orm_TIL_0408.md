240408 (Mon)

플러터 과정 26일차


메모
-
statefulWidget 생명주기
initState = 처음 한번
dispose = 끝날 때 한번
state = 매번

외부의 생성자는 은닉화 하지 않는 편이다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/86296f50-858e-40b3-b09a-5faedc04c2f9/dff3ee72-5ec6-40ce-a5d7-8fef17438ac9/Untitled.png)

setState를 동작 시키는 기본 조합


# MVVM (Model - View - ViewModel) 패턴

개념: 프로그램의 비지니스 로직과, 프레젠테이션 로직을 UI로 명확하게 분리하는 패턴입니다.

Model

데이터를 다루는 부분, 비지니스 로직이다.

데이터와 비즈니스 로직을 담당하는 부분입니다.

데이터를 가져오고 저장하는 역할을 수행한다.

보통 데이터베이스 ,네트워ㅓ크 요청 또는 파일 시스템과 같은 데이터 소스와 상호작용합니다.

View

레이아웃과 화면을 보여주는 역할

사용자 인터페이스를 담당하는 부분입니다.

사용자가 보는 화면을 표시하고, 사용자 입력을 처리합니다.

ViewModel

View와 Model 사이에서 중재자 역할을 한다.

view에서 발생하는 이벤트를 감지하고, 해당 이벤트에 맞는 비즈니스 로직을 수행한다.

Model과 상호작용하여 데이터를 가져오거나 업데이트하고, view에 데이터를 업데이트하는 역할을 합니다.

view에서 표시할 데이터를 가공하여 제공하는 역할을 합니다.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/86296f50-858e-40b3-b09a-5faedc04c2f9/bdc4698c-9ec2-4e3c-a439-725da19be277/Untitled.png)

## MVVM 특징

언뜻 보기에는 MVP와 비슷한 부분이 많습니다. 그러나 MVP는 View와 Presenter 사이의 의존관계가 1:1로 형성되어있다면, **MVVM은 View와 ViewModel사이의 관계가 1대n**으로 되어있습니다. 또한 데이터 바인딩을 이용한다면 **View**와 **ViewModel** 사이의 의존성을 없앨 수 있습니다.

변수는 viewmodel만 있다.

모델은 레파지토리라고도 하고 데이터이다.

뷰모델은 변수가 들어가있고 변화하는 코드가 있다.

뷰는  ui만 구성되어 있는 것.

예시)

모델은 원유

뷰모델은 치즈 가공, 우유 가공, 버터 가공

뷰는 제품  치즈, 우유, 버터
