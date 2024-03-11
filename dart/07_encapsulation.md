## 캡슐화 Encapsulation
### 캡슐화란?
> 데이터와, 데이터를 처리하는 행위를 묶고, 외부에는 그 행위를 보여주지 않는 것. 정보 은닉 개념중 하나이다.

캡슐화는 객체의 속성(Field)과 행위(Method)를 하나로 묶고, 외부로 부터 내부를 감싸 숨겨 은닉한다. 또한 외부의 잘못된 접근으로 값이 의도치 않게 변하는 것을 방지하는 보호 효과도 누릴 수 있다.

```dart
//헉 실수로 죽여버렸다.
class Inn{
  void checkIn(Hero hero){
    hero.hp = -100;
  }
}

```
#### 접근 제한자 Access Modifier
멤버변수에 대한 접근 지정자로는 private과 public 두가지가 있다.

![image](https://github.com/Gunbam27/TIL/assets/95085649/a0ca4c74-ee13-4267-977c-53acfb554944)

private 접근 제한: 오로지 클래스 내부에서만 사용할 수 있습니다. <br/>
public 접근 제한: 모든 클래스에서 아무런 제한 없이 필드와 메소드를 사용할 수 있도록 해줍니다. 

#### getter와 setter
> 메서드를 경유한 필드 조작

getter : 값을 가져옴.메개변수는 없고, 리턴값만 있는 메서드로 정의.read only <br/>
setter : 값을 수정함.매개변수만 있고, 리턴값은 없는 메서드로 정의.write only

```dart
//getter의 사용
//return된 값만 필요하고 굳이 변수로 등록할 일이 없다면 변수등록을 안해도 된다. 
class Hero {
  static int money = 100;
  String name;
  int _hp;
}

Hero({required this.name,required int hp,this.sword}) : _hp = hp;

int get hp => _hp;

```

```dart
//setter의 사용
class Wand {
  String _name;
  double power;

  String get name => _name;

  Wand({
    required String name,
    required this.power,
  }) : _name = name;

  set name(String value) {
    if (value.length < 3) {
      throw Exception('글자가 너무 짧습니다.');
    }
    _name = value;
  }
}

```
