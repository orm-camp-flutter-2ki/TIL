# FutureBuilder
- future를 ui로 표현하는 방법
<br/>

## StatefulWidget + setState()
- data(api), repository 를 사용
- 내용에 `.map()`을 사용

```dart
ListView(
        children: _todos
            .map((e) => ListTile(
                  title: Text(e.title),
                ))
            .toList());
```
<br/>

### 주의할 점
- `build`  에 데이터 요청(로직) 금지
- `setState()` 할 때마다 호출된다….

```dart
  @override
  Widget build(BuildContext context) {
    todoRepository.getTodos().then((todos) {
      setState(() {
        _todos = todos;
      });
    });
```
<br/>

### data 요청은 어디서?
- `initState()`에서 요청하면 된다. 한번 만 수행하는 생성자 같은 느낌….

```dart
  List<Todos> _todos = [];	

  @override
  void initState(BuildContext context) {
	  super.initState();
	  
    todoRepository.getTodos().then((todos) {
      setState(() {
        _todos = todos;
      });
    });
```
<br/>

### 기타 등…
```dart
// 로딩이 돌아가는...
CirculatProgressIndicator();
```
<br/>

## FutureBuilder
- Future 함수의 결과를 `Widget`으로 변환하는 widget
- snapshot에 데이터와 에러 정보 등이 들어있다.

```dart
FutureBuilder<List<Todo>>(
        future: todoRepository._getTodos(),
        // future: _getVideos(),
        // 파라미터 타입 생략 가능
        builder: (BuildContext context, AsyncSnapshot<List<Todo>> snapshot) {
          switch(snapshot.connectionState){
            
            case ConnectionState.none:
              // error 처리
            case ConnectionState.waiting:
	            return const CircularProgressIndicator();
              // waiting 처리
            case ConnectionState.active:
              // active 처리
            case ConnectionState.done:
		            return ListView(
					        children: _todos
					            .map((e) => ListTile(
					                  title: Text(e.title),
					                ))
					            .toList());
              // data 처리
          }
      }
)
```
<br/>

### 주의할 점
- `FutureBuilder` 안에 `FutureBuilder`는 `callback` 지옥…
<br/>

### 에러 처리도 가능
- 터지는게 아니라 error에 대한 값이 들어와 error에 대한 처리를 해줄 수 있다

```dart
if(snapshot.connectionState ==
		ConnectionState.done) {
	if (snapshot.hasError) {
		return SomethingWentWrong();
		// error 처리
	}
	...
}
```
<br/>
