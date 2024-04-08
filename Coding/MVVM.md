## 📖MVVM
<br>

### 📄MVVM 개요

<br>

- 앱의 확장성과 유지보수의 편의성을 고려하여 아키텍처를 적용하는 것이 중요함
- 현재 모바일 앱에 가장 적합한 아키텍처 중 하나가 MVVM임

<br>

### 📄 MVVM 구조

<br>


![Pasted image 20240408231250](https://github.com/hwangtaewook/TIL/assets/87569211/20897107-7088-4ae0-a06b-eab13172a873)


<br>

### 📄 ViewModel

-  Repository에서 제공한 데이터를 UI로 표시하기 쉬운 형태로 변환해줌
- 화면에 표시할 데이터, 로딩 상태, 액션 등을 캡슐화 해줌
- 하나의 View에 하나의 ViewModel
- 메서드는 void로 작성

<br>

### 📄 ChangeNotifier
- Flutter에서 제공하는 옵저버 패턴을 가진 상태 알림이
- notifyListeners()를 호출하여 변경사항을 알림
- 데이터 바인딩 구현의 핵심

#### ✏️ ChangeNotifier 예

```dart
main_view_model.dart

void increment() {  
  _counter++;  
  notifyListeners();  
}
```


- main_view_model의 increment 메서드 끝에 notifyListeners()가 있어 호출 후 View에 알려줌



```dart
main.dart

@override  
void initState() {  
  super.initState();  
  viewModel.addListener(updateUI); // ViewModel에 대한 상태 변화를 감지하여 UI 업데이트  
}  
  
@override  
void dispose() {  
  viewModel.removeListener(updateUI); // Dispose될 때 리스너 제거  
  super.dispose();  
}  
  
void updateUI() {  
  setState(() {}); // UI 업데이트  
}
```
- addListener을 통해 상태 변화 감지후 UI 업데이트
- removeListener을 통해 메모리 누수 방지
