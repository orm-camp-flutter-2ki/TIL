## 📖 Debounce
<br>

### 📄 Debounce 란?

-  이벤트가 발생한 후에 일정 시간이 지나기 전에만 해당 이벤트를 처리하는 방식으로 동작함
-  빠른 이벤트의 처리를 제어하고 의도치 않은 동작을 방지함
<br>

### 📄 사용 예
```dart
class SearchListViewModel with ChangeNotifier {  
  final GetPhotoUseCase _getPhotoUseCase;  
  Timer? _timer;  
  
  SearchListViewModel({  
    required GetPhotoUseCase getPhotoUseCase,  
  }) : _getPhotoUseCase = getPhotoUseCase;  
  
  SearchListState _state = const SearchListState();  
  
  SearchListState get state => _state;  
  
  void onSearch(String query) async {  
    _timer?.cancel();  
  
    _timer = Timer(const Duration(milliseconds: 500), () async {  
      _state = state.copyWith(isLoading: true);  
      notifyListeners();  
    });  
    _state = state.copyWith(  
      photos: await _getPhotoUseCase.execute(query),  
      isLoading: false,  
    );  
    notifyListeners();  
  }  
}
```
