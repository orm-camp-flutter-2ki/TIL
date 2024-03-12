# Collection
## List
- 순서대로 쌓여있는 구조
- item 의 중복 허용
- 크기를 정하지 않고 요소를 추가할 때마다 크기가 증가
- \[\] 로 표기
- List 의 탐색 방법
  
  ```
  List<String> names = ['홍길동', '한석봉', '이순신', '강감찬', '세종대왕'];
  for (int i = 0; i < names.length; i++) {
    print(names[i]);
  }

  for (final name in names) {
    print(name);
  }

  names.forEach((name) {
    print(name);
  }

  names.forEach(print);
  ```  
## Set
- 순서가 없는 집합
- item 의 중복 불가
- \{ \} 로 표기
- List d의 contains 보다 압도적으로 빠르다.
  ```
  Set<int> lottoSet = {1, 2, 3, 4};

  print(lottoSet.contains(1));  // true
  print(lottoSet.contains(5));  // false
  ```

## iterator
- List 또는 Set 에서 요소를 탐색할 수 있다.
  
  ```
  // List 에서
  List<int> subjects = [10, 50, 100, 100, 50];
  
  final iterator = subjects.iterator;
  while (iterator.moveNext()) {
    print(iterator.current);
  }

  // Set 에서
  Set<int> lottoSet = {1, 2, 3, 4, 5, 6};

  final iterator = lottoSet.iterator;
  while (iterator.moveNext()) {
    print(iterator.current);
  }  
  ```

## Map
- key - value 가 쌍으로 저장
- key 의 중복 불가
  
  ```
  Map<String, dynamic> gildong = {
    'name' : '홍길동',
    'id' : 0,
    'age' : 20,
  };
  ```

- Json 처럼 사용할 수도 있다.
  
  ```
  List<Map<String, dynamic>> students = [
    {
      'name' : '홍길동',
      'id' : 0,
      'age' : 20,
    },
    {
      'name' : '한석봉',
      'id' : 1,
      'age' : 22,
    },
  ];
  ```

- Map 에 저장된 값 하나씩 얻기.

  ```
  Map<String, dynamic> gildong = {
    'name' : '홍길동',
    'id' : 0,
    'age' : 20,
  };

  gildong.entries.forEach((element) {
    print(element.key);
  });

  gildong.entries.forEach((element) {
    print(element.value);
  });
  ```

- Map 은 순서를 보장하지 않기 때문에 매번 출력 결과의 순서가 다르게 표시될 수 있다.
- 컬렉션 안에 컬렉션을 넣을 수 있다.
  
  ```
  Map<String, List<String>>
  List<List<Hero>>
  ```
