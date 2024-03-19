## 제네릭(Generic)
> 제네릭은 클래스에 사용할 데이터 타입을 컴파일 시에 미리 지정하는 방법이다. 타입을 나중에 원하는 형태로 정의할 수 있다. Type safe 효과
```dart
//제네릭을 사용한 Pocket 클래스
//이후 값을 입력하면 해당 값의 타입이 E자리에 들어가게 된다.
class Pocket<E> {
  E? _data;

  void put(E data) {
    _data = data;
  }

  E? get() {
    return _data;
  }
}
```

## 열거형 (Enum)
> 상수들이 집합을 이루는 자료형이다. 리팩토링 시 변경 범위가 최소화 된다. 내용을 추가해도 Enum 코드만 수정하면 된다. 휴먼 에러 최소화.

```dart
//간단한 열거형 선언
//type과 count는 다릇곳에서 작성해야한다.
//switch문과 쓰이는 경우가 많다.
enum KeyType {
  padlock,
  button,
  dial,
  finger,
}

//향상된 열거형 선언
enum KeyType {
  padlock(type: 'padlock', count: 1024),
  button(type: 'button', count: 10000),
  dial(type: 'dial', count: 30000),
  finger(type: 'finger', count: 1000000);

  final String type;
  final int count;

  const KeyType({required this.type, required this.count});
}
```
향상된 열거형 선언을 쓰기위해서는 몇가지 규칙이 있다
- 변수는 모두 final로 선언되어야 한다.
- 생성자는 무조건 const여야 한다.
- index, hashCode, == 연산자들을 override할 수 없다.
- 인스턴스는 시작부에 선언되어야 하며, 인스턴스가 하나 이상 있어야 한다.
 
