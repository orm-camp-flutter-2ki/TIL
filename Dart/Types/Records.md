# Records
[공식문서](https://dart.dev/language/records)  

Records는 익명, 불변, 집합 타입으로 다른 컬렉션 타입처럼 여러 객체를 하나의 객체로 묵는다.  
    => Unlike other collection types, records are fixed-sized, heterogeneous, and typed.

<br>

### Record 문법
- Record 표현식은 괄호안의 `,`로 구분된 named 혹은 positional 필드이다.  
    => `var record = ('first', a: 2, b: true, 'last');`
- 파라미터와 리턴 타입에 Record를 사용할 땐, 괄호에 타입을 넣으면 된다.  
    => `(int, int) wap((int, int) record) {...}`
- Record의 named 필드는 Record 타입의 일부이다.  
    ```dart
    ({int a, int b}) recordAB = (a: 1, b: 2);
    ({int x, int y}) recordXY = (x: 3, y: 4);

    // Compile error! These records don't have the same type.
    // recordAB = recordXY;
    ```
- positional 필드에도 이름을 붙일 수 있지만, 이 이름은 타입의 일부가 아니다
    ```dart
    (int a, int b) recordAB = (1, 2);
    (int x, int y) recordXY = (3, 4);

    recordAB = recordXY; // OK.
    ```   
=> 함수의 positional 파라미터의 이름이 함수의 시그니처에 영향을 주지 않는 것과 동일

<br>

### Record 필드
- Record는 built-in getter를 통해 접근할 수 있다.  
    => Record는 불변이기 때문에 setter는 없음
- named 필드에 대해 동일한 name으로 접근할 수 있고, positional 필드에 대해 `$<position>` 형태로 positional 필드의 순서를 통해 접근할 수 있다.  
    => 이때, named 필드는 순서에서 무시된다.  
    => `var record = ('first', a: 2, 'last')`  
    => `record.$1` = 'first'  
    => `record.a` = 2  
    => `record.$2` = 'last'  

<br>

### Record 타입
- Record는 별개의 타입 선언이 존재하지 않고, 필드에 의해 타입이 지정된다.
- Record의 형태(필드, 필드의 타입, 필드의 이름)가 Record의 타입을 결정한다.
- Record는 내부에 다양한 타입을 동시에 담을 수 있다.   
    ```dart
    (num, Object) pair = (42, 'a');

    var first = pair.$1; // Static type `num`, runtime type `int`.
    var second = pair.$2; // Static type `Object`, runtime type `String`.
    ```

<br>

### Record 동등성
- 두 Record가 동일한 형태(필드의 집합)를 갖고 있고, 각 필드가 서로 같은 값을 같는 다면 동등하다.
- named 필드의 순서는 Record의 형태에 영향을 주지 않기 때문에, 순서의 차이는 동등성에 영향을 주지 않는다.
- Record는 자신이 가진 필드의 구조를 통해 `hashCode`와 `==` 메서드를 자동으로 정의한다.
    ```dart
    (int x, int y, int z) point = (1, 2, 3);
    (int r, int g, int b) color = (1, 2, 3);

    print(point == color); // Prints 'true'.

    ({int x, int y, int z}) point = (x: 1, y: 2, z: 3);
    ({int r, int g, int b}) color = (r: 1, g: 2, b: 3);

    print(point == color); // Prints 'false'. Lint: Equals on unrelated types.
    ```

<br>

### 다중 리턴
- Record는 함수가 다양한 값들을 묶어 한번에 반환할 수 있도록 해준다.
- 반환 받은 Record는 패턴 매칭을 통해 구조분해하여 변수에 할당할 수 있다.  
    => 구조분해선언  
    ```dart
    // Returns multiple values in a record:
    (String name, int age) userInfo(Map<String, dynamic> json) {
    return (json['name'] as String, json['age'] as int);
    }

    final json = <String, dynamic>{
    'name': 'Dash',
    'age': 10,
    'color': 'blue',
    };

    // Destructures using a record pattern with positional fields:
    var (name, age) = userInfo(json);

    /* Equivalent to:
    var info = userInfo(json);
    var name = info.$1;
    var age  = info.$2;
    */
    ```
- named 필드의 이름을 통해 구조분해를 할 수도 있다.  
    ```dart
    ({String name, int age}) userInfo(Map<String, dynamic> json)
    // ···
    // Destructures using a record pattern with named fields:
    final (:name, :age) = userInfo(json);
    ```
=> 클래스 선언, 컬렉션 등, 다른 방법으로 함수의 여러 값 반환을 구현할 수 있지만, 코스트가 더 크고 type safety하지 않을 수 있다.