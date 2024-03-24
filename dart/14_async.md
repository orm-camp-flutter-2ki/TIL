# Async, 비동기

Dart에서의 순서에 따른 프로그래밍을 할 때 대표적으로
동기식 프로그램링과 비동기식 프로그래밍으로 나뉩니다.

### Sync Programming, 동기식 프로그래밍
- 코드가 순서대로 실행됩니다.
- 작업이 완료될 때까지 프로그램이 중단될 수 없습니다.
- 이전 작업이 실행이 완료되어야 다음 작업으로 이어집니다.

일반적으로 별다른 키워드를 사용하지 않는 이상
동기식으로 진행됩니다.

### Async Programming, 비동기식 프로그래밍
- 임의의 순서 혹은 동시에 작업이 진행될 수 있습니다.
- Future, async, await과 같은 키워드가 사용됩니다.


#### Future
미래에 완성이 되는 타입입니다.
```dart
Future<String> name;
Future<int> age;
```
await 등을 사용해서 Future 타입을 해소하면 <> 안에 있는 타입으로 바뀝니다.
Future.delayed와 같은 것도 사용이 가능합니다.
```dart
print('start');

Future.delayed(Duration(seconds: 2), () {
  print('2 seconds');
});

print('end');

// start, end, 2 seconds 순으로 출력
```

#### async, await
Future 함수를 사용하려면 async 키워드를 지정해줘야 합니다.
추가로 async 키워드가 붙은 함수 내에서
대기하고 싶은 비동기 함수를 시행하려면 await 키워드를 붙여줘야 합니다.
```dart
Future<String> getPassword(String password) async {
  String result = await findPassword(password);
  return result;
}
```

