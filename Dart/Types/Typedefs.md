# Typedefs
[공식문서](https://dart.dev/language/typedefs) 

`typedef` 키워드를 통해 타입의 별명을 지정하여 간편하게 타입을 명시할 수 있다.
```dart
typedef IntList = List<int>;
IntList il = [1, 2, 3];
```
타입 별명 역시 타입 파라미터를 가질 수 있다.
```dart
typedef ListMapper<X> = Map<X, List<X>>;
Map<String, List<String>> m1 = {}; // Verbose.
ListMapper<String> m2 = {}; // Same thing but shorter and clearer.
```

함수에 대해서도 타입 별명을 지정할 수는 있지만, inline function type을 사용하길 권장한다.
```dart
typedef Compare<T> = int Function(T a, T b);

int sort(int a, int b) => a - b;

void main() {
  assert(sort is Compare<int>); // True!
}
```