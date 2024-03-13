# Collection
[공식문서](https://dart.dev/language/collections) 

Dart는 list, set, map을 기본 내장된 컬렉션으로 제공한다.

<br>

## List

프로그래밍 언어에서 가장 일반적인 컬렉션은 array 혹은 정렬된 개체 그룹이다.  
Dart는 array가 List 객체이기 때문에 list라고 부른다.

<br>

###  List 특징
- `[]`로 둘러쌓이고, `,`로 구분된 목록으로 list 리터럴을 만들 수 있다.
    => `var list = [1, 2, 3];`
- list의 idx는 0부터 시작한다.
- list 리터럴 앞에 `cost` 키워드를 붙여 list를 컴파일 상수로 만들 수 있다.

<br>

### List 생성
- 일반적인 List 타입 지정과, 빈 list 생성  
    ```dart
    List<String> strList = [];
    var strList = <String>[];
    ```
- list 리터럴(값)을 통한 list 생성  
    ```dart
    List<String> strList = ['대', '한', '민', '국'];
    ```
- named 생성자를 통한 list 생성
    ```dart
    // growable: true 인자를 추가하여 mutable로 생성도 가능

    List<String> strList = List.filled(3, '초기값'); // ['초기값', '초기값', '초기값']
    //List.filled(int length, E fill, {bool growable = false});

    List<String> origin = ['안', '녕']; 
    List<String> strList = List.of(origin); // ['안', '녕']
    // List.of(Iterable<E> elements, {bool growable = true});

    List<int> nums = List.generate(5, (int idx) => idx * 2); // [0, 2, 4, 6, 8]
    // List.generate(int length, E generator(int index), {bool growable = true});
    ```

<br>

## Set

Set은 순서가 없는 고유한 값들의 집합이다.

<br>

###  Set 특징
- `{}`로 둘러쌓이고, `,`로 구분된 목록으로 set 리터럴을 만들 수 있다.
    => `var list = {1, 2, 3};`
- Dart의 set 기본 구현체가 LikendHashSet이기 때문에 값을 넣은 순서가 유지된다.
- idx를 통한 원소 접근이 불가능하다.
- set 리터럴 앞에 `cost` 키워드를 붙여 set을 컴파일 상수로 만들 수 있다.

<br>

### Set 생성
- 일반적인 Set 타입 지정과, 빈 set 생성
    ```dart
    Set<String> strSet = {};
    var strset = <String>{};
    ```
- set 리터럴(값)을 통한 set 생성
    ```dart
    Set<String> strSet = {'대', '한', '민', '국'};
    ```
- named 생성자를 통한 set 생성
    ```dart
    Set<String> origin = {'안', '녕'};
    Set<String> strSet = Set.of(origin); // {'안', '녕'}
    // Set.of(Iterable<E> elements) = LinkedHashSet<E>.of;
    ```

<br>

## Map

키, 값 쌍으로 이루어진 객체로 키는 중복되지 않는 유일한 값이다.

###  Map 특징
- `{}`로 둘러쌓이고, `,`로 구분된 `키: 값` 목록으로 map 리터럴을 만들 수 있다.
    => `var list = {1, 2, 3};`
- Dart의 map 기본 구현체가 LikendHashMap이기 때문에 삽입한 키의 순서가 유지된다.
- 키, 값에 대한 타입을 각각 갖는다.  
    => `Map<String, int>`
- 키에 대한 값이 없는 경우, null을 반환한다.
- amp 리터럴 앞에 `cost` 키워드를 붙여 map을 컴파일 상수로 만들 수 있다.

<br>

### Map 생성
- 일반적인 Set 타입 지정과, 빈 set 생성
    ```dart
    Map<String, int> strIntMap = {};
    var strIntMap = <String, int>{};
    ```
- set 리터럴(값)을 통한 set 생성
    ```dart
    Map<String, int> strIntMap = {'나': 1, '너': 2};
    ```
- named 생성자를 통한 set 생성
    ```dart
    Map<String, int> origin = {'나': 1, '너': 2};
    Map<String, int> strIntMap = Map.of(origin); // {'나': 1, '너': 2}
    // Map.of(Map<K, V> other) = LinkedHashMap<K, V>.of;
    ```

<br>

## Operators
### Spread 연산자
Dart는 `...`와 null일 수 있는 값에 대한 `...?` spread 연산자를 지원한다.  
spread 연산자는 컬렉션에 여러 값을 간결하게 삽입할 수 있게 해준다.
```dart
var list = [1, 2, 3];
var list2 = [0, ...list]; // [0, 1, 2, 3]
```

<br>

### Control-flow 연산자
Dart는 조건 분기와 반복문을 통한 컬렉션 생성 연산자를 지원한다.  
- collection if  
    => `[값, 값, if (조건) 조건이 참이면 원소로 들어갈 값]`
- collection if-case  
    => `[값, 값, if (비교할 값 case 패턴) 비교할 값이 패턴과 일치하면 들어갈 값 ]`  
    ex) `[0, 1, if ([1, '나'] case [int x, String y]) 2]` = `[0, 1, 2]`
- collection for  
    => `[값, 값, for (타입 변수명 in 이터러블) 반복문을 통해 넣을 값]`  
    ex) `[0, 1, for (int i in [2, 3]) i]` = `[0, 1, 2, 3]`