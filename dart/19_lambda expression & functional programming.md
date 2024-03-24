## 람다식 Lambda expression
`익명 함수(Anonymous functions)`를 지칭하는 용어이다.

### 익명함수
익명함수란 말그대로 함수의 이름이 없는 함수이다. <br/>
익명함수들은 공통으로 `일급객체(First Class citizen)`라는 특징을 가지고 있다. <br/>
`일급객체`란 변수에 대입 가능한 객체를말한다. `ex)대표적인 1급 객체 : 값, 인스턴스, 함수`

```dart
//아래식처럼 간단하게 표현할 수 있다.
list.sort((a,b)=> a.value.compareTo(b.value));
```
### 함수형 프로그래밍 Functional Programming
- 대입문이 없는 프로그래밍
- 함수형 프로그래밍은 거의 모든 것을 순수 함수로 나누어 문제를 해결하는 기법
- 다트는 객체지향 프로그래밍(OOP)과 함수형 프로그래밍(FP) 특징을 모두 제공하는 멀티 패러다임 언어이다.

#### 고계 함수 (Higher-order function)
> 고계 함수란 함수를 파라미터로 받는 함수이다.where, map, forEach, reduce, fold, any 가 있다. 

- where : 조건을 만족하는 값을 찾아 모아준다.
  ```dart
  final items = [1,2,3,4,5];

  items.where((e)=> e % 2 == 0); //2,4
  ```
  <br/>
- map : 변환하여 Iterable타입으로 반환해준다.
  ```dart
  transactions.map((transaction) => transaction.trader.city);
  //(Cambridge,Cambridge,Cambridge,Milan,Milan,Cambridge)
  ```
  <br/>
- toList() : Iterable값을 List타입으로 변환해준다
  ```dart
  transactions.map((transaction) => transaction.trader.city).toList();
  //[Cambridge,Cambridge,Cambridge,Milan,Milan,Cambridge]
  ```
  <br/>
- toSet() :Set으로 변환하는 함수.중복을 허용하지 않기 때문에 간단히 중복데이터를 제거할 수 있다
  ```dart
  transactions.map((transaction) => transaction.trader.city).toSet();
  //{Cambridge, Milan}
  ```
  <br/>
- forEach : 전체 값을 순회하며 식을 수행한다.
  ```dart
  transactions.map((transaction) => transaction.trader.city).forEach(print);
  //Cambridge Cambridge Cambridge Milan Milan Cambridge
  ```
  <br/>
- reduce : 요소를 하나씩 더하여 줄여나가기(전체값 더하기)
  ```dart
  final items = [1,2,3,4,5];

  items.reduce((e,v)=> max(e,v)); //5
  ```
  <br/>
- fold : fold메서드는 초기값과 함께 사용되며, 리스트의 각 요소를 순회하면서 초기값과 요소를 결합하여 새로운 값을 계산한다.
  ```dart
  final items = [1,2,3,4,5];

  items.fold((0,(previousValue, element)=> return previousValue + element);
  //15
  ```
  <br/>
- any : 있는지 없는지를 bool타입으로 반환한다. 
  ```dart
  transactions.any((transaction) => transaction.trader.city == "Milan");
  //true
  ```
  <br/>
- sort : a>b일때 1, a==b일때 0, a<b일때 -1을 반환하기 때문
  ```dart
    list1.sorted((a,b)=> b.length.compareTo(a.length)) //오름차순
    list1.sorted((a,b)=> a.length.compareTo(b.length)) //내림차순
  ```
### .. cascade 
- 오브젝트를 반환하지 않을때(sort처럼 return 값이 void일 때) 써서 체인메서드를 가능하게 해준다.
- 사용 시 경우에 따라 ()로 감싸서 우선순위를 매겨줘야 한다.
  
### .sorted vs ..sort
- sorted는 링크에서 설치 후 사용 가능하다.
https://pub.dev/packages/collection/install

- sorted는 복사본을 가공한후 List타입으로 리턴한다.
- sort는 void를 리턴한다. 따라서 체인메서드가 불가능 이기에 ..cascade를 사용한다.
- 다만 메서드 체인으로 다른 기능을 호출할 것이 아니라면 cascade를 사용하지 않는다.
- sort는 void이기 때문에 변수에 등록 안된다.
  ```dart
  List list1 = ['one', 'two', 'three'];
  
  //..sort
  list1..sort((a, b) => b.length.compareTo(a.length)).map((transaction) => transaction.trader.name);
  print(list1); // [three,one,two] 가 반환 Why? list1에 덮어 씌우니까
  ```
  ```dart
  //.sorted
  list1.sorted((a, b) => b.length.compareTo(a.length)); //프린트 시 [three, one, two] 반환
  print(list1); // [one, two, three] 가 반환. list1의 값이 재할당 되지 않았다. Why? list1을 복사해서 가공하니까
```
