> #### 🙋🏻Model class?<br>
- View에 보여질 데이터를 담는 객체<br>
 View == 눈에 보이는 부분<br>
- 비슷한 용어들<br>
도메인 모델<br>
Entity<br>
DTO<br>
POJO<br>
데이터 클래스 (tojson ,fromjson,copyWith,toString,==operetor,get)<br>ex)<br>
![](https://velog.velcdn.com/images/hee462/post/67260556-97a9-49b5-a61d-256e5dccfd48/image.png)
#### 책임과 역할<br>
- 모델 객체 클래스의 속성에 대한 데이터를 조회할 수 있는 클래스<br>
- 별도의 기능을 가지지 않는 순수한 클래스<br>
- 데이터 소스를 앱에 필요한 형태로 변환하여 앱 개발을 편리하게 해 주는 역할<br>

>####  모델링 방법<br>
- DDD(Domain Driven Design)<br>
** Domain 의 정의**<br>
`유사한 업무의 집합`<br>
특정 상황(주문, 결재, 로그인)이나 특정 객체(유저, 손님)가 중심이 될 수 있음<br>
**모델 클래스**<br>
도메인을 `클래스`로 작성한 것<br>
_왜 클래스로 작성해야 할까? 그냥 JSON (Map) 으로 사용하면 안 됨?_<br>
 클래스를 사용하여 관련된 데이터와 로직을 캡슐화-> JSON이나 Map을 사용하면 이러한 복잡성을 표현하기가 훨씬 어려움<br>
- ORM(Object-relational mapping)<br>
데이터 소스가 DB 인 경우 DB 와 모델간 `상호 변환`을 도와주는 기법<br>
ORM은 DB 를 활용할 경우에 다시 정리 할 예정<br>





