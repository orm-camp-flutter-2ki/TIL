240318 (Mon)

플러터 과정 11일차

## 제네릭 
객체 지향에서 지원하는 것
List<E> class & Map<K, V> class

<> 안을 제네릭이라고 부른다.

타입을 나중에 원하는 형태로 정의할 수있음

타입 안전 (type safe) 효과

#### 제네릭을 사용하지 않는 Pocket 클래스(ver 1)
```dart
class Pocket {
Object? _data;

void put(Object data) {
_data = data;

}

Object? get() {
return _data;

}
}
```

#### 제네릭을 사용한 Pocket 클래스 (ver 2)
```dart
class Pocket<E> {
E? _data;

void put(E data) {
data = data;

E? get() {
return _data;

}
}
```

#### 타입에 제약을 추가한 Pocket 클래스 (ver 3)
```dart
class Pocket<E extends book> {
E? _data;

void put(E data) {
data = data;

E? get() {
return _data;

}

}
```

