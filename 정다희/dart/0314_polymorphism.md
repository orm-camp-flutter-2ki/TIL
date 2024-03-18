# 다형성
- 핸들, 왼쪽 브레이크, 오른쪽 엑셀인것 = 차, 버스, 그랜저...
- 세부적인 부분은 다르겠지만 크게보면 모두 차이다.

## 이렇게 하는 이유?
동일한 동작을 보장, 강제하기 위해서.

## 활용방법
선언을 상위 개념으로,인스턴스 생성은 하위 개념으로 한다.

하나의 참조를 통해 다양한 객체의 메소드를 호출할 수 있음.

```dart

abstract class Animal {
  void speak();
}

class Dog extends Animal {
  @override
  void speak(){
    print('멍멍');
  }
}

class Cat extends Animal {
  @override
  void speak(){
    print('야옹');
  }
}

void makeAnimalSpeak(Animal animal){
  aimal.speak();
}

void main(){
  Animal myCat = Cat();
  Animal myDog = Dog();
  makeAnimalSpeak(myCat); // 야옹
  makeAnimalSpeak(myDog); // 멍멍
}

```

## 장점
- 코드 재사용성
- 유연성
- 유지보수 용이함

## dart는 오버로딩을 지원하지 않음. 
그래서 다른 타입의 parameter를 받는 메소드를 받고싶으면 이름을 바꿔서 메소드를 추가해줬어야 했음
하지만 다형성을 사용하면 그러지 않아도 됨!