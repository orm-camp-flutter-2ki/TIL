[Test Double](https://tecoble.techcourse.co.kr/post/2020-09-19-what-is-test-double/)
    - 테스트를 진행하기 어려운 경우에 테스트가 가능하도록 만들어주는 객체
    

> 모호한 경계를 가지므로 용어에 집착하지 말자
우리는 그냥 Mock 으로 통일함.
![](https://velog.velcdn.com/images/hee462/post/75a158ad-fb82-4a60-9e16-8db25ba65de1/image.png)


####  Mock 객체 활용
- 테스트를 위해 지속적인 API 호출은 서버에도 부담되고, 속도가 느리거나 예기치않은 실패가 생길 수 있다.
![](https://velog.velcdn.com/images/hee462/post/fa9e29e1-d88a-4a76-85ba-bb5032c55ae3/image.png)

-  인터넷이 끊어지거나 서버가 죽거나 등등 하는 경우도 있다
   그런 경우를 대비해서 Mock 객체를 사용해서 테스트를 진행하는게 좋다.
- `Mock 을 사용하려면 Interface를 통한 다형성을 구현`해서 쓰는게 좋다.![](https://velog.velcdn.com/images/hee462/post/2087ca03-9788-4640-818c-6c9977769f02/image.png)

     객체간 의존성이 생기면 테스트가 불편하기 때문에, 의존성 주입을 통해서 의존성 분리해주는게 좋다.
- 테스트를 위해 다양한 Mock class를 제공해주는 라이브러리도 많음.

> http 라이브러리  
`import ‘package:http/testing.dart’` 
- `Client` MockClient 를 제공한다.
- 응답값과 상태값을 내가 맘대로 지정해서 보낼 수 있다.


 >mockito 라이브러리<br>
 `import 'https://pub.dev/packages/mockito'`
- 비동기 메서드 테스트하기
 테스트 케이스의 expect 문에서 어떤 결과값이 아니라, 실제 메서드를 호출하고 이것에 대한 결과를 확인
  ```dart
  await expectLater(() async {
  final MaskStore store = await repo.getStore();
  }, throwsException);
 ```
 - repo.getStore가 비동기 메서드이고, 이 메서드가 실패를 했을때 예외처리를 잘 하는지를 확인
 - 이럴 때 위처럼 `expectLater` 메서드를 통해서 검증하면 된다.!
