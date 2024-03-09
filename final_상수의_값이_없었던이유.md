# final 상수의 값이 없었던 이유
## 1. 정적프로퍼티를 사용하지않은 이유

```dart
// 기존코드
static final int maximumHp = 50;
static final int maximumMp = 10;

Cleric(this.name, {this.hp = 50, this.mp = 10});
```
1. 제 코드의 생섬함수는 매직넘버를 사용해서 구현되어 있었습니다.
2. 이유는 처초에 제가 위에 선언한 정적 프로퍼티를 활용하여 값을 채워주려 시도하였으나,
3. 에러가 발생하여 "이건 안되나보다"라고 하고 빠르게 넘어간 개념이였습니다. (실수)

## 2. 에러를 살펴보게됨
```dart
// 1차수정코드
static final int maximumHp = 50;
static final int maximumMp = 10;

Cleric(this.name, {this.hp = Cleric.maximumHp, this.mp = Cleric.maximumMp});
```

```dart
1. Error: Member not found: 'maximumHP'. // maximumHP라는 멤버를 찾을 수 없음.

2. Context: The invocation of 'maximumMp' is not allowed in a constant expression.0
// 상수 표현(constant expression)에서 'maximumMp'를 호출하는 것은 허용되지 않습니다.
```

1. 왜 찾을 수 없다고 하는거지? 난 분명히 위에서 선언했는데 생각하였는데...

## 3. 해결
```dart
Cleric secondCleric = Cleric("아서스", hp: 20, mp: 3);

static const int maximumHP = 10;
static const int maximumMP = 10;
```
1. 정답은 const(컴파일시점)와 final(런타임시점)로 선언한 변수들이 메모리에 올라가는 시점에 있었습니다.
2. 제 코드는 두 정적변수를 final로 선언해두었습니다.
3. 따라서, 제가 Cleric이라는 인스턴스를 생성하는 시점 이전에는 `Class.maximumHP`가 아직 메모리에 올라가있지 않은 상태였습니다.
4. 즉, 해당 정적변수에 값이 할당되지 않은 시점에 `Class.maximumHP` 라는 정적변수를 호출하였으므로 에러가 발생하는 것이였습니다.
5. 따라서, 위와 같이 const를 사용해주면 컴파일시점에 변수를 미리 메모리에 올려두므로 Cleric의 생성자로 Cleric을 사용 할 수 있게 되었습니다!
