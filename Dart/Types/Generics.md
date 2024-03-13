# Generics
[공식문서](https://dart.dev/language/generics)   

제네릭은 객체나 함수의 파라미터 타입을 객체나 함수 내부가 아닌, 호출하는 외부에서 지정할 수 있도록 하는 것이다.

## Generics를 사용하는 이유
제네릭은 일반적으로 type-safety를 위해 사용되지만, 2가지 추가적인 이점이 있다.  
1. 적절한 제네릭 타입 지정은 코드 작성에 도움을 준다.  
    list의 타입 파라미터를 지정함으로써 협업하는 개발자들에게 해당 list 원소 타입이 무엇인지 명시할 수 있다.

2. 제네릭을 통해 코드 중복을 줄일 수 있다.  
    제네릭은 하나의 인터페이스와 구현체를 다양한 타입과 공유할 수 있게 해주면서도, 정적 (타입) 분석을 지원받을 수 있게 해준다.  
    아래의 코드는 제네릭을 사용함으로써 각 타입별로 코드를 중복 작성할 필요를 없애고, 인자로 받은 타입 파라미터를 통해 코드 내부에서 정적 분석 역시 여전히 적용되게 해준다.
    ```dart
    abstract class Cache<T> {
        T getByKey(String key);
        void setByKey(String key, T value);
    }
    ```

<br>

### Collection에서 Generics
컬렉션 리터럴을 만들 때, 컬렉션이 담고 있는 원소의 타입을 괄호 앞에 명시한다.  
이 역시 제네릭이며, parameterized 리터럴이라고도 부른다.  
(Parameterized : 타입이 지정된 or 타입을 지정하는)
```dart
var names = <String>['Seth', 'Kathy', 'Lars'];
var uniqueNames = <String>{'Seth', 'Kathy', 'Lars'};
```
컬렉션의 생성자에도 parameterized 타입을 지정하여 컬렉션의 내부 원소 타입을 지정할 수 잇다.
```dart
var views = Map<int, View>();
```

<br>

### Generic의 타입 파라미터는 reified
Dart에서 제네릭 타입 파라미터는 기본적으로 reified(구체화)된다.  
기본적으로 제네릭의 타입 파라미터를 본문에서 소거하는 Java, Kotlin과 달리, Dart는 런타임에 컬렉션의 원소에 대한 타입 검사가 가능하다.
```dart
var names = <String>[];
names.addAll(['Seth', 'Kathy', 'Lars']);
print(names is List<String>); // true
// Java, Kotlin은 name이 List타입인 것 까지만 확인 가능
```

<br>

### 타입 파라미터의 상한
`extends` 키워드를 통해 타입 파라미터의 상한을 정할 수 있다.  
아래의 코드에서 클래스 Foo의 타입 파라미터는 `SomeBaseClass`를 포함한 하위 타입만 가능하다.
```dart
class Foo<T extends SomeBaseClass> {
  // Implementation goes here...
  String toString() => "Instance of 'Foo<$T>'";
}
```
타입 파라미터를 생략할 경우, 기본적으로 상한 타입으로 지정된다.
```dart
var foo = Foo();
print(foo); // Instance of 'Foo<SomeBaseClass>'
```