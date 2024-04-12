# InheritiedWidget

일반적으로 생성자를 통해서 부모 클래스에서 자식 클래스로
데이터 전달이 가능합니다.
```dart
class A {
  B b;
  A(this.b);
}

class B {
  C c;
  B(this.c);
}
...

void main () {
  final instance = A(B(C()));
}
```
이렇게 의존성을 주입하면 코드의 재사용을 높이고 결합도를 낮출 수 있습니다.
그러나 전달받고 싶은 데이터가 상당히 상위에 위치해있으면
계속계속 자식 클래스에 데이터를 전달하며 여러 클래스를 거쳐야 합니다.
InheritedWidget은 그런 번거로움을 막아줍니다.

```dart
Theme.of(context).colorScheme.primary;
MediaQuery.of(context).size.width
```
context라는 위젯 트리 정보를 알고 있는 객체를 이용하여
Theme.of와 MediaQuery.of같이 상위에 있는 위젯을 곧바로 사용할 수 있습니다.

또한 Provider와 GetX같은 상태 관리 패키지에서도 이용됩니다.
