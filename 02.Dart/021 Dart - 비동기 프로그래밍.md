---
title: 021 Dart - 비동기 프로그래밍
author: Kim Donghyeok
created_at: 2024-03-21
updated_at: 2024-03-21
tags:
  - 생존코딩
  - 오름캠프
  - dart
---

# 동기 (sync) 프로그래밍

코드가 순서대로 실행된다.

작업이 완료될 때까지 프로그램이 중단될 수 없다.

모든 작업은 이전 작업의 실행이 완료 될 때까지 기다려야 한다.

# 동기와 비동기

동기는 기존 작업의 응답을 받기 전까지 다음 작업을 시작 할 수 없다

비동기는 기존 작업의 응답을 기다리면서 다음 작업을 시작 할 수 있다.

![[240321_Pasted image 20240321104214.png]](/02.Dart/_resources/240321_Pasted%20image%2020240321104214.png)

작업이 완료될 때까지 기다리지 않기 때문에 효율적으로 프로그램이 동작한다.

![[240321_Pasted image 20240321104313.png]](/02.Dart/_resources/240321_Pasted%20image%2020240321104313.png)

![[240321_Pasted image 20240321104433.png]](/02.Dart/_resources/240321_Pasted%20image%2020240321104433.png)

# 비동기 (async) 프로그래밍

임의의 순서로 또는 동시에 작업이 실행 될 수 있다.

비동기를 처리하는 방법에는 콜백, Futurem async-await 방식이 있다.

## 콜백 함수

비동기는 현재코드의 실행결과를 기다리지 않고 이후 코드를 수행하는 기법이다.  
컴퓨팅 자원을 효율적으로 사용하는 기법이지만 정확한 순서를 지켜 수행해야 하는지를 고려해야 한다.  
비동기 코드를 순서대로 실행하는 가장 일반적인 방안으로 **콜백(Callback)** 이 있다.  
콜백은 **실행 가능한 함수를 인자로 전달**하여, **특정 상황이 발생할 때 호출**되게 하는 방식이다.  

## Future

미래에 완료되는 객체

JavaScript 의 Promise 에 대응

Future 는 '미래' 에 받아올 값을 의미

```dart
Future<String> name;
Future<int> number;
FutureM<Person> person;
```

### Future 작성

Dart 및 Flutter 의 많은 API 는 Future 타입을 리턴한다.

다음 코드는 비동기 코드를 시뮬레이트 하기 위해 5초 후에 실행되는 Future 함수를 정의 한 것이다.

```dart
final delay = Future.delayed(Duration(seconds: 5));
```

### async-await

Future 함수는 함수 본문 앞에 async 앞에 키워드를 지정해줘야 한다.

대기하고 싶은 비동기 함수를 실행 할 때 await 키워드를 사용해주면 코드를 작성한 순서대로 실행된다.

```dart
Future<bool> myFuture() async {  
  await Future.delayed(Duration(seconds: 1));  
  
  print('myFuture');  
  return true;  
}
```

```dart
void main() async {
 print('시작');  
   
 final delay = await Future.delayed(Duration(seconds: 1), () {  
   print('콜백');  
 });  
   
 print('끝');
}

// 결과
// 시작
// 콜백
// 끝
```

### then()

Future 함수는 결과를 then() 함수를 통해서 받을 수 있다.

then() 함수로 전달되는 콜백 함수에 다음에 실행할 코드를 작성하면 된다.

다음 코드가 Future 라면 계속해서 then() 을 이어서 전달 받을 수 있다.

불필요한 인자는 \_를 쓰는 것이 관례이다.

## Future 핸들링

Future는 성공(then)일 수 도 오류(catchError)일 수도 있다.

### then() 사용의 문제점

- 콜백보다는 편하지만 동기식 코드보다는 결과예측이 어렵다.
- 단계가 많아지면 then()을 연결하는 체이닝 방식을 사용하는 것이 만만치 않다.
- 로직이 복잡해지면 적절한 예외처리하기에 용이하지 않다.

## 예외처리의 정석

```dart
Future<String> getData() async {
 try {
  // 데이터를 가져오는 비동기 작업
  var data = await _getDataFromAPI();
  return data;
 } catch (error) {
  // 데이터를 가져오는데 실패했을 때 처리
  print('데이터를 가져오는데 실패 했습니다.: $error');
  return '';
 }
}
```

# 병렬(Parallelism) 처리

병렬처리는 동시에 어려가지 일을 진행하는 것이다.

Future 함수는 await 없이 사용하면 동시에 여러개를 실행 할 수 있다.

VS 동시성 (Concurrency) = 동시에 실행되는 것 같아 보임

![[240321_Pasted image 20240321114001.png]](/02.Dart/_resources/240321_Pasted%20image%2020240321114001.png)

---

# 정리

1. 비동기를 다루는 방법을 모두 말할 수 있어야 한다.
2. await 키워드 뒤에는 반드시 Future 타입이 와야한다.
3. await 키워드 뒤에는 async 키워드가 있는 함수에서만 사용 할 수 있다.
4. 에러처리나 가독성, 처리상황에 따라 적절한 코드를 잘 선택할 수 있어야 한다.
