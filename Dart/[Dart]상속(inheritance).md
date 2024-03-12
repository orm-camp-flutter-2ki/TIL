> ##  상속(inheritance)?
이전에 만든 class와 닮았지만, 일부 다른 클래스를 만들경우 확장하여 기능을 추가하는것
클래스 생성시 `class 서브클래스 extends 슈퍼클래스` 와 같이 생성하여 부모의 속성을 상속받을 수 있다.

```dart
class SuperHero extends Hero {
  //부모의 생성자로 한번 생성을 해야한다.
  SuperHero({required super.name, required super.hp});
}
```

> ##  super?
위에서 살펴본 this가 자기자신이라면 부모 클래스를 지칭하는 키워드는 바로 super이다.
#### _실제로 예습문제 풀면서, super.attackt() 하지 않아서 , 생성자 호출안됨 꼭 확인하면서 사용할껏!!_
![](https://velog.velcdn.com/images/hee462/post/c147866e-f662-4918-b08c-6edfc629bd93/image.png)

> ##  override
이번엔 override라는 annotation에 대해서 알아보겠다. annotation은 주석문이라는 뜻인데 Dart/Flutter에서는 @로 사용되는 것이 annotation을 지칭하는 키워드라고 생각하면 된다.
override는 재정의라는 뜻으로 바로 부모 class를 재정의 한다는 뜻이다.
이게 무슨 말이냐면 만약 class를 상속받은 자식 class에서 부모 class와 똑같은 메소드가 사용된다면 어떤 일이 일어나냐면 바로.. 아무런 일도 일어나지는 않는다.
같은 메소드를 사용한다고 해서 에러가 발생하지는 않는다. 알아서 잘 작동시켜준다. 하지만 @override 키워드를 작성하여 주석문을 추가해 주어야 디버깅이나 문법 구조를 원활하게 이해하고 작성할 수 있다.

```dart
@override
void attack(){
  super.attack(); //부모 메서드 그대로 실행한다는 코드.
  print('추가로, 레이저 빔을 날렸다!');
}
```

> ### ⭐️정리!
 - **올바른 상속**
올바른 상속은 “is-a 원칙” 이라고 하는 규칙에 따른 상속을 말한다
)SuperHero is a Hero (o)
)Inn is a King (x)
 - **잘못된 상속**
현실 세계의 등장인물 사이에 개념적으로 `is-a 관계`가 되지 못 함에도 불구하고 상속을 사용한 경우가 잘못 된 상속 이다.
 잘못된 상속을 하면 안 되는 이유
 _ex) house 가 item 을 상속받았다면, 집은 아이템이다(뭔가이상)
  마법사가 캐릭터를 상속받았다면, 마법사는 캐릭터이다 처럼 말에 모순없어야함_
- 클래스를 확장할 때 현실세계와의 모순이 생긴다
- 객체 지향의 3대 특징 중 1가지 “다형성" 을 이용할 수 없게 된다
![](https://velog.velcdn.com/images/hee462/post/a84f232e-ecfa-4a6a-ae19-444a3f217d84/image.png)

