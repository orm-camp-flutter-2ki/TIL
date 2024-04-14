## Provider
> Flutter의 상태관리 라이브러리중 하나

## 상태관리란?
상태 `=` 데이터 `=` 변수 <br/>
변수를 수정하면 알아서 바뀌게 하자<br/>
어떻게? 👉 InheritedWidget + (ValueNotifier 또는 ChangeNotifier)를 사용해서

![image](https://github.com/Gunbam27/TIL/assets/95085649/b84f6ed4-4700-4bcc-a747-f26451e6577b)

## Provider 쓰는법
준비물 : Provider <a href="https://pub.dev/packages/provider/install">설치</a>

1.ViewModel에 with ChangeNotifier 사용하여 생성. 
```dart
class SearchListViewModel with ChangeNotifier {
  //뷰모델에는 상수x변수o!
  //메서드는 void로!
}
```
2.View(스크린)코드

```dart
//StatefulWidget위젯으로 선언! 이유는 StatelessWidget은 context에 접근할 수 없어서~
@override
Widget build(BuildContext context){
  final viewModel = context.watch<SearchListViewModel>();
}
```
- StatefulWidget위젯으로 선언해준다.
- 빌드메서드 안에서 context.watch로 뷰모델을 감싸주어 선언(관찰 대상!)
- 단발성 접근시 `context.read<뷰모델 타입>().increase();`
- consumer : UI를 자주 빨리 많이 바꿔서 그려야하는데 성능을 좋게 하기 위해 해당 부분만 리빌드 할 때 사용한다.
  
3.최상단에 ChangeNotifier 제공할 부분에 ChangeNotifierProvider 위젯으로 감싸기
```dart
home: ChangeNotifierProvider(
        create: (_) {
          return SearchListViewModel(
            photoRepositoryImpl: PhotoRepositoryImpl(photoApi: PhotoApi()),
          );
        },
        child: SearchListScreen(),
      ),
```
child로 들어가있는 SearchListScreen()가 보여줄 화면이고,<br/>
데이터가 들어가있는 ViewModel과 생성자로 필요한 애들(의존하는애들)을 create에 넣어준다

### 추가적인부분)
- 위젯을 분리해서 쓸때는 뷰모델 값을 넘기는게 아닌 클래스값을 가져와서 쓴다.
```dart
//분리한 위젯
class ImageCardWidget extends StatelessWidget {
  final Photo photo;

const ImageCardWidget({
  super.key,,
  required this.photo,
});

@override
Widget build(BuildContext context){
  return Image.network(photo.url);
  }
}
```

```dart
//분리된 곳에서 쓸때
children:viewModel.photos.map((e)=>ImageCardWidget(photo:e)).toList()
```
    
