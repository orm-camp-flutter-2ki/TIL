# 다트 기본 문법

#### 다트 값 입력 & 출력
값 입력 받는 방법 : `String? input = stdin.readLineSync();`<br/>
한 줄에 여러 값 입력 받는 방법 : `List<String>? input = stdin.readLineSync()?.split(' ');`<br/>
여러 줄에 여러 값 입력 받는 방법 : <br/>
```
List<int> list = [];
  for(int i=0;i<5;i++){
    String? input = stdin.readLineSync();
    int? number = input != null ? int.tryParse(input) : null;
    if(number != null){
      list.add(number);
    }
  }
```

값 출력 하는 방법 : `print('OK');`

### 다트 반복문

리스트의 길이 만큼 반복한다.
+ ```
  for(int i = 0; i < list.length; i++){
    print(i);
  }
  ```

numbers안의 요소들을 출력한다.
+ ```
  for (int number in numbers) {
    print(number);
  }
  ```
+ ```
  numbers.forEach((number) {
    print(number);
  });
  ```

count가 5보다 작을 때까지 count를 출력한다.
+ ```
  while (count < 5) {
    print(count);
    count++;
  }
  ```

무한 루프
+ ```
  while (true) {
    print(무한으로 출력됩니다);
  }
  ```
  
