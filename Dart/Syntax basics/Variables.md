# Variables

### 기본 형태 : `[타입] [변수명] = [초기값];`

### 변수 타입에 `var`을 지정하여 타입 추론 가능

<br/>

## Null safety

### 변수 타입 뒤에 `?`를 붙여 nullable한 타입으로 만들 수 있다.
- nullable한 타입은 초기화하지 않아도 null로 초기화
- non-nullable한 타입은 초기화 없이 접근시, 런타임 에러 발생
```dart
void main() {
  String nonNull;
  String? nullable;

  print(nonNull); // Error: Non-nullable variable 'nonNull' must be assigned before it can be used.
  print(nullable); // null 출력
}
```

<br/>

## `late` 변수
### `late` 변경자를 통해 변수를 선언하는 경우
1. non-nullable한 변수를 선언 이후, 초기화 하고 싶은 경우
2. [지연 초기화](#지연-초기화란)를 하는 경우  

하지만 1, 2 모두 일반적인 non-nullable한 변수를 선언해서 사용해도 문제 없어 보인다.  
(초기화 이전에 non-nullable한 변수에 접근하는 경우 컴파일러가 에러를 표시해주었다)  
왜 굳이 `late` 변수를 사용해야 할까?

<br/>

### `late` 변수를 사용하는 이유
non-nullable한 변수를 선언만 하고 초기화를 하지 않고 접근하는 경우, 아래의 상황에서 컴파일러가 이를 정상적으로 감지 하지 못한다.
- top-level 선언
- instance 변수

즉, 초기화의 범위를 컴파일러가 단정할 수 없는 경우, 애러임에도 에러가 표시되지 않거나, 정상적으로 초기화하여도 에러가 표시될 수 있다.  

따라서, [위와 같은 경우](#late-변경자를-통해-변수를-선언하는-경우)에는 `late` 변경자를 쓰는 것이 더 바람직하다.

<br/>

### 지연 초기화란?
지연 초기화는 변수의 선언보다 초기화의 시점이 더 늦는 것을 뜻하며, 아래의 경우에서 유용하다.
1. 변수가 사용되지 않을 가능성이 큰 경우  
    => 굳이 미리 초기화할 필요가 없음

2. 초기화의 비용이 큰 경우  
    => 초기화를 최대한 미룰 수록 메모리 사용 및 병목현상을 최소화할 수 있음

3. instance 변수로 초기화되고 초기화 과정에서 `this`에 접근하는 경우  
    => 초기화에 필요한 참조가 변수 선언 시점에 아직 없음


## ~~Final and Const~~