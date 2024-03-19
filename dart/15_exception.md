## 예외 (Exception)
> 프로그램을 만들다 보면 수없이 많은 예외 상황이 발생한다.(문법 에러, 런타임 에러, 논리에러)

> 이러한 예외 상황을 무시하고 싶을 때도 있고, 적절한 처리를 하고 싶을 때도 있다.

> 원하는 대로 예외를 처리하기 위해서 try ~ catch, throw Exception 구문을 이용해 보자.

### try catch
```dart
void main(){
  try{
    someError();  //시도할 코드
  } catch(e){
    print(e);    //오류가 나면 실행할 코드
  }
}
```

### throw
- 에러를 발생시키는 코드. 아래쪽에 try catch문이 있고 그 함수에서 에러를 핸들링하고 싶을때 아래로 던진다.
```dart
//위와 이어지는 코드
void someError(){
  // 실행하고자 하는 코드
  throw Exception('에러가 발생했습니다.');
}
```

### rethrow
- 위쪽 함수에서 에러를 핸들링하고 싶을때 위로 던진다.
```dart
void main (List<String> arguments) {
  try {
    someError2();
  } catch (e) {
    print(e);
  }
}

void someError2() {
  try {
    someError();
  } catch (e) {
    rethrow;
  }
}

void someError() {
// 실행하고자 하는 코드
throw Exception('에러가 발생했습니다.');
}
```

### finally
- 나중에 꼭 해야하는 처리를 할 수 있다. try문 실행하던 catch문을 실행하던지 간에, 꼭 실행된다.
```dart
try{
  someError2();
} catch {
  print('에러 발생');
} finally {
  print('무조건 실행되는 코드');
}
``` 
