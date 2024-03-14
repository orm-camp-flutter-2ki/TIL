> ###  다형성(polymorphsim)?
동일한 인터페이스나 추상 클래스를 구현했지만 타입이 다양한 객체를 동일하게 다룰 수 있게 해주는 능력입니다.<br>
_예시)_<br> ![](https://velog.velcdn.com/images/hee462/post/2a3a4713-e1ef-427b-97cc-b61e33bec40d/image.png)<br>
`두 가지 다른 타입의 객체가 동일하게 사용되는 능력`을 **다형성**이라고 합니다.
다형성은 주로 `상속`과 `인터페이스`를 통해 구현되는데, 
코드의 `재사용성`과 `유연성`을 높여줍니다.
한 번 작성한 코드를 다양한 타입의 객체에 적용할 수 있으며,
새로운 타입이 추가되더라도 기존 코드를 수정하지 않고도 사용할 수 있습니다. 이를 통해 코드의 `유지보수성`과 `확장성`을 향상시킵니다.

> ###   다형성을 활용하는 방법
- 선을 상위 개념으로 인스턴스 생성은 하위 개념으로 한다![](https://velog.velcdn.com/images/hee462/post/4a027932-147a-4196-aca4-af75672b9158/image.png)
- 인터페이스를 변수의 타입으로 사용한다
- 타입 변경 방법(cast) ->  as는 형변환, type casting 이라고 하고, is는 type 을 검사!
_ex) 하지만 as타입 위험하니까 is형으로 확인하고 is형으로 사용할것_
 ![](https://velog.velcdn.com/images/hee462/post/2a90eb41-d787-469e-9cef-69caf163dd75/image.png)
 
>  ⭐️ 한장정리!
 ![](https://velog.velcdn.com/images/hee462/post/1f7ec237-1764-4104-adab-8de649097f31/image.png)
