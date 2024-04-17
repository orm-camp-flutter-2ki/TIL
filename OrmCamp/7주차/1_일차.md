
## 📖 Shimmer
<br>

### 📄Shimmer란 무엇인가

-  Shimmer는 한국말로 희미하게 반짝인다는 뜻임
-  데이터가 로딩되지 않았을 때 CircularProgressIndicator()를 통해 로딩중임을 표현할 수 있음
-  Shimmer는 대신 데이터의 모양을 희미하게 표현해 줌

<br>

### 📄 사용방법

#### ✏️ 설치

```dart
flutter pub add shimmer
```

#### ✏️ 데이터와 Shimmer

```dart
list_item.dart

Container(  
  decoration: BoxDecoration(  
    borderRadius: BorderRadius.circular(20),  
    color: const Color(0xff333D79),
    ...
)
```
- 이러한 형태의 데이터 Container가 있음

```dart
loading_ui.dart

Shimmer.fromColors( // 반짝임 효과
  baseColor: Colors.grey.shade300,  
  highlightColor: Colors.grey.shade100,  
  child: Padding(  
    padding: const EdgeInsets.symmetric(vertical: 8, horizontal: 16),  
    child: Container(  
      decoration: BoxDecoration(  
        borderRadius: BorderRadius.circular(20),  
        color: Colors.grey,  
      ),  
      width: double.infinity,  
      height: 78,  
    ),  
  ),  
);
```
- Shimmer.fromColors를 통해 같은 모양으로 만들어 줌

#### ✏️ 삼항연산자

```dart
ListView(  
  children: viewModel.isLoading  
      ? List.generate(5, (index) => LoadingUI())  
      : viewModel.subways  
          .map((subway) => ListItem(subway: subway))  
          .toList(),  
)
```
- 삼항 연산자를 통해 로딩중에는 Shimmer가 나오도록 데이터가 넘어오면 ListItem이 넘어오도록 설정해 줌
