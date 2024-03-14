# 추상클래스와 인터페이스
- 추상클래스가 되려면, 반드시 추상 메소드(선언만 되고 구현이 안된 것. void 중괄호가 없는 것)가 있어야 함. 모든 메소드가 추상메소드

'''
// 추상클래스
abstract class TangibleAsset {
  String name;
  int price;
  String color;

  TangibleAsset(this.name, this.price, this.color);
}

class Book extends TangibleAsset {
  // String name;
  // int price;
  // String color;
  String isbn;

  Book({
    required super.name,
    required super.price,
    required super.color,
    required this.isbn,
  }) : super(name, price, color); //옛날방식
}

//부모 클래스인 TangibleAsset의 생성자를 호출하는 역할

//'super'는 부모 클래스의 생성자나 메서드를 호출할 때 사용됩니다. 
//이 경우에는 TangibleAsset 클래스의 생성자를 호출하여 부모 클래스의 필드를 초기화합니다.
//즉, Computer 클래스의 생성자를 호출할 때 name, price, color 파라미터를 받아와서 
//TangibleAsset 클래스의 생성자를 호출하여 해당 파라미터들을 부모 클래스의 속성에 전달하게 됩니다. 
//이렇게 함으로써 코드의 중복을 방지하고 상속을 통해 부모 클래스의 기능을 재사용할 수 있습니다.


class Computer extends TangibleAsset { 
  // String name;
  // int price;
  // String color;
  String makerName;

  Computer({
    required super.name, //현재 방식 super.
    required super.price,
    required super.color,
    required this.makerName,
  }) : super(name, price, color); //옛날방식
}
'''

- 인터페이스
    - 다중 상속 금지했으니, 기능 하나는 더 쓰고 싶을 때, 필드를 가지지 않음
    - 꼭 메소드가 반드시 있어야 할 필요없음
    - Dart3부터 interface 키워드 추가(implements 사용 강제)
- ‘_’ private
    '''
    int _hp;
    '''