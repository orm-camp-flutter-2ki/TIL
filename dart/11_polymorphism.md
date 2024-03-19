## 다형성(Polymorphism)
> 하나의 객체가 여러 가지 타입을 가질 수 있는 것을 의미한다.
> 각 요소(객체)들이 다양한 자료형(type)에 속하는 것이 허가되는 성질을 가리킨다

### 다형성의 구현
1. 인터페이스 정의 (공통 메서드 통합)
```dart
abstract interface class Drawable {
  void draw();
}
```
2. 인터페이스 구현
```dart
class House implements Drawable {
  void draw() {
    ...
  }
}

```

3. class 생성시 선언부를 인터페이스로 선언
 ```dart
Drawable element = House(...);
List<Drawable> elements = [ ];
elements.add(Dog(...));
 ```

### 다형성 생성시 주의할 점
- Is a 관계가 맞는지 생각해볼 것!
- 타입검사해본 후 as 키워드를 사용하여 타입 캐스팅을 수행한다
