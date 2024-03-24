## 동기 프로그래밍 (Sync programming)
> 코드가 순서대로 실행된다. 작업이 완료될 때까지 프로그램이 중단될 수 없다. 모든 작업은 이전 작업의 실행이 완료될 때까지 기다려야 한다.

- 기본적으로 Dart는 동기형 프로그램이다.

## 비동기 프로그래밍 (Async programming)
> 임의의 순서로 또는 동시에 작업이 실행될 수 있다. 비동기를 처리하는 방법에는 콜백, Future+then , Future+async & await 방식이 있다.
- 우리는 Future, async & await를 주로 사용할 예정~
  
![image](https://github.com/Gunbam27/TIL/assets/95085649/115d272c-8384-4592-a7a4-e9727515ddc4)

### Future
아직은 값&결과를 모르지만 미래에 완성이 되면 값&결과를 알 수 있는 객체입니다.
`await`을 사용해서 `Future 타입을 해소`하면 <> 안에 있는 타입으로 바뀝니다.
```dart
Future<String> name;
Future<int> age;
```
### then()
- Future 함수는 결과를 then() 함수를 통해서 받을 수 있다.
- then() 함수로 전달되는 콜백 함수에 다음에 실행할 코드를 작성하면 된다.
- 다음 코드가 Future라면 계속해서 then() 을 이어서 결과를 전달받을 수 있다.
- 불필요한 인자는 _ 를 쓰는 것이 관례이다.
```dart
final user = {
  'email': 'abc@abc.com',
  'password': '123456',
  'name': 'John Doe',
}；

saveDb(user)
  .then ((_) → sendEmail(user))
  .then ((_) → getResult(user))
  .then ((value) → print(value));
```

### async, await
Future 함수를 사용하려면 async 키워드를 지정해줘야 합니다.
추가로 async 키워드가 붙은 함수 내에서
대기하고 싶은 비동기 함수를 시행하려면 await 키워드를 붙여줘야 합니다.
```dart
Future<String> getPassword(String password) async {
  String result = await findPassword(password);
  return result;
}
```
### Future.wait
- Future.wait() 는 모든 처리가 끝날때 까지 기다린다
- 몇 초의 시간이 걸릴지 생각해보자

```dart
Future<int> getInt1() async{
  await Future.delayed(Duration(seconds: 1));
}

Future<int> getInt2() async{
  await Future.delayed(Duration(seconds: 1));
}

Future<int> getInt3() async{
  await Future.delayed(Duration(seconds: 1));
}

Future<void> printParallelInts() async {
  List<Future<int>> futures = [
    getInt1(),
    getInt2(),
    getInt3(),
  ];

List<int> results = await Future.wait(futures);

print(results); //정답은 1초
}
```
### Future.delayed

```dart
print('start');
Future.delayed(Duration(seconds: 2), () {
  print('2 seconds');
});
print('end');
// start, end, 2 seconds 순으로 출력
```

```dart
print('start');
await Future.delayed(Duration(seconds: 2), () {
  print('2 seconds');
});
print('end');
// start, 2 seconds, end 순으로 출력
```
### 예외처리 try catch
```dart
Future<String> getData() async {
  try {
  // 데이터를 가져오는 비동기 작업
  var data = await _getDataFromAPI() ;
  return data;
} catch (error) {
  // 데이터를 가져오는 데 실패했을 때 처리
  print ('데이터를 가져오는 데 실패했습니다: $error'):
  return '';
  }
}
```
### Future.timeout
```dart
void main() async {
  try{
    //5초후 타임아웃에러가 발생되는 코드
    await timeoutFuture().timeout(Duration(seconds: 5));
  }catch(e){
    print('timeout');
  }
}

//6초가 지연되는 코드
Future<String> timeoutFuture() async {
  await Future.delayed(Duration(seconds: 6));
  return 'ok';
}
```
