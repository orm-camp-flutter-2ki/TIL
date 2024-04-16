---
title: 004 Navigation
author: Kim Donghyeok
created_at: 2024-04-24
updated_at: 2024-04-24
tags:
  - 생존코딩
  - 오름캠프
  - flutter
---

# Navigation

> <https://docs.flutter.dev/ui/navigation>

![alt](https://upload.wikimedia.org/wikipedia/commons/2/29/Data_stack.svg)

Navigation

- 어떤 화면에서 다른화면으로 화면전환 되는것을 말한다.
- Navigation 은 Stack 구조로 관리 된다
  - pop : 다른 화면으로 전환
  - push : 이전 화면으로 되돌아 오기

## route

flutter 에서 navigation 은  MaterialApp 의 route 속성을 통해 어떤 path 를 통해 어떤 화면으로 전환 될 것인지 정의한다.

```dart
@override
Widget build(BuildContext context) {
  return MaterialApp(
    routes: {
      '/': (context) => HomeScreen(),
      '/details': (context) => DetailScreen(),
    },
  );
}
```

## navpush

어떠한 사용자 동작을 통해 다른 화면으로 이동하려면 `Navigator.push` 메소드를 통해 다른 화면으로 이동한다.

```dart
onPressed : () {
  Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => DetailScreen()).
    );
}
```

## navpop

다시 원래 화면으로 돌아오려면 `Navigator.pop` 메소드를 통해 이전 화면으로 되돌아 간다.

```dart
onPressed: () {
    Navigator.pop(context);
}
```

## Named Route

Named Route 는 MaterialApp 의 route 에 이름을 가진 route 를 정의하여 사용한다.

```dart
MaterialApp(
  title: 'Named Routes Demo',
  // Start the app with the "/" named route. In this case, the app starts
  // on the FirstScreen widget.
  initialRoute: '/',
  routes: {
    // When navigating to the "/" route, build the FirstScreen widget.
    '/': (context) => const FirstScreen(),
    // When navigating to the "/second" route, build the SecondScreen widget.
    '/second': (context) => cosnst SecondScreen(),
  },
)
```

이후 원하는 화면으로 이동하고자 할 때 `Navigator.pushNamed` 메소드를 이용하여 원하는 화면으로 이동한다.

```dart
// Within the `FirstScreen` widget
onPressed: () {
  // Navigate to the second screen using a named route.
  Navigator.pushNamed(context, '/second');
}
```

다만, Named Route 방식은 뒤로가기 방식이 지원되지 않기 때문에 일반적인 route 방식을 주로 사용한다.

## Passing data to another screen

다른 화면으로 이동했을 때 보여주고자 하는 데이터가 있을 경우에 어떻게 할까?

먼저 데이터를 보여주고자 하는 화면에 데이터를 담을 수 있는 필드를 정의한다.

```dart
class DetailScreen extends StatelessWidget {
    final Ad ad;

    const DetailScreen({Key? key, required this.ad}) : super(Key: key);

    @override
    Widget build(BuildContext context) {...}
}
```

그리고 `Navigator.push` 메소드에서 이동하고자 하는 페이지의 생성자에 인자로 넘겨준다.

```dart
onTap: () async {
    Ad returnAd = await Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => DetailScreen(ad: ad)),
    );
}
```

## return data from screen

아래 코드에서 `Navigator.push` 메소드에서 `returnAd` 라는 변수를 반환 받고 있는 것을 알 수가 있다.

 ```dart
onTap: () async {
    Ad returnAd = await Navigator.push(
        context,
        MaterialPageRoute(builder: (context) => DetailScreen(ad: ad)),
    );
}
```

`Navigator.push` 메소드는 Future 를 반환하는 메소드이기 때문에 반환받은 값을 통해 데이터를 접근 할 수 있다.

# go_router

> <https://pub.dev/packages/go_router>

화면의 갯수가 많은 중급 이상 규모의 앱에서는 `go_router` 라는 패키지를 사용하여 고급 라우팅을 사용하게 할 수가 있다.

`go_router` 는 웹 라우팅도 지원하기 때문에 flutter web 을 지원할 예정이라면 사용이 필수!

## route

기본적으로 MaterialApp.route 와 유사하게 작성한다.

path 는 route 구성은 웹 URI 구성을 따른다.

```dart
final router = GoRouter(
    routes: [
        GoRoute(
            path: '/',
            builder: (context, state) => HomeScreen(),
        )
    ],
)
```

## context.push

`context.push` 메소드는 `Navigator.push` 메소드와 같이 원하는 화면으로 이동하는데 사용한다.

stack에 push

```dart
build(Context context) {
    return TextButton(
        onPressed: () => context.push('/detail'),
    )
}
```

## context.go

`context.go` 메소드는 `Navigator.replace` 메소드와 같이 현재 화면을 다른 화면으로 교체하는데 사용한다.

```dart
build(Context context) {
    return TextButton(
        onPressed: () => context.go('/detail'),
    )
}
```

## passing data in go_router

go_router 에서는 queryParameter 속성을 이용하여 이동할 화면에  데이터를 전달 할 수 있다.

```dart
context.push(
    Uri(
        path: '/collection_summary',
        queryParameters: {'tokenId' : '1'},
).toString());
```

```dart
GoRoute(
    path: '/collection_summary',
    builder: (context, state) {
        num collectionId = num.parse(state.queryParams['collectionId']!);
    }
)
```

toJson() 으로 직렬화가 가능하다면 String 으로 변환하여 객체를 전달 가능하다.

어떤 데이터라도 직렬화, 역직렬화를 통해 주고 받을 수 있음

```dart
final person = Person(name: '홍길동', age: 10);

context.push(
    Uri(
        path: '/second',
        queryParameters: {'person': jsonEncode(person.toJson())},    
    ).toString(),
)
```

```dart
GoRoute(
    path: '/second',
    builder: (BuildContext context, GoRouteState state) {
        final person = Person.fromJson(jsonDecode(state.uri.queryParameters['person']!));
        return Second(person: person);
    }
)
```

`context.push` 의 `extra` 속성을 통해 객체를 직렬화 하지 않고 전달할 수도 있음

```dart
const todo = Todo(1, 1, 't', false);
context.push('/todo', extra: todo);
```

```dart
GoRoute(
    path: '/todo',
    builder: (context, state) {
        final todo = state.extra as Todo;
        return TodoList(todo: todo);
    }
)
```

## Nested Route

라우터 내부에 라우터를 구성 가능

```dart
GoRoute(
    path: '/',
    builder: (context, state) {...},
    routes: [
        GoRoute(
            path: 'details',
            builder: (context, state) {...}
        ),
    ]
)
```
