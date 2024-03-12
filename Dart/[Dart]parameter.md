
![](https://velog.velcdn.com/images/hee462/post/98b5131a-b75f-4248-9f97-6571e2a64688/image.png)


> Named Parameter ?
- Named Parameter란 다트 선언자에서, 매개변수의 위치가 아닌 이름을 통해 생성자에 쓰일 변수를 받아오는 방식
- 멤버변수가 nullable variable이 아닌 경우에는 생성자에서 변수의 이름 앞에 `required` 를 반드시 작성해주어야 하며,
객체를 생성할 때 변수의 `초기화 값`을 넣어주지 않으면 Dart 컴파일러가 오류를 발생시킨다.
 _
  `nullable?` 상황 예시를 들자면 회원가입할 때 이름, 생년월일, 성별은 필수입력(required)이고, 집전화번호는 선택사항이라면 이때 집전화 없는 사람도 있으니까 즉, null 이 들 어 올 수 있으니 nullable하게 ?를 사용합니다.
지금 예제에서는 용사가 칼을 획득할 수도 있고, 팔수도 있고 게임 시나리오에 따라 달라짐_
![](https://velog.velcdn.com/images/hee462/post/9557bf9c-fe22-46da-9129-a90e7265328d/image.png)

> Optional Parameter ?
- 컬리브라켓 `{  }` 으로 감싸져 있다. 
- 컬리 브라켓 안에 있는 값은 옵셔널이다.
- 값을 할당하려면 `콜론(:)` 을 꼭 붙여야 한다.
- 컬리 브라켓 안에 있는 파라미터의 순서는 상관이 없다. 
-  함수에 많은 파라미터를 넘겨줄 때 혼란을 피할 수 있다. 
-  함수 작성시에 순서보라는 파라미터의 이름을 참조하기 때문에 좀 더 유연한 편이다. 






> Positional parameter?
 * Positional parameter를 사용하면, 초기화 할 멤버변수의 종류, 조합, 순서 등에 따라 수많은 생성자를 오버로딩(Overloading) 해주어야 하기 때문에 반복적이고 비효율적인 코드이다.
 * **[   ] **: 로 감싼 Parameter는 `위치`를 뜻하며,정해진 위치에 값을 저장한다.
하지만 








