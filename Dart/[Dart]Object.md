> ###  Object
+ Object는 모든 클래스의 부모 클래스이며, 모든 dart클래스는 암묵적으로 Object클래스를 상속하고 있다.
+ Object클래스는 모든 dart객체의 공통된 메서드를 정의하고 있다.
+ 이 메서드들은 모든 객체에서 사용할 수 있으며, 필요에 따라 오버라이딩하여 사용할 수 있다.



> ####  1. toString()
   객체를 문자열로 표현하는 메서드. 기본적으로 클래스 이름과 객체의 해시 코드를 반환하며, 필요에 따라 오버라이딩하여 사용자가 정의한 형식으로 객체를 문자열로 표현할 수 있다.<br/>
_**ex**)_<br>
![](https://velog.velcdn.com/images/hee462/post/9f0f584f-a55a-439c-a7f9-fd66b7584fa7/image.png)
>#### 2. hashCode
   객체의 해시코드를 반환하는 메서드. hashCode는 객체의 식별자 역할을 한다. 동일한 객체에 대해서는 항상 동일한 해시코드를 반환해야 한다.<br/>
   _**ex**)_
  ![](https://velog.velcdn.com/images/hee462/post/e041f9ed-a928-49ea-a173-f9f0673b8734/image.png)
>3. operator ==<br>
   객체의 동등성 비교를 위한 연산자. 두 객체가 동일한지를 판단하는데 사용된다.<br>
_**ex**)_<br>
![](https://velog.velcdn.com/images/hee462/post/a7eadc66-da8e-452a-9a59-04383b793f6f/image.png)
