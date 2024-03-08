## Null Safety
> Null : 값이 없음. 즉 할당되지 않은 상태. (0조차 아니다)
<br/>

### 1. Null이 가능한 타입
null을 허용하려면 타입 뒤에 ?를 붙여야 한다.

```dart
int i = null; //error
int? i = null //가능
int? i        //가능
```
string 과 string?은 다른 타입이다.
<br/>
<br/>
### 2. Null 처리에 관한 기능
```dart
??
//앞에 객체가 null인 경우 ?? 뒤에 작성한 값으로 반환한다.
int value = nullableValue ?? 0

!
//nullable인 값을 Null이 아님을 보증함. 개발자에게 책임이 따르므로 주의해서 사용해야 함.
int? nullableValue = 10;
int value = nullableValue!;

?.
//null이 아니면 해당코드를 수행하고 null이면 null을 반환
int? nullableValue = 10;
print(nullableValue?.toString()); //10출력

int? nullableValue = null;
print(nullableValue?.toString()); //null 출력

```
<br/>

### 3. Null Safety의 장점
- null을 허용하지 않는 변수는 null이 아님을 100% 보장한다.
- 개발자의 실수를 미연에 방지할 수 있다.
- 항상 예측이 가능한 코딩을 할 수 있다.
- 컴파일러가 변수의 널 검사를 진행하지 않아도 되기 때문에 컴파일 속도가 대폭 향상된다.
